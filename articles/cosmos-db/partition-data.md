---
title: "aaaPartitioning e la scalabilità orizzontale nel database di Azure Cosmos | Documenti Microsoft"
description: "Informazioni sul funzionamento della modalità di partizionamento nel database di Azure Cosmos, come tooconfigure partizionamento e le chiavi di partizione e come toopick hello destra chiave di partizione per l'applicazione."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Come toopartition e la scala in Azure Cosmos DB

[Database di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) è toohelp di servizio progettato un database distribuito e più modelli globali è ottenere scalabilità e prestazioni rapido e prevedibile facilmente insieme all'applicazione di si sviluppa. In questo articolo viene fornita una panoramica del partizionamento può essere usato per tutti i dati di hello modelli in Azure Cosmos DB e viene descritto come configurare la scala di Azure Cosmos DB contenitori tooeffectively delle applicazioni.

Il partizionamento e le chiavi di partizione sono illustrati anche in questo video di Azure Friday con Scott Hanselman e Shireesh Thota, responsabile principale della progettazione di Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Partizionamento in Azure Cosmos DB
In Azure Cosmos DB è possibile archiviare dati ed eseguire query senza schema con tempi di risposta nell'ordine di millisecondi su qualsiasi scala. Cosmos DB offre contenitori per l'archiviazione di dati denominati **raccolte (per i documenti), grafici o tabelle**. I contenitori sono risorse logiche e possono comprendere una o più partizioni fisiche o server. numero di Hello di partizioni è determinato dal DB Cosmos in base alle dimensioni di archiviazione hello e velocità effettiva di provisioning hello del contenitore di hello. Ogni partizione in Cosmos DB ha una quantità fissa di archiviazione supportata da unità SSD associata e viene replicata per la disponibilità elevata. Gestione delle partizioni è completamente gestiti da Azure Cosmos DB, e non si dispone di codice complesso toowrite o gestire le partizioni. I contenitori di Cosmos DB sono illimitati in termini di risorse di archiviazione e di velocità effettiva. 

![orizzontale](./media/introduction/azure-cosmos-db-partitioning.png) 

Il partizionamento è trasparente tooyour applicazione. COSMOS DB supporta veloce letture e scritture, query, la logica transazionale, livelli di coerenza e controllo di accesso con granularità fine tramite la risorsa di metodi/API tooa singolo contenitore. Hello servizio gestisce la distribuzione dei dati tra partizioni e routing partizione corretta toohello le richieste di query. 

Per il partizionamento, ogni elemento deve avere una chiave di partizione e una chiave di riga che lo identificano in modo univoco. La chiave di partizione funge da partizione logica per i dati e fornisce a Cosmos DB un limite naturale per la distribuzione dei dati tra partizioni. In sintesi, il partizionamento in Azure Cosmos DB funziona nel modo seguente:

* Si esegue il provisioning di un contenitore Cosmos DB con velocità effettiva di `T` richieste/s
* Dietro le quinte hello partizioni disposizioni Cosmos DB necessari tooserve `T` richieste/s. Se `T` è superiore alla velocità effettiva massima hello per ogni partizione `t`, quindi esegue il provisioning Cosmos DB `N`  =  `T/t` partizioni
* COSMOS DB alloca spazio della chiave di partizione hello gli hash delle chiavi in modo uniforme tra hello `N` partizioni. Ogni partizione fisica ospita quindi 1-N valori di chiave di partizione (partizioni logiche)
* Quando una partizione fisica `p` raggiunge il limite di archiviazione, DB Cosmos divide perfettamente `p` in due partizioni nuovo `p1` e `p2` e distribuisce i valori corrispondenti tooroughly metà hello chiavi tooeach di hello partizioni. Operazione di divisione è invisibile tooyour applicazione.
* Analogamente, quando si esegue il provisioning della velocità effettiva superiore `t*N` velocità effettiva, DB Cosmos suddivide in uno o più le partizioni toosupport hello una velocità effettiva

