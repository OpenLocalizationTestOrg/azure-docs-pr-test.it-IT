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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="da10a-103">Partizionamento nel database di Cosmos di Azure usando l'API DocumentDB hello</span><span class="sxs-lookup"><span data-stu-id="da10a-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="da10a-104">[Database di Microsoft Azure Cosmos](../cosmos-db/introduction.md) è toohelp di servizio progettato un database distribuito e più modelli globali è ottenere scalabilità e prestazioni rapido e prevedibile facilmente insieme all'applicazione di si sviluppa.</span><span class="sxs-lookup"><span data-stu-id="da10a-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="da10a-105">In questo articolo viene fornita una panoramica di come toowork con il partizionamento dei contenitori DB Cosmos con hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="da10a-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="da10a-106">Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="da10a-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="da10a-107">tooget avviato con il codice, scaricare il progetto hello da [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="da10a-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="da10a-108">Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="da10a-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="da10a-109">Come funziona il partizionamento in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="da10a-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="da10a-110">Come si configura il partizionamento in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="da10a-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="da10a-111">Quali sono le chiavi di partizione, e come scegliere la chiave di partizione corretta hello per la mia applicazione?</span><span class="sxs-lookup"><span data-stu-id="da10a-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="da10a-112">tooget avviato con il codice, scaricare il progetto hello da [Azure Cosmos DB prestazioni test Driver esempio](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="da10a-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="da10a-113">Chiavi di partizione</span><span class="sxs-lookup"><span data-stu-id="da10a-113">Partition keys</span></span>

<span data-ttu-id="da10a-114">Nell'API DocumentDB hello, si specifica definizione chiave di partizione hello sotto forma di hello di un percorso JSON.</span><span class="sxs-lookup"><span data-stu-id="da10a-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="da10a-115">Hello nella tabella seguente vengono illustrati esempi di definizioni di chiave di partizione e i valori hello tooeach corrispondente.</span><span class="sxs-lookup"><span data-stu-id="da10a-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="da10a-116">chiave di partizione Hello è specificata come un percorso, ad esempio `/department` rappresenta hello reparto di proprietà.</span><span class="sxs-lookup"><span data-stu-id="da10a-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="da10a-117"><strong>Chiave di partizione</strong></span><span class="sxs-lookup"><span data-stu-id="da10a-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="da10a-118"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="da10a-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="da10a-119">/department</span><span class="sxs-lookup"><span data-stu-id="da10a-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="da10a-120">Corrisponde toohello valore doc.department in cui doc è elemento hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="da10a-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="da10a-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="da10a-122">Corrisponde toohello valore doc.properties.name in cui doc è elemento hello (proprietà annidate).</span><span class="sxs-lookup"><span data-stu-id="da10a-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="da10a-123">/id</span><span class="sxs-lookup"><span data-stu-id="da10a-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="da10a-124">Valore toohello doc.id corrispondente (chiave id e una partizione sono hello stessa proprietà).</span><span class="sxs-lookup"><span data-stu-id="da10a-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="da10a-125">/"nome reparto"</span><span class="sxs-lookup"><span data-stu-id="da10a-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="da10a-126">Corrisponde toohello valore doc ["Nome reparto"] in cui doc è elemento hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="da10a-127">sintassi di Hello per la chiave di partizione è specifica del percorso toohello simile di indicizzazione di percorsi di criteri con una differenza chiave hello che hello percorso corrisponde a proprietà toohello anziché il valore di hello, ad esempio non è presente alcun carattere jolly alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="da10a-128">Ad esempio, per indicizzare i valori nel reparto si specifica /department/?,</span><span class="sxs-lookup"><span data-stu-id="da10a-128">For example, you would specify /department/?</span></span> <span data-ttu-id="da10a-129">hello tooindex valori nel reparto, ma specifica /department come definizione di chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="da10a-130">chiave di partizione Hello è indicizzata in modo implicito e non da escludere dall'indicizzazione mediante indicizzazione sostituiscono i criteri.</span><span class="sxs-lookup"><span data-stu-id="da10a-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="da10a-131">Esaminare la modalità scelta hello della chiave di partizione influisce sulle prestazioni di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="da10a-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="da10a-132">Utilizzo di hello Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="da10a-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="da10a-133">Azure Cosmos DB ha aggiunto il supporto per il partizionamento automatico con la [versione 2015-12-16 dell'API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="da10a-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="da10a-134">Nei contenitori toocreate partizionata ordine, è necessario scaricare le versioni SDK 1.6.0 o supportato più recente in uno dei hello piattaforme SDK (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="da10a-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="da10a-135">Creazione di contenitori</span><span class="sxs-lookup"><span data-stu-id="da10a-135">Creating containers</span></span>
<span data-ttu-id="da10a-136">Hello esempio seguente viene illustrato un toocreate frammento di codice .NET un contenitore toostore dispositivo i dati di telemetria 20.000 di unità di richiesta al secondo di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="da10a-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="da10a-137">Hello SDK Imposta valore OfferThroughput hello (che a sua volta imposta hello `x-ms-offer-throughput` intestazione della richiesta in hello API REST).</span><span class="sxs-lookup"><span data-stu-id="da10a-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="da10a-138">Di seguito viene impostato in modo hello `/deviceId` come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="da10a-139">scelta di Hello della chiave di partizione viene salvata insieme resto hello di hello i metadati del contenitore come nome e i criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="da10a-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="da10a-140">Per questo esempio, abbiamo scelto `deviceId` poiché è noto che (a) poiché si tratta di un numero elevato di dispositivi, operazioni di scrittura può essere distribuiti in modo uniforme tra partizioni e consentendo ci tooscale hello volumi massive tooingest di database di dati e (b) molte richieste hello come recupero di lettura più recente di hello, per un dispositivo sono deviceId singolo tooa con ambito e possono essere recuperati da una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="da10a-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

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

<span data-ttu-id="da10a-141">Questo metodo rende un'API REST di chiamare tooCosmos DB e servizio hello verrà eseguito il provisioning di un numero di partizioni in base alla velocità effettiva richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="da10a-142">È possibile modificare la velocità effettiva hello di un contenitore come le prestazioni evolversi delle esigenze.</span><span class="sxs-lookup"><span data-stu-id="da10a-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="da10a-143">Lettura e scrittura di elementi</span><span class="sxs-lookup"><span data-stu-id="da10a-143">Reading and writing items</span></span>
<span data-ttu-id="da10a-144">A questo punto si inseriscono i dati in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="da10a-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="da10a-145">Di seguito è una classe di esempio contenente la lettura di un dispositivo e un tooinsert tooCreateDocumentAsync chiamata di un nuovo dispositivo di lettura in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="da10a-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="da10a-146">Questo è un esempio di utilizzo hello API DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="da10a-146">This is an example leveraging hello DocumentDB API:</span></span>

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

<span data-ttu-id="da10a-147">Di seguito leggere la chiave di partizione e l'id elemento di hello, aggiornarlo e come passaggio finale, quindi eliminarlo dall'id e la chiave di partizione. Si noti che le letture hello includano un valore PartitionKey (toohello corrispondente `x-ms-documentdb-partitionkey` intestazione della richiesta in hello API REST).</span><span class="sxs-lookup"><span data-stu-id="da10a-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="da10a-148">Esecuzione di query sui contenitori partizionati</span><span class="sxs-lookup"><span data-stu-id="da10a-148">Querying partitioned containers</span></span>
<span data-ttu-id="da10a-149">Quando si eseguono query dei dati in contenitori partizionati Cosmos DB automaticamente le route hello partizioni toohello query corrispondenti valori di chiave partizione toohello specificati nel filtro hello (se presenti).</span><span class="sxs-lookup"><span data-stu-id="da10a-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="da10a-150">Ad esempio, questa query è indirizzato toojust hello partizione contenente hello chiave di partizione "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="da10a-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="da10a-151">Hello query seguente non dispone di un filtro sulla chiave di partizione hello (DeviceId) e viene disposta tooall partizioni in cui viene eseguita sull'indice della partizione hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="da10a-152">Si noti che è necessario toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello API REST) toohave hello SDK tooexecute una query tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="da10a-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="da10a-153">Cosmos DB supporta le [funzioni di aggregazione](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` su contenitori partizionati con SQL a partire da SDK 1.12.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="da10a-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="da10a-154">Le query devono includere un unico operatore di aggregazione e devono includere un solo valore nella proiezione hello.</span><span class="sxs-lookup"><span data-stu-id="da10a-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="da10a-155">Esecuzione di query in parallelo</span><span class="sxs-lookup"><span data-stu-id="da10a-155">Parallel query execution</span></span>
<span data-ttu-id="da10a-156">Hello Cosmos DB SDK alla 1.9.0 e versioni successive supportano opzioni di esecuzione di query parallele, che consentono a bassa latenza tooperform esegue query su raccolte partizionate, anche quando sono necessari tootouch un numero elevato di partizioni.</span><span class="sxs-lookup"><span data-stu-id="da10a-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="da10a-157">Ad esempio, hello seguente query è configurato toorun in parallelo tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="da10a-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="da10a-158">È possibile gestire l'esecuzione parallela di query ottimizzando hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="da10a-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="da10a-159">Impostando `MaxDegreeOfParallelism`, è possibile controllare hello grado di parallelismo, ovvero hello massimo numero di partizioni del contenitore toohello connessioni di rete simultanee.</span><span class="sxs-lookup"><span data-stu-id="da10a-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="da10a-160">Se si imposta questo troppo-1, livello hello di parallelismo è gestito da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="da10a-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="da10a-161">Se hello `MaxDegreeOfParallelism` viene omesso o impostato too0, ovvero il valore di predefinito hello, saranno presenti partizioni di una singola rete connessione toohello contenitore.</span><span class="sxs-lookup"><span data-stu-id="da10a-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="da10a-162">Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client.</span><span class="sxs-lookup"><span data-stu-id="da10a-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="da10a-163">Se si omette questo parametro o impostare troppo-1, numero di hello di elementi memorizzato nel buffer durante l'esecuzione di query parallele è gestito da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="da10a-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="da10a-164">Dato hello stesso stato dell'insieme di hello, una query parallela restituisce risultati hello stesso ordine come in esecuzione seriale.</span><span class="sxs-lookup"><span data-stu-id="da10a-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="da10a-165">Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o superiore), problemi di Azure Cosmos DB SDK hello hello query in parallelo tra partizioni e unisce i risultati ordinati parzialmente in hello client side tooproduce risultati ordinati globalmente.</span><span class="sxs-lookup"><span data-stu-id="da10a-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="da10a-166">Esecuzione di stored procedure</span><span class="sxs-lookup"><span data-stu-id="da10a-166">Executing stored procedures</span></span>
<span data-ttu-id="da10a-167">È inoltre possibile eseguire le transazioni atomiche sui documenti con hello stesso ID del dispositivo, ad esempio, se si gestiscono le aggregazioni o hello stato più recente di un dispositivo in un singolo elemento.</span><span class="sxs-lookup"><span data-stu-id="da10a-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="da10a-168">Nella sezione successiva hello, verranno esaminate come è possibile spostare i contenitori toopartitioned dai contenitori singola partizione.</span><span class="sxs-lookup"><span data-stu-id="da10a-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da10a-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da10a-169">Next steps</span></span>
<span data-ttu-id="da10a-170">In questo articolo è fornita una panoramica delle modalità toowork con il partizionamento del database di Azure Cosmos contenitori con hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="da10a-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="da10a-171">Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere anche l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="da10a-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="da10a-172">Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="da10a-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="da10a-173">Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="da10a-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="da10a-174">Iniziare a scrivere codice con hello [SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="da10a-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="da10a-175">Informazioni sulla [velocità effettiva con provisioning in Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="da10a-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

