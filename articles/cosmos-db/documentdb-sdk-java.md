---
title: 'Azure Cosmos DB: risorse, SDK e API Java di DocumentDB | Microsoft Docs'
description: Altre informazioni sui hello Java API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure SDK per Java DocumentDB DB Cosmos.
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
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="3d5c0-103">Azure Cosmos DB: risorse e note sulla versione di DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="3d5c0-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d5c0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3d5c0-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="3d5c0-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="3d5c0-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="3d5c0-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d5c0-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="3d5c0-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3d5c0-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="3d5c0-108">Java</span><span class="sxs-lookup"><span data-stu-id="3d5c0-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="3d5c0-109">Python</span><span class="sxs-lookup"><span data-stu-id="3d5c0-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="3d5c0-110">REST</span><span class="sxs-lookup"><span data-stu-id="3d5c0-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="3d5c0-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="3d5c0-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="3d5c0-112">SQL</span><span class="sxs-lookup"><span data-stu-id="3d5c0-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="3d5c0-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="3d5c0-114">Maven</span><span class="sxs-lookup"><span data-stu-id="3d5c0-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="3d5c0-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-115">**API documentation**</span></span></td><td>[<span data-ttu-id="3d5c0-116">Documentazione di riferimento API Java</span><span class="sxs-lookup"><span data-stu-id="3d5c0-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="3d5c0-117">**Contribuiscono tooSDK**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="3d5c0-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="3d5c0-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="3d5c0-119">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-119">**Get started**</span></span></td><td>[<span data-ttu-id="3d5c0-120">Introduzione a hello SDK per Java</span><span class="sxs-lookup"><span data-stu-id="3d5c0-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="3d5c0-121">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="3d5c0-122">Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3d5c0-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="3d5c0-123">**Runtime attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="3d5c0-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="3d5c0-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="3d5c0-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="3d5c0-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="3d5c0-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="3d5c0-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="3d5c0-127">Correzioni di bug importanti toorequest elaborazione durante partizione divide.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="3d5c0-128">Risolto un problema con hello sicuro e BoundedStaleness livelli di coerenza.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="3d5c0-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="3d5c0-130">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="3d5c0-131">Risolto un bug nella raccolta in modalità di sessione di lettura.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="3d5c0-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="3d5c0-133">Supporto abilitato per la raccolta partizionata con valore ridotto di 2.500 UR/s e riduzione con incrementi di 100 UR/s.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="3d5c0-134">Correzione di un bug in assembly nativo hello in alcune query possono essere NullRef eccezione.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="3d5c0-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="3d5c0-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="3d5c0-136">Correzione di un bug nella configurazione del motore di query hello che può generare eccezioni per le query in modalità di Gateway.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="3d5c0-137">Corretti alcuni bug nel contenitore di sessione hello che possono generare un'eccezione "Resource proprietario non trovato" per le richieste immediatamente dopo la creazione della raccolta.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="3d5c0-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="3d5c0-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="3d5c0-139">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="3d5c0-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="3d5c0-140">Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="3d5c0-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="3d5c0-141">Aggiunta del supporto per la modifica del feed.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-141">Added support for change feed.</span></span>
* <span data-ttu-id="3d5c0-142">Aggiunta del supporto per informazioni sulla quota della raccolta tramite RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="3d5c0-143">Aggiunta del supporto per la registrazione dello script della procedura archiviata tramite RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="3d5c0-144">Risoluzione di un bug in cui una query in modalità DirectHttps rischiava di bloccarsi in presenza di errori di limitazione.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="3d5c0-145">Risoluzione di un bug in modalità di coerenza di sessione.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="3d5c0-146">Risoluzione di un bug che potrebbe causare l'eccezione NullReferenceException in HttpContext quando la frequenza delle richieste è elevata.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="3d5c0-147">Miglioramento delle prestazioni della modalità DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="3d5c0-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="3d5c0-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="3d5c0-149">Aggiunta del supporto del proxy basato su istanza di client semplice con l'API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="3d5c0-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="3d5c0-150">Aggiunta API DocumentClient.close() tooproperly arresto DocumentClient dell'istanza.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="3d5c0-151">Prestazioni migliorate di query in modalità di connettività diretta mediante derivazione hello piano di query da un assembly nativo hello anziché hello Gateway.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="3d5c0-152">Impostare FAIL_ON_UNKNOWN_PROPERTIES = false, in modo che gli utenti non devono toodefine JsonIgnoreProperties nella loro POJO.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="3d5c0-153">Sottoposta a refactoring registrazione toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="3d5c0-154">Risoluzione di altri bug nel lettore di coerenza.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="3d5c0-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="3d5c0-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="3d5c0-156">Correzione di un bug in hello connessione gestione tooprevent perdite di connessione in modalità di connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="3d5c0-157">Correzione di un bug nella query TOP hello in cui è possibile eccezione NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="3d5c0-158">Miglioramento delle prestazioni, riducendo il numero di hello di chiamata di rete per la cache interna di hello.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="3d5c0-159">Aggiunta del codice di stato, di ActivityID e dell'URI della richiesta in DocumentClientException per una migliore risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="3d5c0-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="3d5c0-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="3d5c0-161">Risolto un problema nella gestione connessione hello per la stabilità.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="3d5c0-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="3d5c0-163">Aggiunta del supporto per il livello di coerenza BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="3d5c0-164">Aggiunta del supporto per la connettività diretta per le operazioni CRUD delle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="3d5c0-165">Risoluzione di un bug in una query di un database con SQL.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="3d5c0-166">Correzione di un bug nella cache di hello sessione in cui i token di sessione può essere impostato in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="3d5c0-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="3d5c0-168">Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="3d5c0-169">Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="3d5c0-170">Aggiunta del supporto per la coerenza assoluta.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="3d5c0-171">Aggiunta del supporto per le richieste basate su nomi quando si utilizza la connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="3d5c0-172">Toomake fisso ActivityId rimangono coerenti tra tutti i tentativi di richiesta.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="3d5c0-173">Correzione di un bug relativi toohello cache della sessione durante la ricreazione di una raccolta con hello stesso nome.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="3d5c0-174">Aggiunta Polygon e LineString DataTypes quando si specifica il criterio di indicizzazione per la raccolta criteri per le query spaziali di geo-fencing.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="3d5c0-175">Risoluzione dei problemi con Java Doc per Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="3d5c0-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="3d5c0-177">Correzione di un bug in PartitionKeyDefinitionMap toocache raccolte con partizione singola e non crea aggiuntivo recuperare partizione richieste di chiavi.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="3d5c0-178">Correzione di un nuovo tentativo toonot bug quando viene fornito un valore di chiave di partizione corretto.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="3d5c0-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="3d5c0-180">Supporto aggiunto hello per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="3d5c0-181">Aggiunta del supporto per la ripetizione automatica per le richieste limitate con hello toocustomize opzioni max tentativi e ripetere max tempo di attesa.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="3d5c0-182">Vedere RetryOptions e ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="3d5c0-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="3d5c0-183">IPartitionResolver basato su codice di partizionamento personalizzato è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="3d5c0-184">Usare le raccolte partizionate per un'archiviazione e una velocità effettiva superiori.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="3d5c0-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="3d5c0-186">Aggiunta del supporto per il criterio di ripetizione per la limitazione.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="3d5c0-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="3d5c0-188">Aggiunto il supporto di (durata TTL) toolive di tempo per i documenti.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="3d5c0-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="3d5c0-190">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="3d5c0-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="3d5c0-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="3d5c0-192">Correzione di un bug in valori di hash toogenerate HashPartitionResolver in toobe little-endian coerente con altri SDK.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="3d5c0-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="3d5c0-194">Aggiungi intervallo & Hash tooassist resolver partizione con le applicazioni di partizionamento orizzontale tra più partizioni.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="3d5c0-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="3d5c0-196">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-196">Implement Upsert.</span></span> <span data-ttu-id="3d5c0-197">Aggiunta di nuovi metodi di upsertXXX toosupport Upsert funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="3d5c0-198">Implementazione del routing basato su ID.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-198">Implement ID Based Routing.</span></span> <span data-ttu-id="3d5c0-199">Nessuna modifica API pubblica, tutte modifiche interne.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="3d5c0-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="3d5c0-201">Versione ignorato il numero di versione toobring in allineamento con altri SDK</span><span class="sxs-lookup"><span data-stu-id="3d5c0-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="3d5c0-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="3d5c0-203">Supporta l'indice geospaziale</span><span class="sxs-lookup"><span data-stu-id="3d5c0-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="3d5c0-204">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-204">Validates id property for all resources.</span></span> <span data-ttu-id="3d5c0-205">Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="3d5c0-206">Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="3d5c0-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="3d5c0-208">Implementa criteri di indicizzazione V2</span><span class="sxs-lookup"><span data-stu-id="3d5c0-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="3d5c0-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="3d5c0-210">SDK con disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="3d5c0-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="3d5c0-211">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="3d5c0-211">Release & Retirement Dates</span></span>
<span data-ttu-id="3d5c0-212">Microsoft invierà una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="3d5c0-213">Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="3d5c0-214">Qualsiasi tooCosmos richiesta database usando un SDK ritirato verranno rifiutati dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="3d5c0-215">Tutte le versioni di hello DocumentDB SDK per Java precedente tooversion **1.0.0** verrà ritirato **29 febbraio 2016**.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="3d5c0-216">Versione</span><span class="sxs-lookup"><span data-stu-id="3d5c0-216">Version</span></span> | <span data-ttu-id="3d5c0-217">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="3d5c0-217">Release Date</span></span> | <span data-ttu-id="3d5c0-218">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="3d5c0-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3d5c0-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="3d5c0-220">11 luglio 2017</span><span class="sxs-lookup"><span data-stu-id="3d5c0-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="3d5c0-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="3d5c0-222">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="3d5c0-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="3d5c0-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="3d5c0-224">11 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="3d5c0-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="3d5c0-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="3d5c0-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="3d5c0-226">21 febbraio 2017</span><span class="sxs-lookup"><span data-stu-id="3d5c0-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="3d5c0-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="3d5c0-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="3d5c0-228">31 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="3d5c0-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="3d5c0-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="3d5c0-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="3d5c0-230">24 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="3d5c0-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="3d5c0-232">30 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="3d5c0-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="3d5c0-234">28 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="3d5c0-236">26 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="3d5c0-238">03 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="3d5c0-240">30 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="3d5c0-242">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="3d5c0-244">30 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="3d5c0-246">27 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="3d5c0-248">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="3d5c0-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="3d5c0-250">31 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="3d5c0-252">04 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="3d5c0-254">05 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="3d5c0-256">05 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="3d5c0-258">05 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="3d5c0-260">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3d5c0-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="3d5c0-262">12 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="3d5c0-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3d5c0-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="3d5c0-264">07 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="3d5c0-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-265">0.9.5-prelease</span></span> |<span data-ttu-id="3d5c0-266">09 marzo 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-266">Mar 09, 2015</span></span> |<span data-ttu-id="3d5c0-267">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-267">February 29, 2016</span></span> |
| <span data-ttu-id="3d5c0-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-268">0.9.4-prelease</span></span> |<span data-ttu-id="3d5c0-269">17 febbraio 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-269">February 17, 2015</span></span> |<span data-ttu-id="3d5c0-270">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-270">February 29, 2016</span></span> |
| <span data-ttu-id="3d5c0-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-271">0.9.3-prelease</span></span> |<span data-ttu-id="3d5c0-272">13 gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="3d5c0-272">January 13, 2015</span></span> |<span data-ttu-id="3d5c0-273">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-273">February 29, 2016</span></span> |
| <span data-ttu-id="3d5c0-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-274">0.9.2-prelease</span></span> |<span data-ttu-id="3d5c0-275">19 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="3d5c0-275">December 19, 2014</span></span> |<span data-ttu-id="3d5c0-276">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-276">February 29, 2016</span></span> |
| <span data-ttu-id="3d5c0-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-277">0.9.1-prelease</span></span> |<span data-ttu-id="3d5c0-278">19 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="3d5c0-278">December 19, 2014</span></span> |<span data-ttu-id="3d5c0-279">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-279">February 29, 2016</span></span> |
| <span data-ttu-id="3d5c0-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="3d5c0-280">0.9.0-prelease</span></span> |<span data-ttu-id="3d5c0-281">10 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="3d5c0-281">December 10, 2014</span></span> |<span data-ttu-id="3d5c0-282">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="3d5c0-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="3d5c0-283">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3d5c0-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="3d5c0-284">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3d5c0-284">See Also</span></span>
<span data-ttu-id="3d5c0-285">toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.</span><span class="sxs-lookup"><span data-stu-id="3d5c0-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

