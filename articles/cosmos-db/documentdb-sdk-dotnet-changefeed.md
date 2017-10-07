---
title: aaaAzure DocumentDB .NET modifica Feed processore SDK & risorse | Documenti Microsoft
description: Altre informazioni sui hello modifica Feed processore API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello DocumentDB .NET modifica Feed processore SDK.
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
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="af612-103">SDK del processore dei feed delle modifiche di DocumentDB .NET: download e note sulla versione</span><span class="sxs-lookup"><span data-stu-id="af612-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af612-104">.NET</span><span class="sxs-lookup"><span data-stu-id="af612-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="af612-105">Feed delle modifiche .NET</span><span class="sxs-lookup"><span data-stu-id="af612-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="af612-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="af612-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="af612-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="af612-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="af612-108">Java</span><span class="sxs-lookup"><span data-stu-id="af612-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="af612-109">Python</span><span class="sxs-lookup"><span data-stu-id="af612-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="af612-110">REST</span><span class="sxs-lookup"><span data-stu-id="af612-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="af612-111">Provider di risorse REST</span><span class="sxs-lookup"><span data-stu-id="af612-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="af612-112">SQL</span><span class="sxs-lookup"><span data-stu-id="af612-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="af612-113">**Download dell'SDK**</span><span class="sxs-lookup"><span data-stu-id="af612-113">**SDK download**</span></span></td><td>[<span data-ttu-id="af612-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="af612-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="af612-115">**Documentazione sull'API**</span><span class="sxs-lookup"><span data-stu-id="af612-115">**API documentation**</span></span></td><td>[<span data-ttu-id="af612-116">Documentazione di riferimento sull'API della libreria del processore dei feed delle modifiche</span><span class="sxs-lookup"><span data-stu-id="af612-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="af612-117">**Introduzione**</span><span class="sxs-lookup"><span data-stu-id="af612-117">**Get started**</span></span></td><td>[<span data-ttu-id="af612-118">Introduzione a hello DocumentDB modifica Feed processore .NET SDK</span><span class="sxs-lookup"><span data-stu-id="af612-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="af612-119">**Framework attualmente supportato**</span><span class="sxs-lookup"><span data-stu-id="af612-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="af612-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="af612-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="af612-121">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="af612-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="af612-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="af612-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="af612-123">Aggiungere un tooobtain metodo una stima delle rimanenti toobe lavoro elaborate in hello modifica Feed.</span><span class="sxs-lookup"><span data-stu-id="af612-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="af612-124">Compatibile con [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.13.2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="af612-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="af612-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="af612-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="af612-126">SDK con disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="af612-126">GA SDK</span></span>
* <span data-ttu-id="af612-127">Compatibile con [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) 1.14.1 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="af612-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="af612-128">Date di rilascio e di ritiro</span><span class="sxs-lookup"><span data-stu-id="af612-128">Release & Retirement dates</span></span>
<span data-ttu-id="af612-129">Microsoft invierà una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.</span><span class="sxs-lookup"><span data-stu-id="af612-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="af612-130">Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="af612-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="af612-131">Qualsiasi tooCosmos richiesta database usando un SDK ritirato verranno rifiutati dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="af612-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="af612-132">Versione</span><span class="sxs-lookup"><span data-stu-id="af612-132">Version</span></span> | <span data-ttu-id="af612-133">Data di rilascio</span><span class="sxs-lookup"><span data-stu-id="af612-133">Release Date</span></span> | <span data-ttu-id="af612-134">Data di ritiro</span><span class="sxs-lookup"><span data-stu-id="af612-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="af612-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="af612-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="af612-136">13 agosto 2017</span><span class="sxs-lookup"><span data-stu-id="af612-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="af612-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="af612-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="af612-138">07 luglio 2017</span><span class="sxs-lookup"><span data-stu-id="af612-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="af612-139">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="af612-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="af612-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="af612-140">See also</span></span>
<span data-ttu-id="af612-141">toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio.</span><span class="sxs-lookup"><span data-stu-id="af612-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

