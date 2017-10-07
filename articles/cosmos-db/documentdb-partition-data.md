---
title: "aaaPartitioning e scalabilità in Azure Cosmos DB | Documenti Microsoft"
description: "Informazioni sul funzionamento della modalità di partizionamento nel database di Azure Cosmos, come tooconfigure partizionamento e le chiavi di partizione e come toopick hello destra chiave di partizione per l'applicazione."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Partizionamento nel database di Cosmos di Azure usando l'API DocumentDB hello

[Database di Microsoft Azure Cosmos](../cosmos-db/introduction.md) è toohelp di servizio progettato un database distribuito e più modelli globali è ottenere scalabilità e prestazioni rapido e prevedibile facilmente insieme all'applicazione di si sviluppa. 

In questo articolo viene fornita una panoramica di come toowork con il partizionamento dei contenitori DB Cosmos con hello API DocumentDB. Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md). 

tooget avviato con il codice, scaricare il progetto hello da [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:   

* Come funziona il partizionamento in Azure Cosmos DB?
* Come si configura il partizionamento in Azure Cosmos DB?
* Quali sono le chiavi di partizione, e come scegliere la chiave di partizione corretta hello per la mia applicazione?

tooget avviato con il codice, scaricare il progetto hello da [Azure Cosmos DB prestazioni test Driver esempio](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Chiavi di partizione

Nell'API DocumentDB hello, si specifica definizione chiave di partizione hello sotto forma di hello di un percorso JSON. Hello nella tabella seguente vengono illustrati esempi di definizioni di chiave di partizione e i valori hello tooeach corrispondente. chiave di partizione Hello è specificata come un percorso, ad esempio `/department` rappresenta hello reparto di proprietà. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Chiave di partizione</strong></p></td>
            <td valign="top"><p><strong>Descrizione</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Corrisponde toohello valore doc.department in cui doc è elemento hello.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Corrisponde toohello valore doc.properties.name in cui doc è elemento hello (proprietà annidate).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Valore toohello doc.id corrispondente (chiave id e una partizione sono hello stessa proprietà).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"nome reparto"</p></td>
            <td valign="top"><p>Corrisponde toohello valore doc ["Nome reparto"] in cui doc è elemento hello.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> sintassi di Hello per la chiave di partizione è specifica del percorso toohello simile di indicizzazione di percorsi di criteri con una differenza chiave hello che hello percorso corrisponde a proprietà toohello anziché il valore di hello, ad esempio non è presente alcun carattere jolly alla fine di hello. Ad esempio, per indicizzare i valori nel reparto si specifica /department/?, hello tooindex valori nel reparto, ma specifica /department come definizione di chiave di partizione hello. chiave di partizione Hello è indicizzata in modo implicito e non da escludere dall'indicizzazione mediante indicizzazione sostituiscono i criteri.
> 
> 

Esaminare la modalità scelta hello della chiave di partizione influisce sulle prestazioni di hello dell'applicazione.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Utilizzo di hello Azure Cosmos DB SDK
Azure Cosmos DB ha aggiunto il supporto per il partizionamento automatico con la [versione 2015-12-16 dell'API REST](/rest/api/documentdb/). Nei contenitori toocreate partizionata ordine, è necessario scaricare le versioni SDK 1.6.0 o supportato più recente in uno dei hello piattaforme SDK (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Creazione di contenitori
Hello esempio seguente viene illustrato un toocreate frammento di codice .NET un contenitore toostore dispositivo i dati di telemetria 20.000 di unità di richiesta al secondo di velocità effettiva. Hello SDK Imposta valore OfferThroughput hello (che a sua volta imposta hello `x-ms-offer-throughput` intestazione della richiesta in hello API REST). Di seguito viene impostato in modo hello `/deviceId` come chiave di partizione hello. scelta di Hello della chiave di partizione viene salvata insieme resto hello di hello i metadati del contenitore come nome e i criteri di indicizzazione.

Per questo esempio, abbiamo scelto `deviceId` poiché è noto che (a) poiché si tratta di un numero elevato di dispositivi, operazioni di scrittura può essere distribuiti in modo uniforme tra partizioni e consentendo ci tooscale hello volumi massive tooingest di database di dati e (b) molte richieste hello come recupero di lettura più recente di hello, per un dispositivo sono deviceId singolo tooa con ambito e possono essere recuperati da una singola partizione.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Questo metodo rende un'API REST di chiamare tooCosmos DB e servizio hello verrà eseguito il provisioning di un numero di partizioni in base alla velocità effettiva richiesta hello. È possibile modificare la velocità effettiva hello di un contenitore come le prestazioni evolversi delle esigenze. 

### <a name="reading-and-writing-items"></a>Lettura e scrittura di elementi
A questo punto si inseriscono i dati in Cosmos DB. Di seguito è una classe di esempio contenente la lettura di un dispositivo e un tooinsert tooCreateDocumentAsync chiamata di un nuovo dispositivo di lettura in un contenitore. Questo è un esempio di utilizzo hello API DocumentDB:

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

Di seguito leggere la chiave di partizione e l'id elemento di hello, aggiornarlo e come passaggio finale, quindi eliminarlo dall'id e la chiave di partizione. Si noti che le letture hello includano un valore PartitionKey (toohello corrispondente `x-ms-documentdb-partitionkey` intestazione della richiesta in hello API REST).

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a>Esecuzione di query sui contenitori partizionati
Quando si eseguono query dei dati in contenitori partizionati Cosmos DB automaticamente le route hello partizioni toohello query corrispondenti valori di chiave partizione toohello specificati nel filtro hello (se presenti). Ad esempio, questa query è indirizzato toojust hello partizione contenente hello chiave di partizione "XMS-0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hello query seguente non dispone di un filtro sulla chiave di partizione hello (DeviceId) e viene disposta tooall partizioni in cui viene eseguita sull'indice della partizione hello. Si noti che è necessario toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello API REST) toohave hello SDK tooexecute una query tra partizioni.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Cosmos DB supporta le [funzioni di aggregazione](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` su contenitori partizionati con SQL a partire da SDK 1.12.0 e versioni successive. Le query devono includere un unico operatore di aggregazione e devono includere un solo valore nella proiezione hello.

### <a name="parallel-query-execution"></a>Esecuzione di query in parallelo
Hello Cosmos DB SDK alla 1.9.0 e versioni successive supportano opzioni di esecuzione di query parallele, che consentono a bassa latenza tooperform esegue query su raccolte partizionate, anche quando sono necessari tootouch un numero elevato di partizioni. Ad esempio, hello seguente query è configurato toorun in parallelo tra partizioni.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
È possibile gestire l'esecuzione parallela di query ottimizzando hello seguenti parametri:

* Impostando `MaxDegreeOfParallelism`, è possibile controllare hello grado di parallelismo, ovvero hello massimo numero di partizioni del contenitore toohello connessioni di rete simultanee. Se si imposta questo troppo-1, livello hello di parallelismo è gestito da hello SDK. Se hello `MaxDegreeOfParallelism` viene omesso o impostato too0, ovvero il valore di predefinito hello, saranno presenti partizioni di una singola rete connessione toohello contenitore.
* Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client. Se si omette questo parametro o impostare troppo-1, numero di hello di elementi memorizzato nel buffer durante l'esecuzione di query parallele è gestito da hello SDK.

Dato hello stesso stato dell'insieme di hello, una query parallela restituisce risultati hello stesso ordine come in esecuzione seriale. Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o superiore), problemi di Azure Cosmos DB SDK hello hello query in parallelo tra partizioni e unisce i risultati ordinati parzialmente in hello client side tooproduce risultati ordinati globalmente.

### <a name="executing-stored-procedures"></a>Esecuzione di stored procedure
È inoltre possibile eseguire le transazioni atomiche sui documenti con hello stesso ID del dispositivo, ad esempio, se si gestiscono le aggregazioni o hello stato più recente di un dispositivo in un singolo elemento. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
Nella sezione successiva hello, verranno esaminate come è possibile spostare i contenitori toopartitioned dai contenitori singola partizione.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è fornita una panoramica delle modalità toowork con il partizionamento del database di Azure Cosmos contenitori con hello API DocumentDB. Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere anche l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md). 

* Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB. Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).
* Iniziare a scrivere codice con hello [SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/)
* Informazioni sulla [velocità effettiva con provisioning in Azure Cosmos DB](request-units.md)

