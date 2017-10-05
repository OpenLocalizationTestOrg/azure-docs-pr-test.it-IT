---
title: Dimensioni delle macchine virtuali Linux | Documentazione Microsoft
description: Elenca le diverse dimensioni disponibili per le macchine virtuali Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: fe7a92901ae25aa99ef71f09c416e6c6ad30d39b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="dc921-103">Dimensioni delle macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="dc921-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="dc921-104">Questo articolo descrive le dimensioni e le opzioni disponibili per le macchine virtuali di Azure che è possibile usare per eseguire le app Linux e i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dc921-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="dc921-105">Offre anche considerazioni sulla distribuzione da tenere presenti quando si prevede di usare queste risorse.</span><span class="sxs-lookup"><span data-stu-id="dc921-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="dc921-106">Questo articolo è disponibile anche per le [macchine virtuali Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc921-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="dc921-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="dc921-107">Type</span></span>                     | <span data-ttu-id="dc921-108">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="dc921-108">Sizes</span></span>           |    <span data-ttu-id="dc921-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dc921-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="dc921-110">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="dc921-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="dc921-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="dc921-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="dc921-112">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="dc921-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="dc921-113">Soluzione ideale per test e sviluppo, database medio-piccoli e server Web con traffico da medio a ridotto.</span><span class="sxs-lookup"><span data-stu-id="dc921-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="dc921-114">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="dc921-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="dc921-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="dc921-115">Fs, F</span></span>             | <span data-ttu-id="dc921-116">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="dc921-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="dc921-117">Soluzione idonea per server Web con livelli medi di traffico, dispositivi di rete, processi batch e server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="dc921-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="dc921-118">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="dc921-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="dc921-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="dc921-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="dc921-120">Rapporto elevato tra memoria e CPU.</span><span class="sxs-lookup"><span data-stu-id="dc921-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="dc921-121">Soluzione ideale per server di database relazionali, cache medio-grandi e analisi in memoria.</span><span class="sxs-lookup"><span data-stu-id="dc921-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="dc921-122">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="dc921-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="dc921-123">Ls</span><span class="sxs-lookup"><span data-stu-id="dc921-123">Ls</span></span>                | <span data-ttu-id="dc921-124">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="dc921-124">High disk throughput and IO.</span></span> <span data-ttu-id="dc921-125">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="dc921-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="dc921-126">GPU</span><span class="sxs-lookup"><span data-stu-id="dc921-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="dc921-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="dc921-127">NV, NC</span></span>            | <span data-ttu-id="dc921-128">Macchine virtuali specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video,</span><span class="sxs-lookup"><span data-stu-id="dc921-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="dc921-129">disponibili con GPU singole o più GPU.</span><span class="sxs-lookup"><span data-stu-id="dc921-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="dc921-130">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="dc921-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="dc921-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="dc921-131">H, A8-11</span></span>          | <span data-ttu-id="dc921-132">Le nostre macchine virtuali con CPU più veloci e potenti, con interfacce di rete ad alta velocità effettiva facoltative (RDMA).</span><span class="sxs-lookup"><span data-stu-id="dc921-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="dc921-133">Per informazioni sui prezzi di varie dimensioni, vedere [Prezzi di Macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="dc921-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="dc921-134">Per la disponibilità delle dimensioni di VM nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="dc921-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="dc921-135">Per trovare i limiti generali delle VM di Azure, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="dc921-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="dc921-136">Altre informazioni su come le [unità di calcolo di Azure](../windows/acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc921-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="dc921-137">API REST</span><span class="sxs-lookup"><span data-stu-id="dc921-137">Rest API</span></span>

<span data-ttu-id="dc921-138">Per informazioni sull'uso dell'API REST per query relative alle dimensioni delle macchine virtuali, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc921-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- <span data-ttu-id="dc921-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Elencare le dimensioni delle macchine virtuali disponibili per il ridimensionamento)</span><span class="sxs-lookup"><span data-stu-id="dc921-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="dc921-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Elencare le dimensioni delle macchine virtuali disponibili per una sottoscrizione)</span><span class="sxs-lookup"><span data-stu-id="dc921-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="dc921-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Elencare le dimensioni delle macchine virtuali disponibili in un set di disponibilità)</span><span class="sxs-lookup"><span data-stu-id="dc921-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="dc921-142">Unità di calcolo di Azure</span><span class="sxs-lookup"><span data-stu-id="dc921-142">ACU</span></span>

<span data-ttu-id="dc921-143">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc921-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc921-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc921-144">Next steps</span></span>

<span data-ttu-id="dc921-145">Altre informazioni sulle diverse dimensioni di macchina virtuale disponibili:</span><span class="sxs-lookup"><span data-stu-id="dc921-145">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="dc921-146">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="dc921-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="dc921-147">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="dc921-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="dc921-148">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="dc921-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="dc921-149">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="dc921-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="dc921-150">GPU</span><span class="sxs-lookup"><span data-stu-id="dc921-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="dc921-151">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="dc921-151">High performance compute</span></span>](sizes-hpc.md)



