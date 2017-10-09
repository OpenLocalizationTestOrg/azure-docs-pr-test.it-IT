---
title: dischi aaaManage Azure con Azure PowerShell hello | Documenti Microsoft
description: 'Esercitazione: gestire i dischi di Azure con hello Azure PowerShell'
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="6e398-103">Gestire i dischi di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e398-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="6e398-104">Macchine virtuali di Azure utilizzano il sistema operativo macchine virtuali di dischi toostore hello, applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="6e398-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="6e398-105">Quando si crea una macchina virtuale è importante toochoose una dimensione del disco e il carico di lavoro di configurazione appropriato toohello previsto.</span><span class="sxs-lookup"><span data-stu-id="6e398-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="6e398-106">Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM.</span><span class="sxs-lookup"><span data-stu-id="6e398-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="6e398-107">Vengono fornite informazioni su:</span><span class="sxs-lookup"><span data-stu-id="6e398-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e398-108">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="6e398-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6e398-109">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="6e398-109">Data disks</span></span>
> * <span data-ttu-id="6e398-110">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="6e398-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="6e398-111">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="6e398-111">Disk performance</span></span>
> * <span data-ttu-id="6e398-112">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="6e398-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="6e398-113">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="6e398-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6e398-114">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6e398-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="6e398-115">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6e398-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="6e398-116">Dischi di Azure predefiniti</span><span class="sxs-lookup"><span data-stu-id="6e398-116">Default Azure disks</span></span>

<span data-ttu-id="6e398-117">Quando viene creata una macchina virtuale di Azure, due dischi sono macchina virtuale toohello automaticamente collegato.</span><span class="sxs-lookup"><span data-stu-id="6e398-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="6e398-118">**Disco del sistema operativo** : i dischi del sistema operativo possono essere dimensionati backup too1 terabyte e host hello del sistema operativo di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6e398-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="6e398-119">disco del sistema operativo Hello è assegnata una lettera di unità di *c:* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e398-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="6e398-120">disco Hello la memorizzazione nella cache di configurazione del disco del sistema operativo hello è ottimizzato per le prestazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6e398-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="6e398-121">disco del sistema operativo Hello **non** ospitare applicazioni o i dati.</span><span class="sxs-lookup"><span data-stu-id="6e398-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="6e398-122">Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6e398-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="6e398-123">**Disco temporaneo** -i dischi temporanei utilizzano un'unità SSD che si trova in hello stesso host hello VM Azure.</span><span class="sxs-lookup"><span data-stu-id="6e398-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="6e398-124">I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="6e398-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="6e398-125">Tuttavia, se hello macchina virtuale viene spostata tooa nuovo host, i dati archiviati in un disco temporaneo viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="6e398-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="6e398-126">dimensione di Hello del disco temporaneo hello è determinata dalla hello dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e398-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="6e398-127">Ai dischi temporanei viene assegnata una lettera di unità *d:* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e398-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="6e398-128">Dimensioni del disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="6e398-128">Temporary disk sizes</span></span>

