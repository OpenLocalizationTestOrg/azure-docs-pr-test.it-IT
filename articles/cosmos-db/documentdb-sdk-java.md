---
title: 'Azure Cosmos DB: risorse, SDK e API Java di DocumentDB | Microsoft Docs'
description: Informazioni complete sull'SDK e sull'API Java, incluse le date di rilascio e di ritiro e le modifiche apportate tra le singole versioni di Azure Cosmos DB DocumentDB Java SDK.
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="46e69-103">Azure Cosmos DB: risorse e note sulla versione di DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="46e69-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46e69-104">.NET</span><span class="sxs-lookup"><span data-stu-id="46e69-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="46e69-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="46e69-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="46e69-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="46e69-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="46e69-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="46e69-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="46e69-108">Java</span><span class="sxs-lookup"><span data-stu-id="46e69-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="46e69-109">Python</span><span class="sxs-lookup"><span data-stu-id="46e69-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="46e69-110">REST</span><span class="sxs-lookup"><span data-stu-id="46e69-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="46e69-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="46e69-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="46e69-112">SQL</span><span class="sxs-lookup"><span data-stu-id="46e69-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="46e69-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="46e69-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="46e69-114">Maven</span><span class="sxs-lookup"><span data-stu-id="46e69-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="46e69-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="46e69-115">**API documentation**</span></span></td><td>[<span data-ttu-id="46e69-116">Documentazione di riferimento API Java</span><span class="sxs-lookup"><span data-stu-id="46e69-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="46e69-117">**Contribuire all'SDK**</span><span class="sxs-lookup"><span data-stu-id="46e69-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="46e69-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="46e69-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="46e69-119">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="46e69-119">**Get started**</span></span></td><td>[<span data-ttu-id="46e69-120">Introduzione a SDK Java</span><span class="sxs-lookup"><span data-stu-id="46e69-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="46e69-121">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="46e69-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="46e69-122">Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="46e69-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="46e69-123">**Runtime attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="46e69-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="46e69-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="46e69-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="46e69-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="46e69-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="46e69-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="46e69-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="46e69-127">Correzioni di bug importanti per richiedere l'elaborazione durante le suddivisioni delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="46e69-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="46e69-128">Risolto un problema relativo ai livelli di coerenza Strong e BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="46e69-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="46e69-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="46e69-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="46e69-130">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="46e69-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="46e69-131">Risolto un bug nella raccolta in modalità di sessione di lettura.</span><span class="sxs-lookup"><span data-stu-id="46e69-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="46e69-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="46e69-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="46e69-133">Supporto abilitato per la raccolta partizionata con valore ridotto di 2.500 UR/s e riduzione con incrementi di 100 UR/s.</span><span class="sxs-lookup"><span data-stu-id="46e69-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="46e69-134">Correzione di un bug nell'assembly nativo che può causare l'eccezione NullRef in alcune query.</span><span class="sxs-lookup"><span data-stu-id="46e69-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="46e69-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="46e69-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="46e69-136">Correzione di un bug nella configurazione del motore di query che può generare eccezioni per le query in modalità Gateway.</span><span class="sxs-lookup"><span data-stu-id="46e69-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="46e69-137">Correzione di alcuni bug nel contenitore della sessione che possono generare un'eccezione "Risorsa proprietario non trovata" per le richieste immediatamente dopo la creazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="46e69-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="46e69-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="46e69-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="46e69-139">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="46e69-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="46e69-140">Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="46e69-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="46e69-141">Aggiunta del supporto per la modifica del feed.</span><span class="sxs-lookup"><span data-stu-id="46e69-141">Added support for change feed.</span></span>
* <span data-ttu-id="46e69-142">Aggiunta del supporto per informazioni sulla quota della raccolta tramite RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="46e69-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="46e69-143">Aggiunta del supporto per la registrazione dello script della procedura archiviata tramite RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="46e69-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="46e69-144">Risoluzione di un bug in cui una query in modalità DirectHttps rischiava di bloccarsi in presenza di errori di limitazione.</span><span class="sxs-lookup"><span data-stu-id="46e69-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="46e69-145">Risoluzione di un bug in modalità di coerenza di sessione.</span><span class="sxs-lookup"><span data-stu-id="46e69-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="46e69-146">Risoluzione di un bug che potrebbe causare l'eccezione NullReferenceException in HttpContext quando la frequenza delle richieste è elevata.</span><span class="sxs-lookup"><span data-stu-id="46e69-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="46e69-147">Miglioramento delle prestazioni della modalità DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="46e69-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="46e69-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="46e69-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="46e69-149">Aggiunta del supporto del proxy basato su istanza di client semplice con l'API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="46e69-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="46e69-150">Aggiunta dell'API DocumentClient.close() per arrestare correttamente l'istanza di DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="46e69-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="46e69-151">Miglioramento delle prestazioni delle query nella modalità di connettività diretta, tramite derivazione del piano di query dall'assembly nativo invece che dal gateway.</span><span class="sxs-lookup"><span data-stu-id="46e69-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="46e69-152">Impostare FAIL_ON_UNKNOWN_PROPERTIES = false in modo che gli utenti non debbano definire JsonIgnoreProperties in POJO.</span><span class="sxs-lookup"><span data-stu-id="46e69-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="46e69-153">Refactoring della registrazione per usare SLF4J.</span><span class="sxs-lookup"><span data-stu-id="46e69-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="46e69-154">Risoluzione di altri bug nel lettore di coerenza.</span><span class="sxs-lookup"><span data-stu-id="46e69-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="46e69-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="46e69-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="46e69-156">Risoluzione di un bug nella gestione della connessione per impedire perdite di connessione nella modalità di connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="46e69-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="46e69-157">Risoluzione di un bug nella query TOP in cui è possibile che venga generata un'eccezione NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="46e69-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="46e69-158">Miglioramento delle prestazioni tramite la riduzione del numero di chiamate di rete per le cache interne.</span><span class="sxs-lookup"><span data-stu-id="46e69-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="46e69-159">Aggiunta del codice di stato, di ActivityID e dell'URI della richiesta in DocumentClientException per una migliore risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="46e69-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="46e69-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="46e69-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="46e69-161">Risoluzione di un problema nella gestione della connessione per una migliore stabilità.</span><span class="sxs-lookup"><span data-stu-id="46e69-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="46e69-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="46e69-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="46e69-163">Aggiunta del supporto per il livello di coerenza BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="46e69-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="46e69-164">Aggiunta del supporto per la connettività diretta per le operazioni CRUD delle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="46e69-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="46e69-165">Risoluzione di un bug in una query di un database con SQL.</span><span class="sxs-lookup"><span data-stu-id="46e69-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="46e69-166">Risoluzione di un bug nella cache della sessione in cui i token di sessione possono essere impostati in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="46e69-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="46e69-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="46e69-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="46e69-168">Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="46e69-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="46e69-169">Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="46e69-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="46e69-170">Aggiunta del supporto per la coerenza assoluta.</span><span class="sxs-lookup"><span data-stu-id="46e69-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="46e69-171">Aggiunta del supporto per le richieste basate su nomi quando si utilizza la connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="46e69-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="46e69-172">Correzione rendere ActivityId coerente tra tutti i tentativi di richiesta.</span><span class="sxs-lookup"><span data-stu-id="46e69-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="46e69-173">Correzione del bug correlato alla cache di sessione quando si ricrea una raccolta con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="46e69-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="46e69-174">Aggiunta Polygon e LineString DataTypes quando si specifica il criterio di indicizzazione per la raccolta criteri per le query spaziali di geo-fencing.</span><span class="sxs-lookup"><span data-stu-id="46e69-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="46e69-175">Risoluzione dei problemi con Java Doc per Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="46e69-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="46e69-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="46e69-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="46e69-177">Risolto un bug in PartitionKeyDefinitionMap per memorizzare nella cache le raccolte a partizione singola ed evitare richieste aggiuntive di chiavi di partizione da recuperare.</span><span class="sxs-lookup"><span data-stu-id="46e69-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="46e69-178">Risolto un bug per non eseguire un nuovo tentativo se viene fornito un valore di chiave di partizione errato.</span><span class="sxs-lookup"><span data-stu-id="46e69-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="46e69-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="46e69-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="46e69-180">Aggiunta del supporto per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="46e69-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="46e69-181">Aggiunta del supporto per la ripetizione automatica delle richieste limitate con la possibilità di personalizzare il numero massimo di tentativi e il relativo tempo di attesa massimo.</span><span class="sxs-lookup"><span data-stu-id="46e69-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="46e69-182">Vedere RetryOptions e ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="46e69-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="46e69-183">IPartitionResolver basato su codice di partizionamento personalizzato è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="46e69-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="46e69-184">Usare le raccolte partizionate per un'archiviazione e una velocità effettiva superiori.</span><span class="sxs-lookup"><span data-stu-id="46e69-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="46e69-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="46e69-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="46e69-186">Aggiunta del supporto per il criterio di ripetizione per la limitazione.</span><span class="sxs-lookup"><span data-stu-id="46e69-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="46e69-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="46e69-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="46e69-188">Aggiunta del supporto per la durata (TTL) relativa ai documenti.</span><span class="sxs-lookup"><span data-stu-id="46e69-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="46e69-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="46e69-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="46e69-190">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="46e69-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="46e69-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="46e69-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="46e69-192">Risolto un bug in HashPartitionResolver per generare valori hash in little endian per coerenza con altri SDK.</span><span class="sxs-lookup"><span data-stu-id="46e69-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="46e69-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="46e69-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="46e69-194">Aggiungi resolver per partizioni hash e a intervalli come supporto per applicazioni di partizionamento orizzontale in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="46e69-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="46e69-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="46e69-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="46e69-196">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="46e69-196">Implement Upsert.</span></span> <span data-ttu-id="46e69-197">Nuovi metodi upsertXXX aggiunti per supportare la funzionalità Upsert.</span><span class="sxs-lookup"><span data-stu-id="46e69-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="46e69-198">Implementazione del routing basato su ID.</span><span class="sxs-lookup"><span data-stu-id="46e69-198">Implement ID Based Routing.</span></span> <span data-ttu-id="46e69-199">Nessuna modifica API pubblica, tutte modifiche interne.</span><span class="sxs-lookup"><span data-stu-id="46e69-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="46e69-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="46e69-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="46e69-201">Versione ignorata per riportare il numero di versione in allineamento con altri SDK</span><span class="sxs-lookup"><span data-stu-id="46e69-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="46e69-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="46e69-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="46e69-203">Supporta l'indice geospaziale</span><span class="sxs-lookup"><span data-stu-id="46e69-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="46e69-204">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="46e69-204">Validates id property for all resources.</span></span> <span data-ttu-id="46e69-205">Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="46e69-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="46e69-206">Aggiunge la nuova intestazione "stato di trasformazione dell'indice" a ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="46e69-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="46e69-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="46e69-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="46e69-208">Implementa criteri di indicizzazione V2</span><span class="sxs-lookup"><span data-stu-id="46e69-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="46e69-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="46e69-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="46e69-210">SDK con disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="46e69-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="46e69-211">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="46e69-211">Release & Retirement Dates</span></span>
<span data-ttu-id="46e69-212">Microsoft invierà una notifica almeno **12 mesi** prima del ritiro di un SDK per agevolare la transizione a una versione più recente o supportata.</span><span class="sxs-lookup"><span data-stu-id="46e69-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="46e69-213">Le nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunte solo all'SDK corrente, è quindi consigliabile eseguire sempre l'aggiornamento alla versione più recente dell'SDK quanto prima.</span><span class="sxs-lookup"><span data-stu-id="46e69-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="46e69-214">Qualsiasi richiesta inviata a Cosmos DB con un SDK ritirato verrà rifiutata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="46e69-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="46e69-215">Tutte le versioni dell'SDK DocumentDB per Java precedenti alla versione **1.0.0** verranno ritirate il **29 febbraio 2016**.</span><span class="sxs-lookup"><span data-stu-id="46e69-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="46e69-216">Versione</span><span class="sxs-lookup"><span data-stu-id="46e69-216">Version</span></span> | <span data-ttu-id="46e69-217">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="46e69-217">Release Date</span></span> | <span data-ttu-id="46e69-218">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="46e69-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="46e69-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="46e69-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="46e69-220">11 luglio 2017</span><span class="sxs-lookup"><span data-stu-id="46e69-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="46e69-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="46e69-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="46e69-222">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="46e69-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="46e69-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="46e69-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="46e69-224">11 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="46e69-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="46e69-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="46e69-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="46e69-226">21 febbraio 2017</span><span class="sxs-lookup"><span data-stu-id="46e69-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="46e69-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="46e69-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="46e69-228">31 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="46e69-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="46e69-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="46e69-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="46e69-230">24 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="46e69-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="46e69-232">30 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="46e69-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="46e69-234">28 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="46e69-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="46e69-236">26 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="46e69-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="46e69-238">03 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="46e69-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="46e69-240">30 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="46e69-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="46e69-242">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="46e69-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="46e69-244">30 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="46e69-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="46e69-246">27 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="46e69-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="46e69-248">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="46e69-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="46e69-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="46e69-250">31 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="46e69-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="46e69-252">04 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="46e69-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="46e69-254">05 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="46e69-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="46e69-256">05 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="46e69-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="46e69-258">05 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="46e69-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="46e69-260">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="46e69-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="46e69-262">12 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="46e69-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="46e69-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="46e69-264">07 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="46e69-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-265">0.9.5-prelease</span></span> |<span data-ttu-id="46e69-266">09 marzo 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-266">Mar 09, 2015</span></span> |<span data-ttu-id="46e69-267">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-267">February 29, 2016</span></span> |
| <span data-ttu-id="46e69-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-268">0.9.4-prelease</span></span> |<span data-ttu-id="46e69-269">17 febbraio 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-269">February 17, 2015</span></span> |<span data-ttu-id="46e69-270">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-270">February 29, 2016</span></span> |
| <span data-ttu-id="46e69-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-271">0.9.3-prelease</span></span> |<span data-ttu-id="46e69-272">13 gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="46e69-272">January 13, 2015</span></span> |<span data-ttu-id="46e69-273">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-273">February 29, 2016</span></span> |
| <span data-ttu-id="46e69-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-274">0.9.2-prelease</span></span> |<span data-ttu-id="46e69-275">19 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="46e69-275">December 19, 2014</span></span> |<span data-ttu-id="46e69-276">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-276">February 29, 2016</span></span> |
| <span data-ttu-id="46e69-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-277">0.9.1-prelease</span></span> |<span data-ttu-id="46e69-278">19 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="46e69-278">December 19, 2014</span></span> |<span data-ttu-id="46e69-279">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-279">February 29, 2016</span></span> |
| <span data-ttu-id="46e69-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="46e69-280">0.9.0-prelease</span></span> |<span data-ttu-id="46e69-281">10 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="46e69-281">December 10, 2014</span></span> |<span data-ttu-id="46e69-282">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="46e69-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="46e69-283">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="46e69-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="46e69-284">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="46e69-284">See Also</span></span>
<span data-ttu-id="46e69-285">Per altre informazioni su Cosmos DB, vedere la pagina del servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="46e69-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

