---
title: aaaAzure monitoraggio delle prestazioni di Service Fabric | Documenti Microsoft
description: Informazioni sui contatori delle prestazioni per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="c83e0-103">Metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c83e0-103">Performance metrics</span></span>

<span data-ttu-id="c83e0-104">Metriche devono essere raccolti toounderstand hello prestazioni del cluster nonché hello applicazioni in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c83e0-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="c83e0-105">Per i cluster di Service Fabric, è consigliabile raccogliere hello seguenti contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c83e0-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="c83e0-106">Nodi</span><span class="sxs-lookup"><span data-stu-id="c83e0-106">Nodes</span></span>

<span data-ttu-id="c83e0-107">Per le macchine di hello del cluster, prendere in considerazione la raccolta dei seguenti contatori delle prestazioni toobetter comprendere hello carico in ogni computer e rendere cluster appropriati scalabilità decisioni hello.</span><span class="sxs-lookup"><span data-stu-id="c83e0-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="c83e0-108">Categoria contatore</span><span class="sxs-lookup"><span data-stu-id="c83e0-108">Counter Category</span></span> | <span data-ttu-id="c83e0-109">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="c83e0-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c83e0-110">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-111">Avg. Disk Read Queue Length</span><span class="sxs-lookup"><span data-stu-id="c83e0-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="c83e0-112">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-113">Avg. Disk Write Queue Length</span><span class="sxs-lookup"><span data-stu-id="c83e0-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="c83e0-114">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-115">Avg. Disk sec/Read</span><span class="sxs-lookup"><span data-stu-id="c83e0-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="c83e0-116">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-117">Avg. Disk sec/Write</span><span class="sxs-lookup"><span data-stu-id="c83e0-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="c83e0-118">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-119">Letture disco/sec </span><span class="sxs-lookup"><span data-stu-id="c83e0-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="c83e0-120">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-121">Byte letti da disco/sec </span><span class="sxs-lookup"><span data-stu-id="c83e0-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="c83e0-122">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-123">Scritture disco/sec</span><span class="sxs-lookup"><span data-stu-id="c83e0-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="c83e0-124">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c83e0-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c83e0-125">Byte scritti su disco/sec</span><span class="sxs-lookup"><span data-stu-id="c83e0-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="c83e0-126">Memoria</span><span class="sxs-lookup"><span data-stu-id="c83e0-126">Memory</span></span> | <span data-ttu-id="c83e0-127">MByte disponibili</span><span class="sxs-lookup"><span data-stu-id="c83e0-127">Available MBytes</span></span> |
| <span data-ttu-id="c83e0-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="c83e0-128">PagingFile</span></span> | <span data-ttu-id="c83e0-129">% Usage</span><span class="sxs-lookup"><span data-stu-id="c83e0-129">% Usage</span></span> |
| <span data-ttu-id="c83e0-130">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="c83e0-130">Process(Total)</span></span> | <span data-ttu-id="c83e0-131">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="c83e0-131">% Processor Time</span></span> |
| <span data-ttu-id="c83e0-132">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-132">Process (per service)</span></span> | <span data-ttu-id="c83e0-133">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="c83e0-133">% Processor Time</span></span> |
| <span data-ttu-id="c83e0-134">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-134">Process (per service)</span></span> | <span data-ttu-id="c83e0-135">ID Process</span><span class="sxs-lookup"><span data-stu-id="c83e0-135">ID Process</span></span> |
| <span data-ttu-id="c83e0-136">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-136">Process (per service)</span></span> | <span data-ttu-id="c83e0-137">Private Bytes</span><span class="sxs-lookup"><span data-stu-id="c83e0-137">Private Bytes</span></span> |
| <span data-ttu-id="c83e0-138">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-138">Process (per service)</span></span> | <span data-ttu-id="c83e0-139">Thread Count</span><span class="sxs-lookup"><span data-stu-id="c83e0-139">Thread Count</span></span> |
| <span data-ttu-id="c83e0-140">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-140">Process (per service)</span></span> | <span data-ttu-id="c83e0-141">Virtual Bytes</span><span class="sxs-lookup"><span data-stu-id="c83e0-141">Virtual Bytes</span></span> |
| <span data-ttu-id="c83e0-142">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-142">Process (per service)</span></span> | <span data-ttu-id="c83e0-143">Working Set</span><span class="sxs-lookup"><span data-stu-id="c83e0-143">Working Set</span></span> |
| <span data-ttu-id="c83e0-144">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-144">Process (per service)</span></span> | <span data-ttu-id="c83e0-145">Working Set - Private</span><span class="sxs-lookup"><span data-stu-id="c83e0-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="c83e0-146">Applicazioni e servizi .NET</span><span class="sxs-lookup"><span data-stu-id="c83e0-146">.NET applications and services</span></span>

