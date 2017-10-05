---
title: Uso del supporto del feed delle modifiche in Azure Cosmos DB | Microsoft Docs
description: Usare il supporto del feed delle modifiche di Azure Cosmos DB per tenere traccia delle modifiche nei documenti, eseguire elaborazioni basate su eventi come i trigger e mantenere aggiornati i sistemi di cache e analisi.
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
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="79f83-104">Uso del supporto del feed delle modifiche in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79f83-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="79f83-105">[Azure Cosmos DB](../cosmos-db/introduction.md) è un servizio di database con replica a livello globale rapido e flessibile, usato per archiviare volumi elevati di dati transazionali e operativi, con una latenza stimabile in pochissimi millisecondi a cifra singola per le operazioni di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="79f83-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="79f83-106">Tutto questo lo rende particolarmente adatto per le applicazioni IoT, di videogiochi, del settore della vendita al dettaglio e di registrazioni di operazioni.</span><span class="sxs-lookup"><span data-stu-id="79f83-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="79f83-107">Un modello di progettazione comune in tali applicazione consta nel tenere traccia delle modifiche apportate ai dati di Azure Cosmos DB, aggiornare le viste materializzate, eseguire analisi in tempo reale, memorizzare i dati nell'archiviazione offline sicura e attivare notifiche su determinati eventi in base a tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="79f83-108">Il **supporto del feed delle modifiche** in Azure Cosmos DB consente di creare soluzioni efficienti e scalabili per ognuno di questi modelli.</span><span class="sxs-lookup"><span data-stu-id="79f83-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="79f83-109">Con il supporto al feed delle modifiche, Azure Cosmos DB offre un elenco di documenti all'interno di una raccolta di Azure Cosmos DB, nell'ordine in cui questi sono stati modificati.</span><span class="sxs-lookup"><span data-stu-id="79f83-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="79f83-110">Il feed può essere usato per tenere traccia delle modifiche ai dati presenti nella raccolta e per eseguire operazioni come quelle seguenti:</span><span class="sxs-lookup"><span data-stu-id="79f83-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="79f83-111">Attivare una chiamata a un'API quando un documento viene inserito o modificato</span><span class="sxs-lookup"><span data-stu-id="79f83-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="79f83-112">Eseguire l'elaborazione in tempo reale (flusso) per gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="79f83-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="79f83-113">Sincronizzare i dati con una cache, un motore di ricerca o un data warehouse</span><span class="sxs-lookup"><span data-stu-id="79f83-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="79f83-114">Le modifiche in Azure Cosmos DB sono persistenti e possono essere elaborate in modo asincrono. Vengono inoltre distribuite a uno o più consumer per l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="79f83-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="79f83-115">Verranno ora esaminate le API per il feed delle modifiche e verrà illustrato come usarle per creare applicazioni scalabili in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="79f83-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="79f83-116">Questo articolo mostra come usare il feed di modifiche di Azure Cosmos DB e l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="79f83-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Uso del feed delle modifiche di Azure Cosmos DB per agevolare le analisi in tempo reale e gli scenari di calcolo guidati dagli eventi](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="79f83-118">Il supporto per il feed di modifiche è attualmente disponibile solo per l'API DocumentDB. Non sono attualmente supportate l'API Graph e l'API di tabella.</span><span class="sxs-lookup"><span data-stu-id="79f83-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="79f83-119">Casi d'uso e scenari</span><span class="sxs-lookup"><span data-stu-id="79f83-119">Use cases and scenarios</span></span>
<span data-ttu-id="79f83-120">Il feed delle modifiche consente di elaborare con efficienza set di dati di grandi dimensioni con volumi elevati di scritture e rappresenta un'alternativa alle query di interi set di dati per individuare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="79f83-121">Ad esempio, è possibile eseguire in modo efficiente le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="79f83-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="79f83-122">Aggiornare una cache, un indice di ricerca o un data warehouse con i dati archiviati in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="79f83-123">Implementare la suddivisione in livelli e l'archiviazione a livello di applicazione, in altre parole archiviare i dati più usati ("hot data") in Azure Cosmos DB e trasferire quelli meno usati ("cold data") in [Archivio BLOB di Azure](../storage/common/storage-introduction.md) o [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79f83-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="79f83-124">Implementare analisi in batch sui dati usando [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="79f83-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="79f83-125">Implementare [pipeline lambda in Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="79f83-126">Azure Cosmos DB offre una soluzione di database scalabile che può gestire sia l'inserimento che le query e implementare architetture lambda con costo totale di proprietà ridotto.</span><span class="sxs-lookup"><span data-stu-id="79f83-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="79f83-127">Effettuare migrazioni senza alcun tempo di inattività a un altro account Azure Cosmos DB con uno schema di partizionamento differente.</span><span class="sxs-lookup"><span data-stu-id="79f83-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="79f83-128">**Pipeline lambda con Azure Cosmos DB per l'inserimento e le query:**</span><span class="sxs-lookup"><span data-stu-id="79f83-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda basate su Azure Cosmos DB per l'inserimento e le query](./media/change-feed/lambda.png)

<span data-ttu-id="79f83-130">È possibile usare Azure Cosmos DB per ricevere e archiviare i dati di eventi da dispositivi, sensori, infrastrutture e applicazioni, per poi elaborarli in tempo reale con [Analisi di flusso di Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79f83-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="79f83-131">Nelle app Web e per dispositivi mobili [senza server](http://azure.com/serverless) è possibile tenere traccia di eventi come le modifiche al profilo, alle preferenze o alle località dei clienti per attivare determinate azioni come l'invio di notifiche push ai lori dispositivi tramite [Funzioni di Azure](../azure-functions/functions-bindings-documentdb.md) o [Servizi app](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="79f83-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="79f83-132">Se si usa Azure Cosmos DB per creare un gioco, è ad esempio possibile usare il feed delle modifiche per implementare classifiche in tempo reale in base ai punteggi delle partite completate.</span><span class="sxs-lookup"><span data-stu-id="79f83-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="79f83-133">Funzionamento del feed delle modifiche in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="79f83-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="79f83-134">Azure Cosmos DB offre la possibilità di leggere in modo incrementale gli aggiornamenti effettuati a una raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="79f83-135">Questo feed di modifiche ha le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="79f83-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="79f83-136">Le modifiche sono persistenti in Azure Cosmos DB e possono essere elaborate in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="79f83-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="79f83-137">Le modifiche ai documenti all'interno di una raccolta sono immediatamente disponibili nel feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="79f83-138">Ogni modifica apportata a un documento viene visualizzata una sola volta nel feed delle modifiche e i client gestiscono la logica di checkpoint.</span><span class="sxs-lookup"><span data-stu-id="79f83-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="79f83-139">La libreria del processore del feed delle modifiche fornisce funzionalità di checkpoint automatici e semantica di tipo "at least once".</span><span class="sxs-lookup"><span data-stu-id="79f83-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="79f83-140">Solo la modifica più recente per un determinato documento viene inclusa nel registro modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="79f83-141">Le modifiche intermedie potrebbero non essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="79f83-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="79f83-142">Il feed delle modifiche è ordinato in base all'ordine di modifica in ciascun valore di chiave della partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="79f83-143">Non esiste alcun ordine garantito tra i valori partition-key.</span><span class="sxs-lookup"><span data-stu-id="79f83-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="79f83-144">Le modifiche possono essere sincronizzate da qualsiasi punto nel tempo, in altre parole non è previsto un periodo di conservazione fisso per cui sono disponibili le modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="79f83-145">Le modifiche sono disponibili in blocchi di intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="79f83-146">Questa funzionalità consente di apportare modifiche da raccolte di grandi dimensioni per poi elaborarle in parallelo da più consumer/server.</span><span class="sxs-lookup"><span data-stu-id="79f83-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="79f83-147">Le applicazioni possono richiedere più feed delle modifiche alla volta nella stessa raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="79f83-148">Il feed di modifiche di Azure Cosmos DB è abilitato per impostazione predefinita per tutti gli account.</span><span class="sxs-lookup"><span data-stu-id="79f83-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="79f83-149">È possibile usare la [velocità effettiva con provisioning](request-units.md) nell'area di scrittura o in qualsiasi [area di lettura](distribute-data-globally.md) per leggere dal feed delle modifiche, proprio come ogni altra operazione da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="79f83-150">Il feed delle modifiche include le operazioni di aggiunte e aggiornamenti eseguite sui documenti all'interno della raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="79f83-151">È possibile acquisire le eliminazioni impostando un flag "eliminazione temporanea" all'interno dei documenti al posto delle eliminazioni.</span><span class="sxs-lookup"><span data-stu-id="79f83-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="79f83-152">In alternativa, è possibile impostare un periodo di scadenza delimitato per i documenti tramite la [funzionalità TTL](time-to-live.md), ad esempio 24 ore, e usare il valore di tale proprietà per acquisire le eliminazioni.</span><span class="sxs-lookup"><span data-stu-id="79f83-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="79f83-153">Con questa soluzione è necessario elaborare le modifiche in un intervallo di tempo minore rispetto al periodo di scadenza TTL.</span><span class="sxs-lookup"><span data-stu-id="79f83-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="79f83-154">Il feed delle modifiche è disponibile per ciascun intervallo di chiavi di partizioni all'interno nella raccolta dei documenti ed è pertanto possibile distribuirlo a uno o più consumer per l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="79f83-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Elaborazione distribuita del feed delle modifiche di Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="79f83-156">Sono disponibili alcune opzioni per l'implementazione di un feed di modifiche nel codice client.</span><span class="sxs-lookup"><span data-stu-id="79f83-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="79f83-157">Le sezioni immediatamente successive illustrano come implementare il feed di modifiche tramite l'API REST di Azure Cosmos DB e gli SDK di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="79f83-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="79f83-158">Per le applicazioni .NET è tuttavia consigliabile usare la nuova [Libreria del processore dei feed delle modifiche](#change-feed-processor) per l'elaborazione di eventi dal feed di modifiche, poiché semplifica la lettura delle modifiche tra le partizioni e abilita l'esecuzione in parallelo di più thread.</span><span class="sxs-lookup"><span data-stu-id="79f83-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="79f83-159"><a id="rest-apis"></a>Uso dell'API REST e degli SDK di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="79f83-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="79f83-160">Azure Cosmos DB offre contenitori elastici di archiviazione e velocità effettiva chiamati **raccolte**.</span><span class="sxs-lookup"><span data-stu-id="79f83-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="79f83-161">I dati nelle raccolte vengono raggruppati in modo logico tramite [chiavi di partizione](partition-data.md), per motivi di scalabilità e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="79f83-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="79f83-162">Azure Cosmos DB offre varie API per l'accesso ai dati, tra cui la ricerca per ID (Read/Get), le query e i feed di lettura (analisi).</span><span class="sxs-lookup"><span data-stu-id="79f83-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="79f83-163">È possibile ottenere il feed delle modifiche popolando due nuove intestazioni di richiesta nell'API `ReadDocumentFeed` di DocumentDB. Il feed può essere elaborato in parallelo su più intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="79f83-164">API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="79f83-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="79f83-165">Esaminiamo brevemente il funzionamento di ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="79f83-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="79f83-166">Azure Cosmos DB supporta la lettura di un feed di documenti all'interno di una raccolta tramite l'API `ReadDocumentFeed`.</span><span class="sxs-lookup"><span data-stu-id="79f83-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="79f83-167">La richiesta seguente restituisce ad esempio una pagina di documenti all'interno della raccolta `serverlogs`.</span><span class="sxs-lookup"><span data-stu-id="79f83-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="79f83-168">È possibile limitare i risultati usando l'intestazione `x-ms-max-item-count` e riprendere le letture inviando nuovamente la richiesta con un'intestazione `x-ms-continuation` restituita nella risposta precedente.</span><span class="sxs-lookup"><span data-stu-id="79f83-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="79f83-169">Quando eseguita da un singolo client, `ReadDocumentFeed` passa da un risultato all'altro sulle partizioni in modo seriale.</span><span class="sxs-lookup"><span data-stu-id="79f83-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="79f83-170">**Feed di documenti con lettura seriale**</span><span class="sxs-lookup"><span data-stu-id="79f83-170">**Serial read document feed**</span></span>

<span data-ttu-id="79f83-171">È anche possibile recuperare il feed di documenti usando uno degli [SDK di Azure Cosmos DB](documentdb-sdk-dotnet.md) supportati.</span><span class="sxs-lookup"><span data-stu-id="79f83-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="79f83-172">Il frammento di codice seguente mostra ad esempio come usare il [metodo ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span><span class="sxs-lookup"><span data-stu-id="79f83-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="79f83-173">Esecuzione distribuite di ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="79f83-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="79f83-174">Per le raccolte che contengono terabyte di dati o più o che ricevono volumi di aggiornamenti di grandi dimensioni, l'esecuzione seriale di un feed di lettura da una singola macchina client potrebbe non essere una soluzione pratica.</span><span class="sxs-lookup"><span data-stu-id="79f83-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="79f83-175">Per supportare questi scenari di Big Data, Azure Cosmos DB offre API per distribuire in modo trasparente le chiamate `ReadDocumentFeed` su più lettori/consumer client.</span><span class="sxs-lookup"><span data-stu-id="79f83-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="79f83-176">**ReadDocumentFeed distribuito**</span><span class="sxs-lookup"><span data-stu-id="79f83-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="79f83-177">Per offrire l'elaborazione scalabile delle modifiche incrementali, Azure Cosmos DB supporta un modello a scalabilità orizzontale per l'API del feed delle modifiche, basato sugli intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="79f83-178">È possibile ottenere un elenco degli intervalli di chiavi di partizione per una raccolta tramite una chiamata `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="79f83-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="79f83-179">Per ogni intervallo di chiavi di partizioni, è possibile eseguire un'operazione `ReadDocumentFeed` per leggere i documenti con chiavi di partizione comprese in tale intervallo.</span><span class="sxs-lookup"><span data-stu-id="79f83-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="79f83-180">Recupero degli intervalli di chiavi di partizione per una raccolta</span><span class="sxs-lookup"><span data-stu-id="79f83-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="79f83-181">È possibile recuperare gli intervalli di chiavi di partizione richiedendo la risorsa `pkranges` all'interno di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="79f83-182">Ad esempio, la richiesta seguente recupera l'elenco di intervalli di chiavi di partizione per la raccolta `serverlogs`:</span><span class="sxs-lookup"><span data-stu-id="79f83-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="79f83-183">Questa richiesta restituisce la risposta seguente che contiene i metadati sugli intervalli di chiavi di partizione:</span><span class="sxs-lookup"><span data-stu-id="79f83-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

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


<span data-ttu-id="79f83-184">**Partition Key Range Properties** (Proprietà dell'intervallo di chiavi di partizione): ogni intervallo di chiavi di partizione include le proprietà dei metadati nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="79f83-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="79f83-185">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="79f83-185">Header name</span></span></th>
        <th><span data-ttu-id="79f83-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79f83-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-187">id</span><span class="sxs-lookup"><span data-stu-id="79f83-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="79f83-188">L'ID per l'intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-188">The ID for the partition key range.</span></span> <span data-ttu-id="79f83-189">Si tratta di un ID stabile e univoco in ciascuna raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="79f83-190">Deve essere usato nella chiamata seguente per leggere le modifiche in base all'intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="79f83-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="79f83-192">Il valore hash di chiave di partizione massimo per l'intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="79f83-193">Solo per uso interno.</span><span class="sxs-lookup"><span data-stu-id="79f83-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="79f83-194">minInclusive</span></span></td>
        <td><span data-ttu-id="79f83-195">Il valore hash di chiave di partizione minimo per l'intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="79f83-196">Solo per uso interno.</span><span class="sxs-lookup"><span data-stu-id="79f83-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="79f83-197">È possibile farlo usando uno degli [SDK di Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="79f83-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="79f83-198">Ad esempio, il frammento seguente illustra come recuperare intervalli di chiavi di partizione in .NET usando il metodo [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="79f83-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="79f83-199">Azure Cosmos DB supporta il recupero di documenti per ogni intervallo di chiavi di partizione tramite l'impostazione dell'intestazione `x-ms-documentdb-partitionkeyrangeid` facoltativa.</span><span class="sxs-lookup"><span data-stu-id="79f83-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="79f83-200">Esecuzione di un ReadDocumentFeed incrementale</span><span class="sxs-lookup"><span data-stu-id="79f83-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="79f83-201">ReadDocumentFeed supporta i seguenti scenari/attività per l'elaborazione incrementale di modifiche apportate alle raccolte di Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="79f83-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="79f83-202">Lettura di tutte le modifiche ai documenti fin dall'inizio, ovvero dalla creazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="79f83-203">Lettura di tutte le modifiche agli aggiornamenti futuri dei documenti a partire dal momento corrente oppure tutte le modifiche da un momento specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="79f83-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="79f83-204">Lettura di tutte le modifiche ai documenti da una versione logica della raccolta (ETag).</span><span class="sxs-lookup"><span data-stu-id="79f83-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="79f83-205">È possibile creare checkpoint dei consumer in base all'ETag restituito dalle richieste read-feed incrementali.</span><span class="sxs-lookup"><span data-stu-id="79f83-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="79f83-206">Le modifiche includono aggiunte e aggiornamenti ai documenti.</span><span class="sxs-lookup"><span data-stu-id="79f83-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="79f83-207">Per acquisire le eliminazioni, è necessario usare una proprietà "eliminazione temporanea" all'interno di documenti oppure usare la [proprietà TTL integrata](time-to-live.md) per segnalare un'eliminazione in sospeso nel feed delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="79f83-208">La tabella seguente elenca la [richiesta](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e le [intestazioni delle risposte](/rest/api/documentdb/common-documentdb-rest-response-headers.md) per operazioni ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="79f83-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="79f83-209">**Intestazioni delle richieste per ReadDocumentFeed incrementale**:</span><span class="sxs-lookup"><span data-stu-id="79f83-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="79f83-210">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="79f83-210">Header name</span></span></th>
        <th><span data-ttu-id="79f83-211">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79f83-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="79f83-212">A-IM</span></span></td>
        <td><span data-ttu-id="79f83-213">Deve essere impostata su "Incremental feed" (Feed incrementale) oppure omessa</span><span class="sxs-lookup"><span data-stu-id="79f83-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="79f83-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="79f83-215">Nessuna intestazione: restituisce tutte le modifiche fin dall'inizio (creazione della raccolta)</span><span class="sxs-lookup"><span data-stu-id="79f83-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="79f83-216">"*": restituisce tutte le nuove modifiche ai dati all'interno della raccolta</span><span class="sxs-lookup"><span data-stu-id="79f83-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="79f83-217">&lt;etag&gt;: se impostato su un ETag di raccolta, restituisce tutte le modifiche effettuate da quel timestamp logico</span><span class="sxs-lookup"><span data-stu-id="79f83-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="79f83-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="79f83-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="79f83-219">Formato di ora RFC 1123. Ignorata se viene specificata l'intestazione If-None-Match</span><span class="sxs-lookup"><span data-stu-id="79f83-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="79f83-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="79f83-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="79f83-221">L'ID dell'intervallo di chiavi di partizione per la lettura dei dati.</span><span class="sxs-lookup"><span data-stu-id="79f83-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="79f83-222">**Intestazioni delle risposte per ReadDocumentFeed incrementale**:</span><span class="sxs-lookup"><span data-stu-id="79f83-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="79f83-223">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="79f83-223">Header name</span></span></th>
        <th><span data-ttu-id="79f83-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79f83-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-225">etag</span><span class="sxs-lookup"><span data-stu-id="79f83-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="79f83-226">Il numero di sequenza logica (LSN) dell'ultimo documento restituito nella risposta.</span><span class="sxs-lookup"><span data-stu-id="79f83-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="79f83-227">Un ReadDocumentFeed incrementale può essere ripreso inviando nuovamente questo valore in If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="79f83-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="79f83-228">Ecco una richiesta di esempio per restituire tutte le modifiche incrementali nella raccolta dalla versione logica/ETag `28535` con intervallo di chiavi di partizione = `16`:</span><span class="sxs-lookup"><span data-stu-id="79f83-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="79f83-229">Le modifiche vengono ordinate in base all'ora in ciascun valore di chiave di partizione all'interno dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="79f83-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="79f83-230">Non esiste alcun ordine garantito tra i valori partition-key.</span><span class="sxs-lookup"><span data-stu-id="79f83-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="79f83-231">Se sono presenti più risultati di quanti sia possibile visualizzare in una singola pagina, è possibile leggere la pagina successiva inviando nuovamente la richiesta con l'intestazione `If-None-Match` avente un valore uguale a `etag` della risposta precedente.</span><span class="sxs-lookup"><span data-stu-id="79f83-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="79f83-232">Se sono stati inseriti o aggiornati più documenti in modo transazionale in una procedura o in un trigger archiviati, questi verranno restituiti in un'unica pagina di risposta.</span><span class="sxs-lookup"><span data-stu-id="79f83-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="79f83-233">Il feed delle modifiche può consentire di ottenere un numero maggiore di elementi in una pagina rispetto a quanto specificato in `x-ms-max-item-count` in caso di inserimento o aggiornamento di più documenti in stored procedure o trigger.</span><span class="sxs-lookup"><span data-stu-id="79f83-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="79f83-234">Quando si usa .NET SDK (1.17.0), impostare il campo `StartTime` in `ChangeFeedOptions` per restituire direttamente i documenti modificati dal momento indicato da `StartTime` quando si chiama `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="79f83-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="79f83-235">Specificando `If-Modified-Since` usando l'API REST, la richiesta restituirà non i documenti stessi, ma il token di continuazione o `etag` nell'intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="79f83-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="79f83-236">Per restituire i documenti modificati nel periodo specificato, è necessario usare il token di continuazione `etag` nella richiesta successiva con `If-None-Match` per restituire i documenti effettivi.</span><span class="sxs-lookup"><span data-stu-id="79f83-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="79f83-237">.NET SDK fornisce le classi helper [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) per l'accesso alle modifiche apportate a una raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="79f83-238">Il frammento seguente mostra come recuperare tutte le modifiche dall'inizio usando l'SDK di .NET da un singolo client.</span><span class="sxs-lookup"><span data-stu-id="79f83-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

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
<span data-ttu-id="79f83-239">Il frammento seguente, invece, mostra come elaborare le modifiche in tempo reale con Azure Cosmos DB usando il supporto al feed delle modifiche e la funzione precedente.</span><span class="sxs-lookup"><span data-stu-id="79f83-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="79f83-240">La prima chiamata restituisce tutti i documenti nella raccolta e la seconda restituisce solo i due documenti creati dall'ultimo checkpoint.</span><span class="sxs-lookup"><span data-stu-id="79f83-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="79f83-241">È inoltre possibile filtrare il feed delle modifiche usando la logica lato client per elaborare eventi specifici.</span><span class="sxs-lookup"><span data-stu-id="79f83-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="79f83-242">Ad esempio, ecco un frammento di codice che usa LINQ lato client per elaborare solo gli eventi di modifica della temperatura dai sensori del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79f83-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="79f83-243"><a id="change-feed-processor"></a>Libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="79f83-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="79f83-244">Un'altra opzione consiste nell'usare la [libreria del processore dei feed delle modifiche di Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), che può semplificare la distribuzione dell'elaborazione di eventi da un feed di modifiche in più consumer.</span><span class="sxs-lookup"><span data-stu-id="79f83-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="79f83-245">La libreria è ottimale per la creazione di lettori di feed di modifiche nella piattaforma .NET.</span><span class="sxs-lookup"><span data-stu-id="79f83-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="79f83-246">Di seguito sono elencati alcuni flussi di lavoro che risulterebbero semplificati tramite l'uso della libreria del processore dei feed delle modifiche rispetto ai metodi inclusi in altri SDK di Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="79f83-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="79f83-247">Pull degli aggiornamenti dal feed di modifiche quando i dati vengono archiviati in più partizioni</span><span class="sxs-lookup"><span data-stu-id="79f83-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="79f83-248">Spostamento o replica di dati da una raccolta a un'altra</span><span class="sxs-lookup"><span data-stu-id="79f83-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="79f83-249">Esecuzione parallela di azioni attivate da aggiornamenti ai dati e ai feed di modifiche</span><span class="sxs-lookup"><span data-stu-id="79f83-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="79f83-250">Benché l'uso delle API in Cosmos SDK fornisca un accesso preciso agli aggiornamenti dei feed di modifiche in ogni partizione, l'uso della libreria del processore dei feed delle modifiche semplifica la lettura delle modifiche tra le partizioni e in più thread in esecuzione parallela.</span><span class="sxs-lookup"><span data-stu-id="79f83-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="79f83-251">Invece di leggere manualmente le modifiche da ogni contenitore e salvare un token di continuazione per ogni partizione, il processore dei feed di modifiche gestisce automaticamente la lettura delle modifiche nelle partizioni tramite un meccanismo di lease.</span><span class="sxs-lookup"><span data-stu-id="79f83-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="79f83-252">La libreria è disponibile come pacchetto NuGet, [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/), e dal codice sorgente come [esempio](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor) di GitHub.</span><span class="sxs-lookup"><span data-stu-id="79f83-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="79f83-253">Informazioni sulla libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="79f83-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="79f83-254">L'implementazione del processore dei feed di modifiche prevede quattro componenti principali, ovvero la raccolta monitorata, la raccolta di lease, l'host del processore e i consumer.</span><span class="sxs-lookup"><span data-stu-id="79f83-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="79f83-255">**Raccolta monitorata:** la raccolta monitorata include i dati da cui viene generato il feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="79f83-256">Eventuali inserimenti e modifiche alla raccolta monitorata vengono riflessi nel feed di modifiche della raccolta.</span><span class="sxs-lookup"><span data-stu-id="79f83-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="79f83-257">**Raccolta di lease:** la raccolta di lease coordina l'elaborazione dei feed di modifiche in più processi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="79f83-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="79f83-258">Una raccolta separata viene usata per archiviare i lease con un lease per partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="79f83-259">È consigliabile archiviare questa raccolta di lease in un account diverso, con un'area di scrittura più vicina alla posizione in cui è in esecuzione il processore dei feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="79f83-260">Un oggetto lease contiene gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="79f83-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="79f83-261">Owner: specifica l'host proprietario del lease.</span><span class="sxs-lookup"><span data-stu-id="79f83-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="79f83-262">Continuation: specifica la posizione (token di continuazione) nel feed di modifiche per una partizione specifica.</span><span class="sxs-lookup"><span data-stu-id="79f83-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="79f83-263">Timestamp: data dell'ultimo aggiornamento del lease. Il timestamp può essere usato per verificare se il lease viene considerato scaduto.</span><span class="sxs-lookup"><span data-stu-id="79f83-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="79f83-264">**Host del processore:** ogni host determina il numero di partizioni da elaborare in base al numero di istanze di host con lease attivi.</span><span class="sxs-lookup"><span data-stu-id="79f83-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="79f83-265">Quando un host viene avviato, acquisisce lease per bilanciare il carico di lavoro in tutti gli host.</span><span class="sxs-lookup"><span data-stu-id="79f83-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="79f83-266">Un host rinnova periodicamente i lease, in modo che i lease rimangano attivi.</span><span class="sxs-lookup"><span data-stu-id="79f83-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="79f83-267">Un host imposta come checkpoint il token di continuazione più recente sul rispettivo lease per ogni lettura.</span><span class="sxs-lookup"><span data-stu-id="79f83-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="79f83-268">Per garantire la sicurezza della concorrenza, un host verifica il valore ETag per ogni aggiornamento di lease.</span><span class="sxs-lookup"><span data-stu-id="79f83-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="79f83-269">Sono supportate anche altre strategie per i checkpoint.</span><span class="sxs-lookup"><span data-stu-id="79f83-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="79f83-270">All'arresto, un host rilascia tutti i lease ma mantiene le informazioni sulla continuazione, in modo che sia possibile riprendere la lettura dal checkpoint archiviato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="79f83-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="79f83-271">Il numero di host non può attualmente essere superiore al numero di partizioni (lease).</span><span class="sxs-lookup"><span data-stu-id="79f83-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="79f83-272">**Consumer:** i consumer, o processi di lavoro, sono thread che eseguono l'elaborazione del feed di modifiche avviata da ogni host.</span><span class="sxs-lookup"><span data-stu-id="79f83-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="79f83-273">Ogni host di processori può includere più consumer.</span><span class="sxs-lookup"><span data-stu-id="79f83-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="79f83-274">Ogni consumer legge il feed di modifiche dalla partizione a cui è assegnato e invia notifiche al rispettivo host in caso di modifiche e di lease scaduti.</span><span class="sxs-lookup"><span data-stu-id="79f83-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="79f83-275">Per una migliore comprensione dell'interazione tra i quattro elementi del processore dei feed di modifiche, è consigliabile esaminare un esempio nel diagramma seguente.</span><span class="sxs-lookup"><span data-stu-id="79f83-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="79f83-276">La raccolta monitorata archivia i documenti e usa il valore "city" come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="79f83-277">Come si può notare, la partizione blu contiene i documenti con il campo "city" compreso tra "A-E" e così via.</span><span class="sxs-lookup"><span data-stu-id="79f83-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="79f83-278">Sono disponibili due host, ognuno con due consumer che leggono dalle quattro partizioni in parallelo.</span><span class="sxs-lookup"><span data-stu-id="79f83-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="79f83-279">Le frecce mostrano i consumer che leggono da un punto specifico nel feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="79f83-280">Nella prima partizione il colore blu scuro rappresenta le modifiche non lette, mentre il colore blu chiaro rappresenta le modifiche già lette nel feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="79f83-281">Gli host usano la raccolta di lease per archiviare un valore di tipo "continuation" per tenere traccia della posizione di lettura corrente per ogni consumer.</span><span class="sxs-lookup"><span data-stu-id="79f83-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Uso dell'host del processore del feed delle modifiche di Azure Cosmos DB](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="79f83-283">Uso della libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="79f83-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="79f83-284">La sezione seguente illustra come usare la libreria del processore dei feed delle modifiche nel contesto della replica delle modifiche da una raccolta di origine a una raccolta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="79f83-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="79f83-285">In questo caso la raccolta di origine è la raccolta monitorata nel processore dei feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="79f83-286">**Installare e includere il pacchetto NuGet del processore dei feed di modifiche**</span><span class="sxs-lookup"><span data-stu-id="79f83-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="79f83-287">Prima di installare il pacchetto NuGet del processore dei feed di modifiche, è necessario installare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="79f83-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="79f83-288">Microsoft.Azure.DocumentDB, versione 1.13.1 o successiva</span><span class="sxs-lookup"><span data-stu-id="79f83-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="79f83-289">Newtonsoft.Json, versione 9.0.1 o successiva. Installare `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e includerlo come riferimento.</span><span class="sxs-lookup"><span data-stu-id="79f83-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="79f83-290">**Creare una raccolta monitorata, di lease e di destinazione**</span><span class="sxs-lookup"><span data-stu-id="79f83-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="79f83-291">Per usare la libreria del processore dei feed delle modifiche, è necessario che la raccolta di lease venga creata prima dell'esecuzione degli host dei processori.</span><span class="sxs-lookup"><span data-stu-id="79f83-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="79f83-292">Anche in questo caso, è consigliabile archiviare questa raccolta di lease in un account diverso, con un'area di scrittura più vicina alla posizione in cui è in esecuzione il processore dei feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="79f83-293">In questo esempio di spostamento dei dati è necessario creare la raccolta di destinazione prima di eseguire l'host del processore dei feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="79f83-294">Nel codice di esempio viene chiamato un metodo helper per creare la raccolta monitorata, la raccolta di lease e la raccolta di destinazione, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="79f83-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="79f83-295">La creazione di una raccolta ha implicazioni a livello di prezzi, poiché si sta riservando velocità effettiva per l'applicazione per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="79f83-296">Per altre informazioni, visitare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="79f83-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="79f83-297">*Creazione di un host di processori*</span><span class="sxs-lookup"><span data-stu-id="79f83-297">*Creating a processor host*</span></span>

<span data-ttu-id="79f83-298">La classe `ChangeFeedProcessorHost` fornisce un ambiente di runtime thread-safe, multiprocesso e sicuro per le implementazioni del processore di eventi che consente inoltre di gestire lease di checkpoint e di partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="79f83-299">Per usare la classe `ChangeFeedProcessorHost` è possibile implementare `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="79f83-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="79f83-300">Questa interfaccia contiene tre metodi:</span><span class="sxs-lookup"><span data-stu-id="79f83-300">This interface contains three methods:</span></span>

* <span data-ttu-id="79f83-301">`OpenAsync`: questa funzione viene chiamata quando viene aperto l'osservatore del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="79f83-302">È possibile modificarla in modo che esegua un'azione specifica all'apertura di un consumer/osservatore.</span><span class="sxs-lookup"><span data-stu-id="79f83-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="79f83-303">`CloseAsync`: questa funzione viene chiamata quando viene arrestato l'osservatore del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="79f83-304">È possibile modificarla in modo che esegua un'azione specifica alla chiusura di un consumer/osservatore.</span><span class="sxs-lookup"><span data-stu-id="79f83-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="79f83-305">`ProcessChangesAsync`: questa funzione viene chiamata quando nel feed di modifiche sono disponibili nuove modifiche al documento.</span><span class="sxs-lookup"><span data-stu-id="79f83-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="79f83-306">È possibile modificarla in modo che esegua un'azione specifica in corrispondenza di ogni aggiornamento al feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="79f83-307">In questo esempio l'interfaccia `IChangeFeedObserver` viene implementata tramite la classe `DocumentFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="79f83-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="79f83-308">In questo caso la funzione `ProcessChangesAsync` esegue l'upsert (aggiornamento) di un documento dal feed di modifiche nella raccolta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="79f83-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="79f83-309">Questo esempio risulta utile per lo spostamento di dati da una raccolta a un'altra in modo da modificare la chiave di partizione di un set di dati.</span><span class="sxs-lookup"><span data-stu-id="79f83-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="79f83-310">*Esecuzione dell'host di processori*</span><span class="sxs-lookup"><span data-stu-id="79f83-310">*Running the Processor Host*</span></span>

<span data-ttu-id="79f83-311">Prima di avviare l'elaborazione degli eventi, è possibile personalizzare le opzioni relative al feed di modifiche e all'host del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="79f83-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="79f83-312">Nelle tabelle seguenti sono riepilogati i campi specifici che è possibile personalizzare.</span><span class="sxs-lookup"><span data-stu-id="79f83-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="79f83-313">**Opzioni del feed di modifiche**:</span><span class="sxs-lookup"><span data-stu-id="79f83-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="79f83-314">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="79f83-314">Property Name</span></span></th>
        <th><span data-ttu-id="79f83-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79f83-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="79f83-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="79f83-317">Ottiene o imposta il numero massimo di elementi da restituire nell'operazione di enumerazione nel servizio di database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="79f83-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="79f83-319">Ottiene o imposta l'ID di intervallo di chiavi di partizioni per la richiesta corrente nel servizio di database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="79f83-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="79f83-321">Ottiene o imposta il token di continuazione della richiesta nel servizio di database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="79f83-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="79f83-322">SessionToken</span></span></td>
        <td><span data-ttu-id="79f83-323">Ottiene o imposta il token di sessione da usare con la coerenza di sessione nel servizio di database Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="79f83-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="79f83-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="79f83-325">Ottiene o imposta informazioni che indicano se il feed di modifiche nel servizio di database Azure Cosmos DB deve partire dall'inizio (true) o dalla posizione corrente (false).</span><span class="sxs-lookup"><span data-stu-id="79f83-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="79f83-326">Per impostazione predefinita, inizia dalla posizione corrente (false).</span><span class="sxs-lookup"><span data-stu-id="79f83-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="79f83-327">**Opzioni dell'host di feed di modifiche**:</span><span class="sxs-lookup"><span data-stu-id="79f83-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="79f83-328">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="79f83-328">Property Name</span></span></th>
        <th><span data-ttu-id="79f83-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="79f83-329">Type</span></span></th>
        <th><span data-ttu-id="79f83-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="79f83-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="79f83-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="79f83-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="79f83-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="79f83-333">Intervallo per tutti i lease per le partizioni attualmente disponibili nell'istanza ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="79f83-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="79f83-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="79f83-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="79f83-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="79f83-336">Intervallo per l'avvio di un'attività che consente di calcolare se le partizioni sono distribuite equamente tra le istanze di host note.</span><span class="sxs-lookup"><span data-stu-id="79f83-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="79f83-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="79f83-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="79f83-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="79f83-339">Intervallo che indica la durata di un lease su un lease che rappresenta una partizione.</span><span class="sxs-lookup"><span data-stu-id="79f83-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="79f83-340">Se il lease non viene rinnovato entro questo intervallo, risulta scaduto e la proprietà della partizione passa a un'altra istanza di ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="79f83-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="79f83-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="79f83-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="79f83-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="79f83-343">Ritardo tra il polling di una partizione alla ricerca di nuove modifiche al feed, dopo la rimozione di tutte le modifiche correnti.</span><span class="sxs-lookup"><span data-stu-id="79f83-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="79f83-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="79f83-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="79f83-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="79f83-346">Frequenza di applicazione di checkpoint ai lease.</span><span class="sxs-lookup"><span data-stu-id="79f83-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="79f83-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="79f83-348">int</span><span class="sxs-lookup"><span data-stu-id="79f83-348">Int</span></span></td>
        <td><span data-ttu-id="79f83-349">Numero minimo di partizioni per l'host.</span><span class="sxs-lookup"><span data-stu-id="79f83-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="79f83-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="79f83-351">int</span><span class="sxs-lookup"><span data-stu-id="79f83-351">Int</span></span></td>
        <td><span data-ttu-id="79f83-352">Numero massimo di partizioni che possono essere gestite dall'host.</span><span class="sxs-lookup"><span data-stu-id="79f83-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="79f83-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="79f83-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="79f83-354">Booleano</span><span class="sxs-lookup"><span data-stu-id="79f83-354">Bool</span></span></td>
        <td><span data-ttu-id="79f83-355">Indica se all'avvio dell'host è necessario eliminare tutti i lease esistenti e se l'host deve iniziare da zero.</span><span class="sxs-lookup"><span data-stu-id="79f83-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="79f83-356">Per avviare l'elaborazione di eventi, creare un'istanza di `ChangeFeedProcessorHost`, indicando i parametri appropriati per la raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="79f83-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="79f83-357">Chiamare quindi `RegisterObserverAsync` per registrare l'implementazione di `IChangeFeedObserver` (DocumentFeedObserver in questo esempio) nel runtime.</span><span class="sxs-lookup"><span data-stu-id="79f83-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="79f83-358">A questo punto, l'host prova ad acquisire un lease per ogni intervallo di chiavi di partizione nella raccolta di Azure Cosmos DB usando un algoritmo greedy.</span><span class="sxs-lookup"><span data-stu-id="79f83-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="79f83-359">Tali lease durano per un determinato intervallo di tempo e quindi devono essere rinnovati.</span><span class="sxs-lookup"><span data-stu-id="79f83-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="79f83-360">Appena nuovi nodi, in questo caso istanze di lavoro, passano online, inviano prenotazioni di lease e nel tempo il carico passa tra i nodi man mano che ogni host prova ad acquisire più lease.</span><span class="sxs-lookup"><span data-stu-id="79f83-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="79f83-361">Nel codice di esempio viene usata una classe factory (DocumentFeedObserverFactory.cs) per creare un osservatore e quindi viene usato `RegistObserverFactoryAsync` per registrare l'osservatore.</span><span class="sxs-lookup"><span data-stu-id="79f83-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="79f83-362">Con il passare del tempo, viene stabilito un equilibrio.</span><span class="sxs-lookup"><span data-stu-id="79f83-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="79f83-363">Questa funzionalità dinamica consente il ridimensionamento automatico basato su CPU da applicare ai consumer per aumentare o ridurre la capacità.</span><span class="sxs-lookup"><span data-stu-id="79f83-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="79f83-364">Se le modifiche sono disponibili in Azure Cosmos DB con velocità maggiore rispetto ai tempi di elaborazione dei consumer, è possibile usare l'aumento di CPU per i consumer per realizzare una scalabilità automatica sul numero di istanze del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="79f83-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79f83-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79f83-365">Next steps</span></span>
* <span data-ttu-id="79f83-366">Provare gli [esempi di codice relativi al feed delle modifiche di Azure Cosmos DB in GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="79f83-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="79f83-367">Introduzione alla scrittura di codice con gli [SDK di Cosmos DB](documentdb-sdk-dotnet.md) o l'[API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="79f83-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
