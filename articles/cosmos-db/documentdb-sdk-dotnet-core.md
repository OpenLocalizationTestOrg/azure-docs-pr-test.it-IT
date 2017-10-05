---
title: 'Azure Cosmos DB: risorse, SDK e API .NET Core | Microsoft Docs'
description: Informazioni complete sull'SDK e sull'API .NET Core, incluse le date di rilascio e di ritiro e le modifiche apportate tra le singole versioni di Azure Cosmos DB .NET Core SDK.
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
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="27d9d-103">Azure Cosmos DB .NET Core SDK: risorse e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="27d9d-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27d9d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="27d9d-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="27d9d-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="27d9d-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="27d9d-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="27d9d-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="27d9d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="27d9d-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="27d9d-108">Java</span><span class="sxs-lookup"><span data-stu-id="27d9d-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="27d9d-109">Python</span><span class="sxs-lookup"><span data-stu-id="27d9d-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="27d9d-110">REST</span><span class="sxs-lookup"><span data-stu-id="27d9d-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="27d9d-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="27d9d-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="27d9d-112">SQL</span><span class="sxs-lookup"><span data-stu-id="27d9d-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="27d9d-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="27d9d-113">**SDK download**</span></span></td><td>[<span data-ttu-id="27d9d-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="27d9d-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="27d9d-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="27d9d-115">**API documentation**</span></span></td><td>[<span data-ttu-id="27d9d-116">Documentazione di riferimento API .NET</span><span class="sxs-lookup"><span data-stu-id="27d9d-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="27d9d-117">**Esempi**</span><span class="sxs-lookup"><span data-stu-id="27d9d-117">**Samples**</span></span></td><td>[<span data-ttu-id="27d9d-118">Esempi di codice .NET</span><span class="sxs-lookup"><span data-stu-id="27d9d-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="27d9d-119">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="27d9d-119">**Get started**</span></span></td><td>[<span data-ttu-id="27d9d-120">Introduzione ad Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="27d9d-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="27d9d-121">**Esercitazione sull'app Web**</span><span class="sxs-lookup"><span data-stu-id="27d9d-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="27d9d-122">Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="27d9d-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="27d9d-123">**Framework attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="27d9d-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="27d9d-124">.NET standard 1.6 e .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="27d9d-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="27d9d-125">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="27d9d-125">Release Notes</span></span>

<span data-ttu-id="27d9d-126">Azure Cosmos DB .NET Core SDK ha le stesse funzionalità della versione più recente di [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="27d9d-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="27d9d-127">Azure Cosmos DB .NET Core SDK non è ancora compatibile con le app della piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="27d9d-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="27d9d-128">In caso di interesse a .NET Core SDK che supporta le app della piattaforma UWP, inviare un messaggio di posta elettronica a [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27d9d-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="27d9d-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="27d9d-130">Aggiunta del supporto per PartitionKeyRangeId come FeedOption per limitare l'ambito dei risultati di query a un intervallo di chiavi di partizione specifico.</span><span class="sxs-lookup"><span data-stu-id="27d9d-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="27d9d-131">Aggiunta del supporto per StartTime come ChangeFeedOption per avviare la ricerca delle modifiche a partire dall'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="27d9d-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="27d9d-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="27d9d-133">È stato risolto un problema nella classe JsonSerializable che può generare un'eccezione di overflow dello stack.</span><span class="sxs-lookup"><span data-stu-id="27d9d-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="27d9d-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="27d9d-135">Aggiunta del supporto per la definizione di JsonSerializerSettings personalizzate durante la creazione di un'istanza di [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="27d9d-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="27d9d-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="27d9d-137">Supporto di .NET Standard 1.5 come uno dei framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="27d9d-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="27d9d-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="27d9d-139">Risoluzione di un problema riguardante i computer x64 che non supportano l'istruzione SSE4 e generano SEHException durante l'esecuzione di query di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="27d9d-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="27d9d-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="27d9d-141">Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="27d9d-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="27d9d-142">Aggiunta del supporto per le metriche delle query per le singole partizioni.</span><span class="sxs-lookup"><span data-stu-id="27d9d-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="27d9d-143">Aggiunta del supporto per la limitazione delle dimensioni del token di continuazione per le query.</span><span class="sxs-lookup"><span data-stu-id="27d9d-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="27d9d-144">Aggiunta del supporto per una traccia più dettagliata delle richieste non riuscite.</span><span class="sxs-lookup"><span data-stu-id="27d9d-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="27d9d-145">Alcuni miglioramenti delle prestazioni nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="27d9d-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="27d9d-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="27d9d-147">Risolto un problema per cui il valore PartitionKey in FeedOptions veniva ignorato per le query di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="27d9d-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="27d9d-148">Risolto un problema nella gestione trasparente delle partizioni durante l'esecuzione dell'ordinamento per query della partizione trasversale intermedia.</span><span class="sxs-lookup"><span data-stu-id="27d9d-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="27d9d-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="27d9d-150">Correzione di un problema che ha causato deadlock in alcune API asincrone, se usate in un contesto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="27d9d-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="27d9d-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="27d9d-152">Correzioni per rendere l'SDK più resiliente per il failover automatico in determinate condizioni.</span><span class="sxs-lookup"><span data-stu-id="27d9d-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="27d9d-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="27d9d-154">Correzione di un problema che occasionalmente causa un'eccezione WebException, ovvero l'impossibilità di risolvere il nome remoto.</span><span class="sxs-lookup"><span data-stu-id="27d9d-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="27d9d-155">Aggiunta del supporto per la lettura diretta di un documento con tipo includendo nuovi overload all'API ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="27d9d-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="27d9d-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="27d9d-157">Aggiunta del supporto LINQ per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="27d9d-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="27d9d-158">Correzione per un problema di perdita di memoria per l'oggetto ConnectionPolicy provocata dall'uso del gestore eventi.</span><span class="sxs-lookup"><span data-stu-id="27d9d-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="27d9d-159">Correzione per un problema relativo al mancato funzionamento di UpsertAttachmentAsync in caso di uso di ETag.</span><span class="sxs-lookup"><span data-stu-id="27d9d-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="27d9d-160">Correzione di un problema relativo al mancato funzionamento della continuazione della query di tipo order-by tra partizioni in caso di ordinamento in un campo di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="27d9d-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="27d9d-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="27d9d-162">Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="27d9d-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="27d9d-163">Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="27d9d-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="27d9d-164">Velocità effettiva minima ridotta nelle raccolte partizionate da 10.100 UR/s a 2.500 UR/s.</span><span class="sxs-lookup"><span data-stu-id="27d9d-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="27d9d-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="27d9d-166">Azure Cosmos DB .NET Core SDK consente di compilare app [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) veloci e multipiattaforma da eseguire in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="27d9d-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="27d9d-167">L'ultima versione di Azure Cosmos DB .NET Core SDK è completamente compatibile con [Xamarin](https://www.xamarin.com) e può essere usata per compilare applicazioni destinate a iOS, Android e Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="27d9d-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="27d9d-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="27d9d-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="27d9d-169">Azure Cosmos DB .NET Core Preview SDK consente di compilare app [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) veloci e multipiattaforma da eseguire in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="27d9d-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="27d9d-170">Azure Cosmos DB .NET Core Preview SDK ha le stesse funzionalità della versione più recente di [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) e supporta quanto segue.</span><span class="sxs-lookup"><span data-stu-id="27d9d-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="27d9d-171">Tutte le [modalità di connessione](performance-tips.md#networking): modalità gateway, TCP diretto e HTTP diretti.</span><span class="sxs-lookup"><span data-stu-id="27d9d-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="27d9d-172">Tutti i [livelli di coerenza](consistency-levels.md): assoluta, di sessione, con decadimento ristretto e finale.</span><span class="sxs-lookup"><span data-stu-id="27d9d-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="27d9d-173">[Raccolte partizionate](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="27d9d-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="27d9d-174">[Account di database tra più aree e replica geografica](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="27d9d-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="27d9d-175">Per domande su questo SDK, pubblicare un post su [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) o inserire la domanda nel [repository github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="27d9d-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="27d9d-176">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="27d9d-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="27d9d-177">Version</span><span class="sxs-lookup"><span data-stu-id="27d9d-177">Version</span></span> | <span data-ttu-id="27d9d-178">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="27d9d-178">Release Date</span></span> | <span data-ttu-id="27d9d-179">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="27d9d-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="27d9d-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="27d9d-181">10 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="27d9d-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="27d9d-183">07 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="27d9d-185">02 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="27d9d-187">12 giugno 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="27d9d-189">23 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="27d9d-191">10 maggio 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="27d9d-193">19 aprile 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="27d9d-195">29 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="27d9d-197">25 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="27d9d-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="27d9d-199">20 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="27d9d-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="27d9d-201">14 marzo 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="27d9d-203">16 febbraio 2017</span><span class="sxs-lookup"><span data-stu-id="27d9d-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="27d9d-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="27d9d-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="27d9d-205">21 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="27d9d-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="27d9d-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="27d9d-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="27d9d-207">15 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="27d9d-207">November 15, 2016</span></span> |<span data-ttu-id="27d9d-208">31 dicembre 2016</span><span class="sxs-lookup"><span data-stu-id="27d9d-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="27d9d-209">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="27d9d-209">See Also</span></span>
<span data-ttu-id="27d9d-210">Per altre informazioni su Cosmos DB, vedere la pagina del servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="27d9d-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

