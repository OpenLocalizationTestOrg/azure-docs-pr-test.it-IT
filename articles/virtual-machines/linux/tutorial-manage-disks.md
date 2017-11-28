---
title: aaaManage Azure dischi con hello CLI di Azure | Documenti Microsoft
description: 'Esercitazione: gestire i dischi di Azure con hello CLI di Azure'
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="ed469-103">Gestire i dischi di Azure con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="ed469-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="ed469-104">Macchine virtuali di Azure utilizzano il sistema operativo macchine virtuali di dischi toostore hello, applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="ed469-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="ed469-105">Quando si crea una macchina virtuale è importante toochoose una dimensione del disco e il carico di lavoro di configurazione appropriato toohello previsto.</span><span class="sxs-lookup"><span data-stu-id="ed469-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="ed469-106">Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM.</span><span class="sxs-lookup"><span data-stu-id="ed469-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="ed469-107">Vengono fornite informazioni su:</span><span class="sxs-lookup"><span data-stu-id="ed469-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed469-108">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="ed469-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="ed469-109">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="ed469-109">Data disks</span></span>
> * <span data-ttu-id="ed469-110">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="ed469-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="ed469-111">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-111">Disk performance</span></span>
> * <span data-ttu-id="ed469-112">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="ed469-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="ed469-113">Ridimensionamento dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-113">Resizing disks</span></span>
> * <span data-ttu-id="ed469-114">Snapshot dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ed469-115">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ed469-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ed469-116">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="ed469-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ed469-117">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ed469-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="ed469-118">Dischi di Azure predefiniti</span><span class="sxs-lookup"><span data-stu-id="ed469-118">Default Azure disks</span></span>

<span data-ttu-id="ed469-119">Quando viene creata una macchina virtuale di Azure, due dischi sono macchina virtuale toohello automaticamente collegato.</span><span class="sxs-lookup"><span data-stu-id="ed469-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="ed469-120">**Disco del sistema operativo** : i dischi del sistema operativo possono essere dimensionati backup too1 terabyte e host hello del sistema operativo di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ed469-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="ed469-121">disco del sistema operativo Hello viene etichettato *dev/sda* per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ed469-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="ed469-122">disco Hello la memorizzazione nella cache di configurazione del disco del sistema operativo hello è ottimizzato per le prestazioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ed469-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="ed469-123">A causa di questa configurazione, hello disco del sistema operativo **non** ospitare applicazioni o i dati.</span><span class="sxs-lookup"><span data-stu-id="ed469-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="ed469-124">Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ed469-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="ed469-125">**Disco temporaneo** -i dischi temporanei utilizzano un'unità SSD che si trova in hello stesso host hello VM Azure.</span><span class="sxs-lookup"><span data-stu-id="ed469-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="ed469-126">I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="ed469-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="ed469-127">Tuttavia, se hello macchina virtuale viene spostata tooa nuovo host, i dati archiviati in un disco temporaneo viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="ed469-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="ed469-128">dimensione di Hello del disco temporaneo hello è determinata dalla hello dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed469-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="ed469-129">I dischi temporanei vengono etichettati come */dev/sdb* e hanno un punto di montaggio */mnt*.</span><span class="sxs-lookup"><span data-stu-id="ed469-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="ed469-130">Dimensioni del disco temporaneo</span><span class="sxs-lookup"><span data-stu-id="ed469-130">Temporary disk sizes</span></span>

