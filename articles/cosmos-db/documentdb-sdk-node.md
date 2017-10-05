---
title: 'Azure Cosmos DB: risorse, SDK e API Node.js | Microsoft Docs'
description: Informazioni complete sull'SDK e sull'API Node.js, incluse le date di rilascio e di ritiro e le modifiche apportate tra le singole versioni di Azure Cosmos DB Node.js SDK.
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="fecb8-103">Azure Cosmos DB Node.js SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="fecb8-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fecb8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="fecb8-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="fecb8-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="fecb8-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="fecb8-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fecb8-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="fecb8-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="fecb8-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="fecb8-108">Java</span><span class="sxs-lookup"><span data-stu-id="fecb8-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="fecb8-109">Python</span><span class="sxs-lookup"><span data-stu-id="fecb8-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="fecb8-110">REST</span><span class="sxs-lookup"><span data-stu-id="fecb8-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="fecb8-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="fecb8-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="fecb8-112">SQL</span><span class="sxs-lookup"><span data-stu-id="fecb8-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="fecb8-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="fecb8-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="fecb8-114">NPM</span><span class="sxs-lookup"><span data-stu-id="fecb8-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="fecb8-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="fecb8-115">**API documentation**</span></span></td><td>[<span data-ttu-id="fecb8-116">Documentazione di riferimento delle API di Node.js</span><span class="sxs-lookup"><span data-stu-id="fecb8-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="fecb8-117">**Istruzioni per l'installazione dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="fecb8-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="fecb8-118">Istruzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="fecb8-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="fecb8-119">**Contribuire all'SDK**</span><span class="sxs-lookup"><span data-stu-id="fecb8-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="fecb8-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="fecb8-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="fecb8-121">**Esempi**</span><span class="sxs-lookup"><span data-stu-id="fecb8-121">**Samples**</span></span></td><td>[<span data-ttu-id="fecb8-122">Esempi di codice Node.js</span><span class="sxs-lookup"><span data-stu-id="fecb8-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="fecb8-123">**Esercitazione introduttiva**</span><span class="sxs-lookup"><span data-stu-id="fecb8-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="fecb8-124">Introduzione all'SDK di Node.js</span><span class="sxs-lookup"><span data-stu-id="fecb8-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="fecb8-125">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="fecb8-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="fecb8-126">Creare un'applicazione Web Node.js con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fecb8-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="fecb8-127">**Piattaforma attualmente supportata**</span><span class="sxs-lookup"><span data-stu-id="fecb8-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="fecb8-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="fecb8-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="fecb8-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="fecb8-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="fecb8-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="fecb8-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="fecb8-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="fecb8-132">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="fecb8-132">Release notes</span></span>

### <span data-ttu-id="fecb8-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="fecb8-134">Correzione della documentazione di npm.</span><span class="sxs-lookup"><span data-stu-id="fecb8-134">npm documentation fixed.</span></span>

### <span data-ttu-id="fecb8-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="fecb8-136">Correzione di un bug in executeStoredProcedure per cui i documenti coinvolti contenevano caratteri Unicode speciali (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="fecb8-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="fecb8-137">Correzione di un bug nella gestione di documenti con caratteri Unicode nella chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="fecb8-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="fecb8-138">Correzione del supporto per la creazione di raccolte con i supporti di memorizzazione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="fecb8-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="fecb8-139">Problema GitHub n. 114.</span><span class="sxs-lookup"><span data-stu-id="fecb8-139">Github issue #114.</span></span>
* <span data-ttu-id="fecb8-140">Correzione del supporto per il token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="fecb8-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="fecb8-141">Problema GitHub n. 178.</span><span class="sxs-lookup"><span data-stu-id="fecb8-141">Github issue #178.</span></span>

### <span data-ttu-id="fecb8-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="fecb8-143">Aggiunta del supporto per nuovi [livelli di coerenza](consistency-levels.md) denominati ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="fecb8-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="fecb8-144">Aggiunta del supporto per UriFactory.</span><span class="sxs-lookup"><span data-stu-id="fecb8-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="fecb8-145">Correzione di un bug del supporto Unicode.</span><span class="sxs-lookup"><span data-stu-id="fecb8-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="fecb8-146">Problema GitHub n. 171.</span><span class="sxs-lookup"><span data-stu-id="fecb8-146">GitHub issue #171.</span></span>

