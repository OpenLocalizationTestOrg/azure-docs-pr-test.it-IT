---
title: aaaAzure Cosmos DB .NET Core API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello .NET Core API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="89885-103">Azure Cosmos DB .NET Core SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="89885-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89885-104">.NET</span><span class="sxs-lookup"><span data-stu-id="89885-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="89885-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="89885-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="89885-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="89885-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="89885-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="89885-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="89885-108">Java</span><span class="sxs-lookup"><span data-stu-id="89885-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="89885-109">Python</span><span class="sxs-lookup"><span data-stu-id="89885-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="89885-110">REST</span><span class="sxs-lookup"><span data-stu-id="89885-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="89885-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="89885-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="89885-112">SQL</span><span class="sxs-lookup"><span data-stu-id="89885-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="89885-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="89885-113">**SDK download**</span></span></td><td>[<span data-ttu-id="89885-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="89885-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="89885-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="89885-115">**API documentation**</span></span></td><td>[<span data-ttu-id="89885-116">Documentazione di riferimento API .NET</span><span class="sxs-lookup"><span data-stu-id="89885-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="89885-117">**Esempi**</span><span class="sxs-lookup"><span data-stu-id="89885-117">**Samples**</span></span></td><td>[<span data-ttu-id="89885-118">Esempi di codice .NET</span><span class="sxs-lookup"><span data-stu-id="89885-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="89885-119">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="89885-119">**Get started**</span></span></td><td>[<span data-ttu-id="89885-120">Introduzione a hello Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="89885-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="89885-121">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="89885-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="89885-122">Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89885-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="89885-123">**Framework attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="89885-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="89885-124">.NET standard 1.6 e .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="89885-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="89885-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="89885-125">Release Notes</span></span>

<span data-ttu-id="89885-126">Hello Azure Cosmos DB .NET Core SDK dispone di parità di funzionalità con la versione più recente di hello di hello [SDK .NET di Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="89885-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="89885-127">non ancora Hello Azure Cosmos DB .NET Core SDK è compatibile con le app Universal Windows Platform (UWP).</span><span class="sxs-lookup"><span data-stu-id="89885-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="89885-128">Se è interessati a hello .NET Core SDK che supporta le app UWP, inviare posta elettronica troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="89885-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="89885-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="89885-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="89885-130">Aggiunta del supporto per PartitionKeyRangeId come un FeedOption per definire l'ambito di valore di intervallo di chiavi di query risultati tooa partizione specifica.</span><span class="sxs-lookup"><span data-stu-id="89885-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="89885-131">Aggiunta del supporto per StartTime come un toostart ChangeFeedOption cercando modifiche hello dopo tale periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="89885-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="89885-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="89885-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="89885-133">Risolto un problema in hello classe JsonSerializable che potrebbe causare un'eccezione di overflow dello stack.</span><span class="sxs-lookup"><span data-stu-id="89885-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="89885-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="89885-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="89885-135">Aggiunta del supporto per la definizione di JsonSerializerSettings personalizzate durante la creazione di un'istanza di [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="89885-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="89885-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="89885-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="89885-137">Supporto .NET Standard 1.5 come uno dei framework di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="89885-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="89885-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="89885-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="89885-139">Risoluzione di un problema riguardante i computer x64 che non supportano l'istruzione SSE4 e generano SEHException durante l'esecuzione di query di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89885-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="89885-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="89885-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="89885-141">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="89885-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="89885-142">Aggiunta del supporto per le metriche delle query per le singole partizioni.</span><span class="sxs-lookup"><span data-stu-id="89885-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="89885-143">Aggiunta del supporto per la limitazione delle dimensioni di hello hello del token di continuazione per le query.</span><span class="sxs-lookup"><span data-stu-id="89885-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="89885-144">Aggiunta del supporto per una traccia più dettagliata delle richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="89885-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="89885-145">Introdotti alcuni miglioramenti delle prestazioni hello SDK.</span><span class="sxs-lookup"><span data-stu-id="89885-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="89885-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="89885-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="89885-147">Risolto un problema che ignorati valore PartitionKey hello fornito FeedOptions per le query di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="89885-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="89885-148">Risolto un problema nella gestione trasparente delle partizioni durante l'esecuzione dell'ordinamento per query della partizione trasversale intermedia.</span><span class="sxs-lookup"><span data-stu-id="89885-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="89885-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="89885-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="89885-150">Risolto un problema che ha causato deadlock in alcune hello async API quando utilizzato all'interno di contesto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="89885-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="89885-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="89885-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="89885-152">Consente di correggere toomake SDK più failover tooautomatic resiliente a determinate condizioni.</span><span class="sxs-lookup"><span data-stu-id="89885-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="89885-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="89885-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="89885-154">Correzione di un problema che causa un'eccezione WebException: Impossibile risolto nome remoto hello.</span><span class="sxs-lookup"><span data-stu-id="89885-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="89885-155">Hello aggiunto il supporto per lettura diretta di un documento tipizzato tramite l'aggiunta di nuove API tooReadDocumentAsync di overload.</span><span class="sxs-lookup"><span data-stu-id="89885-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="89885-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="89885-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="89885-157">Aggiunta del supporto LINQ per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="89885-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="89885-158">Correzione per un problema di perdita di memoria per oggetto ConnectionPolicy hello causato dall'uso di hello del gestore eventi.</span><span class="sxs-lookup"><span data-stu-id="89885-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="89885-159">Correzione per un problema relativo al mancato funzionamento di UpsertAttachmentAsync in caso di uso di ETag.</span><span class="sxs-lookup"><span data-stu-id="89885-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="89885-160">Correzione di un problema relativo al mancato funzionamento della continuazione della query di tipo order-by tra partizioni in caso di ordinamento in un campo di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="89885-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="89885-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="89885-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="89885-162">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="89885-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="89885-163">Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="89885-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="89885-164">Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.</span><span class="sxs-lookup"><span data-stu-id="89885-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="89885-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="89885-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="89885-166">Hello Azure Cosmos DB .NET Core SDK consente toobuild veloci, multipiattaforma [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun App in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="89885-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="89885-167">Hello ultima versione di hello Azure Cosmos DB .NET Core SDK è completamente [Xamarin](https://www.xamarin.com) compatibile e applicazioni usati toobuild destinate Mono (Linux), iOS e Android.</span><span class="sxs-lookup"><span data-stu-id="89885-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="89885-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="89885-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="89885-169">Hello Azure Cosmos DB .NET Core anteprima SDK consente toobuild veloci, multipiattaforma [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun App in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="89885-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="89885-170">Hello Azure Cosmos DB .NET Core anteprima SDK dispone di parità di funzionalità con la versione più recente di hello di hello [SDK .NET di Azure Cosmos DB](documentdb-sdk-dotnet.md) e supporta hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="89885-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="89885-171">Tutte le [modalità di connessione](performance-tips.md#networking): modalità gateway, TCP diretto e HTTP diretti.</span><span class="sxs-lookup"><span data-stu-id="89885-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="89885-172">Tutti i [livelli di coerenza](consistency-levels.md): assoluta, di sessione, con decadimento ristretto e finale.</span><span class="sxs-lookup"><span data-stu-id="89885-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="89885-173">[Raccolte partizionate](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="89885-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="89885-174">[Account di database tra più aree e replica geografica](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="89885-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="89885-175">Nel caso di domande correlate toothis SDK, registrare troppo[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), o il file di un problema in hello [repository github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="89885-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="89885-176">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="89885-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="89885-177">Version</span><span class="sxs-lookup"><span data-stu-id="89885-177">Version</span></span> | <span data-ttu-id="89885-178">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="89885-178">Release Date</span></span> | <span data-ttu-id="89885-179">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="89885-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="89885-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="89885-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="89885-181">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="89885-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="89885-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="89885-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="89885-183">07 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="89885-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="89885-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="89885-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="89885-185">02 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="89885-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="89885-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="89885-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="89885-187">12 giugno 2017</span><span class="sxs-lookup"><span data-stu-id="89885-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="89885-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="89885-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="89885-189">23 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="89885-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="89885-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="89885-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="89885-191">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="89885-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="89885-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="89885-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="89885-193">19 aprile 2017</span><span class="sxs-lookup"><span data-stu-id="89885-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="89885-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="89885-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="89885-195">29 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="89885-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="89885-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="89885-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="89885-197">25 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="89885-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="89885-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="89885-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="89885-199">20 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="89885-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="89885-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="89885-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="89885-201">14 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="89885-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="89885-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="89885-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="89885-203">16 febbraio 2017</span><span class="sxs-lookup"><span data-stu-id="89885-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="89885-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="89885-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="89885-205">21 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="89885-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="89885-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="89885-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="89885-207">15 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="89885-207">November 15, 2016</span></span> |<span data-ttu-id="89885-208">31 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="89885-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="89885-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="89885-209">See Also</span></span>
<span data-ttu-id="89885-210">toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.</span><span class="sxs-lookup"><span data-stu-id="89885-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

