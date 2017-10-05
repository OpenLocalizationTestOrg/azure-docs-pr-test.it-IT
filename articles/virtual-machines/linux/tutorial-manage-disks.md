---
title: Gestire i dischi di Azure con l'interfaccia della riga di comando di Azure | Microsoft Docs
description: 'Esercitazione: gestire i dischi di Azure con l''interfaccia della riga di comando di Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="14d10-103">Gestire i dischi di Azure con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="14d10-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="14d10-104">Le macchine virtuali di Azure usano dischi per archiviare sistema operativo, applicazioni e dati di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="14d10-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="14d10-105">Quando si crea una VM, è importante scegliere dimensione del disco e configurazione appropriate per il carico di lavoro previsto.</span><span class="sxs-lookup"><span data-stu-id="14d10-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="14d10-106">Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM.</span><span class="sxs-lookup"><span data-stu-id="14d10-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="14d10-107">Vengono fornite informazioni su:</span><span class="sxs-lookup"><span data-stu-id="14d10-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="14d10-108">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="14d10-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="14d10-109">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="14d10-109">Data disks</span></span>
> * <span data-ttu-id="14d10-110">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="14d10-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="14d10-111">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-111">Disk performance</span></span>
> * <span data-ttu-id="14d10-112">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="14d10-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="14d10-113">Ridimensionamento dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-113">Resizing disks</span></span>
> * <span data-ttu-id="14d10-114">Snapshot dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="14d10-115">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="14d10-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="14d10-116">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="14d10-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="14d10-117">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="14d10-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="14d10-118">Dischi di Azure predefiniti</span><span class="sxs-lookup"><span data-stu-id="14d10-118">Default Azure disks</span></span>

<span data-ttu-id="14d10-119">Quando viene creata una macchina virtuale di Azure, due dischi vengono automaticamente collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="14d10-120">**Disco del sistema operativo**: i dischi del sistema operativo possono essere ridimensionati fino a 1 terabyte e ospitano il sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="14d10-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="14d10-121">Il disco del sistema operativo viene etichettato come */dev/sda* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="14d10-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="14d10-122">La configurazione della memorizzazione nella cache del disco del sistema operativo è ottimizzata per le prestazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="14d10-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="14d10-123">A causa di questa configurazione, il disco del sistema operativo **non deve** ospitare applicazioni o i dati.</span><span class="sxs-lookup"><span data-stu-id="14d10-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="14d10-124">Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="14d10-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="14d10-125">**Disco temporaneo**: i dischi temporanei usano un'unità SSD che si trova nello stesso host della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="14d10-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="14d10-126">I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="14d10-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="14d10-127">Tuttavia, se la macchina virtuale viene spostata in un nuovo host, tutti i dati memorizzati su un disco temporaneo vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="14d10-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="14d10-128">Le dimensioni del disco temporaneo sono determinate dalle dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="14d10-129">I dischi temporanei vengono etichettati come */dev/sdb* e hanno un punto di montaggio */mnt*.</span><span class="sxs-lookup"><span data-stu-id="14d10-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="14d10-130">Dimensioni del disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="14d10-130">Temporary disk sizes</span></span>