### <span data-ttu-id="fecb8-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="fecb8-148">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="fecb8-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="fecb8-149">Aggiunta dell'opzione per il controllo del grado di parallelismo per query nella partizione.</span><span class="sxs-lookup"><span data-stu-id="fecb8-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="fecb8-150">Aggiunta dell'opzione per disabilitare la verifica SSL durante l'esecuzione sull'emulatore Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fecb8-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="fecb8-151">Velocità effettiva minima ridotta nelle raccolte partizionate da 10.100 UR/s a 2.500 UR/s.</span><span class="sxs-lookup"><span data-stu-id="fecb8-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="fecb8-152">Correzione del bug del token di continuazione per la raccolta a partizione singola.</span><span class="sxs-lookup"><span data-stu-id="fecb8-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="fecb8-153">Problema GitHub n. 107.</span><span class="sxs-lookup"><span data-stu-id="fecb8-153">Github issue #107.</span></span>
* <span data-ttu-id="fecb8-154">Correzione del bug executeStoredProcedure nella gestione di 0 come parametro singolo.</span><span class="sxs-lookup"><span data-stu-id="fecb8-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="fecb8-155">Problema GitHub n. 155.</span><span class="sxs-lookup"><span data-stu-id="fecb8-155">Github issue #155.</span></span>

### <span data-ttu-id="fecb8-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="fecb8-157">Corretta l'intestazione agente-utente per includere la versione di SDK.</span><span class="sxs-lookup"><span data-stu-id="fecb8-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="fecb8-158">Pulizia del codice di minore entità.</span><span class="sxs-lookup"><span data-stu-id="fecb8-158">Minor code cleanup.</span></span>

