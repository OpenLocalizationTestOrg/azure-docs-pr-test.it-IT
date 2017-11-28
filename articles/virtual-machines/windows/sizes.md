---
title: dimensioni aaaWindows VM in Azure | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibili per le macchine virtuali Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="c31dc-103">Dimensioni per le macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="c31dc-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="c31dc-104">In questo articolo descrive le dimensioni disponibili hello e le opzioni di hello macchine virtuali di Azure è possibile utilizzare toorun le app di Windows e i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c31dc-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="c31dc-105">Fornisce inoltre toobe considerazioni sulla distribuzione conoscere quando si pianifica toouse queste risorse.</span><span class="sxs-lookup"><span data-stu-id="c31dc-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="c31dc-106">Questo articolo è disponibile anche per le [macchine virtuali Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c31dc-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="c31dc-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="c31dc-107">Type</span></span>                     | <span data-ttu-id="c31dc-108">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="c31dc-108">Sizes</span></span>           |    <span data-ttu-id="c31dc-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c31dc-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="c31dc-110">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="c31dc-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="c31dc-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="c31dc-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="c31dc-112">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="c31dc-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="c31dc-113">Ideale per i test e sviluppo, i database di piccole dimensioni toomedium e toomedium bassa il traffico web server.</span><span class="sxs-lookup"><span data-stu-id="c31dc-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="c31dc-114">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="c31dc-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="c31dc-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="c31dc-115">Fs, F</span></span>             | <span data-ttu-id="c31dc-116">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="c31dc-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="c31dc-117">Soluzione idonea per server Web con livelli medi di traffico, dispositivi di rete, processi batch e server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c31dc-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="c31dc-118">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="c31dc-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="c31dc-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="c31dc-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="c31dc-120">Rapporto elevato tra memoria e CPU.</span><span class="sxs-lookup"><span data-stu-id="c31dc-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="c31dc-121">Ideale per i server di database relazionale, cache toolarge medium e analitica in memoria.</span><span class="sxs-lookup"><span data-stu-id="c31dc-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="c31dc-122">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="c31dc-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="c31dc-123">Ls</span><span class="sxs-lookup"><span data-stu-id="c31dc-123">Ls</span></span>                | <span data-ttu-id="c31dc-124">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="c31dc-124">High disk throughput and IO.</span></span> <span data-ttu-id="c31dc-125">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="c31dc-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="c31dc-126">GPU</span><span class="sxs-lookup"><span data-stu-id="c31dc-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="c31dc-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="c31dc-127">NV, NC</span></span>            | <span data-ttu-id="c31dc-128">Macchine virtuali specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video,</span><span class="sxs-lookup"><span data-stu-id="c31dc-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="c31dc-129">disponibili con GPU singole o più GPU.</span><span class="sxs-lookup"><span data-stu-id="c31dc-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="c31dc-130">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="c31dc-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="c31dc-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="c31dc-131">H, A8-11</span></span>          | <span data-ttu-id="c31dc-132">Le nostre macchine virtuali con CPU più veloci e potenti, con interfacce di rete ad alta velocità effettiva facoltative (RDMA).</span><span class="sxs-lookup"><span data-stu-id="c31dc-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="c31dc-133">Per informazioni sui prezzi di hello diverse dimensioni, vedere [macchine virtuali: prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="c31dc-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="c31dc-134">toosee limiti generali in macchine virtuali di Azure, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="c31dc-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="c31dc-135">I costi di archiviazione vengono calcolati separatamente in base alle pagine usate nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="c31dc-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="c31dc-136">Per informazioni dettagliate, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="c31dc-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="c31dc-137">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="c31dc-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="c31dc-138">API REST</span><span class="sxs-lookup"><span data-stu-id="c31dc-138">Rest API</span></span>

<span data-ttu-id="c31dc-139">Per informazioni sull'utilizzo di hello tooquery di API REST per dimensioni di macchina virtuale, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="c31dc-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- <span data-ttu-id="c31dc-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Elencare le dimensioni delle macchine virtuali disponibili per il ridimensionamento)</span><span class="sxs-lookup"><span data-stu-id="c31dc-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="c31dc-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Elencare le dimensioni delle macchine virtuali disponibili per una sottoscrizione)</span><span class="sxs-lookup"><span data-stu-id="c31dc-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="c31dc-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Elencare le dimensioni delle macchine virtuali disponibili in un set di disponibilità)</span><span class="sxs-lookup"><span data-stu-id="c31dc-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="c31dc-143">Unità di calcolo di Azure</span><span class="sxs-lookup"><span data-stu-id="c31dc-143">ACU</span></span>

<span data-ttu-id="c31dc-144">Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.</span><span class="sxs-lookup"><span data-stu-id="c31dc-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c31dc-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c31dc-145">Next steps</span></span>

<span data-ttu-id="c31dc-146">Altre informazioni sulle dimensioni della VM diverse hello disponibili:</span><span class="sxs-lookup"><span data-stu-id="c31dc-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="c31dc-147">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="c31dc-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="c31dc-148">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="c31dc-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="c31dc-149">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="c31dc-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="c31dc-150">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="c31dc-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="c31dc-151">Ottimizzate per la GPU</span><span class="sxs-lookup"><span data-stu-id="c31dc-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="c31dc-152">High Performance Computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="c31dc-152">High performance compute</span></span>](sizes-hpc.md)



