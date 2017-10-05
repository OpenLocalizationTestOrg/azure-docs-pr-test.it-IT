---
title: Monitoraggio delle prestazioni di Azure Service Fabric | Microsoft Docs
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="c1973-103">Metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c1973-103">Performance metrics</span></span>

<span data-ttu-id="c1973-104">Per comprendere le prestazioni del cluster e delle applicazioni in esecuzione al suo interno è necessario raccogliere alcune metriche.</span><span class="sxs-lookup"><span data-stu-id="c1973-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="c1973-105">Per i cluster di Service Fabric è consigliabile raccogliere i contatori delle prestazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="c1973-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="c1973-106">Nodi</span><span class="sxs-lookup"><span data-stu-id="c1973-106">Nodes</span></span>

<span data-ttu-id="c1973-107">Per i computer presenti nel cluster è opportuno raccogliere i contatori delle prestazioni seguenti per comprendere meglio il carico di ogni computer e prendere decisioni appropriate sulla scalabilità del cluster.</span><span class="sxs-lookup"><span data-stu-id="c1973-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="c1973-108">Categoria contatore</span><span class="sxs-lookup"><span data-stu-id="c1973-108">Counter Category</span></span> | <span data-ttu-id="c1973-109">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="c1973-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c1973-110">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-111">Avg.</span><span class="sxs-lookup"><span data-stu-id="c1973-111">Avg.</span></span> <span data-ttu-id="c1973-112">Disk Read Queue Length</span><span class="sxs-lookup"><span data-stu-id="c1973-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="c1973-113">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-114">Avg.</span><span class="sxs-lookup"><span data-stu-id="c1973-114">Avg.</span></span> <span data-ttu-id="c1973-115">Disk Write Queue Length</span><span class="sxs-lookup"><span data-stu-id="c1973-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="c1973-116">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-117">Avg.</span><span class="sxs-lookup"><span data-stu-id="c1973-117">Avg.</span></span> <span data-ttu-id="c1973-118">Disk sec/Read</span><span class="sxs-lookup"><span data-stu-id="c1973-118">Disk sec/Read</span></span> |
| <span data-ttu-id="c1973-119">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-120">Avg.</span><span class="sxs-lookup"><span data-stu-id="c1973-120">Avg.</span></span> <span data-ttu-id="c1973-121">Disk sec/Write</span><span class="sxs-lookup"><span data-stu-id="c1973-121">Disk sec/Write</span></span> |
| <span data-ttu-id="c1973-122">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-123">Letture disco/sec </span><span class="sxs-lookup"><span data-stu-id="c1973-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="c1973-124">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-125">Byte letti da disco/sec </span><span class="sxs-lookup"><span data-stu-id="c1973-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="c1973-126">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-127">Scritture disco/sec</span><span class="sxs-lookup"><span data-stu-id="c1973-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="c1973-128">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="c1973-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="c1973-129">Byte scritti su disco/sec</span><span class="sxs-lookup"><span data-stu-id="c1973-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="c1973-130">Memoria</span><span class="sxs-lookup"><span data-stu-id="c1973-130">Memory</span></span> | <span data-ttu-id="c1973-131">MByte disponibili</span><span class="sxs-lookup"><span data-stu-id="c1973-131">Available MBytes</span></span> |
| <span data-ttu-id="c1973-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="c1973-132">PagingFile</span></span> | <span data-ttu-id="c1973-133">% Usage</span><span class="sxs-lookup"><span data-stu-id="c1973-133">% Usage</span></span> |
| <span data-ttu-id="c1973-134">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="c1973-134">Process(Total)</span></span> | <span data-ttu-id="c1973-135">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="c1973-135">% Processor Time</span></span> |
| <span data-ttu-id="c1973-136">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-136">Process (per service)</span></span> | <span data-ttu-id="c1973-137">% di tempo processore</span><span class="sxs-lookup"><span data-stu-id="c1973-137">% Processor Time</span></span> |
| <span data-ttu-id="c1973-138">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-138">Process (per service)</span></span> | <span data-ttu-id="c1973-139">ID Process</span><span class="sxs-lookup"><span data-stu-id="c1973-139">ID Process</span></span> |
| <span data-ttu-id="c1973-140">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-140">Process (per service)</span></span> | <span data-ttu-id="c1973-141">Private Bytes</span><span class="sxs-lookup"><span data-stu-id="c1973-141">Private Bytes</span></span> |
| <span data-ttu-id="c1973-142">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-142">Process (per service)</span></span> | <span data-ttu-id="c1973-143">Thread Count</span><span class="sxs-lookup"><span data-stu-id="c1973-143">Thread Count</span></span> |
| <span data-ttu-id="c1973-144">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-144">Process (per service)</span></span> | <span data-ttu-id="c1973-145">Virtual Bytes</span><span class="sxs-lookup"><span data-stu-id="c1973-145">Virtual Bytes</span></span> |
| <span data-ttu-id="c1973-146">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-146">Process (per service)</span></span> | <span data-ttu-id="c1973-147">Working Set</span><span class="sxs-lookup"><span data-stu-id="c1973-147">Working Set</span></span> |
| <span data-ttu-id="c1973-148">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-148">Process (per service)</span></span> | <span data-ttu-id="c1973-149">Working Set - Private</span><span class="sxs-lookup"><span data-stu-id="c1973-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="c1973-150">Applicazioni e servizi .NET</span><span class="sxs-lookup"><span data-stu-id="c1973-150">.NET applications and services</span></span>