### <span data-ttu-id="fecb8-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="fecb8-160">Disabilitazione della verifica SSL durante l'uso dell'SDK per l'emulatore(nomehost=host).</span><span class="sxs-lookup"><span data-stu-id="fecb8-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="fecb8-161">Aggiunta del supporto per l'abilitazione della registrazione degli script durante l'esecuzione di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="fecb8-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="fecb8-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="fecb8-163">Aggiunta del supporto per le query in parallelo nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="fecb8-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="fecb8-164">Aggiunta del supporto per le query TOP/ORDER BY nelle raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="fecb8-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="fecb8-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="fecb8-166">Aggiunta del supporto per il criterio di ripetizione dei tentativi delle richieste limitate</span><span class="sxs-lookup"><span data-stu-id="fecb8-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="fecb8-167">(le richieste limitate ricevano un'eccezione troppo grande per la frequenza delle richieste, con codice di errore 429). Per impostazione predefinita, Cosmos DB esegue nove tentativi per ogni richiesta con codice di errore 429, rispettando l'intervallo di tempo di retryAfter specificato nell'intestazione della risposta.</span><span class="sxs-lookup"><span data-stu-id="fecb8-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="fecb8-168">Adesso è possibile impostare un intervallo di tempo fisso per i tentativi come parte della proprietà RetryOptions nell'oggetto ConnectionPolicy se si desidera ignorare il tempo di retryAfter restituito dal server tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="fecb8-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="fecb8-169">Azure Cosmos DB attende al massimo 30 secondi per ogni richiesta che viene limitata (indipendentemente dal numero di tentativi) e restituisce la risposta con il codice di errore 429.</span><span class="sxs-lookup"><span data-stu-id="fecb8-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="fecb8-170">Questo tempo può essere sottoposto a override nella proprietà RetryOptions dell'oggetto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="fecb8-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="fecb8-171">Cosmos DB restituisce ora i parametri x-ms-throttle-retry-count e x-ms-throttle-retry-wait-time-ms come intestazioni di risposta in ogni richiesta per indicare il numero di nuovi tentativi di limitazione e il tempo cumulativo di attesa della richiesta tra i tentativi.</span><span class="sxs-lookup"><span data-stu-id="fecb8-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="fecb8-172">La classe RetryOptions è stata aggiunta, esponendo la proprietà RetryOptions nella classe ConnectionPolicy che può essere utilizzata per eseguire l'override di alcune opzioni di ripetizione dei tentativi predefinite.</span><span class="sxs-lookup"><span data-stu-id="fecb8-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="fecb8-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="fecb8-174">Aggiunta del supporto per gli account di database con più aree.</span><span class="sxs-lookup"><span data-stu-id="fecb8-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="fecb8-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="fecb8-176">Aggiunta del supporto per la funzionalità di durata (TTL) relativa ai documenti.</span><span class="sxs-lookup"><span data-stu-id="fecb8-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="fecb8-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="fecb8-178">Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fecb8-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="fecb8-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="fecb8-180">Correzione del bug RangePartitionResolver.resolveForRead, relativo alla mancata restituzione di collegamenti a causa di un concatenamento non valido dei risultati.</span><span class="sxs-lookup"><span data-stu-id="fecb8-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="fecb8-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="fecb8-182">Corretto hashParitionResolver resolveForRead(): quando la mancata indicazione di una chiave di partizione generava un'eccezione, invece di restituire un elenco di tutti i collegamenti registrati.</span><span class="sxs-lookup"><span data-stu-id="fecb8-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="fecb8-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="fecb8-184">Correzione del problema [n. 100](https://github.com/Azure/azure-documentdb-node/issues/100) relativo all'agente HTTPS dedicato: evitare di modificare l'agente globale per gli scopi di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fecb8-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="fecb8-185">Usare un agente dedicato per tutte le richieste della libreria.</span><span class="sxs-lookup"><span data-stu-id="fecb8-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="fecb8-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="fecb8-187">Correzione del problema [n. 81](https://github.com/Azure/azure-documentdb-node/issues/81) : gestione corretta dei trattini negli ID dei file multimediali.</span><span class="sxs-lookup"><span data-stu-id="fecb8-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="fecb8-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="fecb8-189">Correzione del problema [n. 95](https://github.com/Azure/azure-documentdb-node/issues/95) : avviso di perdita del listener EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="fecb8-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="fecb8-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="fecb8-191">Correzione del problema [n. 92](https://github.com/Azure/azure-documentdb-node/issues/90): ridenominazione della cartella Hash in hash per i sistemi con distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="fecb8-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="fecb8-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="fecb8-193">Implementazione del supporto per il partizionamento orizzontale mediante l'aggiunta di resolver della partizione a intervalli e hash.</span><span class="sxs-lookup"><span data-stu-id="fecb8-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="fecb8-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="fecb8-195">Implementazione di Upsert.</span><span class="sxs-lookup"><span data-stu-id="fecb8-195">Implement Upsert.</span></span> <span data-ttu-id="fecb8-196">Nuovi metodi upsertXXX in documentClient.</span><span class="sxs-lookup"><span data-stu-id="fecb8-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="fecb8-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="fecb8-198">Saltata per riallineare il numero di versione con altri SDK.</span><span class="sxs-lookup"><span data-stu-id="fecb8-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="fecb8-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="fecb8-200">Divisione del wrapper Q promise per il nuovo repository</span><span class="sxs-lookup"><span data-stu-id="fecb8-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="fecb8-201">Aggiornamento del file del pacchetto del Registro di sistema npm</span><span class="sxs-lookup"><span data-stu-id="fecb8-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="fecb8-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="fecb8-203">Implementazione del routing basato su ID</span><span class="sxs-lookup"><span data-stu-id="fecb8-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="fecb8-204">Correzione del problema [n. 49](https://github.com/Azure/azure-documentdb-node/issues/49) : conflitto tra la proprietà current e il metodo current().</span><span class="sxs-lookup"><span data-stu-id="fecb8-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="fecb8-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="fecb8-206">Aggiunta del supporto per l'indice GeoSpatial</span><span class="sxs-lookup"><span data-stu-id="fecb8-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="fecb8-207">Convalida la proprietà id per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="fecb8-207">Validates id property for all resources.</span></span> <span data-ttu-id="fecb8-208">Gli ID per le risorse non possono contenere i caratteri ?, /, #, &#47;&#47; o terminare con uno spazio.</span><span class="sxs-lookup"><span data-stu-id="fecb8-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="fecb8-209">Aggiunge la nuova intestazione "stato di trasformazione dell'indice" a ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="fecb8-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="fecb8-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="fecb8-211">Implementazione del criterio di indicizzazione V2.</span><span class="sxs-lookup"><span data-stu-id="fecb8-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="fecb8-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="fecb8-213">Problema [n. 40](https://github.com/Azure/azure-documentdb-node/issues/40) : implementazione delle configurazioni eslint e grunt nell'SDK core e promise.</span><span class="sxs-lookup"><span data-stu-id="fecb8-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="fecb8-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="fecb8-215">Problema [#45](https://github.com/Azure/azure-documentdb-node/issues/45) : il wrapper promise non include l'intestazione con errore</span><span class="sxs-lookup"><span data-stu-id="fecb8-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="fecb8-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="fecb8-217">Implementazione della possibilità di eseguire query per i conflitti aggiungendo readConflicts, readConflictAsync e queryConflicts</span><span class="sxs-lookup"><span data-stu-id="fecb8-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="fecb8-218">Aggiornamento della documentazione relativa alle API</span><span class="sxs-lookup"><span data-stu-id="fecb8-218">Updated API documentation.</span></span>
* <span data-ttu-id="fecb8-219">Problema [n. 41](https://github.com/Azure/azure-documentdb-node/issues/41) : errore client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="fecb8-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="fecb8-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="fecb8-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="fecb8-221">SDK con disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="fecb8-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="fecb8-222">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="fecb8-222">Release & Retirement Dates</span></span>
<span data-ttu-id="fecb8-223">Microsoft invia una notifica almeno **12 mesi** prima del ritiro di un SDK per agevolare la transizione a una versione più recente o supportata.</span><span class="sxs-lookup"><span data-stu-id="fecb8-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="fecb8-224">Le nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunte solo all'SDK corrente. È quindi consigliabile eseguire sempre l'aggiornamento alla versione più recente dell'SDK quanto prima.</span><span class="sxs-lookup"><span data-stu-id="fecb8-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="fecb8-225">Qualsiasi richiesta inviata a Cosmos DB con un SDK ritirato viene rifiutata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="fecb8-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="fecb8-226">Versione</span><span class="sxs-lookup"><span data-stu-id="fecb8-226">Version</span></span> | <span data-ttu-id="fecb8-227">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="fecb8-227">Release Date</span></span> | <span data-ttu-id="fecb8-228">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="fecb8-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="fecb8-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="fecb8-230">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="fecb8-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="fecb8-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="fecb8-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="fecb8-232">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="fecb8-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="fecb8-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="fecb8-234">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="fecb8-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="fecb8-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="fecb8-236">16 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="fecb8-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="fecb8-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="fecb8-238">27 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="fecb8-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="fecb8-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="fecb8-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="fecb8-240">22 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="fecb8-242">03 ottobre 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="fecb8-244">07 luglio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="fecb8-246">14 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="fecb8-248">26 aprile 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="fecb8-250">29 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="fecb8-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="fecb8-252">08 marzo 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="fecb8-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="fecb8-254">02 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="fecb8-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="fecb8-256">01 febbraio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="fecb8-258">26 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="fecb8-260">22 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="fecb8-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="fecb8-262">4 gennaio 2016</span><span class="sxs-lookup"><span data-stu-id="fecb8-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="fecb8-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="fecb8-264">31 dicembre 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="fecb8-266">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="fecb8-268">06 ottobre 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="fecb8-270">10 settembre 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="fecb8-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="fecb8-272">15 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="fecb8-274">05 agosto 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="fecb8-276">09 luglio 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="fecb8-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="fecb8-278">04 giugno 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="fecb8-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="fecb8-280">23 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="fecb8-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="fecb8-282">15 maggio 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="fecb8-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="fecb8-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="fecb8-284">08 aprile 2015</span><span class="sxs-lookup"><span data-stu-id="fecb8-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="fecb8-285">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="fecb8-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="fecb8-286">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fecb8-286">See also</span></span>
<span data-ttu-id="fecb8-287">Per altre informazioni su Cosmos DB, vedere la pagina del servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="fecb8-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

