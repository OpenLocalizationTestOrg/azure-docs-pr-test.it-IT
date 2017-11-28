---
title: Gestire i dischi di Azure con Azure PowerShell | Microsoft Docs
description: 'Esercitazione: gestire i dischi di Azure con Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="237f8-103">Gestire i dischi di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="237f8-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="237f8-104">Le macchine virtuali di Azure usano dischi per archiviare sistema operativo, applicazioni e dati di VM.</span><span class="sxs-lookup"><span data-stu-id="237f8-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="237f8-105">Quando si crea una VM, è importante scegliere dimensione del disco e configurazione appropriate per il carico di lavoro previsto.</span><span class="sxs-lookup"><span data-stu-id="237f8-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="237f8-106">Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM.</span><span class="sxs-lookup"><span data-stu-id="237f8-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="237f8-107">Vengono fornite informazioni su:</span><span class="sxs-lookup"><span data-stu-id="237f8-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="237f8-108">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="237f8-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="237f8-109">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="237f8-109">Data disks</span></span>
> * <span data-ttu-id="237f8-110">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="237f8-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="237f8-111">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="237f8-111">Disk performance</span></span>
> * <span data-ttu-id="237f8-112">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="237f8-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="237f8-113">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="237f8-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="237f8-114">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="237f8-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="237f8-115">Se è necessario eseguire l'aggiornamento, vedere [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps) (Installare il modulo di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="237f8-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="237f8-116">Dischi di Azure predefiniti</span><span class="sxs-lookup"><span data-stu-id="237f8-116">Default Azure disks</span></span>

<span data-ttu-id="237f8-117">Quando viene creata una macchina virtuale di Azure, due dischi vengono automaticamente collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="237f8-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="237f8-118">**Disco del sistema operativo**: i dischi del sistema operativo possono essere ridimensionati fino a 1 terabyte e ospitano il sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="237f8-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="237f8-119">Al disco del sistema operativo viene assegnata una lettera di unità *c:* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="237f8-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="237f8-120">La configurazione della memorizzazione nella cache del disco del sistema operativo è ottimizzata per le prestazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="237f8-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="237f8-121">Il disco del sistema operativo **non deve** ospitare applicazioni o dati.</span><span class="sxs-lookup"><span data-stu-id="237f8-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="237f8-122">Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="237f8-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="237f8-123">**Disco temporaneo**: i dischi temporanei usano un'unità SSD che si trova nello stesso host della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="237f8-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="237f8-124">I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="237f8-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="237f8-125">Tuttavia, se la macchina virtuale viene spostata in un nuovo host, tutti i dati memorizzati su un disco temporaneo vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="237f8-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="237f8-126">Le dimensioni del disco temporaneo sono determinate dalle dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="237f8-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="237f8-127">Ai dischi temporanei viene assegnata una lettera di unità *d:* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="237f8-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="237f8-128">Dimensioni del disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="237f8-128">Temporary disk sizes</span></span>

