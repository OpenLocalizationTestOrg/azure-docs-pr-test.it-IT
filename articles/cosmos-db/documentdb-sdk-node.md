---
title: aaaAzure Cosmos DB Node.js API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello Node.js API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB Node.js SDK.
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="cf67a-103">Azure Cosmos DB Node.js SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="cf67a-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf67a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cf67a-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="cf67a-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="cf67a-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="cf67a-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="cf67a-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="cf67a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="cf67a-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="cf67a-108">Java</span><span class="sxs-lookup"><span data-stu-id="cf67a-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="cf67a-109">Python</span><span class="sxs-lookup"><span data-stu-id="cf67a-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="cf67a-110">REST</span><span class="sxs-lookup"><span data-stu-id="cf67a-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="cf67a-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="cf67a-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="cf67a-112">SQL</span><span class="sxs-lookup"><span data-stu-id="cf67a-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="cf67a-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="cf67a-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="cf67a-114">NPM</span><span class="sxs-lookup"><span data-stu-id="cf67a-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="cf67a-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="cf67a-115">**API documentation**</span></span></td><td>[<span data-ttu-id="cf67a-116">Documentazione di riferimento delle API di Node.js</span><span class="sxs-lookup"><span data-stu-id="cf67a-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="cf67a-117">**Istruzioni per l'installazione dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="cf67a-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="cf67a-118">Istruzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="cf67a-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="cf67a-119">**Contribuiscono tooSDK**</span><span class="sxs-lookup"><span data-stu-id="cf67a-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="cf67a-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="cf67a-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="cf67a-121">**Esempi**</span><span class="sxs-lookup"><span data-stu-id="cf67a-121">**Samples**</span></span></td><td>[<span data-ttu-id="cf67a-122">Esempi di codice Node.js</span><span class="sxs-lookup"><span data-stu-id="cf67a-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="cf67a-123">**esercitazione introduttiva**</span><span class="sxs-lookup"><span data-stu-id="cf67a-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="cf67a-124">Introduzione a hello Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="cf67a-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="cf67a-125">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="cf67a-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="cf67a-126">Creare un'applicazione Web Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf67a-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="cf67a-127">**Piattaforma attualmente supportata**</span><span class="sxs-lookup"><span data-stu-id="cf67a-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="cf67a-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="cf67a-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="cf67a-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="cf67a-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="cf67a-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="cf67a-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="cf67a-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="cf67a-132">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="cf67a-132">Release notes</span></span>

### <span data-ttu-id="cf67a-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="cf67a-134">Correzione della documentazione di npm.</span><span class="sxs-lookup"><span data-stu-id="cf67a-134">npm documentation fixed.</span></span>

### <span data-ttu-id="cf67a-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="cf67a-136">Correzione di un bug in executeStoredProcedure per cui i documenti coinvolti contenevano caratteri Unicode speciali (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="cf67a-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="cf67a-137">Correzione di un bug nella gestione di documenti con i caratteri Unicode in una chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="cf67a-138">Supporto predefinito per la creazione di raccolte con i supporti di nome hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="cf67a-139">Problema GitHub n. 114.</span><span class="sxs-lookup"><span data-stu-id="cf67a-139">Github issue #114.</span></span>
* <span data-ttu-id="cf67a-140">Correzione del supporto per il token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="cf67a-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="cf67a-141">Problema GitHub n. 178.</span><span class="sxs-lookup"><span data-stu-id="cf67a-141">Github issue #178.</span></span>

### <span data-ttu-id="cf67a-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="cf67a-143">Aggiunta del supporto per nuovi [livelli di coerenza](consistency-levels.md) denominati ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="cf67a-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="cf67a-144">Aggiunta del supporto per UriFactory.</span><span class="sxs-lookup"><span data-stu-id="cf67a-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="cf67a-145">Correzione di un bug del supporto Unicode.</span><span class="sxs-lookup"><span data-stu-id="cf67a-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="cf67a-146">Problema GitHub n. 171.</span><span class="sxs-lookup"><span data-stu-id="cf67a-146">GitHub issue #171.</span></span>

### <span data-ttu-id="cf67a-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="cf67a-148">Supporto aggiunto hello per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="cf67a-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="cf67a-149">Opzione hello aggiunto per il controllo degree of parallelism per tra query della partizione.</span><span class="sxs-lookup"><span data-stu-id="cf67a-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="cf67a-150">Opzione hello aggiunto per disabilitare la verifica SSL durante l'esecuzione dell'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf67a-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="cf67a-151">Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="cf67a-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="cf67a-152">Bug token continuazione di hello predefinito per la raccolta singola partizione.</span><span class="sxs-lookup"><span data-stu-id="cf67a-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="cf67a-153">Problema GitHub n. 107.</span><span class="sxs-lookup"><span data-stu-id="cf67a-153">Github issue #107.</span></span>
* <span data-ttu-id="cf67a-154">Bug di executeStoredProcedure hello predefinito in Gestione 0 come param singolo.</span><span class="sxs-lookup"><span data-stu-id="cf67a-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="cf67a-155">Problema GitHub n. 155.</span><span class="sxs-lookup"><span data-stu-id="cf67a-155">Github issue #155.</span></span>

