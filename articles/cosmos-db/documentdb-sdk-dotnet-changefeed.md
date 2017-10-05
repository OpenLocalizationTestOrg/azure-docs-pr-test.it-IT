---
title: Risorse ed SDK del processore dei feed delle modifiche per Azure DocumentDB .NET | Microsoft Docs
description: Tutte le informazioni sull'SDK e sull'API del processore dei feed delle modifiche, incluse le date di rilascio, le date di ritiro e le modifiche apportate tra le versioni dell'SDK del processore dei feed delle modifiche di DocumentDB .NET.
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 40c796bc5af1220c46950a6fac062ffdd243e59f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="e4a96-103">SDK del processore dei feed delle modifiche di DocumentDB .NET: download e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="e4a96-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4a96-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e4a96-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="e4a96-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="e4a96-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="e4a96-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="e4a96-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="e4a96-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="e4a96-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="e4a96-108">Java</span><span class="sxs-lookup"><span data-stu-id="e4a96-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="e4a96-109">Python</span><span class="sxs-lookup"><span data-stu-id="e4a96-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="e4a96-110">REST</span><span class="sxs-lookup"><span data-stu-id="e4a96-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="e4a96-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="e4a96-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="e4a96-112">SQL</span><span class="sxs-lookup"><span data-stu-id="e4a96-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="e4a96-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="e4a96-113">**SDK download**</span></span></td><td>[<span data-ttu-id="e4a96-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="e4a96-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="e4a96-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="e4a96-115">**API documentation**</span></span></td><td>[<span data-ttu-id="e4a96-116">Documentazione di riferimento sull'API della libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="e4a96-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="e4a96-117">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="e4a96-117">**Get started**</span></span></td><td>[<span data-ttu-id="e4a96-118">Introduzione all'SDK del processore dei feed delle modifiche di DocumentDB .NET</span><span class="sxs-lookup"><span data-stu-id="e4a96-118">Get started with the DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="e4a96-119">**Framework attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="e4a96-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="e4a96-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e4a96-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="e4a96-121">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="e4a96-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="e4a96-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a96-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="e4a96-123">Aggiungere un metodo per ottenere una stima di quanto resta da elaborare nel feed delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="e4a96-123">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="e4a96-124">Compatibile con [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.13.2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e4a96-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="e4a96-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a96-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="e4a96-126">SDK con disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="e4a96-126">GA SDK</span></span>
* <span data-ttu-id="e4a96-127">Compatibile con [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.14.1 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="e4a96-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="e4a96-128">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="e4a96-128">Release & Retirement dates</span></span>
<span data-ttu-id="e4a96-129">Microsoft invierà una notifica almeno **12 mesi** prima del ritiro di un SDK per agevolare la transizione a una versione più recente o supportata.</span><span class="sxs-lookup"><span data-stu-id="e4a96-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="e4a96-130">Le nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunte solo all'SDK corrente. È quindi consigliabile eseguire sempre l'aggiornamento alla versione più recente dell'SDK quanto prima.</span><span class="sxs-lookup"><span data-stu-id="e4a96-130">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="e4a96-131">Qualsiasi richiesta inviata a Cosmos DB con un SDK ritirato verrà rifiutata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="e4a96-131">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="e4a96-132">Versione</span><span class="sxs-lookup"><span data-stu-id="e4a96-132">Version</span></span> | <span data-ttu-id="e4a96-133">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="e4a96-133">Release Date</span></span> | <span data-ttu-id="e4a96-134">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="e4a96-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e4a96-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a96-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="e4a96-136">13 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="e4a96-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="e4a96-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a96-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="e4a96-138">07 luglio 2017</span><span class="sxs-lookup"><span data-stu-id="e4a96-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="e4a96-139">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="e4a96-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="e4a96-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e4a96-140">See also</span></span>
<span data-ttu-id="e4a96-141">Per altre informazioni su Cosmos DB, vedere la pagina del servizio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e4a96-141">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