| <span data-ttu-id="6e398-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="6e398-129">Type</span></span> | <span data-ttu-id="6e398-130">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6e398-130">VM Size</span></span> | <span data-ttu-id="6e398-131">Dimensioni massime del disco temporaneo (GB)</span><span class="sxs-lookup"><span data-stu-id="6e398-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="6e398-132">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="6e398-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6e398-133">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="6e398-133">A and D series</span></span> | <span data-ttu-id="6e398-134">800</span><span class="sxs-lookup"><span data-stu-id="6e398-134">800</span></span> |
| [<span data-ttu-id="6e398-135">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="6e398-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6e398-136">Serie F</span><span class="sxs-lookup"><span data-stu-id="6e398-136">F series</span></span> | <span data-ttu-id="6e398-137">800</span><span class="sxs-lookup"><span data-stu-id="6e398-137">800</span></span> |
| [<span data-ttu-id="6e398-138">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="6e398-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6e398-139">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="6e398-139">D and G series</span></span> | <span data-ttu-id="6e398-140">6144</span><span class="sxs-lookup"><span data-stu-id="6e398-140">6144</span></span> |
| [<span data-ttu-id="6e398-141">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="6e398-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6e398-142">Serie L</span><span class="sxs-lookup"><span data-stu-id="6e398-142">L series</span></span> | <span data-ttu-id="6e398-143">5630</span><span class="sxs-lookup"><span data-stu-id="6e398-143">5630</span></span> |
| [<span data-ttu-id="6e398-144">GPU</span><span class="sxs-lookup"><span data-stu-id="6e398-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6e398-145">Serie N</span><span class="sxs-lookup"><span data-stu-id="6e398-145">N series</span></span> | <span data-ttu-id="6e398-146">1.440</span><span class="sxs-lookup"><span data-stu-id="6e398-146">1440</span></span> |
| [<span data-ttu-id="6e398-147">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="6e398-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6e398-148">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="6e398-148">A and H series</span></span> | <span data-ttu-id="6e398-149">2000</span><span class="sxs-lookup"><span data-stu-id="6e398-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="6e398-150">Dischi dati di Azure</span><span class="sxs-lookup"><span data-stu-id="6e398-150">Azure data disks</span></span>

<span data-ttu-id="6e398-151">È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="6e398-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="6e398-152">I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva.</span><span class="sxs-lookup"><span data-stu-id="6e398-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="6e398-153">Ciascun disco dati ha una capacità massima di 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="6e398-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="6e398-154">dimensioni Hello della macchina virtuale hello determinano il numero di dischi dati può essere collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e398-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="6e398-155">Per ogni core della macchina virtuale, è possibile collegare due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="6e398-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="6e398-156">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6e398-156">Max data disks per VM</span></span>

| <span data-ttu-id="6e398-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="6e398-157">Type</span></span> | <span data-ttu-id="6e398-158">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6e398-158">VM Size</span></span> | <span data-ttu-id="6e398-159">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6e398-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="6e398-160">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="6e398-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6e398-161">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="6e398-161">A and D series</span></span> | <span data-ttu-id="6e398-162">32</span><span class="sxs-lookup"><span data-stu-id="6e398-162">32</span></span> |
| [<span data-ttu-id="6e398-163">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="6e398-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6e398-164">Serie F</span><span class="sxs-lookup"><span data-stu-id="6e398-164">F series</span></span> | <span data-ttu-id="6e398-165">32</span><span class="sxs-lookup"><span data-stu-id="6e398-165">32</span></span> |
| [<span data-ttu-id="6e398-166">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="6e398-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6e398-167">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="6e398-167">D and G series</span></span> | <span data-ttu-id="6e398-168">64</span><span class="sxs-lookup"><span data-stu-id="6e398-168">64</span></span> |
| [<span data-ttu-id="6e398-169">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="6e398-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6e398-170">Serie L</span><span class="sxs-lookup"><span data-stu-id="6e398-170">L series</span></span> | <span data-ttu-id="6e398-171">64</span><span class="sxs-lookup"><span data-stu-id="6e398-171">64</span></span> |
| [<span data-ttu-id="6e398-172">GPU</span><span class="sxs-lookup"><span data-stu-id="6e398-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6e398-173">Serie N</span><span class="sxs-lookup"><span data-stu-id="6e398-173">N series</span></span> | <span data-ttu-id="6e398-174">48</span><span class="sxs-lookup"><span data-stu-id="6e398-174">48</span></span> |
| [<span data-ttu-id="6e398-175">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="6e398-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6e398-176">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="6e398-176">A and H series</span></span> | <span data-ttu-id="6e398-177">32</span><span class="sxs-lookup"><span data-stu-id="6e398-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="6e398-178">Tipi di dischi per la VM</span><span class="sxs-lookup"><span data-stu-id="6e398-178">VM disk types</span></span>

<span data-ttu-id="6e398-179">Azure offre due tipi di dischi.</span><span class="sxs-lookup"><span data-stu-id="6e398-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="6e398-180">Disco standard</span><span class="sxs-lookup"><span data-stu-id="6e398-180">Standard disk</span></span>

<span data-ttu-id="6e398-181">Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni.</span><span class="sxs-lookup"><span data-stu-id="6e398-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="6e398-182">I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.</span><span class="sxs-lookup"><span data-stu-id="6e398-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="6e398-183">Disco premium</span><span class="sxs-lookup"><span data-stu-id="6e398-183">Premium disk</span></span>

<span data-ttu-id="6e398-184">I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD.</span><span class="sxs-lookup"><span data-stu-id="6e398-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="6e398-185">Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione.</span><span class="sxs-lookup"><span data-stu-id="6e398-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="6e398-186">L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="6e398-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="6e398-187">I dischi Premium sono disponibili in tre tipi (P10, P20, P30), dimensione hello del disco di hello determina il tipo di disco hello.</span><span class="sxs-lookup"><span data-stu-id="6e398-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="6e398-188">Quando si seleziona, un valore di hello dimensioni disco viene arrotondato per eccesso tipo successivo toohello.</span><span class="sxs-lookup"><span data-stu-id="6e398-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="6e398-189">Ad esempio, se dimensioni hello sono inferiore al tipo di disco hello 128 GB sarà P10, tra più di 512 P30 129 e 512 P20.</span><span class="sxs-lookup"><span data-stu-id="6e398-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="6e398-190">Prestazioni disco premium</span><span class="sxs-lookup"><span data-stu-id="6e398-190">Premium disk performance</span></span>

|<span data-ttu-id="6e398-191">Tipo di disco di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="6e398-191">Premium storage disk type</span></span> | <span data-ttu-id="6e398-192">P10</span><span class="sxs-lookup"><span data-stu-id="6e398-192">P10</span></span> | <span data-ttu-id="6e398-193">P20</span><span class="sxs-lookup"><span data-stu-id="6e398-193">P20</span></span> | <span data-ttu-id="6e398-194">P30</span><span class="sxs-lookup"><span data-stu-id="6e398-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6e398-195">Dimensioni del disco (arrotondate)</span><span class="sxs-lookup"><span data-stu-id="6e398-195">Disk size (round up)</span></span> | <span data-ttu-id="6e398-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="6e398-196">128 GB</span></span> | <span data-ttu-id="6e398-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="6e398-197">512 GB</span></span> | <span data-ttu-id="6e398-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="6e398-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="6e398-199">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="6e398-199">IOPS per disk</span></span> | <span data-ttu-id="6e398-200">500</span><span class="sxs-lookup"><span data-stu-id="6e398-200">500</span></span> | <span data-ttu-id="6e398-201">2.300</span><span class="sxs-lookup"><span data-stu-id="6e398-201">2,300</span></span> | <span data-ttu-id="6e398-202">5.000</span><span class="sxs-lookup"><span data-stu-id="6e398-202">5,000</span></span> |
<span data-ttu-id="6e398-203">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="6e398-203">Throughput per disk</span></span> | <span data-ttu-id="6e398-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="6e398-204">100 MB/s</span></span> | <span data-ttu-id="6e398-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="6e398-205">150 MB/s</span></span> | <span data-ttu-id="6e398-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="6e398-206">200 MB/s</span></span> |

<span data-ttu-id="6e398-207">Mentre hello sopra tabella identifica massimo di IOPS per disco, un livello di prestazioni superiore può essere ottenuto lo striping di più dischi dati.</span><span class="sxs-lookup"><span data-stu-id="6e398-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="6e398-208">Ad esempio, i dati di 64 dischi possono essere collegati tooStandard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="6e398-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="6e398-209">Se ognuno di questi dischi viene ridimensionato come un P30, è possibile ottenere un massimo di 80.000 operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="6e398-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="6e398-210">Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="6e398-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="6e398-211">Creare e collegare dischi</span><span class="sxs-lookup"><span data-stu-id="6e398-211">Create and attach disks</span></span>

<span data-ttu-id="6e398-212">esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="6e398-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="6e398-213">Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente.</span><span class="sxs-lookup"><span data-stu-id="6e398-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="6e398-214">Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.</span><span class="sxs-lookup"><span data-stu-id="6e398-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="6e398-215">Creare la configurazione iniziale di hello con [New AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="6e398-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="6e398-216">Hello di esempio seguente consente di configurare un disco, ovvero 128 gigabyte di spazio.</span><span class="sxs-lookup"><span data-stu-id="6e398-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="6e398-217">Creare il disco di dati hello con hello [New AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6e398-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="6e398-218">Macchina virtuale di hello Get che si desidera hello toowith di tooadd hello dati disco [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="6e398-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="6e398-219">Aggiungi hello dati disco toohello configurazione della macchina virtuale con hello [Aggiungi AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6e398-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="6e398-220">Aggiornare la macchina virtuale hello con hello [aggiornamento AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.</span><span class="sxs-lookup"><span data-stu-id="6e398-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="6e398-221">Preparare i dischi di dati</span><span class="sxs-lookup"><span data-stu-id="6e398-221">Prepare data disks</span></span>

<span data-ttu-id="6e398-222">Dopo aver macchina virtuale toohello collegato, un disco del sistema operativo hello deve toobe configurato toouse hello disco.</span><span class="sxs-lookup"><span data-stu-id="6e398-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="6e398-223">Hello esempio seguente viene illustrato come toomanually Configura primo disco hello aggiunto toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e398-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="6e398-224">È inoltre possibile automatizzare questo processo utilizzando hello [estensione script personalizzata](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6e398-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="6e398-225">Configurazione manuale</span><span class="sxs-lookup"><span data-stu-id="6e398-225">Manual configuration</span></span>

<span data-ttu-id="6e398-226">Creare una connessione RDP con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="6e398-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="6e398-227">Aprire PowerShell ed eseguire questo script.</span><span class="sxs-lookup"><span data-stu-id="6e398-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="6e398-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e398-228">Next steps</span></span>

<span data-ttu-id="6e398-229">In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6e398-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e398-230">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="6e398-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6e398-231">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="6e398-231">Data disks</span></span>
> * <span data-ttu-id="6e398-232">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="6e398-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="6e398-233">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="6e398-233">Disk performance</span></span>
> * <span data-ttu-id="6e398-234">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="6e398-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="6e398-235">Spostare toohello Avanti toolearn esercitazione sull'automazione di configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e398-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e398-236">Automatizzare la configurazione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="6e398-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