semantica di Hello per le chiavi di partizione è semantica hello toomatch leggermente diverse di ogni API, come illustrato nella seguente tabella hello:

| API | Chiave di partizione | Chiave di riga |
| --- | --- | --- |
| DocumentDB | percorso personalizzato della chiave di partizione | `id` fisso | 
| MongoDB | chiave di partizione personalizzata  | `_id` fisso | 
| Grafico | proprietà chiave di partizione personalizzata | `id` fisso | 
| Tabella | `PartitionKey` fisso | `RowKey` fisso | 

Cosmos DB usa il partizionamento basato su hash. Quando si scrive un elemento, DB Cosmos hash valore di chiave di partizione hello e utilizzare hello eseguito l'hashing toodetermine risultato partizione toostore hello voce. Archivi COSMOS DB tutti gli elementi con hello stessa chiave di partizione in hello stessa partizione fisica. scelta di Hello hello della chiave di partizione è una decisione importante avere toomake in fase di progettazione. È necessario scegliere un nome proprietà che contenga un'ampia gamma di valori e abbia anche modelli di accesso.

> [!NOTE]
> È una migliore toohave pratica una chiave di partizione con molti valori distinti (100s-1000s minimo).
>

I contenitori di Azure Cosmos DB possono essere creati come "fissi" o "illimitati". I contenitori a dimensione fissa hanno un limite massimo di 10 GB e velocità effettiva di 10.000 UR/s. Alcune API consentono toobe chiave di partizione hello omesso per i contenitori di dimensioni fisse. un contenitore come illimitato toocreate, è necessario specificare una velocità effettiva minima di 2500 UR/sec.

## <a name="partitioning-and-provisioned-throughput"></a>Partizionamento e velocità effettiva con provisioning
Cosmos DB è progettato per prestazioni prevedibili. Quando si crea un contenitore, la velocità effettiva viene riservata in termini di **[unità richiesta](request-units.md) (UR) al secondo, con un potenziale add-on per UR al minuto**. Ogni richiesta viene assegnato un addebito di unità di richiesta che è la quantità proporzionale toohello delle risorse di sistema come CPU, memoria e i/o utilizzata dall'operazione hello. La lettura di un documento di 1 KB con coerenza di sessione usa un'unità richiesta. Un'operazione di lettura è 1 UR indipendentemente dal numero di hello di elementi archiviati o hello numero di richieste simultanee in esecuzione in hello contemporaneamente. Gli elementi più grandi richiedono maggiore di unità di richiesta in base alle dimensioni hello. Se si conoscono dimensioni hello le entità e numero di letture di hello toosupport è necessario per l'applicazione, è possibile eseguire il provisioning di quantità esatta di hello di velocità effettiva richiesta per l'applicazione necessita read. 

> [!NOTE]
> tooachieve hello piena velocità effettiva del contenitore di hello, è necessario scegliere una chiave di partizione che consente di tooevenly distribuire le richieste tra alcuni valori di chiave di partizione distinta.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Utilizzo di hello Azure Cosmos DB API
È possibile usare hello portale di Azure o i contenitori di toocreate CLI di Azure e li ridimensionare in qualsiasi momento. Questa sezione viene illustrato come contenitori toocreate e specificare hello velocità effettiva e la partizione di definizione della chiave in ogni hello API supportate.

