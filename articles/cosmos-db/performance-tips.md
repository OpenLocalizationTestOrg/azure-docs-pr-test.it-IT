---
title: suggerimenti aaaPerformance - Azure Cosmos database NoSQL | Documenti Microsoft
description: Informazioni su prestazioni del database Azure Cosmos DB tooimprove opzioni configurazione client
keywords: come tooimprove delle prestazioni del database
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Suggerimenti sulle prestazioni per Azure Cosmos DB
Azure Cosmos DB è un database distribuito veloce e flessibile, facilmente scalabile e con latenza e velocità effettiva garantite. Non sono state apportate modifiche di architettura principali toomake o scrivere codice complesso tooscale il database con DB Cosmos. Aumentare o ridurre le prestazioni è semplice come eseguire una singola chiamata API o una [chiamata al metodo SDK](set-throughput.md#set-throughput-sdk). Tuttavia, poiché Cosmos DB è possibile accedere tramite sono chiamate di rete sono ottimizzazioni sul lato client è possibile apportare tooachieve ottenere prestazioni ottimali.

Se si vogliono migliorare le prestazioni del database, prendere in considerazione hello le opzioni seguenti:

## <a name="networking"></a>Rete
<a id="direct-connection"></a>

1. **Criteri di connessione: usare la modalità di connessione diretta**

    Come un client si connette tooCosmos DB ha implicazioni molto importanti sulle prestazioni, specie in termini di latenza client-side osservata. Sono disponibili due impostazioni di configurazione della chiave per la configurazione del client Criteri di connessione: connessione hello *modalità* hello e [connessione *protocollo*](#connection-protocol).  Hello due modalità disponibili sono:

   1. Modalità gateway (predefinita)
   2. Modalità diretta

      Modalità di gateway è supportata in tutte le piattaforme SDK e hello configurato predefinito.  Se l'applicazione viene eseguita all'interno di una rete aziendale con restrizioni del firewall strict, modalità di Gateway è la scelta migliore hello poiché Usa la porta HTTPS standard hello e un singolo endpoint. salve compromesso di prestazioni, tuttavia, è che la modalità Gateway implica un hop di rete aggiuntiva ogni volta i dati vengono letti o scritti tooCosmos DB. Per questo motivo, la modalità diretta offre prestazioni migliori scadenza toofewer hop di rete.
<a id="use-tcp"></a>
2. **Criteri di connessione: utilizzare protocollo TCP hello**

    Quando si usa la modalità diretta, sono disponibili due opzioni del protocollo:

   * TCP
   * HTTPS

     Cosmos DB offre un modello di programmazione RESTful su HTTPS semplice e aperto. Inoltre, offre un efficiente protocollo TCP, che è anche RESTful nel modello di comunicazione ed è disponibile tramite il client hello .NET SDK. Sia il protocollo TCP diretto che il protocollo HTTPS usano SSL per l'autenticazione iniziale e la crittografia del traffico. Per prestazioni ottimali, utilizzare il protocollo TCP hello quando possibile.

     Quando si utilizza TCP in modalità di Gateway, la porta TCP 443 è hello porta DB Cosmos e 10255 è la porta di MongoDB API hello. Quando si utilizza TCP in modalità diretta, nelle porte di Gateway toohello aggiunta, è necessario porta hello tooensure compreso tra 10000 e 20000 è aperto perché Cosmos DB Usa le porte TCP dinamiche. Se queste porte non sono aperte e si tenta di toouse TCP, viene visualizzato un errore HTTP 503 Servizio non disponibile.

     Modalità di connettività Hello viene configurato durante la costruzione di hello dell'istanza DocumentClient hello con parametro ConnectionPolicy hello. Se viene utilizzata la modalità diretta, è inoltre possibile impostare hello protocollo nel parametro ConnectionPolicy hello.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Poiché TCP è supportato solo in modalità diretta, se viene utilizzata la modalità di Gateway, quindi hello il protocollo HTTPS è sempre utilizzato toocommunicate con hello Gateway e il valore di protocollo hello in hello che connectionpolicy viene ignorato.

    ![Illustrazione di hello Azure Cosmos DB criteri di connessione](./media/performance-tips/connection-policy.png)

3. **Chiamare la latenza di avvio tooavoid OpenAsync alla prima richiesta**

    Per impostazione predefinita, prima richiesta hello ha una latenza maggiore perché contiene una tabella di routing toofetch hello indirizzo. tooavoid questa latenza di avvio su hello prima richiesta, è necessario chiamare OpenAsync() come indicato di seguito una volta durante l'inizializzazione.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Collocare i client nella stessa area di Azure per ottenere prestazioni migliori**

    Quando possibile, sul posto hello di tutte le applicazioni che chiamano DB Cosmos stessa area hello database Cosmos DB. Per un confronto approssimativo, chiama tooCosmos DB all'interno di hello stessa regione completata entro 1-2 ms, ma la latenza di hello tra hello ovest e costa orientale di hello Stati Uniti sono > 50 ms. Questa latenza probabilmente può variare da toorequest richiesta a seconda della route hello impiegato dalla richiesta hello durante il passaggio dal limite di hello client toohello Data Center di Azure. Hello più basso possibile latenza scopo è necessario garantire la chiamata di hello applicazione si trova all'interno di hello stessa area Azure hello provisioning Cosmos DB endpoint. Per un elenco delle aree disponibili, vedere [Aree di Azure](https://azure.microsoft.com/regions/#services).

    ![Illustrazione di hello Azure Cosmos DB criteri di connessione](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Aumentare il numero di thread/attività**

    Poiché le chiamate tooAzure Cosmos DB vengono eseguite su rete hello, potrebbe essere necessario grado di hello toovary parallelismo delle richieste in modo che un'applicazione client hello impiega molto tempo di attesa tra le richieste. Ad esempio, se si sta utilizzando. Del NET [Task Parallel Library](https://msdn.microsoft.com//library/dd460717.aspx), creare nell'ordine di hello di 100s delle attività di lettura o scrittura tooCosmos DB.

## <a name="sdk-usage"></a>Uso dell'SDK
1. **Installare hello SDK più recente**

    Hello Cosmos DB SDK vengono costantemente migliorate tooprovide hello migliori prestazioni. Vedere hello [Cosmos DB SDK](documentdb-sdk-dotnet.md) toodetermine pagine hello SDK più recente ed esaminare i miglioramenti.
2. **Utilizzare un client DB Cosmos singleton per durata hello dell'applicazione**

    Si noti che ogni istanza di DocumentClient è thread-safe ed esegue la gestione efficiente delle connessioni e la memorizzazione nella cache degli indirizzi quando viene usata la modalità diretta. gestione di connessioni efficiente tooallow e prestazioni migliori da DocumentClient, è consigliabile toouse una singola istanza di DocumentClient per AppDomain per durata hello dell'applicazione hello.

   <a id="max-connection"></a>
3. **Aumentare il valore di System.Net MaxConnections per host se si usa la modalità Gateway**.

    COSMOS DB richieste vengono eseguite su HTTPS/REST quando si utilizza la modalità Gateway e sono sottoposti toohello limite di connessioni predefinito per ogni nome host o indirizzo IP. Potrebbe essere necessario tooset hello MaxConnections tooa valore più alto (100-1000) in modo che hello libreria client può utilizzare più connessioni simultanee tooCosmos DB. In .NET SDK 1.8.0 hello e sopra, hello il valore predefinito per [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) è 50 e toochange hello valore, è possibile impostare hello [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa di valore più alto.   
4. **Ottimizzazione delle query parallele per le raccolte partizionate**

     DocumentDB .NET SDK versione alla 1.9.0 e versioni successive di query parallele di supporto, che consentono di tooquery una raccolta partizionata in parallelo (vedere [utilizzo hello SDK](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) hello correlati e [esempi di codice](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) per altre informazioni). Query parallele sono progettate tooimprove query latenza e velocità effettiva sulla loro controparte seriale. Query parallele forniscono due parametri che gli utenti possono ottimizzare toocustom adattamento relativi requisiti, MaxDegreeOfParallelism (): numero massimo di hello toocontrol delle partizioni è quindi possibile eseguire una query in parallelo e (b) MaxBufferedItemCount: numero di hello toocontrol di pre-recupero dei risultati.

    (a) ***Ottimizzazione di MaxDegreeOfParallelism\:*** la query parallela funziona eseguendo query su più partizioni in parallelo. Tuttavia, da una raccolta partizionata singoli vengono recuperati in modo seriale con query toohello riguardo. In tal caso, hello il possibilità massima di raggiungimento di impostazione del numero di partizioni di hello MaxDegreeOfParallelism toohello è hello la maggior parte delle query ad alte prestazioni, purché tutte le altre condizioni di sistema rimangono hello stesso. Se non si conosce il numero di hello di partizioni, è possibile impostare un numero elevato hello MaxDegreeOfParallelism tooa e sistema hello sceglie minimo hello (numero di partizioni, l'input dell'utente fornito) come hello MaxDegreeOfParallelism.

    È importante toonote parallele query producono hello migliori vantaggi se dati hello viene distribuito uniformemente tra tutte le partizioni con query toohello riguardo. Se hello partizionata raccolta verrà partizionata modo tale che tutte o una parte dei dati di hello restituiti da una query è concentrato in alcune partizioni (una partizione nel peggiore dei casi), quindi le prestazioni di hello di query hello potrebbero essere un collo di bottiglia da tali partizioni.

    (b) ***ottimizzazione MaxBufferedItemCount\: *** query parallele è impostato su toopre-fetch progettato durante l'elaborazione batch di risultati corrente hello client hello. Hello la prelettura consente ottimizzazione Latenza complessiva di una query. MaxBufferedItemCount è hello parametro toolimit hello numero di risultati già recuperati. Impostazione MaxBufferedItemCount toohello previsto hello query tooreceive il massimo vantaggio dalla prelettura consente a numero di risultati restituiti (o un numero più alto).

    Si noti che funziona pre-recupero hello stesso modo indipendentemente dal fatto che di hello MaxDegreeOfParallelism ed è un singolo buffer per i dati di hello da tutte le partizioni.  
5. **Attivare GC sul lato server**

    In alcuni casi può essere utile ridurre la frequenza hello di garbage collection. In .NET, impostare [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Implementare il backoff in corrispondenza di intervalli RetryAfter**

    Durante il test delle prestazioni, è necessario aumentare il carico fino a limitare un numero ridotto di richieste. Limitate, hello applicazione client deve intervallo tentativi di backoff sulla limitazione per hello specificata dal server. Rispettando hello backoff assicura che si trascorrono quantità minima di tempo di attesa tra i tentativi. Supporto di criteri di ripetizione è incluso nella versione 1.8.0 e di sopra di hello DocumentDB [.NET](documentdb-sdk-dotnet.md) e [Java](documentdb-sdk-java.md), versione alla 1.9.0 e versioni successive di hello [Node.js](documentdb-sdk-node.md) e [ Python](documentdb-sdk-python.md), e tutte le versioni supportate di hello [.NET Core](documentdb-sdk-dotnet-core.md) SDK. Per altre informazioni, vedere [Superamento dei limiti della velocità effettiva riservata](request-units.md#RequestRateTooLarge) e [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Aumentare il carico di lavoro client**

    Se si sta testando a livelli di velocità effettiva elevata (> 50.000 UR/sec), un'applicazione client hello potrebbe diventare collo di bottiglia hello scadenza toohello macchina coprendo all'utilizzo della CPU o rete. Se si raggiunge questo punto, è possibile continuare ulteriormente account al database Cosmos hello toopush tramite la scalabilità alle applicazioni client in più server.
8. **Memorizzare nella cache gli URI dei documenti per una minore latenza di lettura**

    Memorizzare nella cache URI ogni volta che è possibile per hello ottimizzare le prestazioni di lettura documento.
   <a id="tune-page-size"></a>
9. **Ottimizzazione delle dimensioni della pagina hello per le query/lettura feed per migliorare le prestazioni**

    Quando l'esecuzione di un blocco di lettura di documenti tramite lettura feed funzionalità (ad esempio, ReadDocumentFeedAsync) o quando l'esecuzione di una query SQL di DocumentDB, hello vengono restituiti in modo segmentato se il set di risultati hello è troppo grande. Per impostazione predefinita, i risultati vengono restituiti in blocchi di 100 elementi o 1 MB, a seconda del limite che viene raggiunto prima.

    numero di hello tooreduce di rete tooretrieve di andata e ritorno necessari tutti i risultati applicabili, è possibile aumentare la dimensione di pagina hello utilizzando too1000 tooup di intestazione x-ms-max-item-count richiesta. Nei casi in cui sia necessario toodisplay solo alcuni risultati, ad esempio, se l'API di applicazione o dell'interfaccia utente vengono restituiti solo 10 comporta un tempo, è inoltre possibile ridurre hello dimensioni too10 tooreduce hello velocità effettiva delle pagine utilizzata per letture e le query.

    È inoltre possibile impostare le dimensioni di pagina hello utilizzando hello disponibili Cosmos DB SDK.  ad esempio:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Aumentare il numero di thread/attività**

    Vedere [aumentare del numero di thread/attività](#increase-threads) nella sezione Networking hello.

11. **Usare processi host a 64 bit**

    Hello DocumentDB SDK funziona in un processo host a 32 bit quando si utilizza DocumentDB .NET SDK versione 1.11.4 e versioni successive. Tuttavia, se si usano query tra partizioni, è consigliabile usare l'elaborazione dell'host a 64 bit per migliorare le prestazioni. elaborazione come valore predefinito di hello, pertanto, in ordine toochange che too64 bit, eseguire la procedura seguente in base al tipo di hello dell'applicazione, Hello seguenti tipi di applicazioni è host a 32 bit:

    - Per le applicazioni eseguibili, questo scopo è possibile hello deselezionando **preferisci 32 bit** opzione hello **le proprietà del progetto** finestra hello **compilare** scheda.

    - Per i progetti di test basati su VSTest, questa operazione può essere eseguita selezionando **Test**->**impostazioni Test**->**predefinito architettura del processore X64**, da hello **Test di Visual Studio** opzione di menu.

    - Per le applicazioni Web ASP.NET distribuite localmente, questa operazione può essere eseguita controllando hello **versione a 64 bit hello utilizzo di IIS Express per progetti e siti web**in **strumenti** ->  **Opzioni**->**progetti e soluzioni**->**progetti Web**.

    - Per le applicazioni Web ASP.NET distribuite in Azure, questa operazione può essere eseguita scegliendo hello **piattaforma a 64 bit** in hello **le impostazioni dell'applicazione** su hello portale di Azure.

## <a name="indexing-policy"></a>Criterio di indicizzazione
1. **Usare l'indicizzazione differita per frequenze di inserimento più veloci nei momenti di massima attività**

    DB COSMOS consente toospecify: a livello di raccolta hello-un criterio di indicizzazione che consente di toochoose se si desidera hello documenti in un insieme di toobe automaticamente indicizzato o meno.  È anche possibile scegliere tra aggiornamenti sincroni (coerenti) e asincroni (differiti). Per impostazione predefinita, l'indice di hello viene aggiornato in modo sincrono in ogni istruzione insert, sostituire o eliminazione di una raccolta di toohello del documento. In modo sincrono in modalità attiva hello query toohonor hello stesso [livello di coerenza](consistency-levels.md) a quella di hello documento legge senza alcun ritardo per l'indice di hello troppo "aggiornarsi".

    Questo tipo di indicizzazione può essere considerata per gli scenari in cui i dati vengono scritti in aumenti improvvisi e si desidera tooamortize hello lavoro richiesto tooindex contenuto in un periodo di tempo più lungo. Questo tipo di indicizzazione consente inoltre toouse il provisioning di velocità effettiva in modo efficace e servire richieste di scrittura nei momenti con latenza minima. È importante toonote, tuttavia, quando è abilitata l'indicizzazione differita, vengono alla fine coerenti indipendentemente dal livello di coerenza hello configurato per l'account Cosmos DB hello risultati della query.

    Di conseguenza, la modalità di indicizzazione coerenza (IndexingPolicy.IndexingMode è impostato tooConsistent) comporta hello massima richiesta unità addebito per la scrittura, durante l'indicizzazione di modalità (IndexingPolicy.IndexingMode è impostato tooLazy) e non l'indicizzazione Lazy (IndexingPolicy.Automatic è impostato tooFalse) ha costo pari a zero indicizzazione in fase di hello di scrittura.
2. **Escludere i percorsi non usati dall'indicizzazione per scritture più veloci**

    Criteri di indicizzazione COSMOS DB consentono inoltre toospecify tooinclude percorsi dei documenti o escludere dall'indicizzazione sfruttando l'indicizzazione di percorsi (IndexingPolicy.IncludedPaths e IndexingPolicy.ExcludedPaths). utilizzo di Hello dei percorsi di indicizzazione può offrire prestazioni di scrittura migliorate e archiviazione dell'indice più basso per gli scenari in cui hello modelli di query sono noti in anticipo, come i costi di indicizzazione sono direttamente correlati toohello svariate univoci percorsi indicizzati.  Ad esempio, hello seguente codice mostra come tooexclude un'intera sezione di hello documenti (anche noto come un sottoalbero) dall'indicizzazione mediante hello "*" con caratteri jolly.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).

## <a name="throughput"></a>Velocità effettiva
<a id="measure-rus"></a>

1. **Misurare e ottimizzare per ottenere un utilizzo minore di unità richiesta al secondo**

    COSMOS DB offre un'ampia gamma di operazioni di database, incluse le query relazionale e gerarchiche con funzioni definite dall'utente, stored procedure e trigger: funzionamento nei documenti di hello all'interno di una raccolta di database. costo Hello associata a ognuna di queste operazioni varia in base hello CPU, i/o e quantità di memoria richiesta toocomplete hello operazione. Anziché considerare e la gestione delle risorse hardware, può essere considerato di un'unità di richiesta (RU) come una singola misura per hello le risorse necessarie tooperform varie operazioni di database e servizio richiesta di un'applicazione.

    [Unità richieste](request-units.md) viene effettuato il provisioning per ogni account del database in base al numero di hello unità di capacità acquistato. Il consumo delle unità di richiesta è valutato in base alla frequenza al secondo. Le applicazioni che superano l'unità di richiesta di provisioning hello frequenza per l'account è limitata fino a quando il tasso di hello scende di sotto di hello livello riservato per l'account di hello. Se l'applicazione necessita di un livello superiore di velocità effettiva, sarà possibile acquistare unità di capacità aggiuntive.

    complessità Hello di una query ha un impatto quante unità di richiesta vengono utilizzate per un'operazione. numero di Hello di predicati, natura dei predicati hello, numero di funzioni definite dall'utente e dimensioni di hello del set di dati di origine hello tutti influenzare il costo di hello di operazioni di query.

    overhead hello toomeasure di qualsiasi operazione (creare, aggiornare o eliminare), esaminare l'intestazione x-ms-richiesta addebito hello (o hello proprietà RequestCharge equivalente in ResourceResponse<T> o FeedResponse<T> in .NET SDK hello) toomeasure numero di Hello di unità di richiesta utilizzato da queste operazioni.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    addebito richiesta restituito in questa intestazione Hello rappresenta una frazione della velocità effettiva di provisioning (ad esempio, 2000 RUs al secondo). Ad esempio, se hello query precedente restituisce documenti con 1000 1KB, il costo di hello dell'operazione di hello è 1000. Di conseguenza, all'interno di un secondo, server hello rispetta solo due richieste prima di limitazione delle richieste successive. Per ulteriori informazioni, vedere [unità richieste](request-units.md) hello e [calcolatrice unità richiesta](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Gestire la limitazione della frequenza o una frequenza di richieste troppo elevata**

    Quando un client tenta di velocità effettiva riservati tooexceed hello per un account, è senza riduzione delle prestazioni server hello e Nessun utilizzo della capacità di velocità effettiva oltre il livello di hello riservato. server Hello modalità preemptive terminerà richiesta hello con RequestRateTooLarge (codice di stato HTTP 429) e indicando l'intestazione x-ms-nuovo tentativo-dopo-ms hello restituito hello tempo totale, espresso in millisecondi, che hello utente deve attendere prima di eseguire nuovamente la richiesta hello.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    SDK Hello tutti implicitamente intercettare questa risposta di, rispettare intestazione hello specificata dal server retry-after e ripetere la richiesta hello. A meno che non si accede all'account contemporaneamente da più client, il successivo tentativo di hello avrà esito positivo.

    Se si dispone di più di un client in modo cumulativo operano in modo coerente di sopra di frequenza di richieste di hello, hello numero di tentativi predefinito attualmente too9 set internamente dal client hello potrebbe non essere sufficiente; In questo caso, il client di hello genera un DocumentClientException con applicazione toohello 429 in codice stato. numero di tentativi di Hello predefinito può essere modificato da hello impostazione RetryOptions nell'istanza ConnectionPolicy hello. Per impostazione predefinita, se richiesta hello continua toooperate sopra la frequenza di richieste hello hello DocumentClientException con codice di stato 429 viene restituito dopo un periodo di tempo cumulativo di attesa di 30 secondi. Questo errore si verifica anche quando il numero di tentativi corrente hello è inferiore al conteggio massimo di tentativi di hello, sia essa predefinito hello 9 o un valore definito dall'utente.

    Mentre hello automatizzata comportamento del nuovo tentativo consente tooimprove flessibilità e facilità d'uso per hello la maggior parte delle applicazioni, potrebbero venire conflittuale quando si esegue il benchmark delle prestazioni, soprattutto quando la misurazione della latenza.  Latenza osservata client Hello raggiungerà un picco se esperimento hello raggiunge il limite di server hello e fa sì che il client di hello tentativi toosilently SDK. latenza tooavoid picchi durante gli esperimenti di prestazioni, misura hello addebito restituiti da ogni operazione e verificare che le richieste sono opera di sotto di frequenza di richieste riservato hello. Per altre informazioni, vedere [Unità richiesta](request-units.md).
3. **Progettare documenti di dimensioni minori per ottenere una velocità effettiva maggiore**

    Hello addebito richiesta (ad esempio l'elaborazione della richiesta costo) di un'operazione specificata è direttamente correlato toohello dimensioni del documento hello. Le operazioni sui documenti di grandi dimensioni sono più costose rispetto alle operazioni per i documenti di piccole dimensioni.

## <a name="next-steps"></a>Passaggi successivi
Per un esempio dell'applicazione utilizzata tooevaluate DB Cosmos per scenari ad alte prestazioni in alcuni computer client, vedere [prestazioni e scalabilità test con DB Cosmos](performance-testing.md).

Vedere anche toolearn ulteriori informazioni su progettazione dell'applicazione per la scalabilità e prestazioni elevate, [partizionamento e la scalabilità in Azure Cosmos DB](partition-data.md).