<span data-ttu-id="c1973-151">Se si distribuiscono servizi .NET nel cluster, raccogliere i contatori seguenti.</span><span class="sxs-lookup"><span data-stu-id="c1973-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="c1973-152">Categoria contatore</span><span class="sxs-lookup"><span data-stu-id="c1973-152">Counter Category</span></span> | <span data-ttu-id="c1973-153">Nome contatore</span><span class="sxs-lookup"><span data-stu-id="c1973-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="c1973-154">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-155">ID di processo</span><span class="sxs-lookup"><span data-stu-id="c1973-155">Process ID</span></span> |
| <span data-ttu-id="c1973-156">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-157"># Total committed Bytes</span><span class="sxs-lookup"><span data-stu-id="c1973-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="c1973-158">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-159"># Total reserved Bytes</span><span class="sxs-lookup"><span data-stu-id="c1973-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="c1973-160">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-161"># Bytes in all Heaps</span><span class="sxs-lookup"><span data-stu-id="c1973-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="c1973-162">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-163"># Gen 0 Collections</span><span class="sxs-lookup"><span data-stu-id="c1973-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="c1973-164">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-165"># Gen 1 Collections</span><span class="sxs-lookup"><span data-stu-id="c1973-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="c1973-166">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-167"># Gen 2 Collections</span><span class="sxs-lookup"><span data-stu-id="c1973-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="c1973-168">.NET CLR Memory (per service)</span><span class="sxs-lookup"><span data-stu-id="c1973-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="c1973-169">Percentuale tempo in GC</span><span class="sxs-lookup"><span data-stu-id="c1973-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="c1973-170">Contatori delle prestazioni personalizzati di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c1973-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="c1973-171">Service Fabric genera una quantità significativa di contatori delle prestazioni personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c1973-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="c1973-172">Se è installato l'SDK, è possibile visualizzare l'elenco completo disponibile nel computer Windows mediante l'applicazione Performance Monitor (Start > Performance Monitor).</span><span class="sxs-lookup"><span data-stu-id="c1973-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="c1973-173">Se si usa Reliable Actors, nelle applicazioni che si sta distribuendo nel cluster aggiungere i contatori delle categorie `Service Fabric Actor` e `Service Fabric Actor Method` (vedere [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="c1973-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="c1973-174">Analogamente, se si usa Reliable Services, è necessario raccogliere i contatori delle categorie `Service Fabric Service` e `Service Fabric Service Method`.</span><span class="sxs-lookup"><span data-stu-id="c1973-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="c1973-175">Se si usa Reliable Collection, infine, è consigliabile aggiungere il contatore `Avg. Transaction ms/Commit` della categoria `Service Fabric Transactional Replicator` per raccogliere la latenza di commit media per ogni transazione.</span><span class="sxs-lookup"><span data-stu-id="c1973-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c1973-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1973-176">Next steps</span></span>

* <span data-ttu-id="c1973-177">Altre informazioni sulla [generazione di eventi a livello piattaforma](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c1973-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="c1973-178">Raccogliere metriche delle prestazioni tramite [Diagnostica di Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="c1973-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