### <span data-ttu-id="cf67a-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="cf67a-157">Versione SDK hello tooinclude intestazione agente utente predefinito.</span><span class="sxs-lookup"><span data-stu-id="cf67a-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="cf67a-158">Pulizia del codice di minore entità.</span><span class="sxs-lookup"><span data-stu-id="cf67a-158">Minor code cleanup.</span></span>

### <span data-ttu-id="cf67a-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="cf67a-160">Quando si utilizza hello SDK tootarget hello emulator(hostname=localhost), disabilitare la verifica SSL.</span><span class="sxs-lookup"><span data-stu-id="cf67a-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="cf67a-161">Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="cf67a-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="cf67a-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="cf67a-163">Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="cf67a-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="cf67a-164">Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="cf67a-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="cf67a-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="cf67a-166">Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate</span><span class="sxs-lookup"><span data-stu-id="cf67a-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="cf67a-167">(le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Azure Cosmos DB Ritenta nove volte per ogni richiesta quando viene rilevato il codice di errore 429, rispettando la distinzione tra tempo retryAfter hello nell'intestazione di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="cf67a-168">Un intervallo di tempo predefinito di tentativi ora è possibile impostare come parte di hello RetryOptions proprietà nell'oggetto ConnectionPolicy hello se si desidera che l'ora di retryAfter hello tooignore restituito dal server tra i tentativi di hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="cf67a-169">Azure DB Cosmos ora attende per un massimo di 30 secondi per ogni richiesta che è limitata (indipendentemente dal numero di tentativi) e restituisce risposte hello con codice di errore 429.</span><span class="sxs-lookup"><span data-stu-id="cf67a-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="cf67a-170">Questa volta possa anche essere sottoposto a override in hello proprietà RetryOptions ConnectionPolicy oggetto.</span><span class="sxs-lookup"><span data-stu-id="cf67a-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="cf67a-171">COSMOS DB restituisce x-ms-limitazione--numero di tentativi e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta hello in ogni velocità di richiesta toodenote hello ripetere conteggio e hello cumulativo tempo di richiesta hello attesa tra i tentativi di hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="cf67a-172">classe RetryOptions Hello è stato aggiunto, esposizione hello RetryOptions proprietà sulla classe ConnectionPolicy hello che può essere utilizzati toooverride alcune predefinito hello le opzioni di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="cf67a-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="cf67a-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="cf67a-174">Supporto aggiunto hello per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="cf67a-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="cf67a-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="cf67a-176">Hello aggiunto il supporto per funzionalità tooLive(TTL) Time per i documenti.</span><span class="sxs-lookup"><span data-stu-id="cf67a-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="cf67a-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="cf67a-178">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="cf67a-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="cf67a-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="cf67a-180">Correzione del bug RangePartitionResolver.resolveForRead in cui non restituivano i collegamenti a causa di tooa concat non valido di risultati.</span><span class="sxs-lookup"><span data-stu-id="cf67a-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="cf67a-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="cf67a-182">Corretto hashParitionResolver resolveForRead(): quando la mancata indicazione di una chiave di partizione generava un'eccezione, invece di restituire un elenco di tutti i collegamenti registrati.</span><span class="sxs-lookup"><span data-stu-id="cf67a-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="cf67a-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="cf67a-184">Consente di correggere problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -dedicato agente HTTPS: evitare di modificare l'agente di globale hello per scopi di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf67a-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="cf67a-185">Utilizzare un agente dedicato per tutte le richieste del lib hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="cf67a-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="cf67a-187">Correzione del problema [n. 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestione corretta dei trattini negli ID dei file multimediali.</span><span class="sxs-lookup"><span data-stu-id="cf67a-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="cf67a-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="cf67a-189">Correzione del problema [n. 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avviso di perdita del listener EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="cf67a-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="cf67a-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="cf67a-191">Consente di correggere problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -rinominare toohash Hash cartella per i sistemi tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="cf67a-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="cf67a-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="cf67a-193">Implementazione del supporto per il partizionamento orizzontale mediante l'aggiunta di resolver della partizione a intervalli e hash.</span><span class="sxs-lookup"><span data-stu-id="cf67a-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="cf67a-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="cf67a-195">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="cf67a-195">Implement Upsert.</span></span> <span data-ttu-id="cf67a-196">Nuovi metodi upsertXXX in documentClient.</span><span class="sxs-lookup"><span data-stu-id="cf67a-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="cf67a-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="cf67a-198">Numeri di versione toobring ignorata in allineamento con altri SDK.</span><span class="sxs-lookup"><span data-stu-id="cf67a-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="cf67a-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="cf67a-200">Domande E Split promesse repository toonew wrapper.</span><span class="sxs-lookup"><span data-stu-id="cf67a-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="cf67a-201">Aggiornare il file toopackage per npm del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="cf67a-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="cf67a-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="cf67a-203">Implementazione del routing basato su ID</span><span class="sxs-lookup"><span data-stu-id="cf67a-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="cf67a-204">Correzione del problema [n. 49](https://github.com/Azure/azure-documentdb-node/issues/49) : conflitto tra la proprietà current e il metodo current().</span><span class="sxs-lookup"><span data-stu-id="cf67a-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="cf67a-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="cf67a-206">Aggiunta del supporto per l'indice GeoSpatial</span><span class="sxs-lookup"><span data-stu-id="cf67a-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="cf67a-207">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="cf67a-207">Validates id property for all resources.</span></span> <span data-ttu-id="cf67a-208">Gli ID per le risorse non possono contenere i caratteri ?, /, #, &#47;&#47; o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="cf67a-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="cf67a-209">Aggiunge una nuova intestazione "indice trasformazione lo stato di avanzamento" tooResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="cf67a-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="cf67a-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="cf67a-211">Implementazione del criterio di indicizzazione V2.</span><span class="sxs-lookup"><span data-stu-id="cf67a-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="cf67a-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="cf67a-213">Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) - implementato eslint e grunt le configurazioni di base hello e promise SDK.</span><span class="sxs-lookup"><span data-stu-id="cf67a-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="cf67a-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="cf67a-215">Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) : il wrapper promise non include l'intestazione con errore</span><span class="sxs-lookup"><span data-stu-id="cf67a-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="cf67a-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="cf67a-217">Implementato tooquery possibilità di conflitti aggiungendo readConflicts readConflictAsync e queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="cf67a-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="cf67a-218">Aggiornamento della documentazione relativa alle API</span><span class="sxs-lookup"><span data-stu-id="cf67a-218">Updated API documentation.</span></span>
* <span data-ttu-id="cf67a-219">Problema [n. 41](https://github.com/Azure/azure-documentdb-node/issues/41) : errore client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="cf67a-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="cf67a-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="cf67a-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="cf67a-221">SDK con disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="cf67a-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="cf67a-222">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="cf67a-222">Release & Retirement Dates</span></span>
<span data-ttu-id="cf67a-223">Microsoft fornisce una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.</span><span class="sxs-lookup"><span data-stu-id="cf67a-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="cf67a-224">Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="cf67a-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="cf67a-225">Qualsiasi richiesta tooCosmos database usando un SDK ritirato viene rifiutata dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="cf67a-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="cf67a-226">Versione</span><span class="sxs-lookup"><span data-stu-id="cf67a-226">Version</span></span> | <span data-ttu-id="cf67a-227">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="cf67a-227">Release Date</span></span> | <span data-ttu-id="cf67a-228">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="cf67a-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="cf67a-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="cf67a-230">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="cf67a-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="cf67a-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="cf67a-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="cf67a-232">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="cf67a-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="cf67a-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="cf67a-234">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="cf67a-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="cf67a-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="cf67a-236">16 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="cf67a-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="cf67a-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="cf67a-238">27 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="cf67a-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="cf67a-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="cf67a-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="cf67a-240">22 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="cf67a-242">03 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="cf67a-244">07 luglio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="cf67a-246">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="cf67a-248">26 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="cf67a-250">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="cf67a-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="cf67a-252">08 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="cf67a-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="cf67a-254">02 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="cf67a-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="cf67a-256">01 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="cf67a-258">26 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="cf67a-260">22 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="cf67a-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="cf67a-262">4 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="cf67a-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="cf67a-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="cf67a-264">31 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="cf67a-266">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="cf67a-268">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="cf67a-270">10 settembre 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="cf67a-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="cf67a-272">15 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="cf67a-274">05 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="cf67a-276">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="cf67a-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="cf67a-278">04 giugno 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="cf67a-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="cf67a-280">23 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="cf67a-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="cf67a-282">15 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="cf67a-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="cf67a-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="cf67a-284">08 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="cf67a-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="cf67a-285">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="cf67a-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="cf67a-286">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cf67a-286">See also</span></span>
<span data-ttu-id="cf67a-287">toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.</span><span class="sxs-lookup"><span data-stu-id="cf67a-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