<span data-ttu-id="c83e0-147">Raccogliere i seguenti contatori se si distribuiscono cluster tooyour di .NET services hello.</span><span class="sxs-lookup"><span data-stu-id="c83e0-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="c83e0-148">Categoria contatore</span><span class="sxs-lookup"><span data-stu-id="c83e0-148">Counter Category</span></span> | <span data-ttu-id="c83e0-149">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="c83e0-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c83e0-150">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-151">ID di processo</span><span class="sxs-lookup"><span data-stu-id="c83e0-151">Process ID</span></span> |
| <span data-ttu-id="c83e0-152">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-153"># Total committed Bytes</span><span class="sxs-lookup"><span data-stu-id="c83e0-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="c83e0-154">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-155"># Total reserved Bytes</span><span class="sxs-lookup"><span data-stu-id="c83e0-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="c83e0-156">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-157"># Bytes in all Heaps</span><span class="sxs-lookup"><span data-stu-id="c83e0-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="c83e0-158">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-159"># Gen 0 Collections</span><span class="sxs-lookup"><span data-stu-id="c83e0-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="c83e0-160">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-161"># Gen 1 Collections</span><span class="sxs-lookup"><span data-stu-id="c83e0-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="c83e0-162">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-163"># Gen 2 Collections</span><span class="sxs-lookup"><span data-stu-id="c83e0-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="c83e0-164">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c83e0-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c83e0-165">Percentuale tempo in GC</span><span class="sxs-lookup"><span data-stu-id="c83e0-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="c83e0-166">Contatori delle prestazioni personalizzati di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c83e0-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="c83e0-167">Service Fabric genera una quantità significativa di contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c83e0-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="c83e0-168">Se si dispone di hello SDK installato, si noterà elenco completo di hello sul proprio computer Windows Performance Monitor nell'applicazione in uso (Start > Performance Monitor).</span><span class="sxs-lookup"><span data-stu-id="c83e0-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="c83e0-169">Nelle applicazioni hello si distribuiscono cluster tooyour, se si utilizza Reliable Actors, aggiungere countes da `Service Fabric Actor` e `Service Fabric Actor Method` categorie (vedere [servizio Fabric affidabile attori diagnostica](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="c83e0-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="c83e0-170">Analogamente, se si usa Reliable Services, è necessario raccogliere i contatori delle categorie `Service Fabric Service` e `Service Fabric Service Method`.</span><span class="sxs-lookup"><span data-stu-id="c83e0-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="c83e0-171">Se si utilizzano raccolte affidabile, è consigliabile aggiungere hello `Avg. Transaction ms/Commit` da hello `Service Fabric Transactional Replicator` la latenza media commit hello toocollect per ogni metrica di transazione.</span><span class="sxs-lookup"><span data-stu-id="c83e0-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c83e0-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c83e0-172">Next steps</span></span>

* <span data-ttu-id="c83e0-173">Altre informazioni, vedere [la generazione di eventi a livello di piattaforma hello](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c83e0-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="c83e0-174">Raccogliere metriche delle prestazioni tramite [Diagnostica di Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="c83e0-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
