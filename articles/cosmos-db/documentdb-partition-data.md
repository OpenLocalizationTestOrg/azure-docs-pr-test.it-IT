---
title: "Partizionamento e scalabilità in Azure Cosmos DB | Microsoft Docs"
description: Informazioni sul funzionamento del partizionamento in Azure Cosmos DB, sulla configurazione del partizionamento e delle chiavi di partizione e su come scegliere la chiave di partizione corretta per l'applicazione.
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
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="13a7d-103">Partizionamento in Azure Cosmos DB con l'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="13a7d-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="13a7d-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) è un servizio di database multimodello con distribuzione globale progettato per ottenere prestazioni rapide e prevedibili e per eseguire facilmente il ridimensionamento in base alla crescita dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="13a7d-105">Questo articolo offre una panoramica dell'uso del partizionamento dei contenitori Cosmos DB con l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="13a7d-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="13a7d-106">Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="13a7d-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="13a7d-107">Per iniziare a usare il codice, scaricare il progetto da [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="13a7d-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="13a7d-108">Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="13a7d-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="13a7d-109">Come funziona il partizionamento in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="13a7d-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="13a7d-110">Come si configura il partizionamento in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="13a7d-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="13a7d-111">Cosa sono le chiavi di partizione e come scegliere la chiave di partizione corretta per l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="13a7d-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="13a7d-112">Per iniziare a usare il codice, scaricare il progetto dell'[esempio di driver di test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="13a7d-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="13a7d-113">Chiavi di partizione</span><span class="sxs-lookup"><span data-stu-id="13a7d-113">Partition keys</span></span>

<span data-ttu-id="13a7d-114">Nell'API DocumentDB è necessario specificare la definizione della chiave di partizione sotto forma di percorso JSON.</span><span class="sxs-lookup"><span data-stu-id="13a7d-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="13a7d-115">La tabella seguente mostra esempi di definizioni di chiavi di partizione e i valori corrispondenti a ognuna.</span><span class="sxs-lookup"><span data-stu-id="13a7d-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="13a7d-116">La chiave di partizione viene specificata come percorso, ad esempio `/department` rappresenta la proprietà department.</span><span class="sxs-lookup"><span data-stu-id="13a7d-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="13a7d-117"><strong>Chiave di partizione</strong></span><span class="sxs-lookup"><span data-stu-id="13a7d-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="13a7d-118"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="13a7d-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="13a7d-119">/department</span><span class="sxs-lookup"><span data-stu-id="13a7d-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="13a7d-120">Corrisponde al valore doc.department, in cui doc è l'elemento.</span><span class="sxs-lookup"><span data-stu-id="13a7d-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="13a7d-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="13a7d-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="13a7d-122">Corrisponde al valore doc.properties.name, in cui doc è l'elemento (proprietà annidata).</span><span class="sxs-lookup"><span data-stu-id="13a7d-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="13a7d-123">/id</span><span class="sxs-lookup"><span data-stu-id="13a7d-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="13a7d-124">Corrisponde al valore doc.id (ID e chiave di partizione sono la stessa proprietà).</span><span class="sxs-lookup"><span data-stu-id="13a7d-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="13a7d-125">/"nome reparto"</span><span class="sxs-lookup"><span data-stu-id="13a7d-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="13a7d-126">Corrisponde al valore doc["nome reparto"], in cui doc è l'elemento.</span><span class="sxs-lookup"><span data-stu-id="13a7d-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="13a7d-127">La sintassi della chiave di partizione è simile alla specifica dei percorsi dei criteri di indicizzazione con la differenza fondamentale che il percorso corrisponde alla proprietà anziché al valore, ossia non sono presenti caratteri jolly alla fine.</span><span class="sxs-lookup"><span data-stu-id="13a7d-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="13a7d-128">Ad esempio, per indicizzare i valori nel reparto si specifica /department/?,</span><span class="sxs-lookup"><span data-stu-id="13a7d-128">For example, you would specify /department/?</span></span> <span data-ttu-id="13a7d-129">mentre per la definizione della chiave di partizione si usa /department.</span><span class="sxs-lookup"><span data-stu-id="13a7d-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="13a7d-130">La chiave di partizione viene indicizzata in modo implicito e non può essere esclusa dall'indicizzazione usando override dei criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="13a7d-131">Di seguito viene esaminato come la scelta della chiave di partizione influisce sulle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="13a7d-132">Utilizzo di Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="13a7d-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="13a7d-133">Azure Cosmos DB ha aggiunto il supporto per il partizionamento automatico con la [versione 2015-12-16 dell'API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="13a7d-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="13a7d-134">Per creare contenitori partizionati, è necessario scaricare la versione 1.6.0 o una successiva dell'SDK in una delle piattaforme di SDK supportate (.NET, Node.js, Java, Python e MongoDB).</span><span class="sxs-lookup"><span data-stu-id="13a7d-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="13a7d-135">Creazione di contenitori</span><span class="sxs-lookup"><span data-stu-id="13a7d-135">Creating containers</span></span>
<span data-ttu-id="13a7d-136">L'esempio seguente illustra un frammento .NET per la creazione di un contenitore per archiviare i dati di telemetria dei dispositivi a una velocità effettiva di 20.000 unità richiesta al secondo.</span><span class="sxs-lookup"><span data-stu-id="13a7d-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="13a7d-137">L'SDK imposta il valore OfferThroughput, che a sua volta imposta l'intestazione di richiesta `x-ms-offer-throughput` nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="13a7d-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="13a7d-138">Qui viene impostato `/deviceId` come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="13a7d-139">La scelta della chiave di partizione viene salvata con il resto dei metadati del contenitore, come il nome e i criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="13a7d-140">Per questo esempio è stato scelto `deviceId` per due motivi: (a) considerato il numero elevato di dispositivi, le scritture possono essere distribuite in modo uniforme tra le partizioni consentendo di scalare il database per l'inserimento di volumi elevati di dati e (b) molte richieste, ad esempio il recupero della lettura più recente per un dispositivo, sono limitate a un singolo deviceId e possono essere recuperate da una partizione singola.</span><span class="sxs-lookup"><span data-stu-id="13a7d-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
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

<span data-ttu-id="13a7d-141">Questo metodo effettua una chiamata API REST a Cosmos DB e il servizio eseguirà il provisioning di una serie di partizioni in base alla velocità effettiva richiesta.</span><span class="sxs-lookup"><span data-stu-id="13a7d-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="13a7d-142">È possibile modificare la velocità effettiva di un contenitore in base all'evoluzione delle esigenze in termini di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="13a7d-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="13a7d-143">Lettura e scrittura di elementi</span><span class="sxs-lookup"><span data-stu-id="13a7d-143">Reading and writing items</span></span>
<span data-ttu-id="13a7d-144">A questo punto si inseriscono i dati in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="13a7d-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="13a7d-145">Di seguito è riportata una classe di esempio contenente la lettura di un dispositivo e una chiamata a CreateDocumentAsync per inserire una nuova lettura del dispositivo in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="13a7d-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="13a7d-146">Questo esempio sfrutta l'API DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="13a7d-146">This is an example leveraging the DocumentDB API:</span></span>

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

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
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

<span data-ttu-id="13a7d-147">L'elemento viene letto in base alla chiave di partizione e all'ID, viene aggiornato e infine viene eliminato in base alla chiave di partizione e all'ID. Si noti che le letture includono un valore PartitionKey, corrispondente all'intestazione di richiesta `x-ms-documentdb-partitionkey` nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="13a7d-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="13a7d-148">Esecuzione di query sui contenitori partizionati</span><span class="sxs-lookup"><span data-stu-id="13a7d-148">Querying partitioned containers</span></span>
<span data-ttu-id="13a7d-149">Quando si eseguono query sui dati dei contenitori partizionati, Azure Cosmos DB instrada automaticamente la query alle partizioni corrispondenti ai valori di chiave di partizione specificati nel filtro (se presenti).</span><span class="sxs-lookup"><span data-stu-id="13a7d-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="13a7d-150">Ad esempio, questa query viene instradata solo alla partizione contenente la chiave di partizione "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="13a7d-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="13a7d-151">La query seguente non dispone di un filtro per la chiave di partizione (DeviceId) e viene effettuato il fan-out a tutte le partizioni in cui viene eseguita a fronte dell'indice della partizione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="13a7d-152">Si noti che è necessario specificare EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` nell'API REST) affinché l'SDK esegua una query tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="13a7d-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="13a7d-153">Cosmos DB supporta le [funzioni di aggregazione](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` su contenitori partizionati con SQL a partire da SDK 1.12.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="13a7d-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="13a7d-154">Le query devono includere un unico operatore di aggregazione e un singolo valore nella proiezione.</span><span class="sxs-lookup"><span data-stu-id="13a7d-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="13a7d-155">Esecuzione di query in parallelo</span><span class="sxs-lookup"><span data-stu-id="13a7d-155">Parallel query execution</span></span>
<span data-ttu-id="13a7d-156">Gli SDK di Cosmos DB 1.9.0 e versioni successive supportano opzioni per l'esecuzione di query in parallelo che consentono di eseguire query a bassa latenza sulle raccolte partizionate, anche quando è coinvolto un numero elevato di partizioni.</span><span class="sxs-lookup"><span data-stu-id="13a7d-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="13a7d-157">Ad esempio, la query seguente è configurata in modo da essere eseguita in parallelo tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="13a7d-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="13a7d-158">È possibile gestire l'esecuzione di query in parallelo, ottimizzando i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="13a7d-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="13a7d-159">Impostando `MaxDegreeOfParallelism` è possibile controllare il grado di parallelismo, ossia il numero massimo di connessioni di rete simultanee alle partizioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="13a7d-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="13a7d-160">Se si imposta questo valore su -1, il grado di parallelismo viene gestito dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="13a7d-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="13a7d-161">Se `MaxDegreeOfParallelism` non è specificato o è impostato su 0, ovvero il valore predefinito, esisterà una sola connessione di rete alle partizioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="13a7d-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="13a7d-162">Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client.</span><span class="sxs-lookup"><span data-stu-id="13a7d-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="13a7d-163">Se si omette questo parametro o si imposta su -1, il numero di elementi memorizzati nel buffer durante l'esecuzione di query in parallelo viene gestito dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="13a7d-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="13a7d-164">Considerato lo stato della raccolta, una query in parallelo restituirà i risultati nello stesso ordine dell'esecuzione seriale.</span><span class="sxs-lookup"><span data-stu-id="13a7d-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="13a7d-165">Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o TOP), Azure Cosmos DB SDK esegue la query in parallelo tra le partizioni e unisce i risultati ordinati parzialmente sul lato client per produrre risultati ordinati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="13a7d-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="13a7d-166">Esecuzione di stored procedure</span><span class="sxs-lookup"><span data-stu-id="13a7d-166">Executing stored procedures</span></span>
<span data-ttu-id="13a7d-167">È anche possibile eseguire transazioni atomiche su documenti con lo stesso ID dispositivo, ad esempio se si gestiscono le aggregazioni o lo stato più recente di un dispositivo in un singolo elemento.</span><span class="sxs-lookup"><span data-stu-id="13a7d-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="13a7d-168">Nella sezione successiva verrà illustrato come passare a contenitori partizionati da contenitori a partizione singola.</span><span class="sxs-lookup"><span data-stu-id="13a7d-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13a7d-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13a7d-169">Next steps</span></span>
<span data-ttu-id="13a7d-170">Questo articolo include una panoramica dell'uso del partizionamento dei contenitori Azure Cosmos DB con l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="13a7d-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="13a7d-171">Per una panoramica dei concetti e delle procedure consigliate per il partizionamento con qualsiasi API di Azure Cosmos DB, vedere anche l'articolo relativo a [partizionamento e scalabilità orizzontale](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="13a7d-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="13a7d-172">Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="13a7d-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="13a7d-173">Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="13a7d-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="13a7d-174">Introduzione alla programmazione con gli [SDK](documentdb-sdk-dotnet.md) o l'[API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="13a7d-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="13a7d-175">Informazioni sulla [velocità effettiva di provisioning in Azure Cosmos DB](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="13a7d-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

