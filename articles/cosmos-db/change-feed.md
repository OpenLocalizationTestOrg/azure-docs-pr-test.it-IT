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
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="0755d-104">Utilizzo con il supporto feed hello modifica nel database di Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="0755d-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="0755d-105">[Azure Cosmos DB](../cosmos-db/introduction.md) è un servizio di database con replica a livello globale rapido e flessibile, usato per archiviare volumi elevati di dati transazionali e operativi, con una latenza stimabile in pochissimi millisecondi a cifra singola per le operazioni di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="0755d-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="0755d-106">Tutto questo lo rende particolarmente adatto per le applicazioni IoT, di videogiochi, del settore della vendita al dettaglio e di registrazioni di operazioni.</span><span class="sxs-lookup"><span data-stu-id="0755d-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="0755d-107">Un modello di progettazione comuni in queste applicazioni è tootrack modifiche apportate tooAzure DB Cosmos dati e aggiornare le viste materializzate, eseguono analitica in tempo reale, toocold archiviazione dei dati e notifiche di trigger a determinati eventi in base a queste modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="0755d-108">Hello **modifica feed supporto** nel database di Azure Cosmos consente toobuild efficienti e scalabili soluzioni per ognuno di questi modelli.</span><span class="sxs-lookup"><span data-stu-id="0755d-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="0755d-109">Con modifica feed supporto, DB Cosmos Azure fornisce un elenco ordinato di documenti all'interno di una raccolta di Azure Cosmos DB nell'ordine di hello in cui essi sono stati modificati.</span><span class="sxs-lookup"><span data-stu-id="0755d-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="0755d-110">Questo feed può essere utilizzato toolisten per modifiche toodata insieme hello ed eseguire azioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0755d-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="0755d-111">Attivare tooan una chiamata API quando un documento viene inserito o modificato</span><span class="sxs-lookup"><span data-stu-id="0755d-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="0755d-112">Eseguire l'elaborazione in tempo reale (flusso) per gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="0755d-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="0755d-113">Sincronizzare i dati con una cache, un motore di ricerca o un data warehouse</span><span class="sxs-lookup"><span data-stu-id="0755d-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="0755d-114">Le modifiche in Azure Cosmos DB sono persistenti e possono essere elaborate in modo asincrono. Vengono inoltre distribuite a uno o più consumer per l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="0755d-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="0755d-115">Diamo un'occhiata hello API per i feed di modifica e come è possibile usarli toobuild di applicazioni scalabili in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="0755d-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="0755d-116">In questo articolo viene illustrato come modificare toowork con Azure Cosmos DB feed e hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0755d-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![L'utilizzo di Azure Cosmos DB change feed toopower in tempo reale analitica e scenari di elaborazione basato su eventi](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="0755d-118">Modifica supporto feed viene fornita solo per l'API DocumentDB hello in questa fase. Hello API Graph e API di tabella non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="0755d-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="0755d-119">Casi d'uso e scenari</span><span class="sxs-lookup"><span data-stu-id="0755d-119">Use cases and scenarios</span></span>
<span data-ttu-id="0755d-120">Feed di modifica consente un'elaborazione efficiente di DataSet di grandi dimensioni con un numero elevato di scritture e offre un tooidentify intero set di dati alternativo tooquerying cosa è cambiato.</span><span class="sxs-lookup"><span data-stu-id="0755d-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="0755d-121">Ad esempio, è possibile eseguire hello seguenti in modo efficiente attività:</span><span class="sxs-lookup"><span data-stu-id="0755d-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="0755d-122">Aggiornare una cache, un indice di ricerca o un data warehouse con i dati archiviati in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0755d-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="0755d-123">Implementare la suddivisione in livelli e l'archiviazione dei dati a livello di applicazione, vale a dire memorizzarli "attivo" nel database di Azure Cosmos e age "dati freddo" troppo[archiviazione Blob di Azure](../storage/common/storage-introduction.md) o [archivio Azure Data Lake](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0755d-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="0755d-124">Implementare analisi in batch sui dati usando [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="0755d-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="0755d-125">Implementare [pipeline lambda in Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0755d-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="0755d-126">Azure Cosmos DB offre una soluzione di database scalabile che può gestire sia l'inserimento che le query e implementare architetture lambda con costo totale di proprietà ridotto.</span><span class="sxs-lookup"><span data-stu-id="0755d-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="0755d-127">Eseguire zero tooanother tempi di inattività migrazioni account Azure Cosmos DB con uno schema di partizionamento differente.</span><span class="sxs-lookup"><span data-stu-id="0755d-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="0755d-128">**Pipeline lambda con Azure Cosmos DB per l'inserimento e le query:**</span><span class="sxs-lookup"><span data-stu-id="0755d-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda basate su Azure Cosmos DB per l'inserimento e le query](./media/change-feed/lambda.png)

<span data-ttu-id="0755d-130">È possibile utilizzare Azure Cosmos DB tooreceive e archiviare i dati di evento di dispositivi, sensori, infrastruttura e le applicazioni ed elaborare questi eventi in tempo reale con [Azure flusso Analitica](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), o [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0755d-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="0755d-131">All'interno del [senza](http://azure.com/serverless) web e App per dispositivi mobili, è possibile tenere traccia eventi, ad esempio tootrigger di profilo, le preferenze o alla posizione del cliente tooyour modifiche determinate azioni come l'invio di push dispositivi tootheir notifiche utilizzando [Funzioni di azure](../azure-functions/functions-bindings-documentdb.md) o [servizi App](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0755d-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="0755d-132">Se si usa Azure Cosmos DB toobuild un gioco, è possibile utilizzare ad esempio, in tempo reale classifiche tooimplement feed cambia in base ai punteggi di giochi completati.</span><span class="sxs-lookup"><span data-stu-id="0755d-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="0755d-133">Funzionamento del feed delle modifiche in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0755d-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="0755d-134">DB Cosmos Azure fornisce hello possibilità tooincrementally leggere gli aggiornamenti apportati tooan DB Cosmos Azure insieme.</span><span class="sxs-lookup"><span data-stu-id="0755d-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="0755d-135">Questo feed di modifica è hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0755d-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="0755d-136">Le modifiche sono persistenti in Azure Cosmos DB e possono essere elaborate in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="0755d-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="0755d-137">Toodocuments modifiche all'interno di una raccolta sono disponibili immediatamente in hello modifica feed.</span><span class="sxs-lookup"><span data-stu-id="0755d-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="0755d-138">Ogni documento tooa modifica viene visualizzata una sola volta nel feed modifica hello e client di gestire la logica di checkpoint.</span><span class="sxs-lookup"><span data-stu-id="0755d-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="0755d-139">libreria di feed processore modifiche Hello fornisce funzionalità dei checkpoint automatici e "at least once" semantica.</span><span class="sxs-lookup"><span data-stu-id="0755d-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="0755d-140">La modifica più recente hello solo per un determinato documento è incluso nel registro delle modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="0755d-141">Le modifiche intermedie potrebbero non essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="0755d-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="0755d-142">Hello modifica feed viene ordinato in ordine di modifica all'interno di ogni valore di chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="0755d-143">Non esiste alcun ordine garantito tra i valori partition-key.</span><span class="sxs-lookup"><span data-stu-id="0755d-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="0755d-144">Le modifiche possono essere sincronizzate da qualsiasi punto nel tempo, in altre parole non è previsto un periodo di conservazione fisso per cui sono disponibili le modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="0755d-145">Le modifiche sono disponibili in blocchi di intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="0755d-146">Questa funzionalità consente di apportare modifiche da elaborare in parallelo da più consumer/server toobe di raccolte di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="0755d-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="0755d-147">Le applicazioni possono richiedere per la modifica più feed contemporaneamente su hello stessa raccolta.</span><span class="sxs-lookup"><span data-stu-id="0755d-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="0755d-148">Il feed di modifiche di Azure Cosmos DB è abilitato per impostazione predefinita per tutti gli account.</span><span class="sxs-lookup"><span data-stu-id="0755d-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="0755d-149">È possibile utilizzare il [velocità effettiva di provisioning](request-units.md) nella propria area di scrittura o in una [leggere area](distribute-data-globally.md) tooread da hello modificare feed, esattamente come qualsiasi altra operazione dal database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0755d-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="0755d-150">Hello modifica feed inclusi inserimenti e operazioni di aggiornamento eseguite toodocuments insieme hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="0755d-151">È possibile acquisire le eliminazioni impostando un flag "eliminazione temporanea" all'interno dei documenti al posto delle eliminazioni.</span><span class="sxs-lookup"><span data-stu-id="0755d-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="0755d-152">In alternativa, è possibile impostare un periodo di scadenza per i documenti tramite hello [funzionalità TTL](time-to-live.md), ad esempio, 24 ore e l'utilizzo hello valore della proprietà toocapture Elimina.</span><span class="sxs-lookup"><span data-stu-id="0755d-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="0755d-153">Con questa soluzione, è possibile tooprocess modifiche entro un intervallo di tempo più breve rispetto al periodo di scadenza della durata (TTL) hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="0755d-154">Hello modifica feed è disponibile per ogni intervallo di chiavi di partizione di raccolta del documento hello e pertanto possono essere distribuiti in uno o più consumer per l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="0755d-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Elaborazione distribuita del feed delle modifiche di Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="0755d-156">Sono disponibili alcune opzioni per l'implementazione di un feed di modifiche nel codice client.</span><span class="sxs-lookup"><span data-stu-id="0755d-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="0755d-157">Hello sezioni che immediatamente seguono descrivono come tooimplement hello feed di modifica tramite API REST di Azure Cosmos DB hello e hello SDK di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0755d-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="0755d-158">Tuttavia, per le applicazioni .NET, è consigliabile utilizzare la nuova hello [processore libreria di feed di modifica](#change-feed-processor) per l'elaborazione eventi da hello modificano feed come semplifica la lettura modifiche tra le partizioni e consente a più thread in esecuzione Parallel.</span><span class="sxs-lookup"><span data-stu-id="0755d-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="0755d-159"><a id="rest-apis"></a>Utilizzo di hello REST API e SDK di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0755d-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="0755d-160">Azure Cosmos DB offre contenitori elastici di archiviazione e velocità effettiva chiamati **raccolte**.</span><span class="sxs-lookup"><span data-stu-id="0755d-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="0755d-161">I dati nelle raccolte vengono raggruppati in modo logico tramite [chiavi di partizione](partition-data.md), per motivi di scalabilità e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="0755d-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="0755d-162">Azure Cosmos DB offre varie API per l'accesso ai dati, tra cui la ricerca per ID (Read/Get), le query e i feed di lettura (analisi).</span><span class="sxs-lookup"><span data-stu-id="0755d-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="0755d-163">Hello feed modifica può essere ottenuto tramite due toohello di intestazioni di richiesta DocumentDB nuova `ReadDocumentFeed` API e possono essere elaborati in parallelo tra intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="0755d-164">API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="0755d-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="0755d-165">Esaminiamo brevemente il funzionamento di ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="0755d-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="0755d-166">DB Cosmos Azure supporta la lettura di un feed di documenti all'interno di una raccolta tramite hello `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="0755d-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="0755d-167">Ad esempio, hello richiesta seguente restituisce una pagina di documenti all'interno di hello `serverlogs` insieme.</span><span class="sxs-lookup"><span data-stu-id="0755d-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="0755d-168">Risultati possono essere limitati tramite hello `x-ms-max-item-count` intestazione, operazioni di lettura e può essere ripresi reinviando la richiesta di hello con un `x-ms-continuation` intestazione restituita nella risposta precedente hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="0755d-169">Quando eseguita da un singolo client, `ReadDocumentFeed` passa da un risultato all'altro sulle partizioni in modo seriale.</span><span class="sxs-lookup"><span data-stu-id="0755d-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="0755d-170">**Feed di documenti con lettura seriale**</span><span class="sxs-lookup"><span data-stu-id="0755d-170">**Serial read document feed**</span></span>

<span data-ttu-id="0755d-171">È inoltre possibile recuperare il feed hello di documenti tramite uno dei hello supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0755d-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0755d-172">Ad esempio, hello seguente mostra come hello toouse [ReadDocumentFeedAsync metodo](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span><span class="sxs-lookup"><span data-stu-id="0755d-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="0755d-173">Esecuzione distribuite di ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="0755d-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="0755d-174">Per le raccolte che contengono terabyte di dati o più o che ricevono volumi di aggiornamenti di grandi dimensioni, l'esecuzione seriale di un feed di lettura da una singola macchina client potrebbe non essere una soluzione pratica.</span><span class="sxs-lookup"><span data-stu-id="0755d-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="0755d-175">In ordine toosupport questi scenari di dati di grandi dimensioni, Azure Cosmos DB fornisce API toodistribute `ReadDocumentFeed` chiamate in modo trasparente tra più client lettori/consumer.</span><span class="sxs-lookup"><span data-stu-id="0755d-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="0755d-176">**ReadDocumentFeed distribuito**</span><span class="sxs-lookup"><span data-stu-id="0755d-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="0755d-177">l'elaborazione scalabile tooprovide delle modifiche incrementali, Azure Cosmos DB supporta un modello di scalabilità orizzontale per modifica hello feed API basata su intervalli di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="0755d-178">È possibile ottenere un elenco degli intervalli di chiavi di partizione per una raccolta tramite una chiamata `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="0755d-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="0755d-179">Per ogni intervallo di chiavi di partizione, è possibile eseguire un `ReadDocumentFeed` tooread documenti con le chiavi di partizione all'interno dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="0755d-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="0755d-180">Recupero degli intervalli di chiavi di partizione per una raccolta</span><span class="sxs-lookup"><span data-stu-id="0755d-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="0755d-181">È possibile recuperare intervalli di chiavi di partizione hello hello richiedente `pkranges` risorsa all'interno di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="0755d-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="0755d-182">Ad esempio hello richiesta seguente recupera hello elenco di intervalli di chiavi di partizione per hello `serverlogs` raccolta:</span><span class="sxs-lookup"><span data-stu-id="0755d-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="0755d-183">Questa richiesta restituisce hello risposta contenente i metadati relativi a intervalli di chiavi di partizione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="0755d-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="0755d-184">**Proprietà di intervallo di chiavi di partizione**: ogni intervallo di chiavi di partizione include le proprietà dei metadati hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0755d-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0755d-185">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="0755d-185">Header name</span></span></th>
        <th><span data-ttu-id="0755d-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0755d-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-187">id</span><span class="sxs-lookup"><span data-stu-id="0755d-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="0755d-188">ID di Hello per intervalli di chiavi di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="0755d-189">Si tratta di un ID stabile e univoco in ciascuna raccolta.</span><span class="sxs-lookup"><span data-stu-id="0755d-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="0755d-190">Deve essere utilizzata hello dopo le modifiche tooread chiamata dall'intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="0755d-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="0755d-192">valore di hash di chiave Hello massima di una partizione per intervalli di chiavi di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0755d-193">Solo per uso interno.</span><span class="sxs-lookup"><span data-stu-id="0755d-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="0755d-194">minInclusive</span></span></td>
        <td><span data-ttu-id="0755d-195">valore hash della chiave di Hello minime partizione per intervalli di chiavi di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0755d-196">Solo per uso interno.</span><span class="sxs-lookup"><span data-stu-id="0755d-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="0755d-197">È possibile farlo usando uno dei hello supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0755d-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0755d-198">Ad esempio, hello frammento di codice seguente mostra come chiave di partizione tooretrieve intervalli in .NET utilizzando hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metodo.</span><span class="sxs-lookup"><span data-stu-id="0755d-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="0755d-199">DB Cosmos Azure supporta il recupero di documenti per intervalli di chiavi di partizione mediante impostazione hello facoltativo `x-ms-documentdb-partitionkeyrangeid` intestazione.</span><span class="sxs-lookup"><span data-stu-id="0755d-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="0755d-200">Esecuzione di un ReadDocumentFeed incrementale</span><span class="sxs-lookup"><span data-stu-id="0755d-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="0755d-201">ReadDocumentFeed supporta i seguenti scenari/attività per l'elaborazione incrementale di modifiche apportate nelle raccolte di Azure Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="0755d-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="0755d-202">Lettura di tutte le modifica, ovvero toodocuments dall'inizio di hello, dalla creazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="0755d-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="0755d-203">Lettura di tutte le modifica toofuture aggiornamenti toodocuments dall'ora corrente o tutte le modifiche dopo l'ora specificata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="0755d-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="0755d-204">Leggere tutte le modifiche toodocuments da una versione logica dell'insieme di hello (ETag).</span><span class="sxs-lookup"><span data-stu-id="0755d-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="0755d-205">È possibile consentire agli utenti in base a hello restituito ETag da richieste di lettura feed incrementale checkpoint.</span><span class="sxs-lookup"><span data-stu-id="0755d-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="0755d-206">le modifiche di Hello includono toodocuments inserimenti e aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="0755d-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="0755d-207">Elimina toocapture, è necessario usare una proprietà di "eliminazione temporanea" all'interno dei documenti o utilizzare hello [proprietà di durata (TTL) predefinita](time-to-live.md) toosignal un'eliminazione in sospeso in hello modificare feed.</span><span class="sxs-lookup"><span data-stu-id="0755d-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="0755d-208">Hello seguente tabella elenca hello [richiesta](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [le intestazioni di risposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) per le operazioni di ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="0755d-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="0755d-209">**Intestazioni delle richieste per ReadDocumentFeed incrementale**:</span><span class="sxs-lookup"><span data-stu-id="0755d-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0755d-210">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="0755d-210">Header name</span></span></th>
        <th><span data-ttu-id="0755d-211">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0755d-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="0755d-212">A-IM</span></span></td>
        <td><span data-ttu-id="0755d-213">Deve essere impostato troppo "Feed incrementale", o viene omesso in caso contrario</span><span class="sxs-lookup"><span data-stu-id="0755d-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="0755d-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="0755d-215">Nessuna intestazione: restituisce tutte le modifiche da hello a partire da (creazione raccolta)</span><span class="sxs-lookup"><span data-stu-id="0755d-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="0755d-216">"*": restituisce tutte le nuove modifiche toodata insieme hello</span><span class="sxs-lookup"><span data-stu-id="0755d-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="0755d-217">&lt;eTag&gt;: se impostata tooa raccolta ETag, restituisce tutte le modifiche apportate da tale timestamp logico</span><span class="sxs-lookup"><span data-stu-id="0755d-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="0755d-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="0755d-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="0755d-219">Formato di ora RFC 1123. Ignorata se viene specificata l'intestazione If-None-Match</span><span class="sxs-lookup"><span data-stu-id="0755d-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="0755d-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="0755d-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="0755d-221">Hello ID intervalli di chiavi di partizione per la lettura dei dati.</span><span class="sxs-lookup"><span data-stu-id="0755d-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="0755d-222">**Intestazioni delle risposte per ReadDocumentFeed incrementale**:</span><span class="sxs-lookup"><span data-stu-id="0755d-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="0755d-223">Nome intestazione</span><span class="sxs-lookup"><span data-stu-id="0755d-223">Header name</span></span></th>
        <th><span data-ttu-id="0755d-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0755d-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-225">etag</span><span class="sxs-lookup"><span data-stu-id="0755d-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="0755d-226">numero di sequenza logica di Hello (LSN) dell'ultimo documento restituito nella risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="0755d-227">Un ReadDocumentFeed incrementale può essere ripreso inviando nuovamente questo valore in If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="0755d-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="0755d-228">Ecco un tooreturn di richiesta di esempio tutte le modifiche incrementali nella raccolta dalla versione di hello logico/ETag `28535` e intervalli di chiavi di partizione = `16`:</span><span class="sxs-lookup"><span data-stu-id="0755d-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="0755d-229">Le modifiche sono ordinate per tempo all'interno di ogni valore di chiave di partizione all'interno di intervalli di chiavi di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="0755d-230">Non esiste alcun ordine garantito tra i valori partition-key.</span><span class="sxs-lookup"><span data-stu-id="0755d-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="0755d-231">Se sono presenti più risultati rispetto a visualizzabili in una singola pagina, è possibile leggere pagina di risultati successiva hello reinviando la richiesta di hello con hello `If-None-Match` intestazione con valore uguale toohello `etag` dalla risposta precedente hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="0755d-232">Se più documenti inseriti o aggiornati in modo transazionale all'interno di una stored procedure o trigger, saranno tutti restituiti all'interno di hello stessa pagina di risposta.</span><span class="sxs-lookup"><span data-stu-id="0755d-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="0755d-233">Con il feed di modifica, è possibile ottenere ulteriori elementi restituiti in una pagina, rispetto a quanto specificato `x-ms-max-item-count` nel caso di hello di più documenti inserita o aggiornata all'interno di una stored procedure o trigger.</span><span class="sxs-lookup"><span data-stu-id="0755d-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="0755d-234">Quando si utilizza hello .NET SDK (1.17.0), impostare il campo hello `StartTime` in `ChangeFeedOptions` toodirectly restituito modificare documenti dal `StartTime` quando si chiama `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="0755d-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="0755d-235">Specificando `If-Modified-Since` utilizza hello API REST, la richiesta restituirà i non hello documenti stessi, ma piuttosto il token di continuazione hello o `etag` nell'intestazione di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="0755d-236">documenti di hello tooreturn hello modificato specificato, il token di continuazione hello `etag` deve quindi essere utilizzato nella successiva richiesta di hello con `If-None-Match` tooreturn hello documenti effettivi.</span><span class="sxs-lookup"><span data-stu-id="0755d-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="0755d-237">Hello .NET SDK fornisce hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess modifiche tooa insieme le classi di supporto.</span><span class="sxs-lookup"><span data-stu-id="0755d-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="0755d-238">Hello frammento di codice seguente viene illustrato come tooretrieve tutti cambia dall'inizio hello utilizzando hello .NET SDK da un singolo client.</span><span class="sxs-lookup"><span data-stu-id="0755d-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="0755d-239">E hello frammento di codice seguente viene illustrato come tooprocess cambia in tempo reale con Azure Cosmos DB utilizzando Modifica hello feed supporto e hello funzione precedente.</span><span class="sxs-lookup"><span data-stu-id="0755d-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="0755d-240">Hello prima chiamata restituisce tutti i documenti hello nella raccolta hello e hello secondo restituisce solo hello creati due documenti che sono stati creati dall'ultimo checkpoint hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="0755d-241">È inoltre possibile filtrare i feed di modifica hello tramite eventi di processo tooselectively logica sul lato client.</span><span class="sxs-lookup"><span data-stu-id="0755d-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="0755d-242">Ad esempio, di seguito è riportato un frammento che utilizza tooprocess LINQ sul lato client, solo gli eventi di modifica temperatura da sensori di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0755d-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="0755d-243"><a id="change-feed-processor"></a>Libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="0755d-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="0755d-244">Un'altra opzione consiste hello toouse [libreria DB Cosmos Azure modificare Feed processore](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), che consentono di distribuire facilmente l'elaborazione di una modifica feed tra più consumer di eventi.</span><span class="sxs-lookup"><span data-stu-id="0755d-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="0755d-245">libreria Hello è molto utile per la compilazione di modifica feed lettori sulla piattaforma .NET hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="0755d-246">Alcuni flussi di lavoro che sarebbe stata più semplice tramite metodi hello inclusi in hello libreria processore Feed modifiche hello altri SDK di DB Cosmos includono:</span><span class="sxs-lookup"><span data-stu-id="0755d-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="0755d-247">Pull degli aggiornamenti dal feed di modifiche quando i dati vengono archiviati in più partizioni</span><span class="sxs-lookup"><span data-stu-id="0755d-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="0755d-248">Lo spostamento o la replica dei dati da una raccolta tooanother</span><span class="sxs-lookup"><span data-stu-id="0755d-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="0755d-249">Esecuzione parallela di azioni attivate dal toodata gli aggiornamenti e modifica di feed</span><span class="sxs-lookup"><span data-stu-id="0755d-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="0755d-250">Durante l'uso di API Ciao hello Cosmos SDK offre accesso preciso toochange feed gli aggiornamenti in ogni partizione, l'utilizzo di libreria di Feed processore delle modifiche hello semplifica le modifiche di lettura tra partizioni e di più thread eseguiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="0755d-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="0755d-251">Anziché manualmente legge le modifiche da ogni contenitore e il salvataggio di un token di continuazione per ogni partizione, hello processore Feed modifiche gestisce automaticamente le modifiche di lettura tra partizioni utilizzando un meccanismo di lease.</span><span class="sxs-lookup"><span data-stu-id="0755d-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="0755d-252">libreria Hello è disponibile come pacchetto NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e dal codice sorgente come un archivio Github [esempio](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="0755d-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="0755d-253">Informazioni sulla libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="0755d-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="0755d-254">Esistono quattro componenti principali dell'implementazione hello Feed processore di modifica: hello monitorati insieme, insieme di lease hello, hello processore host e i consumer di hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="0755d-255">**Raccolta monitorato:** raccolta di hello monitorato è hello ai dati da cui hello viene generato il feed di modifica.</span><span class="sxs-lookup"><span data-stu-id="0755d-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="0755d-256">Qualsiasi raccolta toohello monitorato gli inserimenti e le modifiche vengono riflesse nel feed di hello modifica della raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="0755d-257">**Raccolta di lease:** hello lease raccolta coordinate modifica hello feed tra più processi di lavoro di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="0755d-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="0755d-258">Una raccolta separata è lease hello toostore usato con un lease per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="0755d-259">È più vantaggiosa toostore questa raccolta di lease in un altro account con hello scrivere hello toowhere più vicino area Modifica Feed processore è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0755d-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0755d-260">Oggetto lease contiene hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0755d-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="0755d-261">Proprietario: Specifica l'host hello proprietario di lease hello</span><span class="sxs-lookup"><span data-stu-id="0755d-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="0755d-262">Continuazione: Posizione hello (token di continuazione) in modifica hello feed per una determinata partizione</span><span class="sxs-lookup"><span data-stu-id="0755d-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="0755d-263">Timestamp: Ora dell'ultimo aggiornamento lease; Hello timestamp può essere utilizzato toocheck se lease hello è considerato scaduto</span><span class="sxs-lookup"><span data-stu-id="0755d-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="0755d-264">**Host processore:** ogni host determina quanti tooprocess partizioni in base a numero di altre istanze di host presenti presentano lease attivi.</span><span class="sxs-lookup"><span data-stu-id="0755d-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="0755d-265">Quando un host viene avviata, acquisisce il carico di lavoro di lease toobalance hello in tutti gli host.</span><span class="sxs-lookup"><span data-stu-id="0755d-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="0755d-266">Un host rinnova periodicamente i lease, in modo che i lease rimangano attivi.</span><span class="sxs-lookup"><span data-stu-id="0755d-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="0755d-267">Un host checkpoint hello ultimo continuazione token tooits lease per ogni lettura.</span><span class="sxs-lookup"><span data-stu-id="0755d-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="0755d-268">tooensure concorrenza, un host i controlli di sicurezza hello ETag per ogni aggiornamento di lease.</span><span class="sxs-lookup"><span data-stu-id="0755d-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="0755d-269">Sono supportate anche altre strategie per i checkpoint.</span><span class="sxs-lookup"><span data-stu-id="0755d-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="0755d-270">Durante l'arresto, un host rilascia tutti i lease ma mantiene hello informazioni di continuazione, in modo da poter riprendere la lettura da hello stored checkpoint in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="0755d-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="0755d-271">In questo momento il numero di hello di host non può essere maggiore del numero di hello di partizioni (lease).</span><span class="sxs-lookup"><span data-stu-id="0755d-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="0755d-272">**I consumer:** consumer, o thread di lavoro, sono i thread che eseguono modifiche hello feed elaborazione avviata da ogni host.</span><span class="sxs-lookup"><span data-stu-id="0755d-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="0755d-273">Ogni host di processori può includere più consumer.</span><span class="sxs-lookup"><span data-stu-id="0755d-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="0755d-274">Ogni consumer legge hello modifica feed da hello partizione assegnata tooand notifica relativo host delle modifiche e lease scaduti.</span><span class="sxs-lookup"><span data-stu-id="0755d-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="0755d-275">toofurther comprensione dell'interazione tra questi quattro elementi di Feed processore delle modifiche, esaminiamo un esempio in hello seguente diagramma.</span><span class="sxs-lookup"><span data-stu-id="0755d-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="0755d-276">Hello monitorati raccolta documenti di archivi e utilizza city"hello" come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="0755d-277">Vediamo che partizione hello blu contiene documenti con campo "città" hello "A-E" e così via.</span><span class="sxs-lookup"><span data-stu-id="0755d-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="0755d-278">Esistono due host, ciascuno con due consumer lettura dalle partizioni hello quattro in parallelo.</span><span class="sxs-lookup"><span data-stu-id="0755d-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="0755d-279">le frecce di Hello indicano i consumer di hello durante la lettura da un punto specifico in hello modificare feed.</span><span class="sxs-lookup"><span data-stu-id="0755d-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="0755d-280">Nella prima partizione hello, blu scuro hello rappresenta le modifiche da leggere mentre celeste hello rappresenta hello già letto le modifiche nel feed modifica hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="0755d-281">gli host di Hello utilizzano hello lease raccolta toostore una traccia di tookeep "continuazione" valore di hello corrente durante la lettura della posizione per ciascun consumer.</span><span class="sxs-lookup"><span data-stu-id="0755d-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![L'utilizzo di hello Azure Cosmos DB change feed host processore](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="0755d-283">Uso della libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="0755d-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="0755d-284">Hello seguente sezione viene illustrato come toouse hello libreria di Feed processore delle modifiche nel contesto di hello di replica delle modifiche da una raccolta di destinazione tooa raccolta di origine.</span><span class="sxs-lookup"><span data-stu-id="0755d-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="0755d-285">In questo caso, hello origine è hello monitorato insieme nel processore di modifica del Feed.</span><span class="sxs-lookup"><span data-stu-id="0755d-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="0755d-286">**Installare e includere pacchetto NuGet di processore Feed modifica hello**</span><span class="sxs-lookup"><span data-stu-id="0755d-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="0755d-287">Prima di installare il pacchetto NuGet del processore dei feed di modifiche, è necessario installare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0755d-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="0755d-288">Microsoft.Azure.DocumentDB, versione 1.13.1 o successiva</span><span class="sxs-lookup"><span data-stu-id="0755d-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="0755d-289">Newtonsoft.Json, versione 9.0.1 o successiva. Installare `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e includerlo come riferimento.</span><span class="sxs-lookup"><span data-stu-id="0755d-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="0755d-290">**Creare una raccolta monitorata, di lease e di destinazione**</span><span class="sxs-lookup"><span data-stu-id="0755d-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="0755d-291">Raccolta di lease hello hello toouse ordine processore libreria di Feed di modifica, deve toobe creato prima di eseguire hello processore host.</span><span class="sxs-lookup"><span data-stu-id="0755d-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="0755d-292">Nuovamente, si consiglia di archiviare una raccolta di lease in un altro account con un hello toowhere più vicino di scrittura area che modifica Feed processore è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0755d-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0755d-293">In questo esempio lo spostamento dei dati, è necessario raccolta di destinazione hello toocreate prima di eseguire l'host di hello Feed processore delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="0755d-294">Nel codice di esempio hello definiamo un hello toocreate del metodo helper monitorato, associato a un lease e raccolte di destinazione se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="0755d-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="0755d-295">Creazione di una raccolta ha implicazioni, prezzi che si desidera riservare una velocità effettiva per toocommunicate applicazione hello con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0755d-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="0755d-296">Per ulteriori informazioni, visitare hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="0755d-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="0755d-297">*Creazione di un host di processori*</span><span class="sxs-lookup"><span data-stu-id="0755d-297">*Creating a processor host*</span></span>

<span data-ttu-id="0755d-298">Hello `ChangeFeedProcessorHost` classe fornisce un ambiente di runtime thread-safe, multiprocesso e sicuro per le implementazioni del processore di eventi che fornisce anche la gestione di lease di creazione di Checkpoint e di partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="0755d-299">hello toouse `ChangeFeedProcessorHost` (classe), è possibile implementare `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="0755d-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="0755d-300">Questa interfaccia contiene tre metodi:</span><span class="sxs-lookup"><span data-stu-id="0755d-300">This interface contains three methods:</span></span>

* <span data-ttu-id="0755d-301">`OpenAsync`: questa funzione viene chiamata quando viene aperto l'osservatore del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="0755d-302">Quando viene aperto consumer/osservatore può essere modificato tooperform un'azione specifica.</span><span class="sxs-lookup"><span data-stu-id="0755d-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="0755d-303">`CloseAsync`: questa funzione viene chiamata quando viene arrestato l'osservatore del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="0755d-304">Quando viene chiuso consumer/osservatore può essere modificato tooperform un'azione specifica.</span><span class="sxs-lookup"><span data-stu-id="0755d-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="0755d-305">`ProcessChangesAsync`: questa funzione viene chiamata quando nel feed di modifiche sono disponibili nuove modifiche al documento.</span><span class="sxs-lookup"><span data-stu-id="0755d-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="0755d-306">Può essere modificato tooperform un'azione specifica dopo l'aggiornamento ogni modifica del feed.</span><span class="sxs-lookup"><span data-stu-id="0755d-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="0755d-307">In questo esempio, si implementano hello `IChangeFeedObserver` tramite hello `DocumentFeedObserver` classe.</span><span class="sxs-lookup"><span data-stu-id="0755d-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="0755d-308">In questo caso, hello `ProcessChangesAsync` funzione upserts (aggiornamenti) un documento da modifica feed nella raccolta di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="0755d-309">In questo esempio è utile per lo spostamento dei dati da una raccolta tooanother nella chiave di ordinamento toochange hello partizione di un set di dati.</span><span class="sxs-lookup"><span data-stu-id="0755d-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="0755d-310">*Host processore di hello in esecuzione*</span><span class="sxs-lookup"><span data-stu-id="0755d-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="0755d-311">Prima di avviare l'elaborazione degli eventi, è possibile personalizzare le opzioni relative al feed di modifiche e all'host del feed di modifiche.</span><span class="sxs-lookup"><span data-stu-id="0755d-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
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
<span data-ttu-id="0755d-312">campi specifici di Hello che possono essere personalizzati sono riepilogati nella hello le tabelle seguenti.</span><span class="sxs-lookup"><span data-stu-id="0755d-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="0755d-313">**Opzioni del feed di modifiche**:</span><span class="sxs-lookup"><span data-stu-id="0755d-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0755d-314">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="0755d-314">Property Name</span></span></th>
        <th><span data-ttu-id="0755d-315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0755d-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="0755d-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="0755d-317">Ottiene o imposta hello il numero massimo di elementi toobe restituito nell'operazione di enumerazione hello in hello Azure Cosmos DB servizio di database.</span><span class="sxs-lookup"><span data-stu-id="0755d-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="0755d-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="0755d-319">Ottiene o imposta l'id di intervalli di chiavi di partizione hello per la richiesta corrente hello nel servizio di database di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="0755d-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="0755d-321">Ottiene o imposta il token di continuazione di hello richiesta nel servizio di database di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0755d-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="0755d-322">SessionToken</span></span></td>
        <td><span data-ttu-id="0755d-323">Ottiene o imposta il token di sessione hello per l'utilizzo con la coerenza della sessione in hello Azure Cosmos DB servizio di database.</span><span class="sxs-lookup"><span data-stu-id="0755d-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0755d-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="0755d-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="0755d-325">Ottiene o imposta se Modifica feed nel servizio di database di Azure Cosmos DB hello deve iniziare da hello a partire da (true) o da corrente (false).</span><span class="sxs-lookup"><span data-stu-id="0755d-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="0755d-326">Per impostazione predefinita, inizia dalla posizione corrente (false).</span><span class="sxs-lookup"><span data-stu-id="0755d-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="0755d-327">**Opzioni dell'host di feed di modifiche**:</span><span class="sxs-lookup"><span data-stu-id="0755d-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0755d-328">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="0755d-328">Property Name</span></span></th>
        <th><span data-ttu-id="0755d-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="0755d-329">Type</span></span></th>
        <th><span data-ttu-id="0755d-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0755d-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="0755d-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="0755d-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0755d-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="0755d-333">intervallo di Hello per tutti i lease per le partizioni vengono mantenuti attivi dall'istanza ChangeFeedEventHost hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="0755d-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="0755d-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0755d-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="0755d-336">Se le partizioni siano distribuite uniformemente tra le istanze di host noti, Hello tookick intervallo off toocompute un'attività.</span><span class="sxs-lookup"><span data-stu-id="0755d-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="0755d-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="0755d-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0755d-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="0755d-339">intervallo di Hello per cui hello lease viene eseguita su un lease che rappresenta una partizione.</span><span class="sxs-lookup"><span data-stu-id="0755d-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="0755d-340">Se il lease hello non viene rinnovato entro questo intervallo, è scaduto e la proprietà della partizione hello Sposta tooanother ChangeFeedEventHost istanza.</span><span class="sxs-lookup"><span data-stu-id="0755d-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="0755d-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="0755d-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0755d-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="0755d-343">ritardo Hello tra il polling di una partizione per le nuove modifiche su hello feed, dopo tutte le modifiche correnti vengono svuotate.</span><span class="sxs-lookup"><span data-stu-id="0755d-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0755d-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0755d-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0755d-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0755d-346">Hello lease toocheckpoint frequenza.</span><span class="sxs-lookup"><span data-stu-id="0755d-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0755d-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="0755d-348">int</span><span class="sxs-lookup"><span data-stu-id="0755d-348">Int</span></span></td>
        <td><span data-ttu-id="0755d-349">numero minimo di partizioni Hello per host hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0755d-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="0755d-351">int</span><span class="sxs-lookup"><span data-stu-id="0755d-351">Int</span></span></td>
        <td><span data-ttu-id="0755d-352">Hello massimo numero di partizioni hello host può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0755d-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0755d-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="0755d-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="0755d-354">Booleano</span><span class="sxs-lookup"><span data-stu-id="0755d-354">Bool</span></span></td>
        <td><span data-ttu-id="0755d-355">Se nella hello iniziale dell'host hello tutti i lease esistenti deve essere eliminato e host hello deve iniziare da zero.</span><span class="sxs-lookup"><span data-stu-id="0755d-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="0755d-356">creare un'istanza di elaborazione, l'evento toostart `ChangeFeedProcessorHost`, fornendo i parametri appropriati hello per la raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0755d-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="0755d-357">Chiamare quindi `RegisterObserverAsync` tooregister il `IChangeFeedObserver` implementazione (DocumentFeedObserver in questo esempio) con il runtime di hello.</span><span class="sxs-lookup"><span data-stu-id="0755d-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="0755d-358">A questo punto, l'host hello tenta tooacquire un lease in ogni intervallo di chiavi di partizione nella raccolta di Azure Cosmos DB hello usando un algoritmo "greedy".</span><span class="sxs-lookup"><span data-stu-id="0755d-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="0755d-359">Tali lease durano per un determinato intervallo di tempo e quindi devono essere rinnovati.</span><span class="sxs-lookup"><span data-stu-id="0755d-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="0755d-360">Appena nuovi nodi, istanze di lavoro, in questo caso, portare in linea, essi prenotazioni di lease e nel tempo carico hello passa tra i nodi in ogni host tenta tooacquire più lease.</span><span class="sxs-lookup"><span data-stu-id="0755d-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="0755d-361">Nell'esempio di codice hello, utilizziamo un toocreate di classe (DocumentFeedObserverFactory.cs) factory un osservatore e hello `RegistObserverFactoryAsync` osservatore hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="0755d-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

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
<span data-ttu-id="0755d-362">Con il passare del tempo, viene stabilito un equilibrio.</span><span class="sxs-lookup"><span data-stu-id="0755d-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="0755d-363">Questa funzionalità dinamica consente basata sulla CPU tooconsumers toobe applicata la scalabilità automatica per la scalabilità verticale e scalabilità verticale.</span><span class="sxs-lookup"><span data-stu-id="0755d-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="0755d-364">Se le modifiche sono disponibili nel database di Azure Cosmos con maggiore frequenza rispetto ai consumer possono elaborare, aumento della CPU hello sui consumer può essere utilizzato toocause scalabilità automatica sul numero di istanze di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0755d-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0755d-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0755d-365">Next steps</span></span>
* <span data-ttu-id="0755d-366">Provare a hello [Azure Cosmos DB modifica feed esempi di codice su GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="0755d-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="0755d-367">Iniziare a scrivere codice con hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0755d-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
