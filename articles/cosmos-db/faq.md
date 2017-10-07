---
title: aaaAzure DB Cosmos domande frequenti | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti su Azure Cosmos DB, un servizio di database più modelli distribuiti in modo globale. Informazioni su capacità, livelli di prestazioni e scalabilità."
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
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Domande frequenti su Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Nozioni fondamentali su Azure Cosmos DB
### <a name="what-is-azure-cosmos-db"></a>Che cos'è Azure Cosmos DB?
Azure Cosmos DB è un servizio di database multimodello con replica globale che offre avanzate funzionalità di query sui dati privi di schema e consente di ottenere prestazioni configurabili e affidabili e un rapido sviluppo. Tutto avviene tramite una piattaforma gestita che è supportata da power hello e raggiunga di Microsoft Azure. 

Azure DB Cosmos è soluzione hello per videogiochi portatili, web, e applicazioni IoT quando velocità effettiva prevedibile, la disponibilità elevata, bassa latenza e un modello di dati privi di schema sono i requisiti principali. Offre flessibilità dello schema e indicizzazione avanzata e include il supporto di transazioni su più documenti con JavaScript integrato. 

Per altre domande di database, le risposte e le istruzioni per la distribuzione e l'utilizzo di questo servizio, vedere hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Quali tooDocumentDB verificato anomalo?
Hello API DocumentDB è uno dei modelli di dati e le API hello è supportato per il database di Azure Cosmos. Azure Cosmos DB supporta l'utente anche con l'API Graph (anteprima), l'API Table (anteprima) e l'API MongoDB. Per altre informazioni, vedere [Domande di clienti di DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Come ottenere l'account DocumentDB toomy nel portale di Azure hello?
Nel portale di Azure hello, clic sull'icona di Azure Cosmos DB hello nel riquadro di sinistra hello. Se si dispone di un account DocumentDB prima, ora è un account Azure Cosmos DB, con la fatturazione tooyour alcuna modifica.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Quali sono i casi di utilizzo tipici hello per Azure Cosmos DB?
Azure Cosmos DB è una buona scelta per i giochi di dispositivi mobili, web, nuovo, e applicazioni IoT in scala automatiche, prestazioni prevedibili, fast ordine millisecondo dei tempi di risposta e hello possibilità tooquery sui dati privi di schema è importante. Azure DB Cosmos presta toorapid sviluppo e il supporto di iterazione continua di hello applicazione dei modelli di data. Le applicazioni che gestiscono contenuto e dati generati dall'utente rappresentano [casi d'uso comuni di Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Come vengono offerte prestazioni prevedibili in Azure Cosmos DB?
Oggetto [unità richiesta](request-units.md) (RU) è la misura hello di velocità effettiva nel database di Azure Cosmos. Una velocità effettiva di 1 UR corrisponde toohello velocità effettiva di hello GET di un documento di 1 KB. Ogni operazione nel database di Azure Cosmos, tra cui letture, scritture, le query SQL e le esecuzioni di stored procedure, ha un valore di RU deterministico che è basato sul hello velocità effettiva richiesta toocomplete hello. Invece di considerare CPU, I/O e memoria e il modo in cui ognuno di essi influisce sulla velocità effettiva dell'applicazione, è possibile ragionare in termini di singola misura di UR.

Ogni contenitore di Azure Cosmos DB può essere riservato con la velocità effettiva di provisioning in termini di UR di velocità effettiva al secondo. Per le applicazioni di qualsiasi dimensione, è possibile effettuare un benchmark valori RU toomeasure le singole richieste e il provisioning di un totale di hello toohandle contenitore di unità di richiesta in tutte le richieste. È anche possibile applicare la scalabilità verticale o ridurre la velocità effettiva del contenitore come esigenze hello evolve l'applicazione. Per ulteriori informazioni sulle unità di richiesta e per assistenza con la determinazione del contenitore deve, vedere [stima delle esigenze di velocità effettiva](request-units.md#estimating-throughput-needs) e provare a hello [Calcolatrice di velocità effettiva](https://www.documentdb.com/capacityplanner). il termine Hello *contenitore* qui si riferisce insieme di API DocumentDB tooa toorefers, graph API Graph, raccolta di API di MongoDB e tabella tabella API. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>In che modo Azure Cosmos DB supporta diversi modelli di dati, ad esempio chiave/valore, colonne, documenti e grafi?

Chiave/valore (tabella), colonne, documenti e dati del grafico i modelli sono tutti in modo nativo è supportato a causa di hello ARS (Atom, record e delle sequenze) di progettazione che DB Cosmos Azure si basa su. Atom, record e delle sequenze possono essere facilmente mappate e proiettata toovarious i modelli di dati. Hello API per un subset di modelli sono disponibile destra ora (DocumentDB, MongoDB, tabella e sulle API Graph) e altri modelli di data tooadditional specifico sarà disponibili in hello futuro.

DB Cosmos Azure dispone di un schema indipendenti dal motore di indicizzazione in grado di indicizzare automaticamente tutti i dati di hello che inserisce senza richiedere dello schema o gli indici secondari da Developer Edition hello. il motore di Hello si basa su un set di layout logico indice (albero invertito, colonna,) cui separare il layout di archiviazione hello dall'indice hello e sottosistemi di elaborazione delle query. COSMOS DB inoltre dispone di un set di protocolli di rete e API toosupport possibilità hello in modo estendibile e convertirli in modo efficiente toohello core dati modello (1) hello indice logico layout e (2) che identifica in modo univoco in grado di supportare più modelli di dati in modo nativo .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB è conforme alla normativa HIPAA?
Sì, Azure Cosmos DB è conforme alla normativa HIPAA. HIPAA stabilisce i requisiti per hello utilizzare, divulgazione e protezione delle informazioni personali singolarmente integrità. Per ulteriori informazioni, vedere hello [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Quali sono i limiti di archiviazione hello del DB Cosmos Azure?
Non sussiste alcun limite toohello totale dei dati che è un contenitore è possibile archiviare nel database di Azure Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Quali sono i limiti di velocità effettiva hello del DB Cosmos Azure?
Non è una quantità totale di toohello alcun limite di velocità effettiva in grado di supportare un contenitore nel database di Azure Cosmos. Hello idea chiave è toodistribute il carico di lavoro approssimativamente in modo uniforme tra un numero sufficiente di chiavi di partizione.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Quanto costa Azure Cosmos DB?
Per informazioni dettagliate, vedere toohello [dettagli prezzi di Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/) pagina. Azure addebiti di utilizzo DB Cosmos sono determinati dal numero di hello di contenitori di provisioning, il numero di hello di ore erano online al contenitori hello e hello il provisioning della velocità effettiva per ogni contenitore. il termine Hello *contenitori* qui si riferisce insieme di API DocumentDB toohello, graph API Graph, raccolta MongoDB API e tabelle di API di tabella. 

### <a name="is-a-free-account-available"></a>È disponibile un account gratuito?
Se si tooAzure nuova, è possibile iscriversi a un [account gratuito di Azure](https://azure.microsoft.com/free/), che consente di 30 giorni e un tootry credito tutti i servizi di Azure hello e. Se si dispone di una sottoscrizione di Visual Studio, inoltre sono idonei per [libero crediti Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse in qualsiasi servizio di Azure. 

È inoltre possibile utilizzare hello [emulatore di Azure Cosmos DB](local-emulator.md) toodevelop e test dell'applicazione localmente per libero, senza creare una sottoscrizione di Azure. Quando si è soddisfatti delle modalità di funzionamento dell'applicazione nell'emulatore di Azure Cosmos DB hello, è possibile passare un account Azure Cosmos DB nel cloud hello toousing.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Come è possibile ottenere informazioni e supporto aggiuntivi per Azure Cosmos DB?
Se è necessario altro supporto, raggiungere toous su [Overflow dello Stack](http://stackoverflow.com/questions/tagged/azure-cosmosdb) o hello [forum MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), o si pianifica una chat personalmente con i team di progettazione di hello Azure Cosmos DB mediante l'invio di posta elettronica troppo[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Configurazione di Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Come ci si iscrive ad Azure Cosmos DB?
DB Cosmos Azure è disponibile nel portale di Azure hello. Per prima cosa, iscriversi per ottenere una sottoscrizione di Azure. Dopo aver effettuato l'iscrizione, è possibile aggiungere un'API DocumentDB, API Graph (anteprima), l'API di tabella (anteprima) o MongoDB API account tooyour sottoscrizione di Azure.

### <a name="what-is-a-master-key"></a>Che cos'è una chiave master?
Una chiave master è un tooaccess token di sicurezza di tutte le risorse per un account. Gli utenti con chiave hello avere accesso in lettura e scrittura risorse tooall nell'account di database hello. Distribuire le chiavi master con cautela. chiave master di Hello primaria e secondaria chiave master sono disponibili in hello **chiavi** blade di hello [portale di Azure][azure-portal]. Per altre informazioni sulle chiavi, vedere [Visualizzare, copiare e rigenerare le chiavi di accesso](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>Quali sono le aree hello PreferredLocations può essere impostato su? 
Hello PreferredLocations valore può essere impostato tooany di hello Azure aree geografiche in cui è disponibile DB Cosmos. Per un elenco delle aree disponibili, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>C'è nulla che consigliabile tenere conto durante la distribuzione dei dati tra HelloWorld tramite hello Data Center di Azure? 
DB Cosmos Azure è presente in tutte le aree di Azure, come specificato nella hello [aree di Azure](https://azure.microsoft.com/regions/) pagina. Poiché è il servizio di base di hello, ogni nuovo Data Center dispone di una presenza Azure Cosmos DB. 

Quando si imposta un'area, tenere presente che Azure Cosmos DB rispetta i cloud sovrani e per enti pubblici. Di conseguenza, se si crea un account in un'area sovrana non è possibile eseguire la replica all'esterno di tale area. Analogamente, non è possibile abilitare la replica in altre località sovrane da un account esterno. 

## <a name="develop-against-hello-documentdb-api"></a>Lo sviluppo utilizzando l'API DocumentDB hello

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Come avviare lo sviluppo in API DocumentDB hello?
L'API DocumentDB Microsoft è disponibile in hello [portale di Azure][azure-portal]. Per prima cosa, è necessario iscriversi per ottenere una sottoscrizione di Azure. Quando effettua l'iscrizione per una sottoscrizione di Azure, è possibile aggiungere l'API DocumentDB contenitore tooyour sottoscrizione di Azure. Per istruzioni sull'aggiunta di un account Azure Cosmos DB, vedere [Creare un account di database](create-documentdb-dotnet.md#create-account). Se si dispone di un account DocumentDB in hello precedente, ora è un account Azure Cosmos DB. 

[SDK](documentdb-sdk-dotnet.md) per .NET, Python, Node.js, JavaScript e Java. Gli sviluppatori possono inoltre utilizzare hello [RESTful API HTTP](/rest/api/documentdb/) toointeract alle risorse di Azure Cosmos DB da varie piattaforme e le lingue.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>È possibile accedere alcuni tooget esempi già pronti per iniziare?
Esempi per l'API DocumentDB hello [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), e [Python](documentdb-python-samples.md) SDK sono disponibili su GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Non hello dati privi di schema di supporto di API DocumentDB database?
Sì, hello API DocumentDB consente applicazioni toostore arbitrari documenti JSON senza hint o definizioni di schema. Dati sono immediatamente disponibili per query tramite l'interfaccia di query SQL di Azure Cosmos DB hello.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Hello API DocumentDB supporta transazioni ACID?
Sì, hello API DocumentDB supporta le transazioni tra documenti espresse come JavaScript stored procedure e trigger. Le transazioni sono tooa singola partizione all'interno di ogni raccolta di un ambito ed eseguita con semantica ACID "tutto o niente," isolati da altre richieste utente e del codice attualmente in esecuzione. Se vengono generate eccezioni quando l'esecuzione sul lato server hello JavaScript codice dell'applicazione, viene eseguito il rollback dell'intera transazione hello. Per altre informazioni sulle transazioni, vedere [Transazioni del programma del database](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>Che cos'è una raccolta?
Una raccolta è un gruppo di documenti con la logica dell'applicazione JavaScript associata. Una raccolta è un'entità fatturabile, dove hello [costo](performance-levels.md) è determinata dalla velocità effettiva di hello e utilizzata l'archiviazione. Raccolte può estendersi su una o più partizioni o i server e può essere ridimensionato toohandle praticamente illimitate di volumi di archiviazione o una velocità effettiva.

Le raccolte sono anche le entità di fatturazione hello per Azure Cosmos DB. Ogni raccolta è fatturate con tariffe orarie, in base alla velocità effettiva di provisioning hello e spazio di archiviazione utilizzato. Per altre informazioni, vedere [Prezzi di Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Come si crea un database?
È possibile creare un database utilizzando hello [portale di Azure](https://portal.azure.com), come descritto in [aggiungere una raccolta](create-documentdb-dotnet.md#create-collection), uno di hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md), o hello [API REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Come è possibile configurare gli utenti e le autorizzazioni?
È possibile creare utenti e autorizzazioni utilizzando uno dei hello [Cosmos DB API SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Hello API DocumentDB supporta SQL?
Hello linguaggio di query SQL è un subset di funzionalità di query hello è supportato da SQL avanzato. il linguaggio di query di database SQL di Azure Cosmos Hello fornisce RTF operatori relazionali e gerarchici ed estendibilità tramite le funzioni basate su JavaScript, definiti dall'utente (UDF). Consente di grammatica JSON per la modellazione di documenti JSON come alberi con nodi con etichettati, che vengono usati da tecniche di indicizzazione automatica di hello Azure Cosmos DB sia sottolinguaggio di query hello SQL di Azure Cosmos DB. Per informazioni sull'utilizzo di grammatica SQL, vedere hello [QueryDocumentDB] [ query] articolo.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Non hello funzioni di aggregazione SQL supporto API DocumentDB?
Hello API DocumentDB supporta l'aggregazione di bassa latenza su qualsiasi scala tramite le funzioni di aggregazione `COUNT`, `MIN`, `MAX`, `AVG`, e `SUM` tramite hello grammatica SQL. Per altre informazioni, vedere [Funzioni di aggregazione](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>In che modo hello API DocumentDB forniscono concorrenza?
Hello API DocumentDB supporta il controllo della concorrenza ottimistica (OCC) tramite il tag di entità HTTP o ETag. Ogni risorsa API DocumentDB ha un valore ETag e hello ETag è impostato sul server di hello ogni volta che un documento viene aggiornato. intestazione ETag Hello e il valore corrente di hello sono inclusi in tutti i messaggi di risposta. ETag è utilizzabile con hello If-Match intestazione tooallow hello server toodecide se una risorsa deve essere aggiornata. Hello valore If-Match è hello ETag valore toobe confrontato. Se il server di hello valore ETag corrisponde a hello valore ETag, risorse hello viene aggiornata. Se hello ETag non è più corrente, il server di hello Rifiuta operazione hello con un "HTTP 412 Precondizione errore" codice di risposta. client Hello recupera quindi nuovamente hello risorsa tooacquire hello valore ETag corrente per la risorsa hello. Inoltre, ETag è utilizzabile con toodetermine di intestazione If-None-Match hello se è necessario recuperare nuovamente di una risorsa.

concorrenza ottimistica in .NET, usare hello toouse [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) classe. Per un esempio .NET, vedere [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) nell'esempio di hello DocumentManagement su GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Funzionamento delle transazioni in hello API DocumentDB
Hello API DocumentDB supporta transazioni language-integrated tramite JavaScript-stored procedure e trigger. Tutte le operazioni su database negli script vengono eseguite con isolamento dello snapshot. Se è una raccolta unica partizione, l'esecuzione hello è toohello con ambito raccolta. Se la raccolta hello è partizionata, l'esecuzione hello è con ambito toodocuments con hello stesso valore di chiave di partizione insieme hello. Uno snapshot hello versioni del documento (eTag) viene eseguito all'inizio di hello della transazione hello ed eseguito il commit solo se ha esito positivo script hello. Se hello JavaScript genera un errore, viene eseguito il rollback delle transazioni hello. Per altre informazioni, vedere [Programmazione JavaScript lato server per Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Come è possibile eseguire inserimenti in blocco in Cosmos DB?
È possibile eseguire l'inserimento in blocco di documenti in Azure Cosmos DB in uno dei due modi seguenti:

* Hello dati strumento di migrazione, come descritto in [strumento di migrazione di Database per database di Azure Cosmos](import-data.md).
* Stored procedure, descritte in [Programmazione JavaScript lato server per Azure Cosmos DB](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Hello API DocumentDB supporta la memorizzazione nella cache di risorse collegamento?
Sì. Dato che Azure Cosmos DB è un servizio RESTful, i collegamenti alle risorse sono immutabili e possono essere memorizzati nella cache. Il client API DocumentDB può specificare un'intestazione "If-None-Match" per operazioni di lettura di qualsiasi tipo di risorsa documento o una raccolta, quindi aggiornare le copie locali dopo la versione di hello server è stata modificata.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>È disponibile un'istanza locale dell'API DocumentDB?
Sì. Hello [Azure Cosmos DB emulatore](local-emulator.md) fornisce un'emulazione ad alta fedeltà di hello servizio DB Cosmos. Supporta funzionalità identiche tooAzure Cosmos DB, incluso il supporto per la creazione e l'esecuzione di query su documenti JSON, provisioning e scalabilità raccolte e l'esecuzione di stored procedure e trigger. È possibile sviluppare e testare le applicazioni utilizzando l'emulatore di Azure Cosmos DB hello e distribuirli tooAzure su una scala globale effettuando una singola configurazione di modificare l'endpoint della connessione toohello per Azure Cosmos DB.

## <a name="develop-against-hello-api-for-mongodb"></a>Lo sviluppo utilizzando hello API per MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>Che cos'è Azure Cosmos DB API per MongoDB hello?
Hello Azure Cosmos DB API per MongoDB è un livello di compatibilità che consente applicazioni tooeasily e comunicazione in modo trasparente con hello native Azure Cosmos database motore di database tramite esistente, con supporto della community Apache MongoDB APIs e driver. Gli sviluppatori possono ora utilizzare MongoDB strumento catene e competenze toobuild applicazioni esistenti che sfruttano Azure Cosmos DB. Gli sviluppatori trarre vantaggio dalla funzionalità esclusive di hello come dei database Cosmos di Azure, che includono la manutenzione di backup, l'indicizzazione automatica, (finanziario sottoposti a backup service level agreement) e così via.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Come si connette toomy API per il database di MongoDB?
Hello toohello di tooconnect modo più rapido Azure Cosmos DB API per MongoDB è toohead su toohello [portale di Azure](https://portal.azure.com). Tooyour account, quindi, nel menu di navigazione sinistro hello, fare clic su **avvio rapido**. Guida introduttiva è hello migliore modo tooget frammenti tooconnect tooyour database del codice. 

Azure Cosmos DB applica standard e requisiti di sicurezza rigidi. Account di Azure DB Cosmos richiedono l'autenticazione e comunicazioni protette tramite SSL, è necessario che toouse TLSv1.2.

Per ulteriori informazioni, vedere [connettersi tooyour API per il database di MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Sono disponibili codici errore aggiuntivi per un database dell'API per MongoDB?
In aggiunta toohello MongoDB codici di errore comuni, hello MongoDB API ha un proprio i codici di errore specifico:


| Errore               | Codice  | Descrizione  | Soluzione  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | numero totale di Hello di unità di richiesta utilizzata ha superato la frequenza di unità di richiesta provisioning hello per raccolta hello ed è stato limitato. | Prendere in considerazione il ridimensionamento della velocità effettiva hello di raccolta hello da hello portale di Azure o eseguire nuovamente. |
| ExceededMemoryLimit | 16501 | Come servizio multi-tenant, operazione hello ha superato il numero di memoria del client hello. | Ridurre l'ambito hello dell'operazione di hello tramite criteri di query più restrittivi o contattare il supporto tecnico da hello [portale di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Esempio: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Sviluppo con hello tabella API (anteprima)

### <a name="terms"></a>Termini 
Hello Azure Cosmos DB: API di tabella (anteprima) fa riferimento offerta premium toohello da Azure Cosmos DB per il supporto della tabella annunciato in compilazione 2017. 

tabella standard Hello SDK è una tabella di archiviazione di Azure esistente hello SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Come è possibile utilizzare la nuova offerta tabella API (anteprima) di hello? 
API di tabelle di Azure Cosmos DB Hello è disponibile in hello [portale di Azure][azure-portal]. Per prima cosa, è necessario iscriversi per ottenere una sottoscrizione di Azure. Dopo aver effettuato l'iscrizione, è possibile aggiungere un tooyour account Azure Cosmos DB tabella API sottoscrizione di Azure e quindi aggiungere le tabelle tooyour account. 

Durante il periodo di anteprima di hello quando [SDK](../cosmos-db/table-sdk-dotnet.md) sono disponibili per .NET, è possibile iniziare completando hello [tabella API](../cosmos-db/create-table-dotnet.md) Guida introduttiva all'articolo.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>È necessario un nuovo hello di toouse SDK tabella API (anteprima)? 
Sì, hello [tabelle Premium di Azure Storage SDK (anteprima)](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) è disponibile in NuGet. Informazioni aggiuntive sono disponibili sul hello [API .NET di Azure Cosmos DB tabelle: scaricare e note sulla versione](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) pagina. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Come fornire commenti e suggerimenti su hello SDK o i bug?
È possibile condividere i commenti e suggerimenti in uno dei seguenti modi hello:

* [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Forum MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>Che cos'è una stringa di connessione hello che è necessario toouse tooconnect toohello tabella API (anteprima)?
stringa di connessione Hello è:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
È possibile ottenere la stringa di connessione hello dalla pagina di chiavi hello in hello portale di Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Come l'override le impostazioni di configurazione hello per le opzioni di richiesta di hello in hello nuova tabella API (anteprima)?
Per informazioni sulle impostazioni di configurazione, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). È possibile modificare le impostazioni di hello aggiungendoli tooapp.config nella sezione appSettings hello in un'applicazione hello client.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Per i clienti che utilizzano la tabella standard esistente hello SDK sono presenti tutte le modifiche?
Nessuna. Non sono presenti modifiche per i clienti nuovi o esistenti che utilizzano la tabella standard esistente hello SDK. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Come è possibile visualizzare i dati della tabella che viene archiviati nel database di Azure Cosmos per l'utilizzo con l'API di tabella (revisione) hello? 
È possibile utilizzare i dati di hello hello toobrowse portale Azure. È inoltre possibile utilizzare hello codice API tabella (anteprima) o strumenti hello indicati nella risposta successiva hello. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Quali strumenti sono compatibili con hello tabella API (anteprima)? 
È possibile utilizzare una versione precedente di hello di soluzioni di Azure (0.8.9).

Gli strumenti con hello flessibilità tootake una stringa di connessione nel formato hello specificato in precedenza in grado di supportare hello nuova API di tabella (anteprima). Viene fornito un elenco di strumenti tabella su hello [gli strumenti Client di archiviazione di Azure](../storage/common/storage-explorers.md) pagina. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell o Azure CLI funzionano con hello nuova tabella API (anteprima)?
Prevediamo tooadd supporto per PowerShell e CLI di Azure per l'API di tabella (anteprima). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>È la concorrenza hello per le operazioni controllate?
Sì, la concorrenza ottimistica viene fornita tramite un utilizzo hello del meccanismo di ETag hello. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>È hello il modello di query OData supportato per le entità? 
Sì, hello tabella API (anteprima) supporta query OData e query LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>È possibile connettersi toohello tabelle di Azure standard e premium nuove API di tabella (anteprima) side-by-side in hello hello stessa applicazione? 
Sì, è possibile connettersi tramite la creazione di due istanze separate di hello CloudTableClient, ognuno dei quali punta tooits proprietari URI tramite la stringa di connessione hello.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Come eseguire la migrazione un'esistente tabella Azure applicazione toothis nuova offerta di archiviazione?
tootake sfruttare la nuova offerta tabella API hello nella tabella archiviazione dati esistenti, contattare [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Che cos'è una Guida di orientamento hello per questo servizio e quando verrà è offrire altre funzionalità delle API di tabella standard?
Prevediamo tooadd supporto di SAS token, contesto del servizio, statistiche, Client side crittografia, Analitica e altre funzionalità, man mano che si procede verso GA. È possibile fornire commenti e suggerimenti in [UserVoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>È la modalità di espansione delle dimensioni di archiviazione hello eseguita per questo servizio se, ad esempio, iniziare con  *n*  too1 TB aumenterà GB di dati e i dati nel tempo? 
Azure DB Cosmos è progettato tooprovide archiviazione illimitata tramite l'utilizzo di hello di scalabilità orizzontale. monitorare servizio Hello e aumentare in modo efficiente lo spazio di archiviazione. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Modalità di monitoraggio di offerta di hello tabella API (anteprima)
È possibile utilizzare l'API di tabella (anteprima) hello **metriche** riquadro toomonitor richieste e l'utilizzo di archiviazione. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Modalità di calcolo di velocità effettiva di hello, sono necessari?
È possibile utilizzare hello toocalculate di stima della capacità hello TableThroughput necessaria per le operazioni di hello. Per altre informazioni, vedere [Estimate Request Units and Data Storage](https://www.documentdb.com/capacityplanner) (Stimare le unità richiesta e l'archiviazione dei dati). In generale, è possibile rappresentare le entità nel formato JSON e fornire numeri di hello per le operazioni. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>È possibile utilizzare hello nuova tabella API SDK in locale con l'emulatore hello (anteprima)?
Sì, è possibile utilizzare hello tabella API (anteprima) con l'emulatore locale di hello quando si utilizza hello nuovo SDK. nuovo emulatore toodownload, andare troppo[hello utilizzare Azure Cosmos DB emulatore per sviluppo locale e il testing](local-emulator.md). Hello valore StorageConnectionString in App. config deve toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>L'applicazione esistente è possibile utilizzare con hello tabella API (anteprima)? 
superficie di attacco Hello di hello nuova API di tabella (anteprima) è compatibile con hello tabella standard di Azure SDK in hello creare, eliminare, aggiornare e operazioni nell'API .NET hello di query esistente. Assicurarsi di disporre di una chiave di riga, in quanto hello tabella API (anteprima) richiede una chiave di partizione e una chiave di riga. È inoltre previsto tooadd maggiore supporto per il SDK man mano che si procede verso GA di questa offerta di servizio.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>È necessario toomigrate my toohello applicazioni basate su tabella di Azure esistente nuovo SDK se non si desidera che le funzionalità delle API di tabella (anteprima) hello toouse?
No. È possibile creare e usare asset tabella standard esistenti senza interruzioni di alcun tipo. Tuttavia, se non si utilizza hello nuova tabella API (anteprima), è non è possibile beneficiare automatici di indici hello, opzione coerenza hello o distribuzione globale. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Come è possibile aggiungere la replica dei dati hello in premium hello tabella API (anteprima) in più aree di Azure?
È possibile utilizzare un portale di Azure Cosmos DB hello [le impostazioni di replica globale](tutorial-global-distribution-documentdb.md#portal) tooadd aree che sono adatte per l'applicazione. toodevelop un'applicazione distribuita a livello globale, è necessario aggiungere l'applicazione hello PreferredLocation informazioni set toohello area locale per fornire a bassa latenza di lettura. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Cambiamento area primaria scrittura hello per conto di hello in premium hello tabella API (anteprima)
È possibile utilizzare hello Azure Cosmos DB replica globale riquadro portale tooadd un'area e quindi eseguire il failover toohello obbligatorio area. Per istruzioni, vedere l'articolo relativo allo [sviluppo con account Azure Cosmos DB tra più aree](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Come si configurano le aree di lettura preferite per una bassa latenza quando si distribuiscono i dati? 
toohelp leggere dal percorso locale hello, utilizzare il tasto di PreferredLocation hello nel file app. config hello. Per le applicazioni esistenti, hello tabella API (anteprima) genera un errore se LocationMode è impostata. Rimuovere tale codice, poiché premium hello tabella API (anteprima) preleva le informazioni dal file app. config hello. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Come è necessario considerare i livelli di coerenza in hello tabella API (anteprima)? 
Azure Cosmos DB offre compromessi ben ponderati tra coerenza, disponibilità e latenza. DB Cosmos Azure offre cinque livelli di coerenza tooTable agli sviluppatori API (anteprima), è possibile scegliere il modello di coerenza destra hello a livello di tabella hello e apportare le singole richieste durante l'esecuzione di query su dati hello. Quando un client si connette, può specificare un livello di coerenza. È possibile modificare il livello di hello tramite l'impostazione di App. config di hello per hello valore della chiave TableConsistencyLevel hello. 

Hello tabella API (anteprima) fornisce bassa latenza legge con "Leggi le proprie operazioni di scrittura," con la coerenza di sessione come valore predefinito di hello. Per altre informazioni, vedere l'articolo relativo ai [livelli di coerenza](consistency-levels.md). 

Per impostazione predefinita, archiviazione tabelle di Azure fornisce coerenza assoluta all'interno di un'area e la coerenza eventuale in posizioni secondario hello. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Azure Cosmos DB offre più livelli di coerenza rispetto alle tabelle standard?
Sì, per informazioni sulla modalità di distribuzione di natura del database di Azure Cosmos toobenefit da hello, vedere [livelli di coerenza](consistency-levels.md). Poiché per i livelli di coerenza hello vengano fornite garanzie, è possibile utilizzare con confidenza. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Quando è abilitata la distribuzione globale, quanto tempo richiede dati hello tooreplicate?
È commit dati hello in modo durevole nell'area locale hello e push hello tooother aree dati immediatamente pochi millisecondi. Questa replica dipende solo hello tempo di round trip (RTT) del Data Center hello. toolearn ulteriori informazioni su capacità di hello distribuzione globale di Azure Cosmos DB, vedere [DB Cosmos Azure: un servizio di database distribuita a livello globale in Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Può essere modificato livello di coerenza di richiesta di lettura hello?
Con Azure Cosmos DB, è possibile impostare il livello di coerenza hello a livello di contenitore hello (nella tabella di hello). Utilizzando hello SDK, è possibile modificare il livello di hello fornendo hello valore per la chiave TableConsistencyLevel nel file app. config hello. Hello i valori possibili sono: sicuro, con obsolescenza associata, sessione, il prefisso coerente e finale. Per altre informazioni, vedere [Livelli di coerenza dei dati ottimizzabili in Azure Cosmos DB](consistency-levels.md). concetto chiave Hello è che è possibile impostare la coerenza richiesta hello livello a più di impostazione hello per tabella hello. Ad esempio, è possibile impostare hello livello di coerenza per la tabella hello all'eventuale e hello richiesta coerenza al sicuro. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Come account dell'API di tabella (anteprima) premium hello gestite failover se si arresta un'area? 
premium Hello tabella API (anteprima) acquisisce da piattaforma distribuita a livello globale di hello di Azure Cosmos DB. tooensure che l'applicazione può tollerare i tempi di inattività Data Center, abilitare almeno un'area più account hello nel portale di Azure Cosmos DB hello [allo sviluppo con gli account di Azure Cosmos DB multiarea](regional-failover.md). È possibile impostare la priorità hello dell'area di hello tramite il portale di hello [allo sviluppo con gli account di Azure Cosmos DB multiarea](regional-failover.md). 

È possibile aggiungere il numero di aree come account hello e di controllo in cui è possibile eseguire il failover tooby fornendo una priorità di failover. Naturalmente, database hello toouse, è necessario troppo tooprovide un'applicazione non esiste. Nel corso di questa operazione, i clienti non riscontrano tempi di inattività. SDK client Hello viene automaticamente uno spostamento. Ovvero è possibile rilevare area hello verso il basso e automaticamente il failover toohello nuova area.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Premium hello tabella API (anteprima) è abilitato per i backup?
Sì, premium hello tabella API (anteprima) è mutuato dal piattaforma hello del DB Cosmos Azure per i backup. I backup vengono eseguiti automaticamente. Per altre informazioni, vedere [Backup online automatico e ripristino con Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello tabella API (anteprima) indicizza tutti gli attributi di un'entità per impostazione predefinita?
Sì. Per impostazione predefinita vengono indicizzati tutti gli attributi di un'entità. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Questo significa non si dispone di toocreate query di più indici toosatisfy hello? 
Sì. Azure Cosmos DB offre l'indicizzazione automatica di tutti gli attributi senza definizione di schema. Questa automazione libera toofocus gli sviluppatori in un'applicazione hello anziché sulla gestione e la creazione dell'indice. Per altre informazioni, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>È possibile modificare i criteri di indicizzazione hello?
Sì, è possibile modificare i criteri di indicizzazione hello, fornendo la definizione di indice hello. Per altre informazioni, vedere [Funzionalità di Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). È necessario tooproperly codificare e le impostazioni di hello di escape. 

In formato json di stringhe nel file app. config hello:
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

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure DB Cosmos come piattaforma sembra toohave numerose funzionalità, ad esempio l'ordinamento, aggregazioni, gerarchia e altre funzionalità. Si aggiungerà questi toohello funzionalità API tabella? 
Nell'anteprima tabella API hello fornisce hello stessa query funzionalità come l'archiviazione tabelle di Azure. Azure Cosmos DB supporta anche l'ordinamento, le aggregazioni, le query geospaziali, la gerarchia e un'ampia gamma di funzioni predefinite. Si fornirà funzionalità aggiuntive in hello API tabelle in un futuro aggiornamento del servizio. Per altre informazioni, vedere [Query SQL per l'API di DocumentDB di Azure Cosmos DB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Quando è consigliabile modificare TableThroughput per hello tabella API (anteprima)?
È consigliabile modificare TableThroughput quando si applica una delle seguenti condizioni hello:
* Si sta eseguendo un'estrazione, trasformazione e caricamento (ETL) di dati o si desidera tooupload una grande quantità di dati nel periodo di tempo breve. 
* È necessario maggiore velocità effettiva dal contenitore hello al back-end hello. Ad esempio, vedere che la velocità effettiva hello utilizzato è maggiore velocità effettiva di provisioning hello e recupero è limitato. Per altre informazioni, vedere [Impostare la velocità effettiva per i contenitori di Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>È possibile applicare la scalabilità verticale o ridurre la velocità effettiva hello della tabella tabella API (anteprima)? 
Sì, è possibile utilizzare la velocità effettiva hello tooscale del portale di Azure Cosmos DB hello scala riquadro. Per altre informazioni, vedere l'articolo su come [impostare la velocità effettiva](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Per le tabelle appena sottoposte a provisioning viene impostato un valore predefinito di TableThroughput?
Sì, se si esegue l'override hello TableThroughput tramite app. config, non utilizza un contenitore creato in precedenza nel database di Azure Cosmos servizio hello crea una tabella con una velocità effettiva di 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>È qualsiasi modifica di prezzi per i clienti esistenti di API tabella standard hello?
Nessuna. Il prezzo per i clienti esistenti dell'API Table standard non verrà modificato. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Come viene calcolato il prezzo di hello per hello tabella API (anteprima)? 
prezzo Hello dipende da hello allocata TableThroughput. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Come gestire qualsiasi limitazione nelle tabelle di hello nell'API di tabella (anteprima) offerta 
Se la frequenza di richieste hello supera la capacità di hello di velocità effettiva di provisioning hello per contenitore sottostante hello, si verificherà un errore e hello SDK riproverà chiamata hello applicando i criteri di ripetizione hello.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Perché è necessaria una velocità effettiva oltre a PartitionKey e RowKey tootake sfruttare offerta di API di tabella (anteprima) hello premium di Azure Cosmos DB toochoose?
Azure DB Cosmos imposta una velocità effettiva predefinito per il contenitore se non si specifica uno nel file app. config hello. 

Azure Cosmos DB offre garanzie di prestazioni e latenza, con limiti superiori nelle operazioni. Questa garanzia è possibile quando motore hello è possibile applicare la governance sulle operazioni del tenant hello. Impostazione TableThroughput consente di ottenere hello garantisce velocità effettiva e latenza, in quanto piattaforma hello questa capacità di riserva e garantisce l'esito positivo operativa. 

Utilizzando una specifica velocità effettiva di hello, si elastico modificarlo toobenefit da stagionalità hello dell'applicazione, soddisfare le esigenze di velocità effettiva di hello e ridurre i costi.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Azure Storage SDK è stata molto basso costo per me, perché paga solo i dati di hello toostore e si raramente esegue una query. nuova offerta di Azure Cosmos DB Hello sembra toobe Ricarica me, anche se non è stato non eseguita una singola transazione o qualsiasi elemento archiviato. Perché?

Azure DB Cosmos è toobe progettato un sistema distribuito a livello globale, basato su contratto di servizio con garanzie di disponibilità, latenza e velocità effettiva. Quando si riserva una velocità effettiva nel database Cosmos di Azure, è garantito, a differenza di velocità effettiva di hello di altri sistemi. Azure Cosmos DB offre funzionalità aggiuntive che sono state richieste dai clienti, come gli indici secondari e la distribuzione globale. Durante il periodo di anteprima di hello, si forniscono un modello con ottimizzazione per la velocità effettiva e, infine, contiamo tooprovide toomeet un modello di archiviazione ottimizzata esigenze dei clienti. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Quando si inseriscono dati nell'archivio tabelle, non viene mai visualizzata una notifica di raggiungimento della quota che indica che la partizione è piena. Con hello tabella API (anteprima), viene visualizzato questo messaggio. È questa l'offerta limitazione me e la forzatura me toochange applicazione esistente?

Azure Cosmos DB è un sistema basato su contratti di servizio che offre scalabilità illimitata, con garanzie di latenza, velocità effettiva, disponibilità e coerenza. tooensure garantire prestazioni ottimali, assicurarsi che le dimensioni dei dati e indice vengono gestibile e scalabile. limite di 10 GB Hello numero hello di entità o gli elementi per ogni chiave di partizione è tooensure di offrire ottime prestazioni di ricerca e query. tooensure che l'applicazione viene ridimensionata anche per l'archiviazione di Azure, è consigliabile che si *non* creare una partizione a caldo archiviando tutte le informazioni in una partizione e l'esecuzione di query su. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>In modo PartitionKey e RowKey sono ancora necessari con hello nuova API di tabella (anteprima)? 
Sì. Poiché della superficie di attacco di hello di hello tabella API (anteprima) è simile toothat di hello archiviazione tabella SDK, la chiave di partizione hello fornisce dati di hello toodistribute un modo efficiente. chiave di riga Hello è univoco all'interno della partizione. Hello toobe esigenze chiave di riga presenti e non può essere null come in hello standard SDK. lunghezza Hello di RowKey è 255 byte e lunghezza hello di PartitionKey è 100 byte (appena toobe aumentato too1 KB). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Quali sono i messaggi di errore hello per hello tabella API (anteprima)?
Poiché questa versione di anteprima è compatibile con la tabella standard hello, la maggior parte degli errori di hello verrà eseguito il mapping degli errori toohello dalla tabella standard hello. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Motivo per cui + soggetto a limitazione quando si tenta di toocreate numerose tabelle uno dopo l'altro hello tabella API (anteprima)?
Azure Cosmos DB è un sistema basato su contratti di servizio che offre garanzie di latenza, velocità effettiva, disponibilità e coerenza. Poiché si tratta di un sistema di provisioning, si riserva risorse tooguarantee questi requisiti. frequenza di rapido Hello di creazione di tabelle viene rilevato e limitata. Si consiglia di esaminare il tasso di hello di creazione di tabelle e diminuirlo tooless di 5 al minuto. Tenere presente che hello tabella API (anteprima) è un sistema di provisioning. momento di Hello è effettuare il provisioning, si inizierà toopay appositamente. 

## <a name="develop-against-hello-graph-api-preview"></a>Lo sviluppo utilizzando hello API Graph (anteprima)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Come è possibile applicare funzionalità hello dell'API Graph (anteprima) tooAzure Cosmos DB?
È possibile utilizzare una funzionalità di estensione della libreria tooapply hello dell'API Graph (anteprima). denominata Microsoft Azure Graphs e disponibile in NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Sembra che si supporta hello Gremlin grafico attraversamento della lingua. Se si prevede tooadd altre forme di query.
Sì, è previsto il tooadd altri meccanismi per la query in hello future. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Come è possibile utilizzare la nuova offerta API Graph (anteprima) di hello? 
hello avviata, completo di tooget [API Graph](../cosmos-db/create-graph-dotnet.md) Guida introduttiva all'articolo.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Domande di clienti di DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Motivo per cui si sta spostando tooAzure Cosmos DB? 

Azure DB Cosmos è bisestile big successiva di hello nei database di cloud distribuita a livello globale, su larga scala. Come un cliente di DocumentDB, è ora possibile accesso toohello all'avanguardia sistema e delle funzionalità offerte da Azure Cosmos DB.

Azure DB Cosmos avviato come progetto denominato "Florence" nel 2010 tooaddress hello i punti deboli riscontrate dagli sviluppatori per la creazione di applicazioni su larga scala all'interno di Microsoft. problematiche di Hello di creazione di applicazioni distribuite globalmente non sono univoci tooMicrosoft, pertanto è resa disponibile negli sviluppatori tooAzure 2015 hello prima generazione di questa tecnologia in forma di hello di Azure DocumentDB. 

Da quel momento sono state aggiunte nuove importanti funzionalità. DB Cosmos Azure è il risultato di hello. Nell'ambito di questo rilascio, i clienti di DocumentDB, con i relativi dati, diventano in modo automatico e trasparente clienti di Azure Cosmos DB. Queste funzionalità sono nelle aree di hello hello core motore di database, nonché distribuzione globale, scalabilità elastica e i contratti di servizio leader del settore e completi. In particolare, è stato sviluppato la mappa tooefficiently hello Azure Cosmos DB database motore tutti i modelli di dati comuni, sistemi di tipi e API toohello modello dati sottostante di Azure Cosmos DB. 

manifestazione orientati developer corrente di questo lavoro Hello è il nuovo supporto hello per [Gremlin](../cosmos-db/graph-introduction.md) e [le API di archiviazione tabella](../cosmos-db/table-introduction.md). E questo è solo hello inizio. Prevediamo tooadd altre API comuni e i modelli di dati più recenti nel tempo, con ulteriori miglioramenti delle prestazioni e all'archiviazione su scala globale. 

È importante toopoint out che hello DocumentDB [sottolinguaggio SQL](../documentdb/documentdb-sql-query.md) è stata sempre solo uno di hello molte API che hello DB Cosmos di Azure sottostante può supportare. Per gli sviluppatori che utilizzano un servizio completamente gestito, ad esempio Azure Cosmos DB, hello solo il servizio interfaccia toohello è hello API che vengono esposti dal servizio hello. Non cambia nulla per i clienti esistenti di DocumentDB. In DB Cosmos Azure, si ottiene esattamente hello che offre SQL stessa API di DocumentDB. E ora (e in futuro hello), è possibile accedere ad altre funzionalità precedentemente inaccessibile 

Un altro manifestazione del nostro lavoro continuato è foundation hello estesi per la scalabilità globale e flessibile di velocità effettiva e archiviazione. Sono stati apportati numerosi miglioramenti fondamentali toohello sottosistema di distribuzione globale. Uno dei hello molte funzionalità quali orientati developer è hello prefisso coerente modello di coerenza, rendendo un totale cinque modelli coerenza ben definito. Diverse funzionalità ancora più interessanti verranno rilasciate non appena saranno definitive. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>Che cosa è necessario che le risorse di DocumentDB continuano toorun in Azure Cosmos DB tooensure di toodo?

Non occorre toomake alcuna modifica affatto. Le risorse di DocumentDB sono ora risorse Azure Cosmos DB, e si è verificato senza interruzione del servizio di hello quando si è verificato questo spostamento.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>Operazioni di modifiche è necessario toomake per my toowork app con Azure Cosmos DB?

Non esistono toomake le modifiche. Classi, spazi dei nomi e nomi di pacchetti NuGet non sono stati modificati. Come sempre, è consigliabile mantenere il SDK di toodate tootake sfruttare funzionalità più recenti hello e miglioramenti. 

### <a name="whats-changed-in-hello-azure-portal"></a>Novità nel portale di Azure hello?

DocumentDB non apparirà più nel portale di hello come un servizio di Azure. Al suo posto è una nuova icona di Azure Cosmos DB, come illustrato nella seguente immagine hello. Tutte le raccolte sono disponibili come prima ed è ancora possibile ridimensionare la velocità effettiva, modificare i livelli di coerenza e monitorare i contratti di servizio. sono state migliorate le funzionalità di Hello di Esplora dati (anteprima). È possibile ora consente di visualizzare e modificare i documenti, creare ed eseguire query e utilizzare le stored procedure, trigger e funzioni definite dall'utente da un'unica pagina, come illustrato nella seguente immagine hello: 

![Pannello di Azure Cosmos DB raccolte Hello](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Sono presenti modifiche toopricing?

No, il costo di hello dell'esecuzione dell'app in Azure Cosmos DB è hello stesso com'era prima.

### <a name="are-there-changes-toohello-slas"></a>Sono presenti modifiche toohello i contratti di servizio?

No, hello contratti di servizio per la disponibilità, coerenza, latenza e velocità effettiva non vengono modificate e vengono ancora visualizzati nel portale di hello. Per altre informazioni, vedere [Contratto di Servizio per Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![App elenco attività con dati di esempio](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
