---
title: aaaWorking con modifica hello feed supporto nel database di Azure Cosmos | Documenti Microsoft
description: Utilizzare Azure Cosmos DB Modifica supporto feed tootrack modifiche nei documenti ed eseguire l'elaborazione basata su eventi analogamente ai trigger e mantenere aggiornati i sistemi di cache e analitica.
keywords: feed delle modifiche
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Utilizzo con il supporto feed hello modifica nel database di Azure Cosmos
[Azure Cosmos DB](../cosmos-db/introduction.md) è un servizio di database con replica a livello globale rapido e flessibile, usato per archiviare volumi elevati di dati transazionali e operativi, con una latenza stimabile in pochissimi millisecondi a cifra singola per le operazioni di lettura e scrittura. Tutto questo lo rende particolarmente adatto per le applicazioni IoT, di videogiochi, del settore della vendita al dettaglio e di registrazioni di operazioni. Un modello di progettazione comuni in queste applicazioni è tootrack modifiche apportate tooAzure DB Cosmos dati e aggiornare le viste materializzate, eseguono analitica in tempo reale, toocold archiviazione dei dati e notifiche di trigger a determinati eventi in base a queste modifiche. Hello **modifica feed supporto** nel database di Azure Cosmos consente toobuild efficienti e scalabili soluzioni per ognuno di questi modelli.

Con modifica feed supporto, DB Cosmos Azure fornisce un elenco ordinato di documenti all'interno di una raccolta di Azure Cosmos DB nell'ordine di hello in cui essi sono stati modificati. Questo feed può essere utilizzato toolisten per modifiche toodata insieme hello ed eseguire azioni, ad esempio:

* Attivare tooan una chiamata API quando un documento viene inserito o modificato
* Eseguire l'elaborazione in tempo reale (flusso) per gli aggiornamenti
* Sincronizzare i dati con una cache, un motore di ricerca o un data warehouse

Le modifiche in Azure Cosmos DB sono persistenti e possono essere elaborate in modo asincrono. Vengono inoltre distribuite a uno o più consumer per l'elaborazione parallela. Diamo un'occhiata hello API per i feed di modifica e come è possibile usarli toobuild di applicazioni scalabili in tempo reale. In questo articolo viene illustrato come modificare toowork con Azure Cosmos DB feed e hello API DocumentDB. 