| <span data-ttu-id="237f8-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="237f8-129">Type</span></span> | <span data-ttu-id="237f8-130">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="237f8-130">VM Size</span></span> | <span data-ttu-id="237f8-131">Dimensioni massime del disco temporaneo (GB)</span><span class="sxs-lookup"><span data-stu-id="237f8-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="237f8-132">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="237f8-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="237f8-133">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="237f8-133">A and D series</span></span> | <span data-ttu-id="237f8-134">800</span><span class="sxs-lookup"><span data-stu-id="237f8-134">800</span></span> |
| [<span data-ttu-id="237f8-135">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="237f8-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="237f8-136">Serie F</span><span class="sxs-lookup"><span data-stu-id="237f8-136">F series</span></span> | <span data-ttu-id="237f8-137">800</span><span class="sxs-lookup"><span data-stu-id="237f8-137">800</span></span> |
| [<span data-ttu-id="237f8-138">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="237f8-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="237f8-139">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="237f8-139">D and G series</span></span> | <span data-ttu-id="237f8-140">6144</span><span class="sxs-lookup"><span data-stu-id="237f8-140">6144</span></span> |
| [<span data-ttu-id="237f8-141">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="237f8-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="237f8-142">Serie L</span><span class="sxs-lookup"><span data-stu-id="237f8-142">L series</span></span> | <span data-ttu-id="237f8-143">5630</span><span class="sxs-lookup"><span data-stu-id="237f8-143">5630</span></span> |
| [<span data-ttu-id="237f8-144">GPU</span><span class="sxs-lookup"><span data-stu-id="237f8-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="237f8-145">Serie N</span><span class="sxs-lookup"><span data-stu-id="237f8-145">N series</span></span> | <span data-ttu-id="237f8-146">1.440</span><span class="sxs-lookup"><span data-stu-id="237f8-146">1440</span></span> |
| [<span data-ttu-id="237f8-147">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="237f8-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="237f8-148">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="237f8-148">A and H series</span></span> | <span data-ttu-id="237f8-149">2000</span><span class="sxs-lookup"><span data-stu-id="237f8-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="237f8-150">Dischi dati di Azure</span><span class="sxs-lookup"><span data-stu-id="237f8-150">Azure data disks</span></span>

<span data-ttu-id="237f8-151">È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="237f8-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="237f8-152">I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva.</span><span class="sxs-lookup"><span data-stu-id="237f8-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="237f8-153">Ciascun disco dati ha una capacità massima di 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="237f8-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="237f8-154">Le dimensione della macchina virtuale determinano il numero di dischi dati possono essere collegati a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="237f8-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="237f8-155">Per ogni core della macchina virtuale, è possibile collegare due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="237f8-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="237f8-156">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="237f8-156">Max data disks per VM</span></span>

| <span data-ttu-id="237f8-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="237f8-157">Type</span></span> | <span data-ttu-id="237f8-158">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="237f8-158">VM Size</span></span> | <span data-ttu-id="237f8-159">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="237f8-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="237f8-160">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="237f8-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="237f8-161">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="237f8-161">A and D series</span></span> | <span data-ttu-id="237f8-162">32</span><span class="sxs-lookup"><span data-stu-id="237f8-162">32</span></span> |
| [<span data-ttu-id="237f8-163">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="237f8-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="237f8-164">Serie F</span><span class="sxs-lookup"><span data-stu-id="237f8-164">F series</span></span> | <span data-ttu-id="237f8-165">32</span><span class="sxs-lookup"><span data-stu-id="237f8-165">32</span></span> |
| [<span data-ttu-id="237f8-166">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="237f8-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="237f8-167">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="237f8-167">D and G series</span></span> | <span data-ttu-id="237f8-168">64</span><span class="sxs-lookup"><span data-stu-id="237f8-168">64</span></span> |
| [<span data-ttu-id="237f8-169">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="237f8-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="237f8-170">Serie L</span><span class="sxs-lookup"><span data-stu-id="237f8-170">L series</span></span> | <span data-ttu-id="237f8-171">64</span><span class="sxs-lookup"><span data-stu-id="237f8-171">64</span></span> |
| [<span data-ttu-id="237f8-172">GPU</span><span class="sxs-lookup"><span data-stu-id="237f8-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="237f8-173">Serie N</span><span class="sxs-lookup"><span data-stu-id="237f8-173">N series</span></span> | <span data-ttu-id="237f8-174">48</span><span class="sxs-lookup"><span data-stu-id="237f8-174">48</span></span> |
| [<span data-ttu-id="237f8-175">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="237f8-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="237f8-176">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="237f8-176">A and H series</span></span> | <span data-ttu-id="237f8-177">32</span><span class="sxs-lookup"><span data-stu-id="237f8-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="237f8-178">Tipi di dischi per la VM</span><span class="sxs-lookup"><span data-stu-id="237f8-178">VM disk types</span></span>

<span data-ttu-id="237f8-179">Azure offre due tipi di dischi.</span><span class="sxs-lookup"><span data-stu-id="237f8-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="237f8-180">Disco standard</span><span class="sxs-lookup"><span data-stu-id="237f8-180">Standard disk</span></span>

<span data-ttu-id="237f8-181">Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni.</span><span class="sxs-lookup"><span data-stu-id="237f8-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="237f8-182">I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.</span><span class="sxs-lookup"><span data-stu-id="237f8-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="237f8-183">Disco premium</span><span class="sxs-lookup"><span data-stu-id="237f8-183">Premium disk</span></span>

<span data-ttu-id="237f8-184">I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD.</span><span class="sxs-lookup"><span data-stu-id="237f8-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="237f8-185">Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione.</span><span class="sxs-lookup"><span data-stu-id="237f8-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="237f8-186">L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="237f8-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="237f8-187">I dischi premium sono di tre tipi, P10, P20 e P30. Le dimensioni del disco determinano il tipo di disco.</span><span class="sxs-lookup"><span data-stu-id="237f8-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="237f8-188">Quando si effettua la selezione, il valore delle dimensioni di un disco viene arrotondato per eccesso al tipo successivo.</span><span class="sxs-lookup"><span data-stu-id="237f8-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="237f8-189">Ad esempio, se la dimensione è inferiore a 128 GB il tipo di disco sarà P10, se è tra 129 e 512 GB sarà P20 e oltre 512 GB sarà P30.</span><span class="sxs-lookup"><span data-stu-id="237f8-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="237f8-190">Prestazioni disco premium</span><span class="sxs-lookup"><span data-stu-id="237f8-190">Premium disk performance</span></span>

|<span data-ttu-id="237f8-191">Tipo di disco di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="237f8-191">Premium storage disk type</span></span> | <span data-ttu-id="237f8-192">P10</span><span class="sxs-lookup"><span data-stu-id="237f8-192">P10</span></span> | <span data-ttu-id="237f8-193">P20</span><span class="sxs-lookup"><span data-stu-id="237f8-193">P20</span></span> | <span data-ttu-id="237f8-194">P30</span><span class="sxs-lookup"><span data-stu-id="237f8-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="237f8-195">Dimensioni del disco (arrotondate)</span><span class="sxs-lookup"><span data-stu-id="237f8-195">Disk size (round up)</span></span> | <span data-ttu-id="237f8-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="237f8-196">128 GB</span></span> | <span data-ttu-id="237f8-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="237f8-197">512 GB</span></span> | <span data-ttu-id="237f8-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="237f8-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="237f8-199">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="237f8-199">IOPS per disk</span></span> | <span data-ttu-id="237f8-200">500</span><span class="sxs-lookup"><span data-stu-id="237f8-200">500</span></span> | <span data-ttu-id="237f8-201">2.300</span><span class="sxs-lookup"><span data-stu-id="237f8-201">2,300</span></span> | <span data-ttu-id="237f8-202">5.000</span><span class="sxs-lookup"><span data-stu-id="237f8-202">5,000</span></span> |
<span data-ttu-id="237f8-203">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="237f8-203">Throughput per disk</span></span> | <span data-ttu-id="237f8-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="237f8-204">100 MB/s</span></span> | <span data-ttu-id="237f8-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="237f8-205">150 MB/s</span></span> | <span data-ttu-id="237f8-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="237f8-206">200 MB/s</span></span> |

<span data-ttu-id="237f8-207">Sebbene la tabella sopra riportata identifichi il numero massimo di operazioni di I/O al secondo per disco, è possibile raggiungere un livello superiore di prestazioni tramite lo striping di più dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="237f8-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="237f8-208">Ad esempio, è possibile collegare 64 dati dischi alla macchina virtuale Standard_GS5.</span><span class="sxs-lookup"><span data-stu-id="237f8-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="237f8-209">Se ognuno di questi dischi viene ridimensionato come un P30, è possibile ottenere un massimo di 80.000 operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="237f8-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="237f8-210">Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="237f8-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="237f8-211">Creare e collegare dischi</span><span class="sxs-lookup"><span data-stu-id="237f8-211">Create and attach disks</span></span>

<span data-ttu-id="237f8-212">Per completare l'esempio contenuto in questa esercitazione è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="237f8-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="237f8-213">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="237f8-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="237f8-214">Quando si esegue l'esercitazione, sostituire i nomi del gruppo di risorse e delle macchine virtuali dove necessario.</span><span class="sxs-lookup"><span data-stu-id="237f8-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="237f8-215">Creare la configurazione iniziale con [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="237f8-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="237f8-216">L'esempio seguente configura un disco delle dimensioni di 128 GB.</span><span class="sxs-lookup"><span data-stu-id="237f8-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="237f8-217">Creare il disco dati con il comando [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="237f8-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="237f8-218">Ottenere la macchina virtuale a cui si vuole aggiungere il disco dati con il comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="237f8-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="237f8-219">Aggiungere il disco dati alla configurazione della macchina virtuale con il comando [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="237f8-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="237f8-220">Aggiornare la macchina virtuale con il comando [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="237f8-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="237f8-221">Preparare i dischi di dati</span><span class="sxs-lookup"><span data-stu-id="237f8-221">Prepare data disks</span></span>

<span data-ttu-id="237f8-222">Dopo aver collegato un disco alla macchina virtuale, il sistema operativo deve essere configurato per l'uso del disco.</span><span class="sxs-lookup"><span data-stu-id="237f8-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="237f8-223">Nell'esempio seguente viene illustrato come configurare manualmente il primo disco aggiunto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="237f8-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="237f8-224">Questo processo può essere automatizzato tramite l'[estensione dello script personalizzata](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="237f8-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="237f8-225">Configurazione manuale</span><span class="sxs-lookup"><span data-stu-id="237f8-225">Manual configuration</span></span>

<span data-ttu-id="237f8-226">Creare una connessione RDP alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="237f8-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="237f8-227">Aprire PowerShell ed eseguire questo script.</span><span class="sxs-lookup"><span data-stu-id="237f8-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="237f8-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="237f8-228">Next steps</span></span>

<span data-ttu-id="237f8-229">In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="237f8-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="237f8-230">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="237f8-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="237f8-231">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="237f8-231">Data disks</span></span>
> * <span data-ttu-id="237f8-232">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="237f8-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="237f8-233">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="237f8-233">Disk performance</span></span>
> * <span data-ttu-id="237f8-234">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="237f8-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="237f8-235">Passare all'esercitazione successiva per informazioni sull'automazione della configurazione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="237f8-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="237f8-236">Automatizzare la configurazione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="237f8-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