| <span data-ttu-id="ed469-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="ed469-131">Type</span></span> | <span data-ttu-id="ed469-132">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-132">VM Size</span></span> | <span data-ttu-id="ed469-133">Dimensioni massime del disco temporaneo (GB)</span><span class="sxs-lookup"><span data-stu-id="ed469-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="ed469-134">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="ed469-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="ed469-135">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="ed469-135">A and D series</span></span> | <span data-ttu-id="ed469-136">800</span><span class="sxs-lookup"><span data-stu-id="ed469-136">800</span></span> |
| [<span data-ttu-id="ed469-137">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="ed469-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="ed469-138">Serie F</span><span class="sxs-lookup"><span data-stu-id="ed469-138">F series</span></span> | <span data-ttu-id="ed469-139">800</span><span class="sxs-lookup"><span data-stu-id="ed469-139">800</span></span> |
| [<span data-ttu-id="ed469-140">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="ed469-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="ed469-141">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="ed469-141">D and G series</span></span> | <span data-ttu-id="ed469-142">6144</span><span class="sxs-lookup"><span data-stu-id="ed469-142">6144</span></span> |
| [<span data-ttu-id="ed469-143">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="ed469-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="ed469-144">Serie L</span><span class="sxs-lookup"><span data-stu-id="ed469-144">L series</span></span> | <span data-ttu-id="ed469-145">5630</span><span class="sxs-lookup"><span data-stu-id="ed469-145">5630</span></span> |
| [<span data-ttu-id="ed469-146">GPU</span><span class="sxs-lookup"><span data-stu-id="ed469-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="ed469-147">Serie N</span><span class="sxs-lookup"><span data-stu-id="ed469-147">N series</span></span> | <span data-ttu-id="ed469-148">1.440</span><span class="sxs-lookup"><span data-stu-id="ed469-148">1440</span></span> |
| [<span data-ttu-id="ed469-149">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="ed469-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="ed469-150">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="ed469-150">A and H series</span></span> | <span data-ttu-id="ed469-151">2000</span><span class="sxs-lookup"><span data-stu-id="ed469-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="ed469-152">Dischi dati di Azure</span><span class="sxs-lookup"><span data-stu-id="ed469-152">Azure data disks</span></span>

<span data-ttu-id="ed469-153">È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="ed469-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="ed469-154">I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva.</span><span class="sxs-lookup"><span data-stu-id="ed469-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="ed469-155">Ciascun disco dati ha una capacità massima di 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="ed469-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="ed469-156">dimensioni Hello della macchina virtuale hello determinano il numero di dischi dati può essere collegato tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed469-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="ed469-157">Per ogni core della macchina virtuale, è possibile collegare due dischi dati.</span><span class="sxs-lookup"><span data-stu-id="ed469-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="ed469-158">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-158">Max data disks per VM</span></span>

| <span data-ttu-id="ed469-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="ed469-159">Type</span></span> | <span data-ttu-id="ed469-160">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-160">VM Size</span></span> | <span data-ttu-id="ed469-161">Numero massimo di dischi di dati per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="ed469-162">Utilizzo generico</span><span class="sxs-lookup"><span data-stu-id="ed469-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="ed469-163">Serie A e D</span><span class="sxs-lookup"><span data-stu-id="ed469-163">A and D series</span></span> | <span data-ttu-id="ed469-164">32</span><span class="sxs-lookup"><span data-stu-id="ed469-164">32</span></span> |
| [<span data-ttu-id="ed469-165">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="ed469-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="ed469-166">Serie F</span><span class="sxs-lookup"><span data-stu-id="ed469-166">F series</span></span> | <span data-ttu-id="ed469-167">32</span><span class="sxs-lookup"><span data-stu-id="ed469-167">32</span></span> |
| [<span data-ttu-id="ed469-168">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="ed469-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="ed469-169">Serie D e G</span><span class="sxs-lookup"><span data-stu-id="ed469-169">D and G series</span></span> | <span data-ttu-id="ed469-170">64</span><span class="sxs-lookup"><span data-stu-id="ed469-170">64</span></span> |
| [<span data-ttu-id="ed469-171">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="ed469-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="ed469-172">Serie L</span><span class="sxs-lookup"><span data-stu-id="ed469-172">L series</span></span> | <span data-ttu-id="ed469-173">64</span><span class="sxs-lookup"><span data-stu-id="ed469-173">64</span></span> |
| [<span data-ttu-id="ed469-174">GPU</span><span class="sxs-lookup"><span data-stu-id="ed469-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="ed469-175">Serie N</span><span class="sxs-lookup"><span data-stu-id="ed469-175">N series</span></span> | <span data-ttu-id="ed469-176">48</span><span class="sxs-lookup"><span data-stu-id="ed469-176">48</span></span> |
| [<span data-ttu-id="ed469-177">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="ed469-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="ed469-178">Serie A e H</span><span class="sxs-lookup"><span data-stu-id="ed469-178">A and H series</span></span> | <span data-ttu-id="ed469-179">32</span><span class="sxs-lookup"><span data-stu-id="ed469-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="ed469-180">Tipi di dischi per la VM</span><span class="sxs-lookup"><span data-stu-id="ed469-180">VM disk types</span></span>

<span data-ttu-id="ed469-181">Azure offre due tipi di dischi.</span><span class="sxs-lookup"><span data-stu-id="ed469-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="ed469-182">Disco standard</span><span class="sxs-lookup"><span data-stu-id="ed469-182">Standard disk</span></span>

<span data-ttu-id="ed469-183">Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ed469-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="ed469-184">I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.</span><span class="sxs-lookup"><span data-stu-id="ed469-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="ed469-185">Disco premium</span><span class="sxs-lookup"><span data-stu-id="ed469-185">Premium disk</span></span>

<span data-ttu-id="ed469-186">I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD.</span><span class="sxs-lookup"><span data-stu-id="ed469-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="ed469-187">Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione.</span><span class="sxs-lookup"><span data-stu-id="ed469-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="ed469-188">L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS.</span><span class="sxs-lookup"><span data-stu-id="ed469-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="ed469-189">I dischi Premium sono disponibili in tre tipi (P10, P20, P30), dimensione hello del disco di hello determina il tipo di disco hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="ed469-190">Quando si seleziona, un valore di hello dimensioni disco viene arrotondato per eccesso tipo successivo toohello.</span><span class="sxs-lookup"><span data-stu-id="ed469-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="ed469-191">Ad esempio, se la dimensione del disco hello è inferiore a 128 GB, il tipo di disco hello è P10.</span><span class="sxs-lookup"><span data-stu-id="ed469-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="ed469-192">Se la dimensione del disco hello è tra 129 e 512 GB, hello sono un P20.</span><span class="sxs-lookup"><span data-stu-id="ed469-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="ed469-193">Un valore superiore a 512 GB, dimensioni hello sono un P30.</span><span class="sxs-lookup"><span data-stu-id="ed469-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="ed469-194">Prestazioni disco premium</span><span class="sxs-lookup"><span data-stu-id="ed469-194">Premium disk performance</span></span>

|<span data-ttu-id="ed469-195">Tipo di disco di Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="ed469-195">Premium storage disk type</span></span> | <span data-ttu-id="ed469-196">P10</span><span class="sxs-lookup"><span data-stu-id="ed469-196">P10</span></span> | <span data-ttu-id="ed469-197">P20</span><span class="sxs-lookup"><span data-stu-id="ed469-197">P20</span></span> | <span data-ttu-id="ed469-198">P30</span><span class="sxs-lookup"><span data-stu-id="ed469-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed469-199">Dimensioni del disco (arrotondate)</span><span class="sxs-lookup"><span data-stu-id="ed469-199">Disk size (round up)</span></span> | <span data-ttu-id="ed469-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="ed469-200">128 GB</span></span> | <span data-ttu-id="ed469-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="ed469-201">512 GB</span></span> | <span data-ttu-id="ed469-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="ed469-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="ed469-203">Operazioni IOPS al secondo max per disco</span><span class="sxs-lookup"><span data-stu-id="ed469-203">Max IOPS per disk</span></span> | <span data-ttu-id="ed469-204">500</span><span class="sxs-lookup"><span data-stu-id="ed469-204">500</span></span> | <span data-ttu-id="ed469-205">2.300</span><span class="sxs-lookup"><span data-stu-id="ed469-205">2,300</span></span> | <span data-ttu-id="ed469-206">5.000</span><span class="sxs-lookup"><span data-stu-id="ed469-206">5,000</span></span> |
<span data-ttu-id="ed469-207">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="ed469-207">Throughput per disk</span></span> | <span data-ttu-id="ed469-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="ed469-208">100 MB/s</span></span> | <span data-ttu-id="ed469-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="ed469-209">150 MB/s</span></span> | <span data-ttu-id="ed469-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="ed469-210">200 MB/s</span></span> |

<span data-ttu-id="ed469-211">Mentre hello sopra tabella identifica massimo di IOPS per disco, un livello di prestazioni superiore può essere ottenuto lo striping di più dischi dati.</span><span class="sxs-lookup"><span data-stu-id="ed469-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="ed469-212">Ad esempio, una macchina virtuale Standard_GS5 può raggiungere un massimo di 80.000 operazioni di I/O al secondo.</span><span class="sxs-lookup"><span data-stu-id="ed469-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="ed469-213">Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ed469-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="ed469-214">Creare e collegare dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-214">Create and attach disks</span></span>

<span data-ttu-id="ed469-215">I dischi dati possono essere creati e collegati in fase di creazione macchina virtuale o tooan macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="ed469-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="ed469-216">Collegare un disco al momento della creazione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-216">Attach disk at VM creation</span></span>

<span data-ttu-id="ed469-217">Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="ed469-218">Creare una macchina virtuale utilizzando hello [creare vm az]( /cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="ed469-219">Hello `--datadisk-sizes-gb` argomento è utilizzato toospecify che un disco aggiuntivo deve essere creato e collegato macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="ed469-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="ed469-220">toocreate e collegare più di un disco, utilizzare un elenco delimitato da virgole dei valori di dimensioni del disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="ed469-221">Nell'esempio seguente di hello, viene creata una macchina virtuale con dischi di dati di due, entrambi 128 GB.</span><span class="sxs-lookup"><span data-stu-id="ed469-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="ed469-222">Poiché le dimensioni dei dischi hello sono 128 GB, entrambi i dischi sono configurati come P10s, che forniscono numero massimo di 500 IOPS per disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="ed469-223">Collegare tooexisting disco VM</span><span class="sxs-lookup"><span data-stu-id="ed469-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="ed469-224">toocreate e collegare una nuovo disco tooan macchina virtuale esistente, utilizzare hello [collegare il disco di macchina virtuale az](/cli/azure/vm/disk#attach) comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="ed469-225">Hello esempio seguente crea un disco premium, 128 gigabyte di spazio e la collega toohello che macchina virtuale creata nell'ultimo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="ed469-226">Preparare i dischi di dati</span><span class="sxs-lookup"><span data-stu-id="ed469-226">Prepare data disks</span></span>

<span data-ttu-id="ed469-227">Dopo aver macchina virtuale toohello collegato, un disco del sistema operativo hello deve toobe configurato toouse hello disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="ed469-228">Hello di esempio seguente viene illustrato come toomanually configurare un disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="ed469-229">È anche possibile automatizzare questo processo puòcon cloud-init, di cui si parlerà nell'[esercitazione successiva](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ed469-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="ed469-230">Configurazione manuale</span><span class="sxs-lookup"><span data-stu-id="ed469-230">Manual configuration</span></span>

<span data-ttu-id="ed469-231">Creare una connessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="ed469-232">Sostituire l'indirizzo IP di esempio hello con indirizzo IP pubblico della macchina virtuale hello hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="ed469-233">Partizione disco hello con `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="ed469-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="ed469-234">Scrittura di una partizione toohello usando hello `mkfs` comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="ed469-235">Montare il disco nuovo hello in modo che siano accessibile nel sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="ed469-236">disco Hello è ora possibile accedere tramite hello *datadrive* punto di montaggio, che può essere verificato eseguendo hello `df -h` comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="ed469-237">output di Hello Mostra nuova unità hello montato su */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="ed469-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="ed469-238">tooensure che hello unità viene rimontato dopo il riavvio, è necessario aggiungerlo toohello */e così via/fstab* file.</span><span class="sxs-lookup"><span data-stu-id="ed469-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="ed469-239">toodo in tal caso, ottenere hello UUID del disco hello con hello `blkid` utilità.</span><span class="sxs-lookup"><span data-stu-id="ed469-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="ed469-240">output di Hello Visualizza hello UUID dell'unità hello `/dev/sdc1` in questo caso.</span><span class="sxs-lookup"><span data-stu-id="ed469-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="ed469-241">Aggiungere un toohello simile di riga segue toohello */e così via/fstab* file.</span><span class="sxs-lookup"><span data-stu-id="ed469-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="ed469-242">Si noti anche che le barriere di scrittura possono essere disabilitate mediante *barrier=0*; questa configurazione può migliorare le prestazioni del disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="ed469-243">Ora che hello disco è stato configurato, chiudere una sessione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="ed469-244">Ridimensionare il disco della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed469-244">Resize VM disk</span></span>

<span data-ttu-id="ed469-245">Dopo la distribuzione di una macchina virtuale, possono essere aumentati le dimensioni disco del sistema operativo hello o eventuali dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="ed469-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="ed469-246">Aumento delle dimensioni di hello di un disco è utile quando è necessario più spazio di archiviazione o un livello superiore di prestazioni (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="ed469-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="ed469-247">Si noti che non è possibile diminuire le dimensioni dei dischi.</span><span class="sxs-lookup"><span data-stu-id="ed469-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="ed469-248">Prima di aumentare le dimensioni del disco, hello Id o nome del disco hello è necessaria.</span><span class="sxs-lookup"><span data-stu-id="ed469-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="ed469-249">Hello utilizzare [elenco disco az](/cli/azure/vm/disk#list) tooreturn comando tutti i dischi in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed469-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="ed469-250">Prendere nota del nome del disco hello che si desidera tooresize.</span><span class="sxs-lookup"><span data-stu-id="ed469-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="ed469-251">Hello VM deve inoltre essere deallocata.</span><span class="sxs-lookup"><span data-stu-id="ed469-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="ed469-252">Hello utilizzare [az vm deallocare]( /cli/azure/vm#deallocate) comando toostop e deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed469-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="ed469-253">Hello utilizzare [aggiornamento disco az](/cli/azure/vm/disk#update) disco hello tooresize di comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="ed469-254">In questo esempio ridimensiona un disco denominato *myDataDisk* too1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="ed469-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="ed469-255">Una volta completata l'operazione di ridimensionamento hello, avviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed469-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="ed469-256">Se è stato ridimensionato hello disco del sistema operativo, la partizione hello viene estesa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed469-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="ed469-257">Se è stato ridimensionato un disco dati, tutte le partizioni correnti necessario toobe espansa nel sistema operativo di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ed469-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="ed469-258">Snapshot di dischi di Azure</span><span class="sxs-lookup"><span data-stu-id="ed469-258">Snapshot Azure disks</span></span>

<span data-ttu-id="ed469-259">Creare uno snapshot del disco crea un letto solo nel momento copia del disco hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="ed469-260">Gli snapshot macchina virtuale di Azure sono utili per salvare rapidamente lo stato di hello di una macchina virtuale prima di apportare modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="ed469-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="ed469-261">In caso di hello modifiche alla configurazione hello dimostrare toobe indesiderati, stato delle macchine Virtuali può essere ripristinato mediante snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="ed469-262">Quando una macchina virtuale dispone di più di un disco, viene eseguito uno snapshot di ogni disco in modo indipendente da hello ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="ed469-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="ed469-263">Per l'esecuzione di backup coerenti con l'applicazione, prendere in considerazione l'arresto di hello VM prima di eseguire gli snapshot del disco.</span><span class="sxs-lookup"><span data-stu-id="ed469-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="ed469-264">In alternativa, utilizzare hello [servizio Azure Backup](/azure/backup/), che consente di tooperform automatizzata backup mentre hello macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ed469-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="ed469-265">Creare uno snapshot</span><span class="sxs-lookup"><span data-stu-id="ed469-265">Create snapshot</span></span>

<span data-ttu-id="ed469-266">Prima di creare uno snapshot di dischi di macchina virtuale, hello Id o nome del disco hello è necessaria.</span><span class="sxs-lookup"><span data-stu-id="ed469-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="ed469-267">Hello utilizzare [Mostra vm az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id di comando tooreturn hello del disco. In questo esempio, id disco hello è archiviato in una variabile in modo che può essere utilizzato in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="ed469-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="ed469-268">Dopo aver creato id hello del disco della macchina virtuale hello, hello comando seguente crea uno snapshot del disco hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="ed469-269">Creare un disco da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="ed469-269">Create disk from snapshot</span></span>

<span data-ttu-id="ed469-270">Lo snapshot può quindi essere convertito in un disco, che può essere una macchina virtuale di hello toorecreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ed469-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="ed469-271">Ripristinare una macchina virtuale da uno snapshot</span><span class="sxs-lookup"><span data-stu-id="ed469-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="ed469-272">ripristino della macchina virtuale toodemonstrate, macchina virtuale esistente di eliminazione hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="ed469-273">Creare una nuova macchina virtuale dal disco snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="ed469-274">Ricollegare un disco dati</span><span class="sxs-lookup"><span data-stu-id="ed469-274">Reattach data disk</span></span>

<span data-ttu-id="ed469-275">Tutti i dischi di dati necessario macchina virtuale di toohello toobe ricollegato.</span><span class="sxs-lookup"><span data-stu-id="ed469-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="ed469-276">Prima di tutto trovare nome del disco dati hello utilizzando hello [elenco disco az](https://docs.microsoft.com/cli/azure/disk#list) comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="ed469-277">In questo esempio posizioni hello nome del disco hello in una variabile denominata *datadisk*, che viene utilizzato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="ed469-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="ed469-278">Hello utilizzare [collegare il disco di macchina virtuale az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disco hello tooattach di comando.</span><span class="sxs-lookup"><span data-stu-id="ed469-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="ed469-279">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed469-279">Next steps</span></span>

<span data-ttu-id="ed469-280">In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ed469-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed469-281">Dischi del sistema operativo e dischi temporanei</span><span class="sxs-lookup"><span data-stu-id="ed469-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="ed469-282">Dischi dati</span><span class="sxs-lookup"><span data-stu-id="ed469-282">Data disks</span></span>
> * <span data-ttu-id="ed469-283">Dischi Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="ed469-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="ed469-284">Prestazioni dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-284">Disk performance</span></span>
> * <span data-ttu-id="ed469-285">Collegamento e preparazione dei dischi dati</span><span class="sxs-lookup"><span data-stu-id="ed469-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="ed469-286">Ridimensionamento dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-286">Resizing disks</span></span>
> * <span data-ttu-id="ed469-287">Snapshot dei dischi</span><span class="sxs-lookup"><span data-stu-id="ed469-287">Disk snapshots</span></span>

<span data-ttu-id="ed469-288">Spostare toohello Avanti toolearn esercitazione sull'automazione di configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed469-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed469-289">Automatizzare la configurazione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ed469-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