### <a name="documentdb-api"></a>API di DocumentDB
Hello seguente esempio viene illustrato come un contenitore (raccolta) usando toocreate hello API DocumentDB. Per informazioni più dettagliate, vedere [Partizionamento con l'API di DocumentDB](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

È possibile leggere un elemento (documento) utilizzando hello `GET` metodo hello API REST o `ReadDocumentAsync` in uno dei hello SDK.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>API di MongoDB
Con hello MongoDB API, è possibile creare una raccolta partizionata tramite il proprio SDK, driver o lo strumento preferito. In questo esempio hello Shell di Mongo viene usata per la creazione della raccolta hello.

Nella Shell di Mongo hello:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Risultati:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>API di tabella

Con hello API di tabella, specificare la velocità effettiva hello per le tabelle nella configurazione appSettings hello per l'applicazione:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Quindi necessario creare una tabella utilizzando l'archiviazione tabelle di Azure hello SDK. chiave di partizione Hello viene creata implicitamente come hello `PartitionKey` valore. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

È possibile recuperare una singola entità utilizzando hello frammento di codice seguente:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Vedere [allo sviluppo con hello tabella API](tutorial-develop-table-dotnet.md) per altri dettagli.

### <a name="graph-api"></a>API Graph

Con hello API Graph, è necessario utilizzare hello portale di Azure o contenitori toocreate CLI. In alternativa, poiché Azure Cosmos DB è più modelli, è possibile utilizzare uno dei hello toocreate altri modelli e ridimensionare il contenitore grafico.

È possibile leggere alcun bordo utilizzando la chiave di partizione hello e id in Gremlin vertice. Per un grafico con l'area ('USA') come chiave di partizione hello e "Seattle" come chiave di riga hello, ad esempio, è possibile trovare un vertice utilizzando hello la seguente sintassi:

```
g.V(['USA', 'Seattle'])
```

Stesso con bordi, è possibile fare riferimento un bordo con la chiave di partizione hello e la chiave di riga.

```
g.E(['USA', 'I5'])
```

Vedere il [supporto di Gremlin per Cosmos DB](gremlin-support.md) per altri dettagli.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Progettazione per il partizionamento
tooscale in modo efficace con Azure Cosmos DB, è necessario toopick una buona chiave di partizione quando si crea il contenitore. È necessario considerare due aspetti fondamentali nella scelta di una chiave di partizione:

* **Limite per query e transazioni**: la scelta della chiave di partizione deve bilanciare hello necessità tooenable hello ricorso transazioni su hello requisito toodistribute le entità più tooensure di chiavi di partizione una soluzione scalabile. A un'estremità, è possibile impostare hello stessa chiave di partizione per tutti gli elementi, ma ciò potrebbe limitare la scalabilità hello della soluzione. In hello altra estremità, è possibile assegnare una chiave di partizione univoca per ogni elemento, che sarebbe altamente scalabile, ma ne impedisce l'utilizzo delle transazioni tra documento tramite stored procedure e trigger. Una chiave di partizione ideale è che consente di eseguire query efficienti toouse e che disponga di sufficienti cardinalità tooensure la soluzione è scalabile. 
* **Non colli di bottiglia delle prestazioni e archiviazione**: è importante una proprietà che consente di toopick scrive toobe distribuiti in diversi valori distinti. Richieste toohello stessa chiave di partizione non può superare la velocità effettiva hello di una singola partizione e sono limitate. Pertanto, è importante toopick una chiave di partizione che non produce "sensibili" all'interno dell'applicazione. Poiché tutti i dati di hello per una chiave singola partizione deve essere archiviata all'interno di una partizione, è inoltre consigliabile tooavoid le chiavi di partizione con volumi elevati di dati per hello stesso valore. 

Verranno ora esaminati alcuni scenari reali con le chiavi di partizione corrette per ognuno:
* Se si sta implementando un back-end del profilo utente, l'ID utente hello è una buona scelta per la chiave di partizione.
* Se si archiviano dati IoT, ad esempio lo stato del dispositivo, l'ID dispositivo rappresenta la scelta ideale per la chiave di partizione.
* Se si usa Azure Cosmos DB per la registrazione di dati della serie temporale, quindi hello nome host o l'ID del processo è una buona scelta per la chiave di partizione.
* Se si dispone di un'architettura multi-tenant, l'ID tenant hello è una buona scelta per la chiave di partizione.

In alcuni casi come IoT di utilizzo e i profili utente, chiave di partizione hello potrebbe essere hello stesso come id (chiave di documento). In altre come dati della serie temporale hello, potrebbe essere una chiave di partizione diverso da id hello.

### <a name="partitioning-and-loggingtime-series-data"></a>Partizionamento e registrazione di dati di serie temporali
Uno dei casi di utilizzo del database Cosmos comuni hello è per la registrazione e i dati di telemetria. È importante toopick una chiave di partizione valido in quanto potrebbe essere necessario volumi di grandi tooread/scrittura di dati. scelta di Hello dipende dalla lettura e velocità di scrittura e i tipi di query che previsti toorun. Ecco alcuni suggerimenti su come toochoose una chiave di partizione valido.

* Se il caso di utilizzo prevede un tasso di piccole dimensioni scrive totale per un lungo periodo di tempo e necessità tooquery da intervalli di timestamp e altri filtri, utilizzando un rollup di hello timestamp, ad esempio, data una chiave di partizione è un buon approccio. In questo modo è tooquery su tutti i dati di hello per una data da una singola partizione. 
* Se il carico di lavoro prevede molte scritture, scenario più comune, è opportuno usare una chiave di partizione non basata su timestamp in modo che Cosmos DB possa distribuire in modo uniforme le scritture in più partizioni. In questo caso, un nome host, un ID processo, un ID attività o un'altra proprietà con una cardinalità elevata è una scelta efficace. 
* Un terzo approccio è un ibrido uno in cui si dispone di più contenitori, uno per ogni giorno/mese e chiave di partizione hello è una proprietà granulare come nome host. Questa soluzione offre il vantaggio hello che è possibile impostare diversa velocità effettiva basata su finestra temporale hello, ad esempio, contenitore hello per hello mese corrente viene eseguito il provisioning con una velocità effettiva poiché serve le letture e scritture, mentre i mesi precedenti con ridurre la velocità effettiva dopo vengono usati solo letture.

### <a name="partitioning-and-multi-tenancy"></a>Partizionamento e multi-tenancy
Se si implementa un'applicazione multi-tenant usando Cosmos DB, sono disponibili due modelli comuni: una chiave di partizione per ogni tenant e un contenitore per ogni tenant. Di seguito sono hello vantaggi e svantaggi per ognuno:

* Una chiave di partizione per ogni tenant: in questo modello, i tenant vengono collocati all'interno di un singolo contenitore. Le query e gli inserimenti di elementi all'interno di un tenant possono essere tuttavia eseguiti a fronte di una partizione singola. È anche possibile implementare la logica transazionale su tutti gli elementi all'interno di un tenant. Poiché più tenant condividono un contenitore, è possibile risparmiare i costi di archiviazione e velocità effettiva raggruppando le risorse per i tenant all'interno di un singolo contenitore invece di eseguire il provisioning di capacità aggiuntiva per ogni tenant. restituzione di Hello è che non si dispone isolamento delle prestazioni per ogni tenant. Aumento delle prestazioni e velocità applica toohello intero contenitore vs destinata aumenta per tenant.
* Un contenitore per ogni tenant: ogni tenant ha un contenitore proprio. In questo modello è possibile riservare le prestazioni per ogni tenant. Con il nuovo schema tariffario per il provisioning di Cosmos DB, questo modello è più conveniente per applicazioni multi-tenant con un numero ridotto di tenant.

È inoltre possibile utilizzare un approccio a livelli combinazione/collocates titolari di piccole dimensioni e viene eseguita la migrazione di dimensioni maggiori proprio contenitore tootheir a tenant.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stata illustrata una panoramica di concetti e procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB. 

* Informazioni sulla [velocità effettiva con provisioning in Azure Cosmos DB](request-units.md)
* Informazioni sulla [distribuzione globale in Azure Cosmos DB](distribute-data-globally.md)



