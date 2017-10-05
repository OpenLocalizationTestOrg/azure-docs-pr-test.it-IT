---
title: API Python, risorse e SDK per Azure Cosmos DB | Microsoft Docs
description: Informazioni complete sull'SDK e sull'API Python, incluse le date di rilascio e di ritiro e le modifiche apportate tra le singole versioni di Azure Cosmos DB Python SDK.
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="be7b9-103">Azure Cosmos DB Python SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="be7b9-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be7b9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="be7b9-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="be7b9-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="be7b9-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="be7b9-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="be7b9-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="be7b9-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="be7b9-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="be7b9-108">Java</span><span class="sxs-lookup"><span data-stu-id="be7b9-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="be7b9-109">Python</span><span class="sxs-lookup"><span data-stu-id="be7b9-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="be7b9-110">REST</span><span class="sxs-lookup"><span data-stu-id="be7b9-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="be7b9-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="be7b9-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="be7b9-112">SQL</span><span class="sxs-lookup"><span data-stu-id="be7b9-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="be7b9-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="be7b9-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="be7b9-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="be7b9-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="be7b9-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="be7b9-115">**API documentation**</span></span></td><td>[<span data-ttu-id="be7b9-116">Documentazione di riferimento delle API di Python</span><span class="sxs-lookup"><span data-stu-id="be7b9-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="be7b9-117">**Istruzioni per l'installazione dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="be7b9-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="be7b9-118">Istruzioni per l'installazione dell'SDK di Python</span><span class="sxs-lookup"><span data-stu-id="be7b9-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="be7b9-119">**Contribuire all'SDK**</span><span class="sxs-lookup"><span data-stu-id="be7b9-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="be7b9-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="be7b9-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="be7b9-121">**Attività iniziali**</span><span class="sxs-lookup"><span data-stu-id="be7b9-121">**Get started**</span></span></td><td>[<span data-ttu-id="be7b9-122">Introduzione all'SDK di Python</span><span class="sxs-lookup"><span data-stu-id="be7b9-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="be7b9-123">**Piattaforma attualmente supportata**</span><span class="sxs-lookup"><span data-stu-id="be7b9-123">**Current supported platform**</span></span></td><td><span data-ttu-id="be7b9-124">[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="be7b9-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="be7b9-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="be7b9-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="be7b9-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="be7b9-127">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="be7b9-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="be7b9-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="be7b9-129">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="be7b9-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="be7b9-130">Aggiunta di un'opzione per disabilitare la verifica SSL durante l'esecuzione sull'emulatore Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="be7b9-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="be7b9-131">Rimossa la restrizione per cui il modulo delle richieste dipendenti deve essere esattamente 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="be7b9-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="be7b9-132">Velocità effettiva minima ridotta nelle raccolte partizionate da 10.100 UR/s a 2.500 UR/s.</span><span class="sxs-lookup"><span data-stu-id="be7b9-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="be7b9-133">Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="be7b9-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="be7b9-134">Versione API REST incrementata a "2017-01-19" con questo rilascio.</span><span class="sxs-lookup"><span data-stu-id="be7b9-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="be7b9-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="be7b9-136">Modifiche editoriali ai commenti alla documentazione.</span><span class="sxs-lookup"><span data-stu-id="be7b9-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="be7b9-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="be7b9-138">Aggiunto il supporto per Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="be7b9-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="be7b9-139">Aggiunto il supporto per il pool di connessioni con modulo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="be7b9-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="be7b9-140">Aggiunto il supporto per la coerenza di sessione.</span><span class="sxs-lookup"><span data-stu-id="be7b9-140">Added support for session consistency.</span></span>
* <span data-ttu-id="be7b9-141">Aggiunto il supporto per le query TOP/ORDERBY per le raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="be7b9-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="be7b9-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="be7b9-143">Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate</span><span class="sxs-lookup"><span data-stu-id="be7b9-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="be7b9-144">(le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Cosmos DB esegue nove tentativi per ogni richiesta con codice di errore 429, rispettando l'intervallo di tempo di retryAfter specificato nell'intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="be7b9-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="be7b9-145">Adesso è possibile impostare un intervallo di tempo fisso per i tentativi come parte della proprietà RetryOptions nell'oggetto ConnectionPolicy se si desidera ignorare il tempo di retryAfter restituito dal server tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="be7b9-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="be7b9-146">Azure Cosmos DB attende al massimo 30 secondi per ogni richiesta che viene limitata (indipendentemente dal numero di tentativi) e restituisce la risposta con il codice di errore 429.</span><span class="sxs-lookup"><span data-stu-id="be7b9-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="be7b9-147">Questo tempo può essere sottoposto a override nella proprietà RetryOptions dell'oggetto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="be7b9-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="be7b9-148">Cosmos DB restituisce ora i parametri x-ms-throttle-retry-count e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta in ogni richiesta per indicare il numero di nuovi tentativi di limitazione e il tempo cumulativo di attesa della richiesta tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="be7b9-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="be7b9-149">Rimozione della classe RetryPolicy e della proprietà corrispondente (retry_policy) esposta nella classe document_client e introduzione di una classe RetryOptions che espone la proprietà RetryOptions nella classe ConnectionPolicy che può essere utilizzata per eseguire l’override di alcune opzioni di ripetizione dei tentativi predefinite.</span><span class="sxs-lookup"><span data-stu-id="be7b9-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="be7b9-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="be7b9-151">Aggiunta del supporto per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="be7b9-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="be7b9-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="be7b9-153">Aggiunta del supporto per la funzionalità di durata (TTL) relativa ai documenti.</span><span class="sxs-lookup"><span data-stu-id="be7b9-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="be7b9-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="be7b9-155">Correzioni di bug relativi al partizionamento lato server per consentire caratteri speciali nel percorso partitionkey.</span><span class="sxs-lookup"><span data-stu-id="be7b9-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="be7b9-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="be7b9-157">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="be7b9-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="be7b9-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="be7b9-159">Aggiungi resolver per partizioni hash e a intervalli come supporto per applicazioni di partizionamento orizzontale in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="be7b9-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="be7b9-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="be7b9-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="be7b9-161">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="be7b9-161">Implement Upsert.</span></span> <span data-ttu-id="be7b9-162">Nuovi metodi upsertXXX aggiunti per supportare la funzionalità Upsert.</span><span class="sxs-lookup"><span data-stu-id="be7b9-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="be7b9-163">Implementazione del routing basato su ID.</span><span class="sxs-lookup"><span data-stu-id="be7b9-163">Implement ID Based Routing.</span></span> <span data-ttu-id="be7b9-164">Nessuna modifica API pubblica, tutte modifiche interne.</span><span class="sxs-lookup"><span data-stu-id="be7b9-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="be7b9-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="be7b9-166">Supporta l'indice geospaziale.</span><span class="sxs-lookup"><span data-stu-id="be7b9-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="be7b9-167">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="be7b9-167">Validates id property for all resources.</span></span> <span data-ttu-id="be7b9-168">Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="be7b9-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="be7b9-169">Aggiunge la nuova intestazione "stato di trasformazione dell'indice" a ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="be7b9-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="be7b9-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="be7b9-171">Implementazione del criterio di indicizzazione V2.</span><span class="sxs-lookup"><span data-stu-id="be7b9-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="be7b9-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="be7b9-173">Supporto della connessione proxy.</span><span class="sxs-lookup"><span data-stu-id="be7b9-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="be7b9-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="be7b9-175">SDK con disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="be7b9-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="be7b9-176">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="be7b9-176">Release & retirement dates</span></span>
<span data-ttu-id="be7b9-177">Microsoft invierà una notifica almeno **12 mesi** prima del ritiro di un SDK per agevolare la transizione a una versione più recente o supportata.</span><span class="sxs-lookup"><span data-stu-id="be7b9-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="be7b9-178">Le nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunte solo all'SDK corrente, è quindi consigliabile eseguire sempre l'aggiornamento alla versione più recente dell'SDK quanto prima.</span><span class="sxs-lookup"><span data-stu-id="be7b9-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="be7b9-179">Qualsiasi richiesta inviata a Cosmos DB con un SDK ritirato verrà rifiutata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="be7b9-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="be7b9-180">Tutte le versioni dell'SDK per Python di Azure DocumentDB precedenti alla versione **1.0.0** verranno ritirate il **29 febbraio 2016**.</span><span class="sxs-lookup"><span data-stu-id="be7b9-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="be7b9-181">Versione</span><span class="sxs-lookup"><span data-stu-id="be7b9-181">Version</span></span> | <span data-ttu-id="be7b9-182">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="be7b9-182">Release Date</span></span> | <span data-ttu-id="be7b9-183">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="be7b9-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="be7b9-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="be7b9-185">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="be7b9-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="be7b9-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="be7b9-187">01 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="be7b9-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="be7b9-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="be7b9-189">30 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="be7b9-191">29 settembre 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="be7b9-193">07 luglio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="be7b9-195">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="be7b9-197">26 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="be7b9-199">08 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="be7b9-201">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="be7b9-203">03 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="be7b9-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="be7b9-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="be7b9-205">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="be7b9-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="be7b9-207">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="be7b9-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="be7b9-209">06 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="be7b9-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="be7b9-211">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="be7b9-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="be7b9-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="be7b9-213">25 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="be7b9-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="be7b9-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="be7b9-215">07 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="be7b9-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="be7b9-216">0.9.4-prelease</span></span> |<span data-ttu-id="be7b9-217">14 gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="be7b9-217">January 14, 2015</span></span> |<span data-ttu-id="be7b9-218">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-218">February 29, 2016</span></span> |
| <span data-ttu-id="be7b9-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="be7b9-219">0.9.3-prelease</span></span> |<span data-ttu-id="be7b9-220">09 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="be7b9-220">December 09, 2014</span></span> |<span data-ttu-id="be7b9-221">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-221">February 29, 2016</span></span> |
| <span data-ttu-id="be7b9-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="be7b9-222">0.9.2-prelease</span></span> |<span data-ttu-id="be7b9-223">25 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="be7b9-223">November 25, 2014</span></span> |<span data-ttu-id="be7b9-224">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-224">February 29, 2016</span></span> |
| <span data-ttu-id="be7b9-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="be7b9-225">0.9.1-prelease</span></span> |<span data-ttu-id="be7b9-226">23 settembre 2014</span><span class="sxs-lookup"><span data-stu-id="be7b9-226">September 23, 2014</span></span> |<span data-ttu-id="be7b9-227">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-227">February 29, 2016</span></span> |
| <span data-ttu-id="be7b9-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="be7b9-228">0.9.0-prelease</span></span> |<span data-ttu-id="be7b9-229">21 agosto 2014</span><span class="sxs-lookup"><span data-stu-id="be7b9-229">August 21, 2014</span></span> |<span data-ttu-id="be7b9-230">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="be7b9-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="be7b9-231">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="be7b9-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="be7b9-232">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="be7b9-232">See also</span></span>
<span data-ttu-id="be7b9-233">Per altre informazioni su Cosmos DB, vedere la pagina del servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="be7b9-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

