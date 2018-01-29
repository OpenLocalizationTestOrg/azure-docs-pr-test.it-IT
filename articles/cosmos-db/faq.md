---
title: Domande frequenti su Azure Cosmos DB | Microsoft Docs
description: "Risposte alle domande frequenti su Azure Cosmos DB, un servizio di database multimodello distribuito a livello globale. Informazioni su capacità, livelli di prestazioni e scalabilità."
keywords: Domande sui database - Domande frequenti, documentdb, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2018
ms.author: mimig
ms.openlocfilehash: 0f7998ca4000a4ccfd77b173cb3dd9756b4777ae
ms.sourcegitcommit: 828cd4b47fbd7d7d620fbb93a592559256f9d234
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/18/2018
---
# <a name="azure-cosmos-db-faq"></a>Domande frequenti su Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Nozioni fondamentali su Azure Cosmos DB
### <a name="what-is-azure-cosmos-db"></a>Che cos'è Azure Cosmos DB?
Azure Cosmos DB è un servizio di database multimodello con replica globale che offre avanzate funzionalità di query sui dati privi di schema e consente di ottenere prestazioni configurabili e affidabili e un rapido sviluppo. Tutti questi vantaggi sono garantiti da una piattaforma gestita supportata dalla potenza e dalla copertura di Microsoft Azure. 

Azure Cosmos DB è la soluzione ideale per applicazioni Web, per dispositivi mobili, di gioco e IoT in cui velocità effettiva prevedibile, disponibilità elevata, bassa latenza e un modello di dati privo di schema sono requisiti chiave. Offre flessibilità dello schema e indicizzazione avanzata e include il supporto di transazioni su più documenti con JavaScript integrato. 

Per altre domande sui database, risposte e istruzioni per la distribuzione e l'uso di questo servizio, vedere la pagina [Documentazione di Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/).

### <a name="what-happened-to-the-documentdb-api"></a>Che cosa è successo all'API DocumentDB?

L'API SQL (DocumentDB) o API DocumentDB di Azure Cosmos DB è ora denominata API SQL di Azure Cosmos DB. Non è necessaria alcuna modifica per continuare a eseguire le app compilate con l'API DocumentDB. Le funzionalità rimangono invariate.

Se in precedenza si aveva un account dell'API DocumentDB, adesso si ha un account dell'API SQL senza alcun cambiamento nella fatturazione. 

### <a name="what-happened-to-azure-documentdb-as-a-service"></a>Che cosa è successo ad Azure DocumentDB come servizio?

Il servizio Azure DocumentDB è ora incluso nel servizio Azure Cosmos DB e viene visualizzato come API SQL. Le applicazioni basate su Azure DocumentDB verranno eseguite senza modifiche nell'API SQL di Azure Cosmos DB. Azure Cosmos DB supporta anche l'API Graph, l'API Tabelle, l'API MongoDB e l'API Cassandra (anteprima).

### <a name="what-are-the-typical-use-cases-for-azure-cosmos-db"></a>Quali sono i casi d'uso tipici per Azure Cosmos DB?
Azure Cosmos DB è la scelta ideale per le nuove applicazioni Web, per dispositivi mobili, di gioco e IoT in cui scalabilità automatica, prestazioni prevedibili, tempi di risposta rapidi nell'ordine di millisecondi e la possibilità di eseguire query su dati privi di schema sono importanti. Azure Cosmos DB si presta allo sviluppo rapido e al supporto dell'iterazione continua dei modelli di dati delle applicazioni. Le applicazioni che gestiscono contenuto e dati generati dall'utente rappresentano [casi d'uso comuni di Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Come vengono offerte prestazioni prevedibili in Azure Cosmos DB?
Un'[unità richiesta](request-units.md) (UR) è l'unità di misura della velocità effettiva in Azure Cosmos DB. Una velocità effettiva di 1 UR corrisponde alla velocità effettiva dell'operazione GET su un documento da 1 KB. Ogni operazione in Azure Cosmos DB, incluse letture, scritture, query SQL ed esecuzioni di stored procedure, ha un valore di UR deterministico basato sulla velocità effettiva necessaria per completare l'operazione. Invece di considerare CPU, I/O e memoria e il modo in cui ognuno di essi influisce sulla velocità effettiva dell'applicazione, è possibile ragionare in termini di singola misura di UR.

Ogni contenitore di Azure Cosmos DB può essere riservato con la velocità effettiva di provisioning in termini di UR di velocità effettiva al secondo. Per applicazioni di qualsiasi dimensione, è possibile effettuare un benchmark delle singole richieste per misurarne i valori di UR ed effettuare il provisioning di un contenitore per gestire il totale delle unità richiesta tra tutte le richieste. È anche possibile aumentare o ridurre la velocità effettiva del contenitore con il variare delle esigenze dell'applicazione. Per altre informazioni sulle unità richiesta e su come determinare le esigenze a livello di contenitore, vedere [Stima delle esigenze di velocità effettiva](request-units.md#estimating-throughput-needs) e provare il [calcolatore della velocità effettiva](https://www.documentdb.com/capacityplanner). Il termine *contenitore* fa qui riferimento a una raccolta dell'API SQL, un grafo dell'API Graph, una raccolta dell'API MongoDB e una tabella dell'API Tabelle. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>In che modo Azure Cosmos DB supporta diversi modelli di dati, ad esempio chiave/valore, colonne, documenti e grafi?

I modelli di dati chiave/valore (tabella), colonne, documenti e grafi sono tutti supportati a livello nativo grazie alla progettazione ARS (atom, record e sequenze) su cui si basa Azure Cosmos DB. È facilmente possibile eseguire il mapping e la proiezione di atom, record e sequenze in diversi modelli di dati. Le API per un subset di modelli sono già disponibili (API SQL, MongoDB, Tabelle e Graph) e altre, specifiche di modelli di dati aggiuntivi, saranno disponibili in futuro.

Azure Cosmos DB ha un motore di indicizzazione indipendente dallo schema che può indicizzare automaticamente tutti i dati inseriti senza richiedere schemi o indici secondari agli sviluppatori. Il motore si basa su un set di layout di indice logici (invertiti, colonne, albero) che separano il layout di archiviazione dai sottosistemi di elaborazione di indici e query. Cosmos DB riesce anche a supportare un set di API e protocolli di trasmissione in modalità estendibile e a convertirli nel modello di dati principale (1) e nei layout di indice logici (2), supportando in modo esclusivo più modelli di dati a livello nativo.

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB è conforme alla normativa HIPAA?
Sì, Azure Cosmos DB è conforme alla normativa HIPAA. La normativa HIPAA stabilisce i requisiti per l'uso, la divulgazione e la protezione delle informazioni sanitarie personali sensibili. Per altre informazioni, visitare il [Centro protezione Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-the-storage-limits-of-azure-cosmos-db"></a>Quali sono i limiti di archiviazione di Azure Cosmos DB?
In Azure Cosmos DB non esiste alcun limite alla quantità totale di dati che può essere archiviata in un contenitore.