![L'utilizzo di Azure Cosmos DB change feed toopower in tempo reale analitica e scenari di elaborazione basato su eventi](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Modifica supporto feed viene fornita solo per l'API DocumentDB hello in questa fase. Hello API Graph e API di tabella non sono attualmente supportati.

## <a name="use-cases-and-scenarios"></a>Casi d'uso e scenari
Feed di modifica consente un'elaborazione efficiente di DataSet di grandi dimensioni con un numero elevato di scritture e offre un tooidentify intero set di dati alternativo tooquerying cosa è cambiato. Ad esempio, è possibile eseguire hello seguenti in modo efficiente attività:

* Aggiornare una cache, un indice di ricerca o un data warehouse con i dati archiviati in Azure Cosmos DB.
* Implementare la suddivisione in livelli e l'archiviazione dei dati a livello di applicazione, vale a dire memorizzarli "attivo" nel database di Azure Cosmos e age "dati freddo" troppo[archiviazione Blob di Azure](../storage/common/storage-introduction.md) o [archivio Azure Data Lake](../data-lake-store/data-lake-store-overview.md).
* Implementare analisi in batch sui dati usando [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementare [pipeline lambda in Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB. Azure Cosmos DB offre una soluzione di database scalabile che può gestire sia l'inserimento che le query e implementare architetture lambda con costo totale di proprietà ridotto. 
* Eseguire zero tooanother tempi di inattività migrazioni account Azure Cosmos DB con uno schema di partizionamento differente.

**Pipeline lambda con Azure Cosmos DB per l'inserimento e le query:**

![Pipeline lambda basate su Azure Cosmos DB per l'inserimento e le query](./media/change-feed/lambda.png)

È possibile utilizzare Azure Cosmos DB tooreceive e archiviare i dati di evento di dispositivi, sensori, infrastruttura e le applicazioni ed elaborare questi eventi in tempo reale con [Azure flusso Analitica](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

All'interno del [senza](http://azure.com/serverless) web e App per dispositivi mobili, è possibile tenere traccia eventi, ad esempio tootrigger di profilo, le preferenze o alla posizione del cliente tooyour modifiche determinate azioni come l'invio di push dispositivi tootheir notifiche utilizzando [Funzioni di azure](../azure-functions/functions-bindings-documentdb.md) o [servizi App](https://azure.microsoft.com/services/app-service/). Se si usa Azure Cosmos DB toobuild un gioco, è possibile utilizzare ad esempio, in tempo reale classifiche tooimplement feed cambia in base ai punteggi di giochi completati.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Funzionamento del feed delle modifiche in Azure Cosmos DB
DB Cosmos Azure fornisce hello possibilità tooincrementally leggere gli aggiornamenti apportati tooan DB Cosmos Azure insieme. Questo feed di modifica è hello le proprietà seguenti:

* Le modifiche sono persistenti in Azure Cosmos DB e possono essere elaborate in modo asincrono.
* Toodocuments modifiche all'interno di una raccolta sono disponibili immediatamente in hello modifica feed.
* Ogni documento tooa modifica viene visualizzata una sola volta nel feed modifica hello e client di gestire la logica di checkpoint. libreria di feed processore modifiche Hello fornisce funzionalità dei checkpoint automatici e "at least once" semantica.
* La modifica più recente hello solo per un determinato documento è incluso nel registro delle modifiche hello. Le modifiche intermedie potrebbero non essere disponibili.
* Hello modifica feed viene ordinato in ordine di modifica all'interno di ogni valore di chiave di partizione. Non esiste alcun ordine garantito tra i valori partition-key.
* Le modifiche possono essere sincronizzate da qualsiasi punto nel tempo, in altre parole non è previsto un periodo di conservazione fisso per cui sono disponibili le modifiche.
* Le modifiche sono disponibili in blocchi di intervalli di chiavi di partizione. Questa funzionalità consente di apportare modifiche da elaborare in parallelo da più consumer/server toobe di raccolte di grandi dimensioni.
* Le applicazioni possono richiedere per la modifica più feed contemporaneamente su hello stessa raccolta.

Il feed di modifiche di Azure Cosmos DB è abilitato per impostazione predefinita per tutti gli account. È possibile utilizzare il [velocità effettiva di provisioning](request-units.md) nella propria area di scrittura o in una [leggere area](distribute-data-globally.md) tooread da hello modificare feed, esattamente come qualsiasi altra operazione dal database di Azure Cosmos. Hello modifica feed inclusi inserimenti e operazioni di aggiornamento eseguite toodocuments insieme hello. È possibile acquisire le eliminazioni impostando un flag "eliminazione temporanea" all'interno dei documenti al posto delle eliminazioni. In alternativa, è possibile impostare un periodo di scadenza per i documenti tramite hello [funzionalità TTL](time-to-live.md), ad esempio, 24 ore e l'utilizzo hello valore della proprietà toocapture Elimina. Con questa soluzione, è possibile tooprocess modifiche entro un intervallo di tempo più breve rispetto al periodo di scadenza della durata (TTL) hello. Hello modifica feed è disponibile per ogni intervallo di chiavi di partizione di raccolta del documento hello e pertanto possono essere distribuiti in uno o più consumer per l'elaborazione parallela. 

![Elaborazione distribuita del feed delle modifiche di Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

Sono disponibili alcune opzioni per l'implementazione di un feed di modifiche nel codice client. Hello sezioni che immediatamente seguono descrivono come tooimplement hello feed di modifica tramite API REST di Azure Cosmos DB hello e hello SDK di DocumentDB. Tuttavia, per le applicazioni .NET, è consigliabile utilizzare la nuova hello [processore libreria di feed di modifica](#change-feed-processor) per l'elaborazione eventi da hello modificano feed come semplifica la lettura modifiche tra le partizioni e consente a più thread in esecuzione Parallel. 

## <a id="rest-apis"></a>Utilizzo di hello REST API e SDK di DocumentDB
Azure Cosmos DB offre contenitori elastici di archiviazione e velocità effettiva chiamati **raccolte**. I dati nelle raccolte vengono raggruppati in modo logico tramite [chiavi di partizione](partition-data.md), per motivi di scalabilità e prestazioni. Azure Cosmos DB offre varie API per l'accesso ai dati, tra cui la ricerca per ID (Read/Get), le query e i feed di lettura (analisi). Hello feed modifica può essere ottenuto tramite due toohello di intestazioni di richiesta DocumentDB nuova `ReadDocumentFeed` API e possono essere elaborati in parallelo tra intervalli di chiavi di partizione.

### <a name="readdocumentfeed-api"></a>API ReadDocumentFeed
Esaminiamo brevemente il funzionamento di ReadDocumentFeed. DB Cosmos Azure supporta la lettura di un feed di documenti all'interno di una raccolta tramite hello `ReadDocumentFeed` API. Ad esempio, hello richiesta seguente restituisce una pagina di documenti all'interno di hello `serverlogs` insieme. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Risultati possono essere limitati tramite hello `x-ms-max-item-count` intestazione, operazioni di lettura e può essere ripresi reinviando la richiesta di hello con un `x-ms-continuation` intestazione restituita nella risposta precedente hello. Quando eseguita da un singolo client, `ReadDocumentFeed` passa da un risultato all'altro sulle partizioni in modo seriale. 

**Feed di documenti con lettura seriale**

È inoltre possibile recuperare il feed hello di documenti tramite uno dei hello supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md). Ad esempio, hello seguente mostra come hello toouse [ReadDocumentFeedAsync metodo](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Esecuzione distribuite di ReadDocumentFeed
Per le raccolte che contengono terabyte di dati o più o che ricevono volumi di aggiornamenti di grandi dimensioni, l'esecuzione seriale di un feed di lettura da una singola macchina client potrebbe non essere una soluzione pratica. In ordine toosupport questi scenari di dati di grandi dimensioni, Azure Cosmos DB fornisce API toodistribute `ReadDocumentFeed` chiamate in modo trasparente tra più client lettori/consumer. 

**ReadDocumentFeed distribuito**

l'elaborazione scalabile tooprovide delle modifiche incrementali, Azure Cosmos DB supporta un modello di scalabilità orizzontale per modifica hello feed API basata su intervalli di chiavi di partizione.

* È possibile ottenere un elenco degli intervalli di chiavi di partizione per una raccolta tramite una chiamata `ReadPartitionKeyRanges`. 
* Per ogni intervallo di chiavi di partizione, è possibile eseguire un `ReadDocumentFeed` tooread documenti con le chiavi di partizione all'interno dell'intervallo.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Recupero degli intervalli di chiavi di partizione per una raccolta
È possibile recuperare intervalli di chiavi di partizione hello hello richiedente `pkranges` risorsa all'interno di una raccolta. Ad esempio hello richiesta seguente recupera hello elenco di intervalli di chiavi di partizione per hello `serverlogs` raccolta:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Questa richiesta restituisce hello risposta contenente i metadati relativi a intervalli di chiavi di partizione hello seguenti:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Proprietà di intervallo di chiavi di partizione**: ogni intervallo di chiavi di partizione include le proprietà dei metadati hello in hello nella tabella seguente:

<table>
    <tr>
        <th>Nome intestazione</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>ID di Hello per intervalli di chiavi di partizione hello. Si tratta di un ID stabile e univoco in ciascuna raccolta.</p>
            <p>Deve essere utilizzata hello dopo le modifiche tooread chiamata dall'intervallo di chiavi di partizione.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>valore di hash di chiave Hello massima di una partizione per intervalli di chiavi di partizione hello. Solo per uso interno.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>valore hash della chiave di Hello minime partizione per intervalli di chiavi di partizione hello. Solo per uso interno.</td>
    </tr>       
</table>

È possibile farlo usando uno dei hello supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md). Ad esempio, hello frammento di codice seguente mostra come chiave di partizione tooretrieve intervalli in .NET utilizzando hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metodo.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

DB Cosmos Azure supporta il recupero di documenti per intervalli di chiavi di partizione mediante impostazione hello facoltativo `x-ms-documentdb-partitionkeyrangeid` intestazione. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Esecuzione di un ReadDocumentFeed incrementale
ReadDocumentFeed supporta i seguenti scenari/attività per l'elaborazione incrementale di modifiche apportate nelle raccolte di Azure Cosmos DB hello:

* Lettura di tutte le modifica, ovvero toodocuments dall'inizio di hello, dalla creazione della raccolta.
* Lettura di tutte le modifica toofuture aggiornamenti toodocuments dall'ora corrente o tutte le modifiche dopo l'ora specificata dall'utente.
* Leggere tutte le modifiche toodocuments da una versione logica dell'insieme di hello (ETag). È possibile consentire agli utenti in base a hello restituito ETag da richieste di lettura feed incrementale checkpoint.

le modifiche di Hello includono toodocuments inserimenti e aggiornamenti. Elimina toocapture, è necessario usare una proprietà di "eliminazione temporanea" all'interno dei documenti o utilizzare hello [proprietà di durata (TTL) predefinita](time-to-live.md) toosignal un'eliminazione in sospeso in hello modificare feed.

Hello seguente tabella elenca hello [richiesta](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [le intestazioni di risposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) per le operazioni di ReadDocumentFeed.

**Intestazioni delle richieste per ReadDocumentFeed incrementale**:

<table>
    <tr>
        <th>Nome intestazione</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Deve essere impostato troppo "Feed incrementale", o viene omesso in caso contrario</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Nessuna intestazione: restituisce tutte le modifiche da hello a partire da (creazione raccolta)</p>
            <p>"*": restituisce tutte le nuove modifiche toodata insieme hello</p>         
            <p>&lt;eTag&gt;: se impostata tooa raccolta ETag, restituisce tutte le modifiche apportate da tale timestamp logico</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Formato di ora RFC 1123. Ignorata se viene specificata l'intestazione If-None-Match</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Hello ID intervalli di chiavi di partizione per la lettura dei dati.</td>
    </tr>
</table>

**Intestazioni delle risposte per ReadDocumentFeed incrementale**:

<table> <tr>
        <th>Nome intestazione</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>numero di sequenza logica di Hello (LSN) dell'ultimo documento restituito nella risposta hello.</p>
            <p>Un ReadDocumentFeed incrementale può essere ripreso inviando nuovamente questo valore in If-None-Match.</p>
        </td>
    </tr>
</table>

Ecco un tooreturn di richiesta di esempio tutte le modifiche incrementali nella raccolta dalla versione di hello logico/ETag `28535` e intervalli di chiavi di partizione = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Le modifiche sono ordinate per tempo all'interno di ogni valore di chiave di partizione all'interno di intervalli di chiavi di partizione hello. Non esiste alcun ordine garantito tra i valori partition-key. Se sono presenti più risultati rispetto a visualizzabili in una singola pagina, è possibile leggere pagina di risultati successiva hello reinviando la richiesta di hello con hello `If-None-Match` intestazione con valore uguale toohello `etag` dalla risposta precedente hello. Se più documenti inseriti o aggiornati in modo transazionale all'interno di una stored procedure o trigger, saranno tutti restituiti all'interno di hello stessa pagina di risposta.

> [!NOTE]
> Con il feed di modifica, è possibile ottenere ulteriori elementi restituiti in una pagina, rispetto a quanto specificato `x-ms-max-item-count` nel caso di hello di più documenti inserita o aggiornata all'interno di una stored procedure o trigger. 

Quando si utilizza hello .NET SDK (1.17.0), impostare il campo hello `StartTime` in `ChangeFeedOptions` toodirectly restituito modificare documenti dal `StartTime` quando si chiama `CreateDocumentChangeFeedQuery`. Specificando `If-Modified-Since` utilizza hello API REST, la richiesta restituirà i non hello documenti stessi, ma piuttosto il token di continuazione hello o `etag` nell'intestazione di risposta hello. documenti di hello tooreturn hello modificato specificato, il token di continuazione hello `etag` deve quindi essere utilizzato nella successiva richiesta di hello con `If-None-Match` tooreturn hello documenti effettivi. 

Hello .NET SDK fornisce hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess modifiche tooa insieme le classi di supporto. Hello frammento di codice seguente viene illustrato come tooretrieve tutti cambia dall'inizio hello utilizzando hello .NET SDK da un singolo client.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
E hello frammento di codice seguente viene illustrato come tooprocess cambia in tempo reale con Azure Cosmos DB utilizzando Modifica hello feed supporto e hello funzione precedente. Hello prima chiamata restituisce tutti i documenti hello nella raccolta hello e hello secondo restituisce solo hello creati due documenti che sono stati creati dall'ultimo checkpoint hello.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

È inoltre possibile filtrare i feed di modifica hello tramite eventi di processo tooselectively logica sul lato client. Ad esempio, di seguito è riportato un frammento che utilizza tooprocess LINQ sul lato client, solo gli eventi di modifica temperatura da sensori di dispositivo.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Libreria del processore dei feed delle modifiche
Un'altra opzione consiste hello toouse [libreria DB Cosmos Azure modificare Feed processore](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), che consentono di distribuire facilmente l'elaborazione di una modifica feed tra più consumer di eventi. libreria Hello è molto utile per la compilazione di modifica feed lettori sulla piattaforma .NET hello. Alcuni flussi di lavoro che sarebbe stata più semplice tramite metodi hello inclusi in hello libreria processore Feed modifiche hello altri SDK di DB Cosmos includono: 

* Pull degli aggiornamenti dal feed di modifiche quando i dati vengono archiviati in più partizioni
* Lo spostamento o la replica dei dati da una raccolta tooanother
* Esecuzione parallela di azioni attivate dal toodata gli aggiornamenti e modifica di feed 

Durante l'uso di API Ciao hello Cosmos SDK offre accesso preciso toochange feed gli aggiornamenti in ogni partizione, l'utilizzo di libreria di Feed processore delle modifiche hello semplifica le modifiche di lettura tra partizioni e di più thread eseguiti in parallelo. Anziché manualmente legge le modifiche da ogni contenitore e il salvataggio di un token di continuazione per ogni partizione, hello processore Feed modifiche gestisce automaticamente le modifiche di lettura tra partizioni utilizzando un meccanismo di lease.

libreria Hello è disponibile come pacchetto NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e dal codice sorgente come un archivio Github [esempio](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Informazioni sulla libreria del processore dei feed delle modifiche 

Esistono quattro componenti principali dell'implementazione hello Feed processore di modifica: hello monitorati insieme, insieme di lease hello, hello processore host e i consumer di hello. 

**Raccolta monitorato:** raccolta di hello monitorato è hello ai dati da cui hello viene generato il feed di modifica. Qualsiasi raccolta toohello monitorato gli inserimenti e le modifiche vengono riflesse nel feed di hello modifica della raccolta hello. 

**Raccolta di lease:** hello lease raccolta coordinate modifica hello feed tra più processi di lavoro di elaborazione. Una raccolta separata è lease hello toostore usato con un lease per ogni partizione. È più vantaggiosa toostore questa raccolta di lease in un altro account con hello scrivere hello toowhere più vicino area Modifica Feed processore è in esecuzione. Oggetto lease contiene hello gli attributi seguenti: 
* Proprietario: Specifica l'host hello proprietario di lease hello
* Continuazione: Posizione hello (token di continuazione) in modifica hello feed per una determinata partizione
* Timestamp: Ora dell'ultimo aggiornamento lease; Hello timestamp può essere utilizzato toocheck se lease hello è considerato scaduto 

**Host processore:** ogni host determina quanti tooprocess partizioni in base a numero di altre istanze di host presenti presentano lease attivi. 
1.  Quando un host viene avviata, acquisisce il carico di lavoro di lease toobalance hello in tutti gli host. Un host rinnova periodicamente i lease, in modo che i lease rimangano attivi. 
2.  Un host checkpoint hello ultimo continuazione token tooits lease per ogni lettura. tooensure concorrenza, un host i controlli di sicurezza hello ETag per ogni aggiornamento di lease. Sono supportate anche altre strategie per i checkpoint.  
3.  Durante l'arresto, un host rilascia tutti i lease ma mantiene hello informazioni di continuazione, in modo da poter riprendere la lettura da hello stored checkpoint in un secondo momento. 

In questo momento il numero di hello di host non può essere maggiore del numero di hello di partizioni (lease).

**I consumer:** consumer, o thread di lavoro, sono i thread che eseguono modifiche hello feed elaborazione avviata da ogni host. Ogni host di processori può includere più consumer. Ogni consumer legge hello modifica feed da hello partizione assegnata tooand notifica relativo host delle modifiche e lease scaduti.

toofurther comprensione dell'interazione tra questi quattro elementi di Feed processore delle modifiche, esaminiamo un esempio in hello seguente diagramma. Hello monitorati raccolta documenti di archivi e utilizza city"hello" come chiave di partizione hello. Vediamo che partizione hello blu contiene documenti con campo "città" hello "A-E" e così via. Esistono due host, ciascuno con due consumer lettura dalle partizioni hello quattro in parallelo. le frecce di Hello indicano i consumer di hello durante la lettura da un punto specifico in hello modificare feed. Nella prima partizione hello, blu scuro hello rappresenta le modifiche da leggere mentre celeste hello rappresenta hello già letto le modifiche nel feed modifica hello. gli host di Hello utilizzano hello lease raccolta toostore una traccia di tookeep "continuazione" valore di hello corrente durante la lettura della posizione per ciascun consumer. 

![L'utilizzo di hello Azure Cosmos DB change feed host processore](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Uso della libreria del processore dei feed delle modifiche 
Hello seguente sezione viene illustrato come toouse hello libreria di Feed processore delle modifiche nel contesto di hello di replica delle modifiche da una raccolta di destinazione tooa raccolta di origine. In questo caso, hello origine è hello monitorato insieme nel processore di modifica del Feed. 

**Installare e includere pacchetto NuGet di processore Feed modifica hello** 

Prima di installare il pacchetto NuGet del processore dei feed di modifiche, è necessario installare quanto segue: 
* Microsoft.Azure.DocumentDB, versione 1.13.1 o successiva 
* Newtonsoft.Json, versione 9.0.1 o successiva. Installare `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e includerlo come riferimento.

**Creare una raccolta monitorata, di lease e di destinazione** 

Raccolta di lease hello hello toouse ordine processore libreria di Feed di modifica, deve toobe creato prima di eseguire hello processore host. Nuovamente, si consiglia di archiviare una raccolta di lease in un altro account con un hello toowhere più vicino di scrittura area che modifica Feed processore è in esecuzione. In questo esempio lo spostamento dei dati, è necessario raccolta di destinazione hello toocreate prima di eseguire l'host di hello Feed processore delle modifiche. Nel codice di esempio hello definiamo un hello toocreate del metodo helper monitorato, associato a un lease e raccolte di destinazione se non esiste già. 

> [!WARNING]
> Creazione di una raccolta ha implicazioni, prezzi che si desidera riservare una velocità effettiva per toocommunicate applicazione hello con Azure Cosmos DB. Per ulteriori informazioni, visitare hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Creazione di un host di processori*

Hello `ChangeFeedProcessorHost` classe fornisce un ambiente di runtime thread-safe, multiprocesso e sicuro per le implementazioni del processore di eventi che fornisce anche la gestione di lease di creazione di Checkpoint e di partizione. hello toouse `ChangeFeedProcessorHost` (classe), è possibile implementare `IChangeFeedObserver`. Questa interfaccia contiene tre metodi:

* `OpenAsync`: questa funzione viene chiamata quando viene aperto l'osservatore del feed di modifiche. Quando viene aperto consumer/osservatore può essere modificato tooperform un'azione specifica.  
* `CloseAsync`: questa funzione viene chiamata quando viene arrestato l'osservatore del feed di modifiche. Quando viene chiuso consumer/osservatore può essere modificato tooperform un'azione specifica.  
* `ProcessChangesAsync`: questa funzione viene chiamata quando nel feed di modifiche sono disponibili nuove modifiche al documento. Può essere modificato tooperform un'azione specifica dopo l'aggiornamento ogni modifica del feed.  

In questo esempio, si implementano hello `IChangeFeedObserver` tramite hello `DocumentFeedObserver` classe. In questo caso, hello `ProcessChangesAsync` funzione upserts (aggiornamenti) un documento da modifica feed nella raccolta di destinazione hello. In questo esempio è utile per lo spostamento dei dati da una raccolta tooanother nella chiave di ordinamento toochange hello partizione di un set di dati. 

*Host processore di hello in esecuzione*

Prima di avviare l'elaborazione degli eventi, è possibile personalizzare le opzioni relative al feed di modifiche e all'host del feed di modifiche. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
campi specifici di Hello che possono essere personalizzati sono riepilogati nella hello le tabelle seguenti. 

**Opzioni del feed di modifiche**:
<table>
    <tr>
        <th>Nome proprietà</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Ottiene o imposta hello il numero massimo di elementi toobe restituito nell'operazione di enumerazione hello in hello Azure Cosmos DB servizio di database.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Ottiene o imposta l'id di intervalli di chiavi di partizione hello per la richiesta corrente hello nel servizio di database di Azure Cosmos DB hello.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Ottiene o imposta il token di continuazione di hello richiesta nel servizio di database di Azure Cosmos DB hello.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Ottiene o imposta il token di sessione hello per l'utilizzo con la coerenza della sessione in hello Azure Cosmos DB servizio di database.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Ottiene o imposta se Modifica feed nel servizio di database di Azure Cosmos DB hello deve iniziare da hello a partire da (true) o da corrente (false). Per impostazione predefinita, inizia dalla posizione corrente (false).</td>
    </tr>
</table>

**Opzioni dell'host di feed di modifiche**:
<table>
    <tr>
        <th>Nome proprietà</th>
        <th>Tipo</th>
        <th>Descrizione</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>intervallo di Hello per tutti i lease per le partizioni vengono mantenuti attivi dall'istanza ChangeFeedEventHost hello.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Se le partizioni siano distribuite uniformemente tra le istanze di host noti, Hello tookick intervallo off toocompute un'attività.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>intervallo di Hello per cui hello lease viene eseguita su un lease che rappresenta una partizione. Se il lease hello non viene rinnovato entro questo intervallo, è scaduto e la proprietà della partizione hello Sposta tooanother ChangeFeedEventHost istanza.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>ritardo Hello tra il polling di una partizione per le nuove modifiche su hello feed, dopo tutte le modifiche correnti vengono svuotate.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Hello lease toocheckpoint frequenza.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>numero minimo di partizioni Hello per host hello.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>Hello massimo numero di partizioni hello host può essere utilizzato.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Booleano</td>
        <td>Se nella hello iniziale dell'host hello tutti i lease esistenti deve essere eliminato e host hello deve iniziare da zero.</td>
    </tr>
</table>


creare un'istanza di elaborazione, l'evento toostart `ChangeFeedProcessorHost`, fornendo i parametri appropriati hello per la raccolta di Azure Cosmos DB. Chiamare quindi `RegisterObserverAsync` tooregister il `IChangeFeedObserver` implementazione (DocumentFeedObserver in questo esempio) con il runtime di hello. A questo punto, l'host hello tenta tooacquire un lease in ogni intervallo di chiavi di partizione nella raccolta di Azure Cosmos DB hello usando un algoritmo "greedy". Tali lease durano per un determinato intervallo di tempo e quindi devono essere rinnovati. Appena nuovi nodi, istanze di lavoro, in questo caso, portare in linea, essi prenotazioni di lease e nel tempo carico hello passa tra i nodi in ogni host tenta tooacquire più lease. 

Nell'esempio di codice hello, utilizziamo un toocreate di classe (DocumentFeedObserverFactory.cs) factory un osservatore e hello `RegistObserverFactoryAsync` osservatore hello tooregister. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Con il passare del tempo, viene stabilito un equilibrio. Questa funzionalità dinamica consente basata sulla CPU tooconsumers toobe applicata la scalabilità automatica per la scalabilità verticale e scalabilità verticale. Se le modifiche sono disponibili nel database di Azure Cosmos con maggiore frequenza rispetto ai consumer possono elaborare, aumento della CPU hello sui consumer può essere utilizzato toocause scalabilità automatica sul numero di istanze di lavoro.

## <a name="next-steps"></a>Passaggi successivi
* Provare a hello [Azure Cosmos DB modifica feed esempi di codice su GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Iniziare a scrivere codice con hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/).
