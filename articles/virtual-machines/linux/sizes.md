---
title: dimensioni aaaLinux VM in Azure | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibili per le macchine virtuali Linux in Azure.
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
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="7bad3-103">Dimensioni delle macchine virtuali Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="7bad3-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="7bad3-104">In questo articolo descrive le dimensioni disponibili hello e le opzioni di hello macchine virtuali di Azure è possibile utilizzare toorun Linux App e i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7bad3-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="7bad3-105">Fornisce inoltre toobe considerazioni sulla distribuzione conoscere quando si pianifica toouse queste risorse.</span><span class="sxs-lookup"><span data-stu-id="7bad3-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="7bad3-106">Questo articolo è disponibile anche per le [macchine virtuali Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7bad3-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="7bad3-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="7bad3-107">Type</span></span>                     | <span data-ttu-id="7bad3-108">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="7bad3-108">Sizes</span></span>           |    <span data-ttu-id="7bad3-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7bad3-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="7bad3-110">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="7bad3-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="7bad3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="7bad3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="7bad3-112">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="7bad3-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="7bad3-113">Ideale per i test e sviluppo, i database di piccole dimensioni toomedium e toomedium bassa il traffico web server.</span><span class="sxs-lookup"><span data-stu-id="7bad3-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="7bad3-114">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="7bad3-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="7bad3-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="7bad3-115">Fs, F</span></span>             | <span data-ttu-id="7bad3-116">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="7bad3-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="7bad3-117">Soluzione idonea per server Web con livelli medi di traffico, dispositivi di rete, processi batch e server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7bad3-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="7bad3-118">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="7bad3-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="7bad3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="7bad3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="7bad3-120">Rapporto elevato tra memoria e CPU.</span><span class="sxs-lookup"><span data-stu-id="7bad3-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="7bad3-121">Ideale per i server di database relazionale, cache toolarge medium e analitica in memoria.</span><span class="sxs-lookup"><span data-stu-id="7bad3-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="7bad3-122">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="7bad3-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="7bad3-123">Ls</span><span class="sxs-lookup"><span data-stu-id="7bad3-123">Ls</span></span>                | <span data-ttu-id="7bad3-124">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="7bad3-124">High disk throughput and IO.</span></span> <span data-ttu-id="7bad3-125">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="7bad3-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="7bad3-126">GPU</span><span class="sxs-lookup"><span data-stu-id="7bad3-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="7bad3-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="7bad3-127">NV, NC</span></span>            | <span data-ttu-id="7bad3-128">Macchine virtuali specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video,</span><span class="sxs-lookup"><span data-stu-id="7bad3-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="7bad3-129">disponibili con GPU singole o più GPU.</span><span class="sxs-lookup"><span data-stu-id="7bad3-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="7bad3-130">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="7bad3-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="7bad3-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="7bad3-131">H, A8-11</span></span>          | <span data-ttu-id="7bad3-132">Le nostre macchine virtuali con CPU più veloci e potenti, con interfacce di rete ad alta velocità effettiva facoltative (RDMA).</span><span class="sxs-lookup"><span data-stu-id="7bad3-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="7bad3-133">Per informazioni sui prezzi di hello diverse dimensioni, vedere [macchine virtuali: prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="7bad3-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="7bad3-134">Per la disponibilità delle dimensioni di VM nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="7bad3-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="7bad3-135">toosee limiti generali in macchine virtuali di Azure, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7bad3-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="7bad3-136">Altre informazioni su come le [unità di calcolo di Azure](../windows/acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad3-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="7bad3-137">API REST</span><span class="sxs-lookup"><span data-stu-id="7bad3-137">Rest API</span></span>

<span data-ttu-id="7bad3-138">Per informazioni sull'utilizzo di hello tooquery di API REST per dimensioni di macchina virtuale, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="7bad3-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- <span data-ttu-id="7bad3-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Elencare le dimensioni delle macchine virtuali disponibili per il ridimensionamento)</span><span class="sxs-lookup"><span data-stu-id="7bad3-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="7bad3-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Elencare le dimensioni delle macchine virtuali disponibili per una sottoscrizione)</span><span class="sxs-lookup"><span data-stu-id="7bad3-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="7bad3-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Elencare le dimensioni delle macchine virtuali disponibili in un set di disponibilità)</span><span class="sxs-lookup"><span data-stu-id="7bad3-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="7bad3-142">Unità di calcolo di Azure</span><span class="sxs-lookup"><span data-stu-id="7bad3-142">ACU</span></span>

<span data-ttu-id="7bad3-143">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bad3-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bad3-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bad3-144">Next steps</span></span>

<span data-ttu-id="7bad3-145">Altre informazioni sulle dimensioni della VM diverse hello disponibili:</span><span class="sxs-lookup"><span data-stu-id="7bad3-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="7bad3-146">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="7bad3-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="7bad3-147">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="7bad3-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="7bad3-148">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="7bad3-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="7bad3-149">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="7bad3-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="7bad3-150">GPU</span><span class="sxs-lookup"><span data-stu-id="7bad3-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="7bad3-151">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="7bad3-151">High performance compute</span></span>](sizes-hpc.md)