### <a name="what-are-the-throughput-limits-of-azure-cosmos-db"></a>Quali sono i limiti di velocità effettiva di Azure Cosmos DB?
In Azure Cosmos DB non esiste alcun limite alla velocità effettiva totale che può essere supportata da un contenitore. Lo scopo primario è distribuire il carico di lavoro in modo abbastanza uniforme tra un numero sufficientemente elevato di chiavi di partizione.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Quanto costa Azure Cosmos DB?
Per informazioni dettagliate, vedere la pagina [Prezzi di Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Gli addebiti per l'utilizzo di Azure Cosmos DB sono determinati dal numero di contenitori sottoposti a provisioning, dal numero di ore in cui i contenitori sono stati online e dalla velocità effettiva di provisioning per ogni contenitore. Il termine *contenitori* fa qui riferimento a raccolte dell'API SQL, grafi dell'API Graph, raccolte dell'API MongoDB e tabelle dell'API Tabelle. 

### <a name="is-a-free-account-available"></a>È disponibile un account gratuito?
Sì, è possibile ottenere un account gratuito per un tempo limitato, senza alcun impegno. Per iscriversi, visitare la pagina [Prova gratuitamente Azure Cosmos DB](https://azure.microsoft.com/try/cosmosdb/). Per altre informazioni, vedere [Domande frequenti su Azure Cosmos DB](#try-cosmos-db).

I nuovi utenti possono iscriversi per ottenere un [account gratuito di Azure](https://azure.microsoft.com/free/)che è valido 30 giorni e include un credito per provare tutti i servizi di Azure. Se si ha una sottoscrizione di Visual Studio, si ha anche diritto a [crediti Azure gratuiti](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) da usare per qualsiasi servizio di Azure. 

È anche possibile usare l'[emulatore di Azure Cosmos DB](local-emulator.md) per sviluppare e testare gratuitamente l'applicazione in locale, senza creare una sottoscrizione di Azure. Quando si è soddisfatti del funzionamento dell'applicazione nell'emulatore di Azure Cosmos DB, è possibile iniziare a usare l'account Azure Cosmos DB nel cloud.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Come è possibile ottenere informazioni e supporto aggiuntivi per Azure Cosmos DB?

In caso di domande tecniche, inviare un messaggio a uno di questi due forum di domande e risposte:
* [Forum MSDN](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureDocumentDB)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb). Stack Overflow è ideale per domande relative alla programmazione. Assicurarsi che la domanda sia [pertinente](https://stackoverflow.com/help/on-topic) e [specificare il numero massimo possibile di dettagli, in modo che la domanda sia chiara e sia possibile fornire una risposta](https://stackoverflow.com/help/how-to-ask). 

Per richiedere nuove funzionalità, creare una nuova richiesta in [UserVoice](https://feedback.azure.com/forums/263030-azure-cosmos-db).

Per risolvere un problema relativo all'account, inviare una [richiesta di supporto](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) nel portale di Azure.

È possibile inviare altre domande al team all'indirizzo [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). Questo non è tuttavia un alias per il supporto tecnico. 

<a id="try-cosmos-db"></a>
## <a name="try-azure-cosmos-db-subscriptions"></a>Provare gratuitamente Azure Cosmos DB

È ora possibile provare Azure Cosmos DB per un tempo limitato senza alcuna sottoscrizione, gratuitamente e senza impegno. Per registrarsi a una sottoscrizione di prova di Azure Cosmos DB, andare alla pagina [Prova gratuitamente Azure DB Cosmos](https://azure.microsoft.com/try/cosmosdb/). Questa sottoscrizione differisce dalla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/) e può essere usata in aggiunta alla versione di valutazione gratuita di Azure o a una sottoscrizione a pagamento di Azure. 

Le sottoscrizioni di prova di Azure Cosmos DB vengono visualizzate nel portale di Azure accanto alle altre sottoscrizioni associate al proprio ID utente. 

Le condizioni seguenti si applicano alle sottoscrizioni di prova di Azure Cosmos DB:

* Un contenitore per sottoscrizione per account SQL, Gremlin (API Graph) e Tabelle.
* Fino a 3 raccolte per sottoscrizione per gli account MongoDB.
* 10 GB di capacità di archiviazione.
* La replica globale è disponibile nelle seguenti [aree di Azure](https://azure.microsoft.com/regions/): Stati Uniti centrali, Europa settentrionale e Asia sudorientale
* Velocità effettiva massima di 5.000 UR/sec.
* Le sottoscrizioni scadono dopo 24 ore e possono essere estese fino a un massimo di 48 ore totali.
* Non è possibile creare ticket di supporto di Azure per gli account di prova di Azure Cosmos DB. È tuttavia previsto il supporto per i sottoscrittori con piani di supporto attivi. 

## <a name="set-up-azure-cosmos-db"></a>Configurazione di Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Come ci si iscrive ad Azure Cosmos DB?
Azure Cosmos DB è disponibile nel portale di Azure. Per prima cosa, iscriversi per ottenere una sottoscrizione di Azure. Dopo aver effettuato l'iscrizione, è possibile aggiungere un account di API SQL, API Graph, API Tabelle, API MongoDB o API Cassandra alla sottoscrizione di Azure.

### <a name="what-is-a-master-key"></a>Che cos'è una chiave master?
Una chiave master è un token di sicurezza per l'accesso a tutte le risorse di un account. Gli utenti con la chiave hanno accesso in lettura e scrittura a tutte le risorse nell'account del database. Distribuire le chiavi master con cautela. La chiave master primaria e la chiave master secondaria sono disponibili nel pannello **Chiavi** del [portale di Azure][azure-portal]. Per altre informazioni sulle chiavi, vedere [Visualizzare, copiare e rigenerare le chiavi di accesso](manage-account.md#keys).

### <a name="what-are-the-regions-that-preferredlocations-can-be-set-to"></a>Su quali aree è possibile impostare PreferredLocations? 
Il valore di PreferredLocations può essere impostato su qualsiasi area di Azure in cui è disponibile Cosmos DB. Per un elenco delle aree disponibili, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-the-world-via-the-azure-datacenters"></a>Di quali aspetti è consigliabile tenere conto quando si distribuiscono dati nel mondo tramite i data center di Azure? 
Azure Cosmos DB è presente in tutte le aree di Azure, come specificato nella pagina [Aree di Azure](https://azure.microsoft.com/regions/). Dato che si tratta del servizio di base, in ogni nuovo data center è disponibile Azure Cosmos DB. 

Quando si imposta un'area, tenere presente che Azure Cosmos DB rispetta i cloud sovrani e per enti pubblici. Di conseguenza, se si crea un account in un'area sovrana non è possibile eseguire la replica all'esterno di tale area. Analogamente, non è possibile abilitare la replica in altre località sovrane da un account esterno. 

## <a name="develop-against-the-sql-api"></a>Sviluppare con l'API SQL

### <a name="how-do-i-start-developing-against-the-sql-api"></a>Come si inizia a eseguire lo sviluppo con l'API SQL?
Per prima cosa, è necessario iscriversi per ottenere una sottoscrizione di Azure. Dopo aver ottenuto una sottoscrizione di Azure, è possibile aggiungere un contenitore dell'API SQL alla sottoscrizione di Azure. Per istruzioni sull'aggiunta di un account Azure Cosmos DB, vedere [Creare un account di database](create-sql-api-dotnet.md#create-account). 

[SDK](sql-api-sdk-dotnet.md) per .NET, Python, Node.js, JavaScript e Java. Gli sviluppatori possono anche usare le [API HTTP RESTful](/rest/api/documentdb/) per interagire con le risorse di Azure Cosmos DB da un'ampia gamma di piattaforme e linguaggi.

### <a name="can-i-access-some-ready-made-samples-to-get-a-head-start"></a>È possibile accedere a esempi già pronti per iniziare rapidamente?
In GitHub sono disponibili esempi per gli SDK [.NET](sql-api-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](sql-api-nodejs-samples.md) e [Python](sql-api-python-samples.md) per l'API SQL.


### <a name="does-the-sql-api-database-support-schema-free-data"></a>Il database dell'API SQL supporta dati privi di schema?
Sì. L'API SQL consente alle applicazioni di archiviare documenti JSON arbitrari senza hint o definizioni dello schema. I dati sono immediatamente disponibili per l'esecuzione di query tramite l'interfaccia di query SQL di Azure Cosmos DB.  

### <a name="does-the-sql-api-support-acid-transactions"></a>L'API SQL supporta le transazioni ACID?
Sì. L'API SQL supporta le transazioni tra documenti espresse come trigger e stored procedure JavaScript. L'ambito delle transazioni è limitato a una singola partizione in ogni raccolta e le transazioni vengono eseguite con semantica ACID in modalità "tutto o niente", isolate da altro codice e altre richieste utente in esecuzione contemporaneamente. Se vengono generate eccezioni tramite l'esecuzione sul lato server del codice dell'applicazione JavaScript, viene eseguito il rollback dell'intera transazione. Per altre informazioni sulle transazioni, vedere [Transazioni del programma del database](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Che cos'è una raccolta?
Una raccolta è un gruppo di documenti con la logica dell'applicazione JavaScript associata. Una raccolta è un'entità fatturabile, in cui il [costo](performance-levels.md) è determinato dalla velocità effettiva e dallo spazio di archiviazione usato. Le raccolte possono estendersi su una o più partizioni o server e possono essere ridimensionate per gestire volumi praticamente illimitati di archiviazione o velocità effettiva.

Le raccolte sono le entità di fatturazione anche per Azure Cosmos DB. Ogni raccolta viene fatturata su base oraria a seconda della velocità effettiva di provisioning e dello spazio di archiviazione usato. Per altre informazioni, vedere [Prezzi di Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Come si crea un database?
È possibile creare database usando il [portale di Azure](https://portal.azure.com), come descritto in [Aggiungere una raccolta](create-sql-api-dotnet.md#create-collection), uno degli [SDK di Azure Cosmos DB](sql-api-sdk-dotnet.md) o le [API REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Come è possibile configurare gli utenti e le autorizzazioni?
È possibile creare utenti e autorizzazioni usando uno degli [SDK per l'API di Cosmos DB](sql-api-sdk-dotnet.md) o le [API REST](/rest/api/documentdb/).  

### <a name="does-the-sql-api-support-sql"></a>L'API SQL supporta SQL?
Il linguaggio di query SQL supportato dagli account dell'API SQL è un sottoinsieme ottimizzato delle funzionalità di query supportate da SQL Server. Il linguaggio di query SQL di Azure Cosmos DB offre operatori gerarchici e relazionali avanzati ed estendibilità tramite funzioni definite dall'utente basate su JavaScript. La grammatica JSON consente la modellazione di documenti JSON come alberi con nodi con etichetta, che vengono usati sia dalle tecniche di indicizzazione automatica di Azure Cosmos DB che dal dialetto di query SQL di Azure Cosmos DB. Per informazioni sull'uso della grammatica SQL, vedere l'articolo [Query SQL][query].

### <a name="does-the-sql-api-support-sql-aggregation-functions"></a>L'API SQL supporta le funzioni di aggregazione SQL?
L'API SQL supporta l'aggregazione a bassa latenza su qualsiasi scala con le funzioni di aggregazione `COUNT`, `MIN`, `MAX`, `AVG` e `SUM` tramite la grammatica SQL. Per altre informazioni, vedere [Funzioni di aggregazione](sql-api-sql-query.md#Aggregates).

### <a name="how-does-the-sql-api-provide-concurrency"></a>Come viene offerta la concorrenza nell'API SQL?
L'API SQL supporta il controllo della concorrenza ottimistica tramite tag di entità HTTP o ETag. Ogni risorsa dell'API SQL ha un ETag, che viene impostato nel server ogni volta che un documento viene aggiornato. In tutti i messaggi di risposta sono inclusi l'intestazione ETag e il valore corrente. Gli ETag possono essere usati con l'intestazione If-Match per consentire al server di stabilire se una risorsa deve essere aggiornata. Il valore di If-Match è il valore ETag con cui eseguire il confronto. Se il valore ETag corrisponde al valore ETag del server, la risorsa verrà aggiornata. Se l'ETag non è aggiornato, il server rifiuta l'operazione con un codice di risposta di tipo "HTTP 412 - Precondizione non riuscita". Il client recupera quindi nuovamente la risorsa per acquisire il relativo valore ETag aggiornato. Inoltre, gli ETag possono essere usati con l'intestazione If-None-Match per stabilire se è necessario ripetere il recupero di una risorsa.

Per applicare la concorrenza ottimistica in .NET, usare la classe [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) . Per un esempio .NET, vedere [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) nell'esempio DocumentManagement in GitHub.

### <a name="how-do-i-perform-transactions-in-the-sql-api"></a>Come si eseguono le transazioni nell'API SQL?
L'API SQL supporta le transazioni Language Integrated tramite trigger e stored procedure JavaScript. Tutte le operazioni su database negli script vengono eseguite con isolamento dello snapshot. In caso di raccolta con partizione singola, l'ambito dell'esecuzione è limitato alla raccolta. Se la raccolta è partizionata, l'ambito dell'esecuzione è limitato ai documenti con lo stesso valore di chiave di partizione all'interno della raccolta. Viene acquisito uno snapshot delle versioni (ETag) del documento all'inizio della transazione e il commit della transazione viene eseguito solo se lo script ha esito positivo. Se JavaScript genera un errore, viene eseguito il rollback della transazione. Per altre informazioni, vedere [Programmazione JavaScript lato server per Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Come è possibile eseguire inserimenti in blocco in Cosmos DB?
È possibile eseguire l'inserimento in blocco di documenti in Azure Cosmos DB in uno dei due modi seguenti:

* Strumento di migrazione dei dati, descritto in [Strumento di migrazione dei database per Azure Cosmos DB](import-data.md).
* Stored procedure, descritte in [Programmazione JavaScript lato server per Azure Cosmos DB](programming.md).

### <a name="does-the-sql-api-support-resource-link-caching"></a>L'API SQL supporta la memorizzazione nella cache dei collegamenti alle risorse?
Sì. Dato che Azure Cosmos DB è un servizio RESTful, i collegamenti alle risorse sono immutabili e possono essere memorizzati nella cache. I client dell'API SQL possono specificare un'intestazione "If-None-Match" per le letture su qualsiasi raccolta o documento di tipo risorsa e quindi aggiornare le copie locali in seguito alla modifica della versione del server.

### <a name="is-a-local-instance-of-sql-api-available"></a>È disponibile un'istanza locale dell'API SQL?
Sì. L'[emulatore di Azure Cosmos DB](local-emulator.md) offre un'emulazione estremamente fedele del servizio Cosmos DB. Supporta le stesse funzionalità di Azure Cosmos DB, incluso il supporto per la creazione e l'esecuzione di query su documenti JSON, il provisioning e il ridimensionamento delle raccolte e l'esecuzione di stored procedure e trigger. È possibile sviluppare e testare le applicazioni usando l'emulatore di Azure Cosmos DB e distribuirle in Azure su scala globale apportando una singola modifica di configurazione all'endpoint di connessione per Azure Cosmos DB.

## <a name="develop-against-the-api-for-mongodb"></a>Sviluppo con l'API per MongoDB
### <a name="what-is-the-azure-cosmos-db-api-for-mongodb"></a>Che cos'è l'API di Azure Cosmos DB per MongoDB?
L'API di Azure Cosmos DB per MongoDB è un livello di compatibilità che consente alle applicazioni di comunicare in modo facile e trasparente con il motore di database nativo di Azure Cosmos DB usando le API e i driver di Apache MongoDB supportati dalla community. Gli sviluppatori possono ora usare le catene di strumenti e le competenze esistenti di MongoDB per creare applicazioni che sfruttano Azure Cosmos DB. Gli sviluppatori possono trarre vantaggio dalle funzionalità specifiche di Azure Cosmos DB, tra cui l'indicizzazione automatica, la manutenzione di backup, i contratti di servizio con supporto finanziario e così via.

### <a name="how-do-i-connect-to-my-api-for-mongodb-database"></a>Come ci si connette al database dell'API per MongoDB?
Il modo più veloce per connettersi all'API di Azure Cosmos DB per MongoDB consiste nel passare al [portale di Azure](https://portal.azure.com). Accedere al proprio account e quindi fare clic su **Avvio rapido** nel menu di spostamento a sinistra. Avvio rapido è l'approccio ottimale per ottenere i frammenti di codice per la connessione al database. 

Azure Cosmos DB applica standard e requisiti di sicurezza rigidi. Gli account Azure Cosmos DB richiedono l'autenticazione e la comunicazione sicura tramite SSL. Assicurarsi quindi di usare TLSv1.2.

Per altre informazioni, vedere l'articolo su come [connettersi al database dell'API per MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Sono disponibili codici errore aggiuntivi per un database dell'API per MongoDB?
Oltre ai codici errore comuni di MongoDB, l'API per MongoDB include codici errore specifici:


| Tipi di errore               | Codice  | DESCRIZIONE  | Soluzione  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | Il numero totale di unità richiesta utilizzate ha superato il livello di unità richiesta di cui è stato effettuato il provisioning per la raccolta ed è stata applicata la limitazione. | Valutare la possibilità di ridimensionare la velocità effettiva della raccolta dal portale di Azure o provare di nuovo. |
| ExceededMemoryLimit | 16501 | In quanto servizio multi-tenant, l'operazione ha superato il limite di allocazione di memoria del client. | Ridurre l'ambito dell'operazione tramite criteri di query più restrittivi oppure contattare il supporto tecnico dal [portale di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Esempio: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-the-table-api"></a>Sviluppare con l'API Tabelle

### <a name="how-can-i-use-the-table-api-offering"></a>Come si può usare l'offerta API Tabelle? 
L'API Table di Azure Cosmos DB è disponibile nel [portale di Azure][azure-portal]. Per prima cosa, è necessario iscriversi per ottenere una sottoscrizione di Azure. Dopo aver effettuato l'iscrizione, è possibile aggiungere un account API Table di Azure Cosmos DB alla sottoscrizione di Azure e quindi aggiungere tabelle all'account. 

Per informazioni sui linguaggi supportati e sulle guide introduttive associate, vedere [Introduzione all'API Tabelle di Azure Cosmos DB](table-introduction.md).

### <a name="do-i-need-a-new-sdk-to-use-the-table-api"></a>È necessario un nuovo SDK per usare l'API Tabelle? 
No, gli SDK di archiviazione esistenti dovrebbero funzionare ancora. È tuttavia consigliabile ottenere sempre gli SDK più recenti per assicurare il supporto migliore e in molti casi prestazioni superiori. Per un elenco dei linguaggi supportati, vedere [Introduzione all'API Tabelle di Azure Cosmos DB](table-introduction.md).

### <a name="where-is-table-api-not-identical-with-azure-table-storage-behavior"></a>Quali sono le differenze tra il comportamento dell'API Tabelle e quello dell'archiviazione tabelle di Azure?
Esistono alcune differenze a livello di comportamento che gli utenti di archiviazione tabelle di Azure che vogliono creare tabelle con l'API Tabelle di Azure Cosmos DB devono tenere in considerazione:

* L'API Tabelle di Azure Cosmos DB usa un modello di capacità riservata per assicurare prestazioni garantite, ma ciò comporta il pagamento della capacità non appena viene creata la tabella, anche se la capacità non viene usata. L'archiviazione tabelle di Azure prevede solo il pagamento della capacità effettivamente usata. Questo è il motivo per cui l'API Tabelle può offrire un contratto di servizio con 10 ms di lettura e 15 ms di scrittura al 99% mentre l'archiviazione tabelle di Azure offre un contratto di servizio con 10 secondi. Con l'API Tabelle, tuttavia, sono previsti costi anche per le tabelle vuote senza richieste, in modo da assicurare che sia disponibile la capacità per la gestione di eventuali richieste in base al contratto di servizio offerto da Azure Cosmos DB.
* I risultati delle query restituiti dall'API Tabelle non vengono ordinati in base a chiave di partizione/chiave di riga, come avviene in archiviazione tabelle di Azure.
* Le chiavi di riga possono avere una dimensione massima di 255 byte.
* I batch possono contenere solo fino a 2 MB
* CORS non è attualmente supportato.
* I nomi di tabella nell'archiviazione tabelle di Azure non rispettano la distinzione tra maiuscole e minuscole, ma tale distinzione viene rispettata nell'API Tabelle di Azure Cosmos DB.
* Alcuni dei formati interni di Azure Cosmos DB per le informazioni di codifica, ad esempio i campi binari, non offrono attualmente l'efficienza auspicabile. Di conseguenza questo può causare limitazioni impreviste per le dimensioni dei dati. Ad esempio, attualmente non è possibile usare l'intero MB di un'entità tabella per archiviare i dati binari, perché la codifica incrementa le dimensioni dei dati.

Per quanto riguarda l'API REST, sono disponibili alcune opzioni relative a endpoint/query non supportate dall'API Tabelle di Azure Cosmos DB:
| Metodi REST | Opzione relativa a endpoint/query REST | URL della documentazione | Spiegazione |
| ------------| ------------- | ---------- | ----------- |
| GET, PUT | /?restype=service@comp=properties| [Set Table Service Properties](https://docs.microsoft.com/rest/api/storageservices/set-table-service-properties) (Operazione Set Table Service Properties) [Get Table Service Properties](https://docs.microsoft.com/rest/api/storageservices/get-table-service-properties) (Operazione Get Table Service Properties) | Questo endpoint viene usato per configurare le regole CORS, la configurazione di analisi di archiviazione e le impostazioni di registrazione. CORS non è attualmente supportato e l'analisi e la registrazione vengono gestite in modo diverso in Azure Cosmos DB rispetto ad archiviazione tabelle di Azure. |
| OPTIONS | /<table-resource-name> | [Pre-flight CORS table request](https://docs.microsoft.com/rest/api/storageservices/preflight-table-request) (Operazione Pre-flight CORS table request) | Questa è una parte di CORS che non è attualmente supportata da Azure Cosmos DB. |
| GET | /?restype=service@comp=stats | [Get Table Service Stats](https://docs.microsoft.com/rest/api/storageservices/get-table-service-stats) (Operazione Get Table Service Stats) | Fornisce informazioni sulla velocità con cui i dati vengono replicati tra il server primario e i server secondari. Non è necessario in Cosmos DB perché la replica fa parte delle operazioni di scrittura. |
| GET, PUT | /mytable?comp=acl | [Get Table ACL](https://docs.microsoft.com/rest/api/storageservices/get-table-acl) (Operazione Get Table ACL) e [Set Table ACL](https://docs.microsoft.com/rest/api/storageservices/set-table-acl) (Operazione Set Table ACL) | Ottiene e configura i criteri di accesso archiviati usati per gestire le firme di accesso condiviso. Anche se la firma di accesso condiviso è supportata, viene configurata e gestita in modo diverso. |

L'API Tabelle di Azure Cosmos DB supporta inoltre il formato JSON, non ATOM.

Nonostante Azure Cosmos DB supporti le firme di accesso condiviso, non supporta alcuni criteri, in particolare i criteri correlati alle operazioni di gestione, ad esempio il diritto di creare nuove tabelle.

Per .NET SDK in particolare alcune classi e alcuni metodi non sono attualmente supportati da Azure Cosmos DB.

| Classe | Metodo non supportato |
|-------|-------- |
| CloudTableClient | \*ServiceProperties* |
|                  | \*ServiceStats* |
| CloudTable | SetPermissions* |
|            | GetPermissions* |
| TableServiceContext | * (questa classe è in effetti deprecata) |
| TableServiceEntity | " " |
| TableServiceExtensions | " " |
| TableServiceQuery | " " |

Se queste differenze costituiscono un problema per il progetto, contattare [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) e segnalare il problema.

### <a name="how-do-i-provide-feedback-about-the-sdk-or-bugs"></a>Come si forniscono commenti e suggerimenti sull'SDK o sui bug?
È possibile condividere commenti e suggerimenti in uno dei modi seguenti:

* [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Forum MSDN](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureDocumentDB)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb). Stack Overflow è ideale per domande relative alla programmazione. Assicurarsi che la domanda sia [pertinente](https://stackoverflow.com/help/on-topic) e [specificare il numero massimo possibile di dettagli, in modo che la domanda sia chiara e sia possibile fornire una risposta](https://stackoverflow.com/help/how-to-ask).

### <a name="what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-table-api"></a>Quale stringa di connessione è necessario usare per connettersi all'API Tabelle?
La stringa di connessione è:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountName>.table.cosmosdb.azure.com
```
È possibile ottenere la stringa di connessione nella pagina Stringa di connessione del portale di Azure. 

### <a name="how-do-i-override-the-config-settings-for-the-request-options-in-the-net-sdk-for-the-table-api"></a>Come si sostituiscono le impostazioni di configurazione per le opzioni relative alle richieste in .NET SDK per l'API Tabelle?
Per informazioni sulle impostazioni di configurazione, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Alcune impostazioni vengono gestite nel metodo CreateCloudTableClient e altre tramite il file app.config nella sezione appSettings dell'applicazione client.

### <a name="are-there-any-changes-for-customers-who-are-using-the-existing-azure-table-storage-sdks"></a>Sono stati introdotti cambiamenti per i clienti che usano gli SDK di archiviazione tabelle di Azure?
No. Non è stato introdotto alcun cambiamento per i clienti nuovi o esistenti che usano gli SDK di archiviazione tabelle di Azure esistenti. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-the-table-api"></a>Come si visualizzano i dati di tabella archiviati in Azure Cosmos DB da usare con l'API Tabelle? 
Per esplorare i dati si può usare il portale di Azure. È anche possibile usare il codice dell'API Tabelle o gli strumenti illustrati nella risposta successiva. 

### <a name="which-tools-work-with-the-table-api"></a>Quali strumenti è possibile usare con l'API Tabelle? 
È possibile usare [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).

La nuova API Tabelle è supportata dagli strumenti sufficientemente flessibili da accettare una stringa di connessione nel formato specificato in precedenza. Per un elenco degli strumenti di tabella, vedere la pagina [Strumenti client di Archiviazione di Azure](../storage/common/storage-explorers.md). 

### <a name="do-powershell-or-azure-cli-work-with-the-table-api"></a>È possibile usare PowerShell o l'interfaccia della riga di comando di Azure con l'API Tabelle?
È disponibile il supporto per [PowerShell](table-powershell.md). Il supporto per l'interfaccia della riga di comando di Azure non è attualmente disponibile.

### <a name="is-the-concurrency-on-operations-controlled"></a>La concorrenza nelle operazioni è controllata?
Sì. La concorrenza ottimistica è supportata tramite l'uso del meccanismo degli ETag. 

### <a name="is-the-odata-query-model-supported-for-entities"></a>È supportato il modello di query OData per le entità? 
Sì. L'API Tabelle supporta query OData e query LINQ. 

### <a name="can-i-connect-to-azure-table-storage-and-azure-cosmos-db-table-api-side-by-side-in-the-same-application"></a>È supportata la connessione affiancata tra archiviazione tabelle di Azure e l'API Tabelle di Azure Cosmos DB? 
Sì. È possibile connettersi creando due istanze separate di CloudTableClient, ognuna delle quali punta a un URI specifico tramite la stringa di connessione.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-to-this-offering"></a>Come si esegue la migrazione di un'applicazione di archiviazione tabelle di Azure esistente a questa offerta?
Sono supportati [AzCopy](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy) e l'[Utilità di migrazione dati di Azure Cosmos DB](import-data.md).

### <a name="how-is-expansion-of-the-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-to-1-tb-over-time"></a>Come si espandono le dimensioni di archiviazione per questo servizio, se ad esempio *n* GB di dati iniziali crescono nel tempo fino a 1 TB? 
Azure Cosmos DB è progettato per offrire spazio di archiviazione illimitato tramite scalabilità orizzontale. Il servizio può monitorare e aumentare efficacemente lo spazio di archiviazione. 

### <a name="how-do-i-monitor-the-table-api-offering"></a>Come si monitora l'offerta dell'API Tabelle?
È possibile usare il riquadro **Metriche** dell'API Tabelle per monitorare le richieste e l'utilizzo dello spazio di archiviazione. 

### <a name="how-do-i-calculate-the-throughput-i-require"></a>Come si calcola la velocità effettiva necessaria?
È possibile usare lo strumento di stima della capacità per calcolare il valore di TableThroughput necessario per le operazioni. Per altre informazioni, vedere [Estimate Request Units and Data Storage](https://www.documentdb.com/capacityplanner) (Stimare le unità richiesta e l'archiviazione dei dati). In generale, è possibile rappresentare un'entità in formato JSON e specificare i numeri relativi alle operazioni. 

### <a name="can-i-use-the-table-api-sdk-locally-with-the-emulator"></a>È possibile usare l'SDK dell'API Tabelle in locale con l'emulatore?
Attualmente non è possibile.

### <a name="can-my-existing-application-work-with-the-table-api"></a>È possibile usare un'applicazione esistente con l'API Tabelle? 
Sì, è supportata la stessa API.

### <a name="do-i-need-to-migrate-my-existing-azure-table-storage-applications-to-the-sdk-if-i-do-not-want-to-use-the-table-api-features"></a>È necessario eseguire la migrazione delle applicazioni di archiviazione tabelle di Azure esistenti all'SDK se non si vogliono usare le funzionalità dell'API Tabelle?
No. È possibile creare e usare asset di archiviazione tabelle di Azure esistenti senza interruzioni di alcun tipo. Se non si usa l'API Tabelle, tuttavia, non è possibile usufruire dell'indicizzazione automatica, dell'opzione di coerenza aggiuntiva o della distribuzione globale. 

### <a name="how-do-i-add-replication-of-the-data-in-the-table-api-across-multiple-regions-of-azure"></a>Come si aggiunge la replica dei dati nell'API Tabelle in più aree di Azure?
È possibile usare le [impostazioni di replica globale](tutorial-global-distribution-sql-api.md#portal) del portale di Azure Cosmos DB per aggiungere le aree idonee per l'applicazione. Per sviluppare un'applicazione distribuita a livello globale, è consigliabile anche aggiungere l'applicazione con il valore di PreferredLocation impostato sull'area locale, per garantire una bassa latenza di lettura. 

### <a name="how-do-i-change-the-primary-write-region-for-the-account-in-the-table-api"></a>Come si modifica l'area di scrittura primaria per l'account nell'API Tabelle?
È possibile usare il riquadro del portale relativo alla replica globale di Azure Cosmos DB per aggiungere un'area e quindi effettuare il failover nell'area necessaria. Per istruzioni, vedere l'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Come si configurano le aree di lettura preferite per una bassa latenza quando si distribuiscono i dati? 
Per facilitare la lettura dalla località locale, usare la chiave PreferredLocation nel file app.config. Per le applicazioni esistenti, l'API Tabelle genera un errore in caso di impostazione di LocationMode. Rimuovere tale codice, perché l'API Tabelle acquisisce queste informazioni dal file app.config. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-the-table-api"></a>Come funzionano i livelli di coerenza nell'API Tabelle? 
Azure Cosmos DB offre compromessi ben ponderati tra coerenza, disponibilità e latenza. Azure Cosmos DB offre cinque livelli di coerenza per gli sviluppatori che usano l'API Tabelle, consentendo così di scegliere il modello di coerenza appropriato a livello di tabella ed effettuare singole richieste durante l'esecuzione di query sui dati. Quando un client si connette, può specificare un livello di coerenza. È possibile modificare il livello tramite l'argomento consistencyLevel di CreateCloudTableClient. 

L'API Tabelle offre letture a bassa latenza con la "lettura delle proprie scritture", con la coerenza con obsolescenza associata come impostazione predefinita. Per altre informazioni, vedere l'articolo relativo ai [livelli di coerenza](consistency-levels.md). 

Per impostazione predefinita, l'archivio tabelle di Azure offre coerenza assoluta all'interno di un'area e coerenza finale nelle località secondarie. 

### <a name="does-azure-cosmos-db-table-api-offer-more-consistency-levels-than-azure-table-storage"></a>L'API Tabelle di Azure Cosmos DB offre più livelli di coerenza rispetto all'archiviazione tabelle di Azure?
Sì. Per informazioni su come trarre vantaggio dalla natura distribuita di Azure Cosmos DB, vedere l'articolo relativo ai [livelli di coerenza](consistency-levels.md). Grazie alle garanzie associate ai livelli di coerenza, possono essere usati in tutta sicurezza. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-to-replicate-the-data"></a>Quando è abilitata la distribuzione globale, quanto tempo è necessario per replicare i dati?
Azure Cosmos DB esegue il commit permanente dei dati nell'area locale e ne effettua immediatamente il push in altre aree, nell'arco di millisecondi. Questa replica dipende solo dal tempo di round trip del data center. Per altre informazioni sulla funzionalità di distribuzione globale di Azure Cosmos DB, vedere l'articolo relativo ad [Azure Cosmos DB come servizio di database distribuito a livello globale in Azure](distribute-data-globally.md).

### <a name="can-the-read-request-consistency-level-be-changed"></a>È possibile modificare il livello di coerenza delle richieste di lettura?
Con Azure Cosmos DB, è possibile impostare il livello di coerenza a livello di contenitore (nella tabella). Usando .NET SDK, si può modificare il livello specificando il valore della chiave TableConsistencyLevel nel file app.config. I valori possibili sono: Strong, Bounded Staleness, Session, Consistent Prefix ed Eventual. Per altre informazioni, vedere [Livelli di coerenza dei dati ottimizzabili in Azure Cosmos DB](consistency-levels.md). Il concetto chiave è che non è possibile impostare un livello di coerenza delle richieste superiore rispetto all'impostazione della tabella. Ad esempio, non è possibile impostare il livello di coerenza Eventual per la tabella e il livello di coerenza Strong per le richieste. 

### <a name="how-does-the-table-api-handle-failover-if-a-region-goes-down"></a>Come viene gestito il failover dall'API Tabelle se un'area diventa inattiva? 
L'API Tabelle sfrutta i vantaggi della piattaforma distribuita a livello globale di Azure Cosmos DB. Affinché l'applicazione possa tollerare i tempi di inattività del data center, abilitare almeno un'altra area per l'account nel portale di Azure Cosmos DB, come illustrato nell'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). Si può impostare la priorità dell'area usando il portale. Vedere l'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). 

È possibile aggiungere il numero di aree desiderato per l'account e controllare in quale potrà essere effettuato il failover specificando una priorità di failover. Per usare il database, è necessario includere anche un'applicazione. Nel corso di questa operazione, i clienti non riscontrano tempi di inattività. A differenza degli altri SDK, l'[SDK client .NET più recente](table-sdk-dotnet.md) include l'hosting automatico. ovvero può rilevare l'area inattiva ed effettuare automaticamente il failover nella nuova area.

### <a name="is-the-table-api-enabled-for-backups"></a>L'API Tabelle è abilitata per il backup?
Sì, l'API Tabelle sfrutta i vantaggi della piattaforma di Azure Cosmos DB per i backup. I backup vengono eseguiti automaticamente. Per altre informazioni, vedere [Backup online automatico e ripristino con Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-the-table-api-index-all-attributes-of-an-entity-by-default"></a>L'API Tabelle indicizza tutti gli attributi di un'entità per impostazione predefinita?
Sì. Per impostazione predefinita vengono indicizzati tutti gli attributi di un'entità. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-to-create-multiple-indexes-to-satisfy-the-queries"></a>Per soddisfare le query è quindi necessario creare più indici? 
Sì. L'API Tabelle di Azure Cosmos DB offre l'indicizzazione automatica di tutti gli attributi senza definizione di schema. Questa automazione consente agli sviluppatori di concentrarsi sull'applicazione anziché sulla creazione e sulla gestione degli indici. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).

### <a name="can-i-change-the-indexing-policy"></a>È possibile modificare i criteri di indicizzazione?
Sì. È possibile modificare i criteri di indicizzazione specificando la definizione di indice. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). È necessario eseguire correttamente la codifica e l'escape delle impostazioni. 

Per gli SDK non .NET è possibile configurare i criteri di indicizzazione solo nel portale in **Esplora dati**. Passare alla tabella specifica da modificare, quindi selezionare **Scale & Settings** (Scalabilità e impostazioni)->Criteri di indicizzazione, apportare le modifiche e quindi scegliere **Salva**.

Da .NET SDK è possibile inviare i criteri nel file app.config:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-to-have-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-to-the-table-api"></a>Come piattaforma, Azure Cosmos DB offre numerose funzionalità, come l'ordinamento, le aggregazioni, la gerarchia e così via. Queste funzionalità verranno aggiunte all'API Table? 
L'API Tabelle offre le stesse funzionalità di query dell'archiviazione tabelle di Azure. Azure Cosmos DB supporta anche l'ordinamento, le aggregazioni, le query geospaziali, la gerarchia e un'ampia gamma di funzioni predefinite. Le funzionalità aggiuntive verranno incluse nell'API Table in un aggiornamento futuro del servizio. Per altre informazioni, vedere [Query SQL](sql-api-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-the-table-api"></a>Quando è consigliabile modificare TableThroughput per l'API Tabelle?
È consigliabile modificare TableThroughput quando si verifica una delle condizioni seguenti:
* Si esegue un'operazione di estrazione, trasformazione e caricamento (ETL) di dati o si vuole caricare una grande quantità di dati in breve tempo. 
* È necessaria una velocità effettiva superiore dal contenitore al back-end. Ad esempio, si rileva che la velocità effettiva usata è superiore alla velocità effettiva di provisioning e viene applicata la limitazione. Per altre informazioni, vedere [Impostare la velocità effettiva per i contenitori di Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-the-throughput-of-my-table-api-table"></a>È possibile aumentare o ridurre la velocità effettiva di una tabella dell'API Tabelle? 
Sì. È possibile usare il riquadro relativo alla scalabilità del portale di Azure Cosmos DB per ridimensionare la velocità effettiva. Per altre informazioni, vedere l'articolo su come [impostare la velocità effettiva](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Per le tabelle appena sottoposte a provisioning viene impostato un valore predefinito di TableThroughput?
Sì. Se non si sostituisce il valore di TableThroughput in app.config e non si usa un contenitore già creato in Azure Cosmos DB, il servizio crea una tabella con velocità effettiva di 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-the-azure-table-storage-service"></a>I prezzi per i clienti esistenti del servizio archiviazione tabelle di Azure sono cambiati?
No. Il prezzo per i clienti esistenti dell'archiviazione tabelle di Azure non è cambiato. 

### <a name="how-is-the-price-calculated-for-the-table-api"></a>Come viene calcolato il prezzo per l'API Tabelle? 
Il prezzo dipende dal valore di TableThroughput allocato. 

### <a name="how-do-i-handle-any-throttling-on-the-tables-in-table-api-offering"></a>Come si gestisce l'eventuale limitazione nelle tabelle dell'offerta dell'API Tabelle? 
Se la frequenza delle richieste supera la capacità della velocità effettiva di provisioning per il contenitore sottostante, verrà restituito un errore e l'SDK ripeterà la chiamata applicando i criteri di ripetizione dei tentativi.

### <a name="why-do-i-need-to-choose-a-throughput-apart-from-partitionkey-and-rowkey-to-take-advantage-of-the-table-api-offering-of-azure-cosmos-db"></a>Perché è necessario scegliere una velocità effettiva oltre alla chiave di partizione e alla chiave di riga per sfruttare i vantaggi dell'offerta API Tabelle di Azure Cosmos DB?
Azure Cosmos DB imposta una velocità effettiva predefinita per il contenitore, se non se ne specifica una nel file app.config o tramite il portale. 

Azure Cosmos DB offre garanzie di prestazioni e latenza, con limiti superiori nelle operazioni. Questa garanzia è possibile quando il motore può applicare la governance nelle operazioni del tenant. L'impostazione di TableThroughput assicura la velocità effettiva e la latenza garantite, perché la piattaforma riserva tale capacità e garantisce l'esito positivo delle operazioni. 

È possibile usare la specifica della velocità effettiva modificandola in modo elastico per trarre vantaggio dalla stagionalità dell'applicazione, soddisfare le esigenze in termini di velocità effettiva e ridurre i costi.

### <a name="azure-table-storage-has-been-very-inexpensive-for-me-because-i-pay-only-to-store-the-data-and-i-rarely-query-the-azure-cosmos-db-table-api-offering-seems-to-be-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Archiviazione tabelle di può essere molto economico se si eseguono raramente query, perché si paga solo per l'archiviazione dei dati. Con l'offerta relativa all'API Tabelle di Azure Cosmos DB sembra che vengano effettuati addebiti anche se non si esegue alcuna transazione o non si archiviano dati. Perché?

Azure Cosmos DB è progettato come un sistema basato su contratti di servizio distribuito a livello globale con garanzie di disponibilità, latenza e velocità effettiva. La velocità effettiva riservata in Azure Cosmos DB è garantita, a differenza della velocità effettiva di altri sistemi. Azure Cosmos DB offre funzionalità aggiuntive che sono state richieste dai clienti, come gli indici secondari e la distribuzione globale.  

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-azure-table-storage-with-the-table-api-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-to-change-my-existing-application"></a>Quando si inseriscono dati nell'archiviazione tabelle di Azure, non viene mai visualizzata una notifica di raggiungimento della quota che indica che la partizione è piena. Con l'API Tabelle viene visualizzato questo messaggio. Questa offerta impone limitazioni e la modifica dell'applicazione esistente?

Azure Cosmos DB è un sistema basato su contratti di servizio che offre scalabilità illimitata, con garanzie di latenza, velocità effettiva, disponibilità e coerenza. Per assicurarsi le prestazioni Premium garantite, verificare che l'indice e le dimensioni dei dati siano gestibili e scalabili. Il limite di 10 GB per il numero di entità o elementi per chiave di partizione ha lo scopo di assicurare prestazioni di ricerca e di query elevate. Per garantire la scalabilità dell'applicazione anche per Archiviazione di Azure, è consigliabile *non* creare una partizione critica archiviando tutte le informazioni in una partizione ed eseguendo query su di essa. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-the-table-api"></a>La chiave di partizione e la chiave di riga sono ancora necessarie con l'API Tabelle? 
Sì. Dato che la superficie di attacco dell'API Tabelle è simile a quella di Azure Table Storage SDK, la chiave di partizione offre un modo efficiente per distribuire i dati. La chiave di riga è univoca all'interno della partizione. La chiave di riga deve essere presente e non può essere Null come nell'SDK standard. La chiave di riga è lunga 255 byte, mentre la chiave di partizione ha una lunghezza di 1 KB. 

### <a name="what-are-the-error-messages-for-the-table-api"></a>Quali sono i messaggi di errore per l'API Tabelle?
L'archiviazione tabelle di Azure e l'API Tabelle di Azure Cosmos DB usano gli stessi SDK, quindi la maggior parte degli errori sarà uguale.

### <a name="why-do-i-get-throttled-when-i-try-to-create-lot-of-tables-one-after-another-in-the-table-api"></a>Perché quando si prova a creare numerose tabelle una dopo l'altra nell'API Tabelle viene applicata la limitazione?
Azure Cosmos DB è un sistema basato su contratti di servizio che offre garanzie di latenza, velocità effettiva, disponibilità e coerenza. Dato che è un sistema con provisioning, riserva risorse per garantire tali requisiti. La rapida frequenza di creazione delle tabelle viene rilevata e limitata. È consigliabile esaminare la frequenza di creazione di tabelle e ridurla a meno di 5 al minuto. Tenere presente che l'API Tabelle è un sistema con provisioning. Il relativo pagamento ha inizio nel momento in cui ne viene effettuato il provisioning. 

## <a name="develop-against-the-graph-api"></a>Sviluppare con l'API Graph
### <a name="how-can-i-apply-the-functionality-of-graph-api-to-azure-cosmos-db"></a>Come si possono applicare le funzionalità dell'API Graph ad Azure Cosmos DB?
Per applicare le funzionalità dell'API Graph è possibile usare una libreria di estensioni, denominata Microsoft Azure Graphs e disponibile in NuGet. 

### <a name="it-looks-like-you-support-the-gremlin-graph-traversal-language-do-you-plan-to-add-more-forms-of-query"></a>È supportato il linguaggio per l'attraversamento di grafi Gremlin. È prevista l'aggiunta di altre forme di query?
Sì. È prevista in futuro l'aggiunta di altri meccanismi di query. 

### <a name="how-can-i-use-the-new-graph-api-offering"></a>Come si può usare la nuova offerta dell'API Graph? 
Per iniziare, vedere la guida introduttiva all'[API Graph](../cosmos-db/create-graph-dotnet.md).

<a id="cassandra"></a> 
## <a name="develop-with-the-apache-cassandra-api-preview"></a>Sviluppare con l'API Apache Cassandra (anteprima)

### <a name="what-is-the-protocol-version-supported-in-the-private-preview-is-there-a-plan-to-support-other-protocols"></a>Qual è la versione del protocollo supportata nell'anteprima privata? È previsto il supporto per altri protocolli?
L'API Apache Cassandra per Azure Cosmos DB supporta attualmente CQL versione 4. In caso di feedback sul supporto di altri protocolli, segnalarlo sul sito del [feedback UserVoice](https://feedback.azure.com/forums/263030-azure-cosmos-db) o inviare un messaggio di posta elettronica all'indirizzo [askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com). 

### <a name="why-is-choosing-a-throughput-for-a-table-a-requirement"></a>Perché la scelta di una velocità effettiva per una tabella rappresenta un requisito?
Azure Cosmos DB configura la velocità effettiva predefinita per il contenitore in base alla posizione in cui è stata creata la tabella, ovvero nel portale o in CQL. Azure Cosmos DB offre garanzie di prestazioni e latenza, con limiti superiori nelle operazioni. Questa garanzia è possibile quando il motore può applicare la governance nelle operazioni del tenant. La configurazione della velocità effettiva assicura la velocità effettiva e la latenza garantite, perché la piattaforma riserva tale capacità e garantisce l'esito positivo delle operazioni. È possibile modificare in modo flessibile la velocità effettiva per usufruire della stagionalità delle applicazioni e ridurre i costi.

Il concetto di velocità effettiva è illustrato nell'articolo [Unità richiesta in Azure Cosmos DB](request-units.md). La velocità effettiva per una tabella viene distribuita equamente tra le partizioni fisiche sottostanti.  

### <a name="what-is-the-default-rus-of-table-when-created-through-cql-what-if-i-need-to-change-it"></a>Qual è la UR/s predefinita di una tabella creata tramite CQL? In che modo la si può modificare, se necessario?
Azure Cosmos DB usa le unità richiesta al secondo (UR/s) come misura per fornire velocità effettiva. Le tabelle create con CQL hanno 400 UR. È possibile modificare le UR dal portale. 

CQL
```
CREATE TABLE keyspaceName.tablename (user_id int PRIMARY KEY, lastname text) WITH cosmosdb_provisioned_throughput=1200
```

.NET
```csharp
int provisionedThroughput = 400;
var simpleStatement = new SimpleStatement($"CREATE TABLE {keyspaceName}.{tableName} (user_id int PRIMARY KEY, lastname text)");
var outgoingPayload = new Dictionary<string, byte[]>();
outgoingPayload["cosmosdb_provisioned_throughput"] = Encoding.UTF8.GetBytes(provisionedThroughput.ToString());
simpleStatement.SetOutgoingPayload(outgoingPayload); 
``` 

### <a name="what-happens-when-throughput-is-exceeded"></a>Cosa accade quando viene superata la velocità effettiva? 
Azure Cosmos DB offre garanzie di prestazioni e latenza, con limiti superiori nelle operazioni. Questa garanzia è possibile quando il motore può applicare la governance nelle operazioni del tenant. Ciò è possibile in base alla configurazione della velocità effettiva, che assicura la velocità effettiva e la latenza garantite, perché la piattaforma riserva tale capacità e garantisce l'esito positivo delle operazioni. Quando si supera questa capacità, viene visualizzato un messaggio di errore di overload a indicare che è stata superata la capacità. 0x1001 Overloaded: the request cannot be processed because "Request Rate is large" (0x1001 In overload: impossibile elaborare la richiesta, poiché "La frequenza delle richieste è troppo elevata"). A questo punto è essenziale esaminare le operazioni che, unitamente al loro volume, determinano questo problema. È possibile avere un'idea della capacità usata che supera la capacità fornita con le metriche nel portale. È poi necessario verificare che la capacità venga usata pressoché equamente tra tutte le partizioni sottostanti. Se si nota che la maggior parte della velocità effettiva viene usata da una partizione, si è in presenza di un'asimmetria del carico di lavoro. 

Sono disponibili metriche che indicano in che modo la velocità effettiva viene usata in intervalli di ore, giorni e sette giorni, tra le partizioni o in modo aggregato. Per altre informazioni, vedere [Eseguire il monitoraggio e il debug con le metriche in Azure Cosmos DB](use-metrics.md).

I log di diagnostica sono illustrati nell'articolo [Registrazione diagnostica di Azure Cosmos DB](logging.md).

### <a name="does-the-primary-key-map-to-the-partition-key-concept-of-azure-cosmos-db"></a>La chiave primaria corrisponde al concetto di chiave di partizione di Azure Cosmos DB?
Sì, la chiave di partizione viene usata per collocare l'entità nella posizione corretta. In Azure Cosmos DB consente di individuare la partizione logica corretta archiviata in una partizione fisica. Il concetto di partizionamento è illustrato in dettaglio nell'articolo [Partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md). Il fulcro della questione è che a oggi una partizione logica non deve superare il limite di 10 GB. 

### <a name="what-happens-when-i-get-a-quota-full-notification-indicating-that-a-partition-is-full"></a>Cosa accade se viene visualizzata una notifica di raggiungimento della quota che indica che la partizione è piena?
Azure Cosmos DB è un sistema basato su contratti di servizio che offre scalabilità illimitata, con garanzie di latenza, velocità effettiva, disponibilità e coerenza. Anche l'API Cassandra consente l'archiviazione illimitata dei dati. Questo tipo di archiviazione illimitata si basa sulla scalabilità orizzontale dei dati usando il partizionamento come concetto chiave. Il concetto di partizionamento è illustrato in dettaglio nell'articolo [Partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).

È necessario rispettare il limite di 10 GB sul numero di entità o elementi per partizione logica. Per assicurare la scalabilità dell'applicazione, è consigliabile *non* creare una partizione critica archiviando tutte le informazioni in una partizione ed eseguendo query su di essa. Questo errore può verificarsi solo in presenza di dati asimmetrici, ovvero con un numero elevato di dati per una chiave di partizione, ad esempio più di 10 GB. La distribuzione dei dati è disponibile nel portale di archiviazione. Un modo per correggere l'errore consiste nel ricreare la tabella e scegliere una chiave primaria (di partizione) granulare, che consente una migliore distribuzione dei dati.

### <a name="is-it-possible-to-use-cassandra-api-as-key-value-store-with-millions-or-billions-of-individual-partition-keys"></a>È possibile usare l'API Cassandra come archivio di valori/chiavi con milioni o miliardi di singole chiavi di partizione?
Azure Cosmos DB può archiviare un numero illimitato di dati grazie alla scalabilità orizzontale di archiviazione, in modo indipendente dalla velocità effettiva. Sì, è comunque possibile usare l'API Cassandra per archiviare e recuperare chiavi e valori specificando la chiave primaria o di partizione corretta. Queste singole chiavi ottengono una specifica partizione logica e si trovano al di sopra della partizione fisica. 

### <a name="is-it-possible-to-create-multiple-tables-with-apache-cassandra-api-of-azure-cosmos-db"></a>È possibile creare più tabelle con l'API Apache Cassandra di Azure Cosmos DB?
Sì, è possibile creare più tabelle con l'API Apache Cassandra. Ogni tabella viene trattata come una singola unità per velocità effettiva e archiviazione. 

### <a name="is-it-possible-to-create-multiple-tables-in-succession"></a>È possibile creare più tabelle in successione?
Azure Cosmos DB è un sistema basato su risorse per attività a livello di dati e di controllo. I contenitori come le raccolte e le tabelle sono entità di runtime sottoposte a provisioning per una determinata capacità di velocità effettiva. La creazione di questi contenitori in rapida successione non è un'attività prevista e potrebbe essere limitata. In presenza di test che creano/eliminano tabelle immediatamente, provare a distanziarli.

### <a name="what-is-maximum-number-of-tables-which-can-be-created"></a>Qual è il numero massimo di tabelle che è possibile creare?
Non è previsto alcun limite fisico sul numero di tabelle. Inviare un messaggio di posta elettronica all'indirizzo [askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com) se è necessario creare un numero elevato di tabelle con dimensione costante totale superiore a 10 TB, rispetto alle consuete decine o centinaia. 

### <a name="what-is-the-maximum--of-keyspace-which-we-can-create"></a>Qual è il numero massimo di keyspace che è possibile creare? 
Non è previsto alcun limite fisico sul numero di keyspace, in quanto sono contenitori di metadati. Inviare un messaggio di posta elettronica all'indirizzo [ askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com) in presenza di un numero elevato di keyspace. 

### <a name="is-it-possible-to-bring-in-lot-of-data-after-starting-from-normal-table"></a>È possibile inserire una quantità elevata di dati dopo l'avvio da una tabella normale? 
La capacità di archiviazione viene gestita automaticamente e aumenta con l'inserimento di dati aggiuntivi. È quindi possibile importare tranquillamente la quantità di dati necessaria senza la gestione e il provisioning dei nodi e così via. 

### <a name="is-it-possible-to-supply-yaml-file-settings-to-configure-apache-casssandra-api-of-azure-cosmos-db-behavior"></a>È possibile fornire le impostazioni del file yaml per configurare il comportamento dell'API Apache Cassandra di Azure Cosmos DB?
L'API Apache Cassandra di Azure Cosmos DB è un servizio di piattaforma. Fornisce compatibilità a livello di protocollo per l'esecuzione di operazioni. Nasconde la complessità della gestione, del monitoraggio e della configurazione. Gli utenti e gli sviluppatori non devono preoccuparsi di disponibilità, rimozioni definitive, cache delle chiavi, cache delle righe, filtri Bloom e di molte altre impostazioni. L'API Apache Cassandra di Azure Cosmos DB fornisce le prestazioni di lettura e di scrittura necessarie, senza l'overhead della configurazione e della gestione.

### <a name="will-apache-cassandra-api-for-azure-cosmos-db-support-node-additioncluster-statusnode-status-commands"></a>L'API Apache Cassandra per Azure Cosmos DB supporterà i comandi per aggiunta nodo/stato del cluster/stato del nodo?
L'API Apache Cassandra è un servizio di piattaforma che semplifica la pianificazione della capacità e la risposta a richieste di elasticità per la velocità effettiva e le risorse di archiviazione. Con Azure Cosmos DB è possibile effettuare il provisioning della velocità effettiva necessaria. È quindi possibile aumentare o ridurre il numero di unità ogni volta che risulta necessario durante la giornata, senza doversi preoccupare di aggiungere/eliminare nodi o gestirli. Non è quindi necessario usare alcuno strumento di gestione di nodi o cluster. 

### <a name="what-happens-with-respect-to-various-config-settings-for-keyspace-creation-like-simplenetwork"></a>Che cosa accade alle diverse impostazioni di configurazione per la creazione del keyspace (semplice/rete)?
Azure Cosmos DB offre la distribuzione globale predefinita per motivi di disponibilità e di bassa latenza. Non è necessario configurare repliche. Viene eseguito il commit durevole nel quorum di tutte le operazioni di scrittura in qualsiasi area in cui vengono scritti i dati, fornendo al tempo stesso garanzie relative alle prestazioni.  

### <a name="what-happens-with-respect-to-various-settings-for-table-metadata-like-bloom-filter-caching-read-repair-change-gcgrace-compression-memtableflushperiod-etc"></a>Che cosa accade alle diverse impostazioni per i metadati di tabella come i filtri Bloom, la memorizzazione nella cache, le modifiche di correzione delle operazioni di lettura, gc_grace e memtable_flush_period di compressione e così via?
Azure Cosmos DB offre prestazioni per operazioni di lettura/scrittura e per velocità effettiva senza che sia necessario modificare le impostazioni di configurazione, evitando così il rischio di alterazioni accidentali.  

### <a name="is-time-to-live-ttl-supported-for-cassandra-tables"></a>La Durata (TTL) è supportata per le tabelle di Cassandra? 
Sì, la Durata (TTL) è supportata. 

### <a name="is-it-possible-to-monitor-node-status-replica-status-gc-and-os-parameters-earlier-with-various-tools-what-needs-to-be-monitored-now"></a>È possibile monitorare in anticipo lo stato dei nodi, lo stato delle repliche, gc e i parametri del sistema operativo con vari strumenti? Cosa deve essere monitorato ora?
Azure Cosmos DB è un servizio di piattaforma che consente di incrementare la produttività, senza doversi preoccupare della gestione e del monitoraggio dell'infrastruttura. È sufficiente occuparsi della velocità effettiva disponibile nelle metriche del portale per individuare eventuali limitazioni delle richieste e aumentare o diminuire la velocità effettiva. Monitorare i [contratti di servizio](monitor-accounts.md).
Usare la [metrica](use-metrics.md) Usare i [log di diagnostica](logging.md).

### <a name="which-client-sdks-can-work-with-apache-cassandra-api-of-azure-cosmos-db"></a>Quali SDK client possono essere usati con l'API Apache Cassandra di Azure Cosmos DB?
In anteprima privata, per i programmi client sono stati usati i driver del client di Apache Cassandra SDK, che usano CQLv3. In caso di uso di altri driver o se si verificano problemi, inviare un messaggio di posta elettronica all'indirizzo [ askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com). 

### <a name="is-composite-partition-key-supported"></a>La chiave di partizione composta è supportata?
Sì, è possibile usare la sintassi normale per creare una chiave di partizione composta. 

### <a name="can-i-use-sstable-loader-for-data-loading"></a>È possibile usare il caricatore sstable per il caricamento di dati?
No, durante l'anteprima il caricatore sstable non è supportato. 

### <a name="can-an-on-premises-cassandra-cluster-be-paired-with-azure-cosmos-dbs-apache-cassandra-api"></a>È possibile associare un cluster Cassandra locale all'API Apache Cassandra di Azure Cosmos DB?
Attualmente Azure Cosmos DB offre un'esperienza ottimizzata per l'ambiente cloud, senza l'overhead delle operazioni. Se è necessaria l'associazione, inviare un messaggio di posta elettronica all'indirizzo [askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com) con una descrizione dello scenario.

### <a name="does-cassandra-api-provide-full-backups"></a>L'API Cassandra fornisce backup completi? 
Azure Cosmos DB fornisce attualmente due backup completi gratuiti, creati a intervalli di quattro ore, in tutte le API. Non è quindi necessario configurare alcuna pianificazione dei backup. Per modificare la conservazione e la frequenza dei backup, inviare un messaggio di posta elettronica all'indirizzo [askcosmosdbcassandra@microsoft.com](mailto:askcosmosdbcassandra@microsoft.com) o aprire un caso di supporto. Informazioni sulla funzionalità di backup sono disponibili nell'articolo [Backup online automatico e ripristino con Azure Cosmos DB](online-backup-and-restore.md). 

### <a name="how-does-the-cassandra-api-account-handle-failover-if-a-region-goes-down"></a>Come viene gestito il failover dall'account dell'API Cassandra se un'area diventa inattiva? 
L'API Cassandra di Azure Cosmos DB sfrutta la piattaforma distribuita a livello globale di Azure Cosmos DB. Affinché l'applicazione possa tollerare i tempi di inattività del data center, abilitare almeno un'altra area per l'account nel portale di Azure Cosmos DB, come illustrato nell'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). Si può impostare la priorità dell'area usando il portale. Vedere l'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). 

È possibile aggiungere il numero di aree desiderato per l'account e controllare in quale potrà essere effettuato il failover specificando una priorità di failover. Per usare il database, è necessario includere anche un'applicazione. Nel corso di questa operazione, i clienti non riscontrano tempi di inattività. 

### <a name="does-the-apache-cassandra-api-index-all-attributes-of-an-entity-by-default"></a>L'API Apache Cassandra indicizza tutti gli attributi di un'entità per impostazione predefinita?
Sì, tutti gli attributi vengono indicizzati per impostazione predefinita da Azure Cosmos DB. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md). Si ottengono sempre i vantaggi delle prestazioni garantite, con indicizzazione coerente e scritture con commit nel quorum durevole. 

### <a name="does-this-mean-i-do-not-have-to-create-multiple-indexes-to-satisfy-the-queries"></a>Per soddisfare le query è quindi necessario creare più indici? 
Sì. Azure Cosmos DB offre l'indicizzazione automatica di tutti gli attributi senza definizione di schema. Questa automazione consente agli sviluppatori di concentrarsi sull'applicazione anziché sulla creazione e sulla gestione degli indici. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).

### <a name="can-i-use-the-new-cassandra-api-sdk-locally-with-the-emulator"></a>È possibile usare l'SDK della nuova API Cassandra in locale con l'emulatore?
Il supporto di questa funzionalità è previsto in futuro. 

### <a name="azure-cosmos-db-as-a-platform-seems-to-have-lot-of-capabilities-such-as-changefeed-and-other-functionality-will-these-capabilities-be-added-to-the-cassandra-api"></a>Come piattaforma, Azure Cosmos DB offre numerose funzionalità, tra cui il feed di modifiche. Queste funzionalità verranno aggiunte all'API Cassandra? 
L'API Apache Cassandra fornisce le stesse funzionalità CQL di Apache Cassandra. In futuro prevediamo la possibilità di includere il supporto per varie funzionalità.

### <a name="feature-x-of-regular-cassandra-api-is-not-working-as-today-where-can-the-feedback-be-provided"></a>Attualmente la funzionalità x dell'API Cassandra standard non funziona: dove è possibile fornire feedback?
Fornire commenti e suggerimenti sul sito del [feedback UserVoice](https://feedback.azure.com/forums/263030-azure-cosmos-db).

[azure-portal]: https://portal.azure.com
[query]: sql-api-sql-query.md
