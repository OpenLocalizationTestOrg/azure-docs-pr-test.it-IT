---
title: aaaAzure Cosmos DB Python API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello Python API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB Python SDK.
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="231a6-103">Azure Cosmos DB Python SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="231a6-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="231a6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="231a6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="231a6-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="231a6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="231a6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="231a6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="231a6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="231a6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="231a6-108">Java</span><span class="sxs-lookup"><span data-stu-id="231a6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="231a6-109">Python</span><span class="sxs-lookup"><span data-stu-id="231a6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="231a6-110">REST</span><span class="sxs-lookup"><span data-stu-id="231a6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="231a6-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="231a6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="231a6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="231a6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="231a6-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="231a6-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="231a6-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="231a6-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="231a6-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="231a6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="231a6-116">Documentazione di riferimento delle API di Python</span><span class="sxs-lookup"><span data-stu-id="231a6-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="231a6-117">**Istruzioni per l'installazione dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="231a6-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="231a6-118">Istruzioni per l'installazione dell'SDK di Python</span><span class="sxs-lookup"><span data-stu-id="231a6-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="231a6-119">**Contribuiscono tooSDK**</span><span class="sxs-lookup"><span data-stu-id="231a6-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="231a6-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="231a6-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="231a6-121">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="231a6-121">**Get started**</span></span></td><td>[<span data-ttu-id="231a6-122">Introduzione a Python SDK hello</span><span class="sxs-lookup"><span data-stu-id="231a6-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="231a6-123">**Piattaforma attualmente supportata**</span><span class="sxs-lookup"><span data-stu-id="231a6-123">**Current supported platform**</span></span></td><td><span data-ttu-id="231a6-124">[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="231a6-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="231a6-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="231a6-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="231a6-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="231a6-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="231a6-127">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="231a6-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="231a6-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="231a6-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="231a6-129">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="231a6-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="231a6-130">Aggiunta di un'opzione per disabilitare la verifica SSL durante l'esecuzione sull'emulatore Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="231a6-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="231a6-131">Rimuovere la restrizione hello di richieste dipendenti modulo toobe 2.10.0 esattamente.</span><span class="sxs-lookup"><span data-stu-id="231a6-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="231a6-132">Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="231a6-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="231a6-133">Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="231a6-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="231a6-134">Versione dell'API REST ha respinto troppo ' 2017-01-19' con questa versione.</span><span class="sxs-lookup"><span data-stu-id="231a6-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="231a6-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="231a6-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="231a6-136">Modifiche editoriali toodocumentation commenti.</span><span class="sxs-lookup"><span data-stu-id="231a6-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="231a6-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="231a6-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="231a6-138">Aggiunto il supporto per Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="231a6-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="231a6-139">Aggiunto il supporto per il pool di connessioni con modulo di richiesta.</span><span class="sxs-lookup"><span data-stu-id="231a6-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="231a6-140">Aggiunto il supporto per la coerenza di sessione.</span><span class="sxs-lookup"><span data-stu-id="231a6-140">Added support for session consistency.</span></span>
* <span data-ttu-id="231a6-141">Aggiunto il supporto per le query TOP/ORDERBY per le raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="231a6-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="231a6-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="231a6-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="231a6-143">Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate</span><span class="sxs-lookup"><span data-stu-id="231a6-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="231a6-144">(le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Azure Cosmos DB Ritenta nove volte per ogni richiesta quando viene rilevato il codice di errore 429, rispettando la distinzione tra tempo retryAfter hello nell'intestazione di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="231a6-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="231a6-145">Un intervallo di tempo predefinito di tentativi ora è possibile impostare come parte di hello RetryOptions proprietà nell'oggetto ConnectionPolicy hello se si desidera che l'ora di retryAfter hello tooignore restituito dal server tra i tentativi di hello.</span><span class="sxs-lookup"><span data-stu-id="231a6-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="231a6-146">Azure DB Cosmos ora attende per un massimo di 30 secondi per ogni richiesta che è limitata (indipendentemente dal numero di tentativi) e restituisce risposte hello con codice di errore 429.</span><span class="sxs-lookup"><span data-stu-id="231a6-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="231a6-147">Questa fase può anche essere sottoposta a override in hello proprietà RetryOptions ConnectionPolicy oggetto.</span><span class="sxs-lookup"><span data-stu-id="231a6-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="231a6-148">COSMOS DB restituisce x-ms-limitazione--numero di tentativi e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta hello in ogni velocità di richiesta toodenote hello tempo di riesecuzione conteggio e hello cummulative hello richiesta di attesa tra i tentativi di hello.</span><span class="sxs-lookup"><span data-stu-id="231a6-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="231a6-149">Classe RetryPolicy hello rimosso e la proprietà corrispondente hello (retry_policy) esposte nella classe document_client hello e introdotto invece una classe RetryOptions esposizione hello RetryOptions proprietà sulla classe ConnectionPolicy che può essere utilizzati toooverride alcune delle predefinito hello le opzioni di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="231a6-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="231a6-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="231a6-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="231a6-151">Supporto aggiunto hello per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="231a6-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="231a6-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="231a6-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="231a6-153">Hello aggiunto il supporto per funzionalità tooLive(TTL) Time per i documenti.</span><span class="sxs-lookup"><span data-stu-id="231a6-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="231a6-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="231a6-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="231a6-155">Correzioni di bug correlati lato tooserver partizionamento tooallow caratteri speciali nel percorso di partitionkey.</span><span class="sxs-lookup"><span data-stu-id="231a6-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="231a6-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="231a6-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="231a6-157">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="231a6-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="231a6-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="231a6-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="231a6-159">Aggiungi intervallo & Hash tooassist resolver partizione con le applicazioni di partizionamento orizzontale tra più partizioni.</span><span class="sxs-lookup"><span data-stu-id="231a6-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="231a6-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="231a6-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="231a6-161">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="231a6-161">Implement Upsert.</span></span> <span data-ttu-id="231a6-162">Aggiunta di nuovi metodi di UpsertXXX toosupport Upsert funzionalità.</span><span class="sxs-lookup"><span data-stu-id="231a6-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="231a6-163">Implementazione del routing basato su ID.</span><span class="sxs-lookup"><span data-stu-id="231a6-163">Implement ID Based Routing.</span></span> <span data-ttu-id="231a6-164">Nessuna modifica API pubblica, tutte modifiche interne.</span><span class="sxs-lookup"><span data-stu-id="231a6-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="231a6-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="231a6-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="231a6-166">Supporta l'indice geospaziale.</span><span class="sxs-lookup"><span data-stu-id="231a6-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="231a6-167">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="231a6-167">Validates id property for all resources.</span></span> <span data-ttu-id="231a6-168">Gli ID per le risorse non possono contenere i caratteri ?, /, #, \, o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="231a6-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="231a6-169">Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="231a6-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="231a6-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="231a6-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="231a6-171">Implementazione del criterio di indicizzazione V2.</span><span class="sxs-lookup"><span data-stu-id="231a6-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="231a6-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="231a6-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="231a6-173">Supporto della connessione proxy.</span><span class="sxs-lookup"><span data-stu-id="231a6-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="231a6-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="231a6-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="231a6-175">SDK con disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="231a6-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="231a6-176">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="231a6-176">Release & retirement dates</span></span>
<span data-ttu-id="231a6-177">Microsoft invierà una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.</span><span class="sxs-lookup"><span data-stu-id="231a6-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="231a6-178">Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="231a6-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="231a6-179">Qualsiasi tooCosmos richiesta database usando un SDK ritirato verranno rifiutati dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="231a6-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="231a6-180">Tutte le versioni di hello Azure DocumentDB SDK per Python precedente tooversion **1.0.0** verrà ritirato **29 febbraio 2016**.</span><span class="sxs-lookup"><span data-stu-id="231a6-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="231a6-181">Versione</span><span class="sxs-lookup"><span data-stu-id="231a6-181">Version</span></span> | <span data-ttu-id="231a6-182">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="231a6-182">Release Date</span></span> | <span data-ttu-id="231a6-183">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="231a6-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="231a6-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="231a6-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="231a6-185">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="231a6-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="231a6-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="231a6-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="231a6-187">01 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="231a6-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="231a6-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="231a6-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="231a6-189">30 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="231a6-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="231a6-191">29 settembre 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="231a6-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="231a6-193">07 luglio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="231a6-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="231a6-195">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="231a6-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="231a6-197">26 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="231a6-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="231a6-199">08 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="231a6-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="231a6-201">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="231a6-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="231a6-203">03 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="231a6-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="231a6-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="231a6-205">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="231a6-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="231a6-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="231a6-207">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="231a6-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="231a6-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="231a6-209">06 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="231a6-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="231a6-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="231a6-211">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="231a6-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="231a6-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="231a6-213">25 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="231a6-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="231a6-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="231a6-215">07 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="231a6-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="231a6-216">0.9.4-prelease</span></span> |<span data-ttu-id="231a6-217">14 gennaio 2015</span><span class="sxs-lookup"><span data-stu-id="231a6-217">January 14, 2015</span></span> |<span data-ttu-id="231a6-218">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-218">February 29, 2016</span></span> |
| <span data-ttu-id="231a6-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="231a6-219">0.9.3-prelease</span></span> |<span data-ttu-id="231a6-220">09 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="231a6-220">December 09, 2014</span></span> |<span data-ttu-id="231a6-221">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-221">February 29, 2016</span></span> |
| <span data-ttu-id="231a6-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="231a6-222">0.9.2-prelease</span></span> |<span data-ttu-id="231a6-223">25 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="231a6-223">November 25, 2014</span></span> |<span data-ttu-id="231a6-224">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-224">February 29, 2016</span></span> |
| <span data-ttu-id="231a6-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="231a6-225">0.9.1-prelease</span></span> |<span data-ttu-id="231a6-226">23 settembre 2014</span><span class="sxs-lookup"><span data-stu-id="231a6-226">September 23, 2014</span></span> |<span data-ttu-id="231a6-227">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-227">February 29, 2016</span></span> |
| <span data-ttu-id="231a6-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="231a6-228">0.9.0-prelease</span></span> |<span data-ttu-id="231a6-229">21 agosto 2014</span><span class="sxs-lookup"><span data-stu-id="231a6-229">August 21, 2014</span></span> |<span data-ttu-id="231a6-230">29 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="231a6-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="231a6-231">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="231a6-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="231a6-232">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="231a6-232">See also</span></span>
<span data-ttu-id="231a6-233">toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.</span><span class="sxs-lookup"><span data-stu-id="231a6-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