| <span data-ttu-id="14d10-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="14d10-131">Type</span></span> | <span data-ttu-id="14d10-132">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-132">VM Size</span></span> | <span data-ttu-id="14d10-133">Dimensioni massime del disco temporaneo (GB)</span><span class="sxs-lookup"><span data-stu-id="14d10-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="14d10-134">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="14d10-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="14d10-135">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="14d10-135">A and D series</span></span> | <span data-ttu-id="14d10-136">800</span><span class="sxs-lookup"><span data-stu-id="14d10-136">800</span></span> |
| [<span data-ttu-id="14d10-137">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="14d10-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="14d10-138">Serie F</span><span class="sxs-lookup"><span data-stu-id="14d10-138">F series</span></span> | <span data-ttu-id="14d10-139">800</span><span class="sxs-lookup"><span data-stu-id="14d10-139">800</span></span> |
| [<span data-ttu-id="14d10-140">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="14d10-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="14d10-141">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="14d10-141">D and G series</span></span> | <span data-ttu-id="14d10-142">6144</span><span class="sxs-lookup"><span data-stu-id="14d10-142">6144</span></span> |
| [<span data-ttu-id="14d10-143">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="14d10-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="14d10-144">Serie L</span><span class="sxs-lookup"><span data-stu-id="14d10-144">L series</span></span> | <span data-ttu-id="14d10-145">5630</span><span class="sxs-lookup"><span data-stu-id="14d10-145">5630</span></span> |
| [<span data-ttu-id="14d10-146">GPU</span><span class="sxs-lookup"><span data-stu-id="14d10-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="14d10-147">Serie N</span><span class="sxs-lookup"><span data-stu-id="14d10-147">N series</span></span> | <span data-ttu-id="14d10-148">1.440</span><span class="sxs-lookup"><span data-stu-id="14d10-148">1440</span></span> |
| [<span data-ttu-id="14d10-149">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="14d10-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="14d10-150">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="14d10-150">A and H series</span></span> | <span data-ttu-id="14d10-151">2000</span><span class="sxs-lookup"><span data-stu-id="14d10-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="14d10-152">Dischi dati di Azure</span><span class="sxs-lookup"><span data-stu-id="14d10-152">Azure data disks</span></span>

<span data-ttu-id="14d10-153">È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="14d10-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="14d10-154">I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva.</span><span class="sxs-lookup"><span data-stu-id="14d10-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="14d10-155">Ciascun disco dati ha una capacità massima di 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="14d10-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="14d10-156">Le dimensione della macchina virtuale determinano il numero di dischi dati possono essere collegati a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="14d10-157">Per ogni core della macchina virtuale, è possibile collegare due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="14d10-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="14d10-158">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-158">Max data disks per VM</span></span>

| <span data-ttu-id="14d10-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="14d10-159">Type</span></span> | <span data-ttu-id="14d10-160">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-160">VM Size</span></span> | <span data-ttu-id="14d10-161">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="14d10-162">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="14d10-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="14d10-163">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="14d10-163">A and D series</span></span> | <span data-ttu-id="14d10-164">32</span><span class="sxs-lookup"><span data-stu-id="14d10-164">32</span></span> |
| [<span data-ttu-id="14d10-165">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="14d10-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="14d10-166">Serie F</span><span class="sxs-lookup"><span data-stu-id="14d10-166">F series</span></span> | <span data-ttu-id="14d10-167">32</span><span class="sxs-lookup"><span data-stu-id="14d10-167">32</span></span> |
| [<span data-ttu-id="14d10-168">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="14d10-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="14d10-169">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="14d10-169">D and G series</span></span> | <span data-ttu-id="14d10-170">64</span><span class="sxs-lookup"><span data-stu-id="14d10-170">64</span></span> |
| [<span data-ttu-id="14d10-171">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="14d10-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="14d10-172">Serie L</span><span class="sxs-lookup"><span data-stu-id="14d10-172">L series</span></span> | <span data-ttu-id="14d10-173">64</span><span class="sxs-lookup"><span data-stu-id="14d10-173">64</span></span> |
| [<span data-ttu-id="14d10-174">GPU</span><span class="sxs-lookup"><span data-stu-id="14d10-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="14d10-175">Serie N</span><span class="sxs-lookup"><span data-stu-id="14d10-175">N series</span></span> | <span data-ttu-id="14d10-176">48</span><span class="sxs-lookup"><span data-stu-id="14d10-176">48</span></span> |
| [<span data-ttu-id="14d10-177">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="14d10-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="14d10-178">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="14d10-178">A and H series</span></span> | <span data-ttu-id="14d10-179">32</span><span class="sxs-lookup"><span data-stu-id="14d10-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="14d10-180">Tipi di dischi per la VM</span><span class="sxs-lookup"><span data-stu-id="14d10-180">VM disk types</span></span>

<span data-ttu-id="14d10-181">Azure offre due tipi di dischi.</span><span class="sxs-lookup"><span data-stu-id="14d10-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="14d10-182">Disco standard</span><span class="sxs-lookup"><span data-stu-id="14d10-182">Standard disk</span></span>

<span data-ttu-id="14d10-183">Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni.</span><span class="sxs-lookup"><span data-stu-id="14d10-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="14d10-184">I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.</span><span class="sxs-lookup"><span data-stu-id="14d10-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="14d10-185">Disco premium</span><span class="sxs-lookup"><span data-stu-id="14d10-185">Premium disk</span></span>

<span data-ttu-id="14d10-186">I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD.</span><span class="sxs-lookup"><span data-stu-id="14d10-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="14d10-187">Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione.</span><span class="sxs-lookup"><span data-stu-id="14d10-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="14d10-188">L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="14d10-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="14d10-189">I dischi premium sono di tre tipi, P10, P20 e P30. Le dimensioni del disco determinano il tipo di disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="14d10-190">Quando si effettua la selezione, il valore delle dimensioni di un disco viene arrotondato per eccesso al tipo successivo.</span><span class="sxs-lookup"><span data-stu-id="14d10-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="14d10-191">Ad esempio, se le dimensioni del disco non superano i 128 GB, il tipo di disco è P10.</span><span class="sxs-lookup"><span data-stu-id="14d10-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="14d10-192">Se le dimensioni del disco vanno da 129 a 512 GB, il tipo sarà un P20.</span><span class="sxs-lookup"><span data-stu-id="14d10-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="14d10-193">Un valore superiore a 512 GB determina un tipo di disco P30.</span><span class="sxs-lookup"><span data-stu-id="14d10-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="14d10-194">Prestazioni disco premium</span><span class="sxs-lookup"><span data-stu-id="14d10-194">Premium disk performance</span></span>

|<span data-ttu-id="14d10-195">Tipo di disco di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="14d10-195">Premium storage disk type</span></span> | <span data-ttu-id="14d10-196">P10</span><span class="sxs-lookup"><span data-stu-id="14d10-196">P10</span></span> | <span data-ttu-id="14d10-197">P20</span><span class="sxs-lookup"><span data-stu-id="14d10-197">P20</span></span> | <span data-ttu-id="14d10-198">P30</span><span class="sxs-lookup"><span data-stu-id="14d10-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="14d10-199">Dimensioni del disco (arrotondate)</span><span class="sxs-lookup"><span data-stu-id="14d10-199">Disk size (round up)</span></span> | <span data-ttu-id="14d10-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="14d10-200">128 GB</span></span> | <span data-ttu-id="14d10-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="14d10-201">512 GB</span></span> | <span data-ttu-id="14d10-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="14d10-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="14d10-203">Operazioni IOPS al secondo max per disco</span><span class="sxs-lookup"><span data-stu-id="14d10-203">Max IOPS per disk</span></span> | <span data-ttu-id="14d10-204">500</span><span class="sxs-lookup"><span data-stu-id="14d10-204">500</span></span> | <span data-ttu-id="14d10-205">2.300</span><span class="sxs-lookup"><span data-stu-id="14d10-205">2,300</span></span> | <span data-ttu-id="14d10-206">5.000</span><span class="sxs-lookup"><span data-stu-id="14d10-206">5,000</span></span> |
<span data-ttu-id="14d10-207">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="14d10-207">Throughput per disk</span></span> | <span data-ttu-id="14d10-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="14d10-208">100 MB/s</span></span> | <span data-ttu-id="14d10-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="14d10-209">150 MB/s</span></span> | <span data-ttu-id="14d10-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="14d10-210">200 MB/s</span></span> |

<span data-ttu-id="14d10-211">Sebbene la tabella sopra riportata identifichi il numero massimo di operazioni di I/O al secondo per disco, è possibile raggiungere un livello superiore di prestazioni tramite lo striping di più dischi di dati.</span><span class="sxs-lookup"><span data-stu-id="14d10-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="14d10-212">Ad esempio, una macchina virtuale Standard_GS5 può raggiungere un massimo di 80.000 operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="14d10-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="14d10-213">Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="14d10-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="14d10-214">Creare e collegare dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-214">Create and attach disks</span></span>

<span data-ttu-id="14d10-215">I dischi dati possono essere creati e collegati al momento della creazione della macchina virtuale o a una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="14d10-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="14d10-216">Collegare un disco al momento della creazione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-216">Attach disk at VM creation</span></span>

<span data-ttu-id="14d10-217">Creare un gruppo di risorse con il comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="14d10-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="14d10-218">Creare una VM con il comando [az vm create]( /cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="14d10-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="14d10-219">L'argomento `--datadisk-sizes-gb` viene usato per specificare che è necessario creare un disco aggiuntivo e collegarlo alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="14d10-220">Per creare e collegare più dischi, usare un elenco delimitato da spazio dei valori delle dimensioni del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="14d10-221">Nell'esempio seguente viene creata una macchina virtuale con due dischi di dati, entrambi di 128 GB.</span><span class="sxs-lookup"><span data-stu-id="14d10-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="14d10-222">Poiché le dimensioni dei dischi sono 128 GB, entrambi i dischi sono configurati come P10, il che garantisce un massimo di 500 operazioni di I/O al secondo per disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="14d10-223">Collegare un disco alla macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="14d10-223">Attach disk to existing VM</span></span>

<span data-ttu-id="14d10-224">Per creare e collegare un nuovo disco a una macchina virtuale esistente, usare il comando [az vm disk attach](/cli/azure/vm/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="14d10-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="14d10-225">Nell'esempio seguente viene creato un disco premium, di 128 gigabyte, che viene collegato alla macchina virtuale creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="14d10-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="14d10-226">Preparare i dischi di dati</span><span class="sxs-lookup"><span data-stu-id="14d10-226">Prepare data disks</span></span>

<span data-ttu-id="14d10-227">Dopo aver collegato un disco alla macchina virtuale, il sistema operativo deve essere configurato per l'uso del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="14d10-228">L'esempio seguente illustra come configurare manualmente un disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="14d10-229">È anche possibile automatizzare questo processo puòcon cloud-init, di cui si parlerà nell'[esercitazione successiva](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="14d10-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="14d10-230">Configurazione manuale</span><span class="sxs-lookup"><span data-stu-id="14d10-230">Manual configuration</span></span>

<span data-ttu-id="14d10-231">Creare una connessione SSH alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="14d10-232">Sostituire l'indirizzo IP di esempio con l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="14d10-233">Eseguire la partizione del disco con `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="14d10-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="14d10-234">Scrivere un file system nella partizione con il comando `mkfs`.</span><span class="sxs-lookup"><span data-stu-id="14d10-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="14d10-235">Montare il nuovo disco in modo che sia accessibile nel sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="14d10-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="14d10-236">È ora possibile accedere al disco tramite il punto di montaggio *datadrive*, che può essere verificato con l'esecuzione del comando `df -h`.</span><span class="sxs-lookup"><span data-stu-id="14d10-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="14d10-237">L'output mostra la nuova unità montata su */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="14d10-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="14d10-238">Per assicurarsi che l'unità venga rimontata dopo un riavvio, è necessario aggiungerla al file */etc/fstab*.</span><span class="sxs-lookup"><span data-stu-id="14d10-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="14d10-239">A tale scopo, ottenere l'UUID del disco con l'utilità `blkid`.</span><span class="sxs-lookup"><span data-stu-id="14d10-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="14d10-240">L'output mostra l'UUID dell'unità, `/dev/sdc1` in questo caso.</span><span class="sxs-lookup"><span data-stu-id="14d10-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="14d10-241">Aggiungere una riga simile alla seguente al file */etc/fstab*.</span><span class="sxs-lookup"><span data-stu-id="14d10-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="14d10-242">Si noti anche che le barriere di scrittura possono essere disabilitate mediante *barrier=0*; questa configurazione può migliorare le prestazioni del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="14d10-243">Ora che il disco è stato configurato, chiudere la sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="14d10-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="14d10-244">Ridimensionare il disco della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="14d10-244">Resize VM disk</span></span>

<span data-ttu-id="14d10-245">Dopo la distribuzione di una macchina virtuale, è possibile aumentare le dimensioni del disco del sistema operativo o dei dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="14d10-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="14d10-246">L'aumento delle dimensioni di un disco è utile quando è necessario un maggiore spazio di archiviazione o un livello superiore di prestazioni, ad esempio P10, P20 e P30.</span><span class="sxs-lookup"><span data-stu-id="14d10-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="14d10-247">Si noti che non è possibile diminuire le dimensioni dei dischi.</span><span class="sxs-lookup"><span data-stu-id="14d10-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="14d10-248">Prima di aumentare le dimensioni del disco, è necessario conoscere l'ID o il nome del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="14d10-249">Usare il comando [az disk list](/cli/azure/vm/disk#list) per restituire tutti i dischi in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="14d10-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="14d10-250">Prendere nota del nome del disco di cui si desidera cambiare le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="14d10-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="14d10-251">La macchina virtuale deve anche essere deallocata.</span><span class="sxs-lookup"><span data-stu-id="14d10-251">The VM must also be deallocated.</span></span> <span data-ttu-id="14d10-252">Usare il comando [aaz vm deallocate]( /cli/azure/vm#deallocate) per arrestare e deallocare la VM.</span><span class="sxs-lookup"><span data-stu-id="14d10-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="14d10-253">Usare il comando [az disk update](/cli/azure/vm/disk#update) per ridimensionare il disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="14d10-254">In questo esempio un disco denominato *myDataDisk* viene ridimensionato a 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="14d10-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="14d10-255">Dopo aver completato l'operazione di ridimensionamento, avviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="14d10-256">Se è stato ridimensionato il disco del sistema operativo, la partizione di espande automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14d10-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="14d10-257">Se è stato ridimensionato un disco dati, tutte le partizioni correnti devono essere estese al sistema operativo delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="14d10-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="14d10-258">Snapshot di dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="14d10-258">Snapshot Azure disks</span></span>

<span data-ttu-id="14d10-259">Quando si crea uno snapshot del disco, viene creata una copia temporizzata di sola lettura del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="14d10-260">Gli snapshot della macchina virtuale di Azure sono utili per salvare rapidamente lo stato di una macchina virtuale prima di apportare modifiche alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="14d10-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="14d10-261">Nel caso in cui le modifiche alla configurazione si rivelino non volute, lo stato della macchina virtuale può essere ripristinato con lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="14d10-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="14d10-262">Quando una macchina virtuale dispone di più dischi, viene acquisito uno snapshot per ciascun disco separatamente dagli altri dischi.</span><span class="sxs-lookup"><span data-stu-id="14d10-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="14d10-263">Per eseguire backup coerenti con l'applicazione, prendere in considerazione l'arresto della macchina virtuale prima di eseguire gli snapshot dei dischi.</span><span class="sxs-lookup"><span data-stu-id="14d10-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="14d10-264">In alternativa, usare il [Servizio Backup di Microsoft Azure](/azure/backup/), che consente di eseguire backup automatici, mentre la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="14d10-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="14d10-265">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="14d10-265">Create snapshot</span></span>

<span data-ttu-id="14d10-266">Prima di creare uno snapshot del disco della macchina virtuale, è necessario conoscere l'ID o il nome del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="14d10-267">Usare il comando [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) per ottenere l'ID del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="14d10-268">In questo esempio l'ID del disco viene archiviato in una variabile in modo da poter essere usato in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="14d10-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="14d10-269">Dopo aver ottenuto l'ID del disco della macchina virtuale, usare il comando seguente per creare lo snapshot del disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="14d10-270">Creare un disco da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="14d10-270">Create disk from snapshot</span></span>

<span data-ttu-id="14d10-271">Lo snapshot può quindi essere convertito in un disco da usare per ricreare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="14d10-272">Ripristinare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="14d10-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="14d10-273">Per illustrare il ripristino della macchina virtuale, eliminare la macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="14d10-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="14d10-274">Creare una nuova macchina virtuale dal disco dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="14d10-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="14d10-275">Ricollegare un disco dati</span><span class="sxs-lookup"><span data-stu-id="14d10-275">Reattach data disk</span></span>

<span data-ttu-id="14d10-276">È necessario ricollegare tutti i dischi dati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14d10-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="14d10-277">Innanzitutto usare il comando [az disk list](https://docs.microsoft.com/cli/azure/disk#list) per trovare il nome del disco dati.</span><span class="sxs-lookup"><span data-stu-id="14d10-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="14d10-278">L'esempio inserisce il nome del disco in una variabile denominata *datadisk*, che viene usata nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="14d10-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="14d10-279">Usare il comando [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) per collegare il disco.</span><span class="sxs-lookup"><span data-stu-id="14d10-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="14d10-280">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14d10-280">Next steps</span></span>

<span data-ttu-id="14d10-281">In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="14d10-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="14d10-282">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="14d10-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="14d10-283">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="14d10-283">Data disks</span></span>
> * <span data-ttu-id="14d10-284">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="14d10-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="14d10-285">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-285">Disk performance</span></span>
> * <span data-ttu-id="14d10-286">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="14d10-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="14d10-287">Ridimensionamento dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-287">Resizing disks</span></span>
> * <span data-ttu-id="14d10-288">Snapshot dei dischi</span><span class="sxs-lookup"><span data-stu-id="14d10-288">Disk snapshots</span></span>

<span data-ttu-id="14d10-289">Passare all'esercitazione successiva per informazioni sull'automazione della configurazione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="14d10-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="14d10-290">Automatizzare la configurazione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="14d10-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
