---
title: Migrazione di VM ad Archiviazione Premium di Azure | Documentazione Microsoft
description: Eseguire la migrazione delle VM esistenti in Archiviazione Premium di Azure. Archiviazione Premium offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con I/O intensivo in esecuzione su Macchine virtuali di Azure.
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: ca893f87b155a92c457e3bf6d9d39aaf86bf5fb3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="5095f-104">Migrazione in Archiviazione Premium di Azure (dischi non gestiti)</span><span class="sxs-lookup"><span data-stu-id="5095f-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-105">Questo articolo descrive come migrare una VM che usa dischi Standard non gestiti a una VM che usa dischi Premium non gestiti.</span><span class="sxs-lookup"><span data-stu-id="5095f-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="5095f-106">È consigliabile usare Azure Managed Disks per le nuove VM e convertire i dischi non gestiti esistenti in dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="5095f-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="5095f-107">Managed Disks gestisce automaticamente gli account di archiviazione sottostanti e non è necessario eseguire questa attività manualmente.</span><span class="sxs-lookup"><span data-stu-id="5095f-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="5095f-108">Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="5095f-109">Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con I/O intensivo.</span><span class="sxs-lookup"><span data-stu-id="5095f-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="5095f-110">Per trarre vantaggio dalla velocità e dalle prestazioni di questi dischi, è possibile migrare i dischi delle VM dell'applicazione ad Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="5095f-111">Lo scopo di questa guida è preparare i nuovi utenti di Archiviazione Premium di Microsoft Azure a eseguire una transizione senza intoppi dal sistema corrente ad Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="5095f-112">Questa guida descrive tre aspetti chiave di questo processo:</span><span class="sxs-lookup"><span data-stu-id="5095f-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="5095f-113">Pianificare la migrazione ad Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="5095f-114">Preparare e copiare i dischi rigidi virtuali in Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="5095f-115">Creare una macchina virtuale di Azure usando Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="5095f-116">È possibile eseguire la migrazione di VM da altre piattaforme ad Archiviazione Premium di Azure o migrare VM esistenti di Azure da Archiviazione Standard ad Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="5095f-117">Questa guida illustra i passaggi per entrambi i due scenari.</span><span class="sxs-lookup"><span data-stu-id="5095f-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="5095f-118">Seguire i passaggi specificati nella sezione pertinente al proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="5095f-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-119">Una panoramica delle funzionalità e dei prezzi di Archiviazione Premium è disponibile in [Archiviazione Premium: archiviazione dalle prestazioni elevate per carichi di lavoro di macchine virtuali di Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="5095f-120">È consigliabile eseguire la migrazione di qualsiasi disco di macchine virtuali che richiede un numero elevato di IOPS ad Archiviazione Premium di Azure per ottenere prestazioni ottimali per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="5095f-121">Se il disco non richiede un numero elevato di IOPS, è possibile limitare i costi mantenendolo in Archiviazione Standard, che archivia i dati dei dischi delle macchine virtuali in unità disco rigido (HDD) invece che in unità SSD.</span><span class="sxs-lookup"><span data-stu-id="5095f-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="5095f-122">Per completare l'intero processo di migrazione, potrebbero essere necessarie altre azioni sia prima che dopo i passaggi descritti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="5095f-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="5095f-123">Tra gli esempi sono incluse la configurazione di reti virtuali o di endpoint oppure l'applicazione di modifiche al codice direttamente nell'applicazione che possono causare tempi di inattività all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="5095f-124">Queste azioni sono univoche per ogni applicazione ed è consigliabile completarle insieme ai passaggi descritti in questa guida per eseguire la transizione completa ad Archiviazione Premium con la massima semplicità possibile.</span><span class="sxs-lookup"><span data-stu-id="5095f-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="5095f-125"><a name="plan-the-migration-to-premium-storage"></a>Pianificare la migrazione ad Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="5095f-126">Questa sezione è preparatoria ai passaggi per la migrazione indicati nell'articolo, e aiuta a prendere la migliore decisione relativamente ai tipi di macchina virtuale e disco.</span><span class="sxs-lookup"><span data-stu-id="5095f-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5095f-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5095f-127">Prerequisites</span></span>
* <span data-ttu-id="5095f-128">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-128">You will need an Azure subscription.</span></span> <span data-ttu-id="5095f-129">Se non è disponibile, è possibile creare una sottoscrizione di [valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) di un mese oppure visitare [Prezzi di Azure](https://azure.microsoft.com/pricing/) per altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="5095f-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="5095f-130">Per eseguire i cmdlet PowerShell è necessario il modulo di Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5095f-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="5095f-131">Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per le istruzioni relative al punto di installazione e all’installazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="5095f-132">Quando si pianifica di usare macchine virtuali di Azure in esecuzione su Archiviazione Premium, è necessario usare macchine virtuali in grado di supportare Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="5095f-133">Con le VM che supportano Archiviazione Premium è possibile usare dischi sia di Archiviazione Standard che di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="5095f-134">I dischi di archiviazione premium saranno disponibili con più tipi di macchine virtuali in futuro.</span><span class="sxs-lookup"><span data-stu-id="5095f-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="5095f-135">Per altre informazioni su tutte le dimensioni e su tutti i tipi di dischi disponibili per le macchine virtuali di Azure, vedere [Dimensioni delle macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Dimensioni dei servizi cloud](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="5095f-136">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="5095f-136">Considerations</span></span>
<span data-ttu-id="5095f-137">Una VM di Azure supporta il collegamento di diversi dischi di Archiviazione Premium e offre alle applicazioni fino a 256 TB di spazio di archiviazione per ogni VM.</span><span class="sxs-lookup"><span data-stu-id="5095f-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="5095f-138">Con Archiviazione Premium le applicazioni possono raggiungere 80.000 IOPS (operazioni di input/output al secondo) per ogni macchina virtuale e 2000 MB al secondo di velocità effettiva dei dischi per ogni macchina virtuale, con una latenza estremamente bassa per le operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="5095f-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="5095f-139">Sono disponibili diverse opzioni in termini di macchine virtuali e dischi.</span><span class="sxs-lookup"><span data-stu-id="5095f-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="5095f-140">Questa sezione aiuta a individuare l'opzione più adatta al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5095f-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="5095f-141">Dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5095f-141">VM sizes</span></span>
<span data-ttu-id="5095f-142">Le specifiche delle dimensioni delle VM di Azure sono elencate in [Dimensioni delle macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5095f-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5095f-143">Esaminare le caratteristiche delle prestazioni delle Macchine virtuali che usano Archiviazione Premium e scegliere le dimensioni delle VM maggiormente indicate per i propri carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5095f-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="5095f-144">Assicurarsi che nella macchina virtuale sia disponibile larghezza di banda sufficiente per gestire il traffico dei dischi.</span><span class="sxs-lookup"><span data-stu-id="5095f-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="5095f-145">Dimensione disco</span><span class="sxs-lookup"><span data-stu-id="5095f-145">Disk sizes</span></span>
<span data-ttu-id="5095f-146">È possibile usare cinque tipi di dischi con la VM, ognuno con limiti di velocità effettiva e IOP specifici.</span><span class="sxs-lookup"><span data-stu-id="5095f-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="5095f-147">Tenere in considerazione questi limiti nella scelta del tipo di disco per la macchina virtuale in base alle esigenze dell’applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.</span><span class="sxs-lookup"><span data-stu-id="5095f-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="5095f-148">Tipo di disco Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-148">Premium Disks Type</span></span>  | <span data-ttu-id="5095f-149">P10</span><span class="sxs-lookup"><span data-stu-id="5095f-149">P10</span></span>   | <span data-ttu-id="5095f-150">P20</span><span class="sxs-lookup"><span data-stu-id="5095f-150">P20</span></span>   | <span data-ttu-id="5095f-151">P30</span><span class="sxs-lookup"><span data-stu-id="5095f-151">P30</span></span>            | <span data-ttu-id="5095f-152">P40</span><span class="sxs-lookup"><span data-stu-id="5095f-152">P40</span></span>            | <span data-ttu-id="5095f-153">P50</span><span class="sxs-lookup"><span data-stu-id="5095f-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="5095f-154">Dimensioni disco</span><span class="sxs-lookup"><span data-stu-id="5095f-154">Disk size</span></span>           | <span data-ttu-id="5095f-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="5095f-155">128 GB</span></span>| <span data-ttu-id="5095f-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="5095f-156">512 GB</span></span>| <span data-ttu-id="5095f-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="5095f-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="5095f-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="5095f-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="5095f-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="5095f-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="5095f-160">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="5095f-160">IOPS per disk</span></span>       | <span data-ttu-id="5095f-161">500</span><span class="sxs-lookup"><span data-stu-id="5095f-161">500</span></span>   | <span data-ttu-id="5095f-162">2300</span><span class="sxs-lookup"><span data-stu-id="5095f-162">2300</span></span>  | <span data-ttu-id="5095f-163">5000</span><span class="sxs-lookup"><span data-stu-id="5095f-163">5000</span></span>           | <span data-ttu-id="5095f-164">7500</span><span class="sxs-lookup"><span data-stu-id="5095f-164">7500</span></span>           | <span data-ttu-id="5095f-165">7500</span><span class="sxs-lookup"><span data-stu-id="5095f-165">7500</span></span>           | 
| <span data-ttu-id="5095f-166">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="5095f-166">Throughput per disk</span></span> | <span data-ttu-id="5095f-167">100 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="5095f-167">100 MB per second</span></span> | <span data-ttu-id="5095f-168">150 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="5095f-168">150 MB per second</span></span> | <span data-ttu-id="5095f-169">200 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="5095f-169">200 MB per second</span></span> | <span data-ttu-id="5095f-170">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="5095f-170">250 MB per second</span></span> | <span data-ttu-id="5095f-171">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="5095f-171">250 MB per second</span></span> |

<span data-ttu-id="5095f-172">A seconda del carico di lavoro, determinare se per la macchina virtuale in uso sono necessari dischi dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="5095f-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="5095f-173">È possibile collegare più dischi dati persistenti alla macchina virtuale in uso.</span><span class="sxs-lookup"><span data-stu-id="5095f-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="5095f-174">Se necessario, è possibile eseguire lo striping dei dischi per aumentare la capacità e le prestazioni del volume.</span><span class="sxs-lookup"><span data-stu-id="5095f-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="5095f-175">Per altre informazioni sullo striping del disco, vedere [qui](storage-premium-storage-performance.md#disk-striping). Se si esegue lo striping di dischi dati di Archiviazione Premium con [Spazi di archiviazione][4], è consigliabile configurare una colonna per ogni disco usato.</span><span class="sxs-lookup"><span data-stu-id="5095f-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="5095f-176">In caso contrario, le prestazioni complessive del volume in cui è stato eseguito lo striping possono essere inferiori al previsto a causa di una distribuzione non uniforme del traffico di dati da un disco a un altro.</span><span class="sxs-lookup"><span data-stu-id="5095f-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="5095f-177">Per le macchine virtuali Linux è possibile usare l'utilità *mdadm* per ottenere lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="5095f-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="5095f-178">Per informazioni dettagliate, vedere l'articolo sulla [configurazione del RAID software in Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="5095f-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="5095f-179">Obiettivi di scalabilità per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5095f-179">Storage account scalability targets</span></span>
<span data-ttu-id="5095f-180">Gli account di Archiviazione Premium hanno i seguenti obiettivi di scalabilità oltre agli [obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="5095f-181">Se le esigenze dell'applicazione superano gli obiettivi di scalabilità di un singolo account di archiviazione, compilare l'applicazione in modo che sia possibile usare più account di archiviazione e partizionare i dati tra tali account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="5095f-182">Capacità account totale</span><span class="sxs-lookup"><span data-stu-id="5095f-182">Total Account Capacity</span></span> | <span data-ttu-id="5095f-183">Larghezza di banda totale per un account di archiviazione con ridondanza locale</span><span class="sxs-lookup"><span data-stu-id="5095f-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="5095f-184">Capacità disco : 35 TB</span><span class="sxs-lookup"><span data-stu-id="5095f-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="5095f-185">Capacità snapshot: 10 TB</span><span class="sxs-lookup"><span data-stu-id="5095f-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="5095f-186">Fino a 50 gigabit al secondo per dati in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="5095f-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="5095f-187">Per altre informazioni sulle specifiche di Archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="5095f-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="5095f-188">Criteri di memorizzazione nella cache su disco</span><span class="sxs-lookup"><span data-stu-id="5095f-188">Disk caching policy</span></span>
<span data-ttu-id="5095f-189">Per impostazione predefinita, il criterio di memorizzazione nella cache su disco è impostato su *Sola lettura* per tutti i dischi di dati Premium e su *Lettura/scrittura* per il disco del sistema operativo Premium collegato alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="5095f-190">Queste impostazioni di configurazione sono consigliate per ottenere prestazioni ottimali per le operazioni di I/O dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="5095f-191">Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5095f-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="5095f-192">Le impostazioni della cache per i dischi dati esistenti possono essere aggiornate mediante il [portale di Azure](https://portal.azure.com) o il parametro *-HostCaching* del cmdlet *Set-AzureDataDisk*.</span><span class="sxs-lookup"><span data-stu-id="5095f-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="5095f-193">Località</span><span class="sxs-lookup"><span data-stu-id="5095f-193">Location</span></span>
<span data-ttu-id="5095f-194">Selezionare una posizione in cui è disponibile il servizio Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="5095f-195">Per informazioni aggiornate sulle località disponibili, vedere [Prodotti in base all'area](https://azure.microsoft.com/regions/#services) .</span><span class="sxs-lookup"><span data-stu-id="5095f-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="5095f-196">Le macchine virtuali presenti nella stessa area dell'account di archiviazione in cui sono archiviati i dischi per la macchina virtuale offrono prestazioni superiori rispetto a quelle ubicate in aree separate.</span><span class="sxs-lookup"><span data-stu-id="5095f-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="5095f-197">Altre impostazioni di configurazione delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="5095f-198">Quando si crea una macchina virtuale di Azure viene richiesto di configurare determinate impostazioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="5095f-199">Tenere presente che esistono alcune impostazioni fisse per la durata della macchina virtuale, mentre è possibile modificarne o aggiungerne altre in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5095f-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="5095f-200">Esaminare queste impostazioni di configurazione della macchina virtuale di Azure e assicurarsi che siano configurate in modo appropriato per soddisfare le esigenze del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5095f-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="5095f-201">Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="5095f-201">Optimization</span></span>
<span data-ttu-id="5095f-202">L'articolo [Archiviazione Premium di Azure: progettata per prestazioni elevate](storage-premium-storage-performance.md) fornisce indicazioni per lo sviluppo di applicazioni a prestazioni elevate mediante l'Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="5095f-203">È possibile usare le linee guida disponibili in questo documento insieme alle procedure consigliate per le prestazioni applicabili alle tecnologie usate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="5095f-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparare e copiare i dischi rigidi virtuali in Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="5095f-205">La sezione seguente offre le linee guida per preparare i dischi rigidi virtuali da una macchina virtuale e per copiarli in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="5095f-206">Scenario 1: Migrazione di VM di Azure esistenti in Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="5095f-207">Scenario 2: Migrazione di VM da altre piattaforme ad Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="5095f-208">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5095f-208">Prerequisites</span></span>
<span data-ttu-id="5095f-209">Di seguito sono indicati i requisiti per preparare i dischi rigidi virtuali per la migrazione:</span><span class="sxs-lookup"><span data-stu-id="5095f-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="5095f-210">Una sottoscrizione di Azure, un account di archiviazione e un contenitore in tale account di archiviazione in cui copiare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="5095f-211">Si noti che l'account di archiviazione di destinazione può essere un account di archiviazione Standard o Premium in base alle esigenze dell’utente.</span><span class="sxs-lookup"><span data-stu-id="5095f-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="5095f-212">Uno strumento per generalizzare il disco rigido virtuale se si pianifica di creare più istanze di macchine virtuali da esso.</span><span class="sxs-lookup"><span data-stu-id="5095f-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="5095f-213">Ad esempio, sysprep per Windows o virt-sysprep per Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5095f-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="5095f-214">Uno strumento per caricare il file del disco rigido virtuale nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="5095f-215">Vedere [Trasferire dati con l'utilità della riga di comando AzCopy](storage-use-azcopy.md) o usare [Esplora archivi di Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="5095f-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="5095f-216">Questa guida descrive la copia del disco rigido virtuale utilizzando lo strumento AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5095f-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-217">Se si sceglie l'opzione di copia sincronizzata con AzCopy, per ottenere prestazioni ottimali copiare il disco rigido virtuale eseguendo uno di questi strumenti da una macchina virtuale di Azure nella stessa area dell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="5095f-218">Se si copia un disco rigido virtuale da una macchina virtuale di Azure in un'area diversa, le prestazioni potrebbero essere più lente.</span><span class="sxs-lookup"><span data-stu-id="5095f-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="5095f-219">Per la copia di una grande quantità di dati su una larghezza di banda limitata, prendere in considerazione l'[uso del servizio di importazione/esportazione di Azure per trasferire i dati nell'archivio BLOB](../storage-import-export-service.md). Ciò consente di trasferire i dati tramite l'invio delle unità disco rigido a un datacenter Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](../storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="5095f-220">È possibile utilizzare il servizio di importazione/esportazione di Azure per copiare dati in un solo account di archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="5095f-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="5095f-221">Una volta che i dati si trovano nell'account di archiviazione standard, è possibile usare l'[API Copy Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) oppure AzCopy per trasferire i dati all'account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="5095f-222">Notare che Microsoft Azure supporta solo file di disco rigido virtuale a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="5095f-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="5095f-223">I file VHDX o i dischi rigidi virtuali dinamici non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="5095f-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="5095f-224">Se si dispone di un disco rigido virtuale dinamico, è possibile convertirlo in un disco a dimensione fissa utilizzando il cmdlet [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) .</span><span class="sxs-lookup"><span data-stu-id="5095f-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="5095f-225"><a name="scenario1"></a>Scenario 1: Migrazione di VM di Azure esistenti in Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="5095f-226">Se si esegue la migrazione di macchine virtuali di Azure esistenti, arrestare la macchina virtuale, preparare i dischi rigidi virtuali a seconda del tipo di disco rigido virtuale desiderato e quindi copiare il disco rigido Virtuale con AzCopy o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5095f-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="5095f-227">La macchina virtuale deve essere completamente inattiva per la migrazione a uno stato pulito.</span><span class="sxs-lookup"><span data-stu-id="5095f-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="5095f-228">Il tempo di inattività proseguirà fino al termine della migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="5095f-229">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="5095f-229">Step 1.</span></span> <span data-ttu-id="5095f-230">Preparare i dischi rigidi virtuali per la migrazione</span><span class="sxs-lookup"><span data-stu-id="5095f-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="5095f-231">Se si esegue la migrazione di macchine virtuali esistenti di Azure ad Archiviazione Premium, il disco rigido virtuale può essere:</span><span class="sxs-lookup"><span data-stu-id="5095f-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="5095f-232">Un'immagine del sistema operativo generalizzata</span><span class="sxs-lookup"><span data-stu-id="5095f-232">A generalized operating system image</span></span>
* <span data-ttu-id="5095f-233">Un disco di sistema operativo univoco</span><span class="sxs-lookup"><span data-stu-id="5095f-233">A unique operating system disk</span></span>
* <span data-ttu-id="5095f-234">Un disco dati</span><span class="sxs-lookup"><span data-stu-id="5095f-234">A data disk</span></span>

<span data-ttu-id="5095f-235">Di seguito vengono illustrati tre scenari per la preparazione dei dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="5095f-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="5095f-236">Uso di un disco rigido virtuale del sistema operativo generalizzato per creare più istanze di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5095f-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="5095f-237">Se si sta caricando un disco rigido virtuale che verrà utilizzato per creare più istanze di macchine virtuali di Azure generiche, è innanzitutto necessario generalizzare il disco rigido virtuale mediante un'utilità sysprep.</span><span class="sxs-lookup"><span data-stu-id="5095f-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="5095f-238">Tale utilità si applica a un disco rigido virtuale che si trova in locale o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="5095f-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="5095f-239">Sysprep consente di rimuovere eventuali informazioni specifiche sul computer dal disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5095f-240">Eseguire un'istantanea o il backup della macchina virtuale prima di generalizzarla.</span><span class="sxs-lookup"><span data-stu-id="5095f-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="5095f-241">L'esecuzione di sysprep eliminerà l'istanza della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="5095f-242">Eseguire i passaggi di seguito per utilizzare sysprep su un disco rigido virtuale di sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="5095f-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="5095f-243">Si noti che l’esecuzione del comando Sysprep richiederà di arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="5095f-244">Per altre informazioni su Sysprep, vedere la [panoramica di Sysprep](http://technet.microsoft.com/library/hh825209.aspx) oppure il [materiale di riferimento tecnico di Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="5095f-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="5095f-245">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5095f-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5095f-246">Immettere il comando seguente per aprire Sysprep:</span><span class="sxs-lookup"><span data-stu-id="5095f-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="5095f-247">Nell'Utilità preparazione sistema selezionare Enter System Out-of-Box Experience (OOBE), selezionare la casella di controllo Generalizza, selezionare **Arresto** e fare clic su **OK**, come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="5095f-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="5095f-248">Sysprep eseguirà la generalizzazione del sistema operativo e arresterà il sistema.</span><span class="sxs-lookup"><span data-stu-id="5095f-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="5095f-249">Per una VM Ubuntu, utilizzare virt-sysprep per ottenere lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="5095f-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="5095f-250">Vedere [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="5095f-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="5095f-251">Vedere alcuni [software open source di provisioning dei server Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) per altri sistemi operativi Linux.</span><span class="sxs-lookup"><span data-stu-id="5095f-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="5095f-252">Uso di un disco rigido virtuale di sistema operativo univoco per creare una singola istanza di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5095f-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="5095f-253">Se si dispone di un'applicazione in esecuzione nella macchina virtuale che richiede i dati specifici del computer, non generalizzare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="5095f-254">Un disco rigido virtuale non generalizzato può essere utilizzato per creare un'istanza univoca di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="5095f-255">Ad esempio, se si dispone di Controller di dominio sul disco rigido virtuale, l'esecuzione di sysprep lo renderà inefficace come controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="5095f-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="5095f-256">Rivedere le applicazioni in esecuzione sulla macchina virtuale e l'impatto dell'esecuzione di sysprep su di esse prima di generalizzare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="5095f-257">Registrare un disco rigido virtuale di dischi dati</span><span class="sxs-lookup"><span data-stu-id="5095f-257">Register data disk VHD</span></span>
<span data-ttu-id="5095f-258">Se si dispone di dischi dati in un'archiviazione di Azure di cui eseguire la migrazione, è necessario assicurarsi che le macchine virtuali che usano questi dischi dati vengano arrestate.</span><span class="sxs-lookup"><span data-stu-id="5095f-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="5095f-259">Attenersi alla procedura descritta di seguito per copiare il disco rigido virtuale in Archiviazione Premium di Azure e registrarlo come disco dati sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="5095f-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="5095f-260">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="5095f-260">Step 2.</span></span> <span data-ttu-id="5095f-261">Crea la destinazione per il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="5095f-261">Create the destination for your VHD</span></span>
<span data-ttu-id="5095f-262">Creare un account di archiviazione per mantenere i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="5095f-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="5095f-263">Considerare i seguenti punti quando si pianifica la posizione in cui archiviare i dischi rigidi virtuali:</span><span class="sxs-lookup"><span data-stu-id="5095f-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="5095f-264">L'account di archiviazione Premium di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-264">The target Premium storage account.</span></span>
* <span data-ttu-id="5095f-265">La posizione dell'account di archiviazione deve essere uguale a quella delle macchine virtuali supportate da Azure che saranno create nella fase finale.</span><span class="sxs-lookup"><span data-stu-id="5095f-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="5095f-266">È possibile eseguire la copia in un nuovo account di archiviazione oppure pianificare di utilizzare lo stesso account di archiviazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5095f-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="5095f-267">Copiare e salvare la chiave dell’account di archiviazione dell'account di archiviazione di destinazione per la fase successiva.</span><span class="sxs-lookup"><span data-stu-id="5095f-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="5095f-268">Per i dischi dati, è possibile scegliere di mantenerne alcuni in un account di archiviazione Standard, ad esempio, i dischi che dispongono di un'archiviazione meno problematica, ma è consigliabile spostare tutti i dati affinché il carico di lavoro di produzione usi l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="5095f-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="5095f-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="5095f-270">Copia del disco rigido virtuale con AzCopy o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5095f-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="5095f-271">Per elaborare una di queste due opzioni è necessario individuare il percorso del container e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="5095f-272">Il percorso del contenitore e la chiave dell'account di archiviazione sono reperibili in **Portale di Azure** > **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="5095f-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="5095f-273">L'URL del contenitore è simile a: "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="5095f-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="5095f-274">Opzione 1: copia di un disco rigido virtuale con AzCopy (copia asincrona)</span><span class="sxs-lookup"><span data-stu-id="5095f-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="5095f-275">Tramite AzCopy è possibile caricare facilmente il disco rigido virtuale in Internet.</span><span class="sxs-lookup"><span data-stu-id="5095f-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="5095f-276">A seconda della dimensione dei dischi rigidi virtuali, tale operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="5095f-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="5095f-277">Ricordarsi di verificare i limiti di ingresso/uscita dell’account di archiviazione quando si utilizza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5095f-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="5095f-278">Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="5095f-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="5095f-279">Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="5095f-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="5095f-280">Aprire Azure PowerShell e passare alla cartella in cui è installato AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5095f-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="5095f-281">Utilizzare il seguente comando per copiare il file di disco rigido virtuale da "Source" a "Destination".</span><span class="sxs-lookup"><span data-stu-id="5095f-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="5095f-282">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5095f-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="5095f-283">Di seguito sono riportate le descrizioni dei parametri utilizzati nel comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="5095f-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="5095f-284">**/Source: *&lt;source&gt;:*** percorso della cartella o URL del contenitore di archiviazione che contiene il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="5095f-285">**/SourceKey: *&lt;source-account-key&gt;:*** chiave dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="5095f-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="5095f-286">**/Dest: *&lt;destination&gt;:*** URL del contenitore di archiviazione in cui copiare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="5095f-287">**/DestKey: *&lt;dest-account-key&gt;:*** chiave dell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="5095f-288">**/Pattern: *&lt;file-name&gt;:*** specificare il nome file del disco rigido virtuale da copiare.</span><span class="sxs-lookup"><span data-stu-id="5095f-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="5095f-289">Per informazioni dettagliate sull'uso dello strumento AzCopy, vedere [Trasferire dati con l'utilità della riga di comando AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="5095f-290">Opzione 2: copia di un disco rigido virtuale con PowerShell (copia sincronizzata)</span><span class="sxs-lookup"><span data-stu-id="5095f-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="5095f-291">È anche possibile copiare il file VHD con il cmdlet di PowerShell Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="5095f-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="5095f-292">Usare il comando seguente in Azure PowerShell per copiare il disco VHD.</span><span class="sxs-lookup"><span data-stu-id="5095f-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="5095f-293">Sostituire i valori in <> con i valori corrispondenti dell'account di archiviazione di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="5095f-294">Per usare questo comando, è necessario un contenitore chiamato vhds nell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="5095f-295">Se il contenitore non esiste, crearne uno prima di eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="5095f-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="5095f-296">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5095f-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="5095f-297"><a name="scenario2"></a>Scenario 2: Migrazione di VM da altre piattaforme ad Archiviazione Premium di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="5095f-298">Se si esegue la migrazione del disco rigido virtuale dall’archiviazione cloud non Azure ad Azure, è necessario innanzitutto esportare il disco rigido virtuale in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="5095f-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="5095f-299">Copiare il percorso di origine completo della directory locale in cui è archiviato il disco rigido virtuale, quindi usare AzCopy per caricarlo in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="5095f-300">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="5095f-300">Step 1.</span></span> <span data-ttu-id="5095f-301">Esportare il disco rigido virtuale in una directory locale</span><span class="sxs-lookup"><span data-stu-id="5095f-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="5095f-302">Copia di un disco rigido virtuale da AWS</span><span class="sxs-lookup"><span data-stu-id="5095f-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="5095f-303">Se si utilizza AWS, esportare l'istanza EC2 in un disco rigido virtuale in un bucket Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="5095f-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="5095f-304">Seguire i passaggi descritti nella documentazione di Amazon per l'esportazione delle istanze di Amazon EC2 per installare lo strumento di interfaccia della riga di comando Amazon EC2 ed eseguire il comando create-instance-export-task per esportare l'istanza di EC2 in un file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="5095f-305">Assicurarsi di usare **VHD** per la variabile DISK&#95;IMAGE&#95;FORMAT quando si esegue il comando **create-instance-export-task**.</span><span class="sxs-lookup"><span data-stu-id="5095f-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="5095f-306">Il file di disco rigido virtuale esportato viene salvato nel bucket Amazon S3 indicato durante tale processo.</span><span class="sxs-lookup"><span data-stu-id="5095f-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="5095f-307">Scaricare il file di disco rigido virtuale dal bucket S3.</span><span class="sxs-lookup"><span data-stu-id="5095f-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="5095f-308">Selezionare il file del disco rigido virtuale e scegliere **Azioni** > **Download**.</span><span class="sxs-lookup"><span data-stu-id="5095f-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="5095f-309">Copia di un disco rigido virtuale da altri cloud non Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="5095f-310">Se si esegue la migrazione del disco rigido virtuale dall’archiviazione cloud non Azure ad Azure, è necessario innanzitutto esportare il disco rigido virtuale in una directory locale.</span><span class="sxs-lookup"><span data-stu-id="5095f-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="5095f-311">Copiare il percorso di origine completo della directory locale in cui è archiviato il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="5095f-312">Copia di un disco rigido virtuale da locale</span><span class="sxs-lookup"><span data-stu-id="5095f-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="5095f-313">Se si esegue la migrazione del disco rigido virtuale da un ambiente locale, è necessario il percorso di origine completo in cui è archiviato il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="5095f-314">Il percorso di origine può essere un percorso server o una condivisione file.</span><span class="sxs-lookup"><span data-stu-id="5095f-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="5095f-315">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="5095f-315">Step 2.</span></span> <span data-ttu-id="5095f-316">Crea la destinazione per il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="5095f-316">Create the destination for your VHD</span></span>
<span data-ttu-id="5095f-317">Creare un account di archiviazione per mantenere i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="5095f-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="5095f-318">Considerare i seguenti punti quando si pianifica la posizione in cui archiviare i dischi rigidi virtuali:</span><span class="sxs-lookup"><span data-stu-id="5095f-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="5095f-319">L'account di archiviazione di destinazione potrebbe essere standard o premium, a seconda delle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="5095f-320">L'area dell'account di archiviazione deve essere uguale a quella delle VM supportate da Azure che saranno create nella fase finale.</span><span class="sxs-lookup"><span data-stu-id="5095f-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="5095f-321">È possibile eseguire la copia in un nuovo account di archiviazione oppure pianificare di utilizzare lo stesso account di archiviazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5095f-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="5095f-322">Copiare e salvare la chiave dell’account di archiviazione dell'account di archiviazione di destinazione per la fase successiva.</span><span class="sxs-lookup"><span data-stu-id="5095f-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="5095f-323">È consigliabile spostare tutti i dati affinché il carico di lavoro di produzione usi l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="5095f-324">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="5095f-324">Step 3.</span></span> <span data-ttu-id="5095f-325">Caricare il disco rigido virtuale in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="5095f-326">Dopo avere creato il disco rigido virtuale nella directory locale, è possibile usare AzCopy o AzurePowerShell per caricare il file con estensione vhd in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="5095f-327">Di seguito sono fornite entrambe le opzioni:</span><span class="sxs-lookup"><span data-stu-id="5095f-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="5095f-328">Opzione 1: uso del comando Add-AzureVhd di Azure PowerShell per caricare il file con estensione vhd</span><span class="sxs-lookup"><span data-stu-id="5095f-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="5095f-329">Un esempio <Uri> potrebbe essere ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="5095f-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="5095f-330">Un esempio <FileInfo> potrebbe essere ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="5095f-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="5095f-331">Opzione 2: uso di AzCopy per caricare il file con estensione vhd</span><span class="sxs-lookup"><span data-stu-id="5095f-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="5095f-332">Tramite AzCopy è possibile caricare facilmente il disco rigido virtuale in Internet.</span><span class="sxs-lookup"><span data-stu-id="5095f-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="5095f-333">A seconda della dimensione dei dischi rigidi virtuali, tale operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="5095f-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="5095f-334">Ricordarsi di verificare i limiti di ingresso/uscita dell’account di archiviazione quando si utilizza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="5095f-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="5095f-335">Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="5095f-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="5095f-336">Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="5095f-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="5095f-337">Aprire Azure PowerShell e passare alla cartella in cui è installato AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5095f-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="5095f-338">Utilizzare il seguente comando per copiare il file di disco rigido virtuale da "Source" a "Destination".</span><span class="sxs-lookup"><span data-stu-id="5095f-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="5095f-339">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5095f-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="5095f-340">Di seguito sono riportate le descrizioni dei parametri utilizzati nel comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="5095f-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="5095f-341">**/Source: *&lt;source&gt;:*** percorso della cartella o URL del contenitore di archiviazione che contiene il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="5095f-342">**/SourceKey: *&lt;source-account-key&gt;:*** chiave dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="5095f-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="5095f-343">**/Dest: *&lt;destination&gt;:*** URL del contenitore di archiviazione in cui copiare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="5095f-344">**/DestKey: *&lt;dest-account-key&gt;:*** chiave dell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="5095f-345">**/BlobType:page:** specifica che la destinazione è un BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="5095f-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="5095f-346">**/Pattern: *&lt;file-name&gt;:*** specificare il nome file del disco rigido virtuale da copiare.</span><span class="sxs-lookup"><span data-stu-id="5095f-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="5095f-347">Per informazioni dettagliate sull'uso dello strumento AzCopy, vedere [Trasferire dati con l'utilità della riga di comando AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5095f-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="5095f-348">Altre opzioni per il caricamento di un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="5095f-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="5095f-349">È inoltre possibile caricare un disco rigido virtuale nell'account di archiviazione utilizzando uno dei seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="5095f-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="5095f-350">API Copy Blob di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="5095f-351">Caricamento di BLOB in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="5095f-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="5095f-352">Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="5095f-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="5095f-353">È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="5095f-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="5095f-354">È possibile usare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) per stimare il tempo in base alla dimensione dei dati e all'unità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5095f-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="5095f-355">Il servizio Importazione/esportazione può essere usato per eseguire la copia in un account di archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="5095f-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="5095f-356">Sarà necessario copiare dall'archiviazione standard all’account di archiviazione premium mediante uno strumento come AzCopy.</span><span class="sxs-lookup"><span data-stu-id="5095f-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="5095f-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Creare macchine virtuali di Azure tramite Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="5095f-358">Dopo aver caricato o copiato il disco rigido virtuale nell'account di archiviazione desiderato, seguire le istruzioni in questa sezione per registrare il disco rigido virtuale come immagine del sistema operativo oppure come disco del sistema operativo, a seconda dello scenario e quindi creare da esso un'istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="5095f-359">Il disco rigido virtuale del disco dati può essere collegato alla macchina virtuale una volta che questa è stata creata.</span><span class="sxs-lookup"><span data-stu-id="5095f-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="5095f-360">Al termine di questa sezione viene fornito un esempio di script di migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="5095f-361">Si tratta di uno script semplificato, che non corrisponde a tutti gli scenari.</span><span class="sxs-lookup"><span data-stu-id="5095f-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="5095f-362">Potrebbe essere necessario aggiornare lo script per farlo corrispondere allo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="5095f-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="5095f-363">Per verificare se lo script è adatto al proprio scenario, vedere [Esempio di script di migrazione](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="5095f-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="5095f-364">Elenco di controllo</span><span class="sxs-lookup"><span data-stu-id="5095f-364">Checklist</span></span>
1. <span data-ttu-id="5095f-365">Attendere il completamento della copia di tutti i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="5095f-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="5095f-366">Verificare che Archiviazione Premium sia disponibile nell'area in cui si eseguirà la migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="5095f-367">Decidere la nuova serie di VM da usare.</span><span class="sxs-lookup"><span data-stu-id="5095f-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="5095f-368">Dovrebbe supportare Archiviazione Premium, con una dimensione basata sulla disponibilità nell'area e sulle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="5095f-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="5095f-369">Decidere le dimensioni esatte della VM da usare.</span><span class="sxs-lookup"><span data-stu-id="5095f-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="5095f-370">Le dimensioni della VM devono essere abbastanza grandi da supportare tutti i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="5095f-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="5095f-371">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="5095f-371">E.g.</span></span> <span data-ttu-id="5095f-372">Se, ad esempio, ci sono 4 dischi dati, la macchina virtuale deve avere 2 o più memorie centrali.</span><span class="sxs-lookup"><span data-stu-id="5095f-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="5095f-373">Considerare anche la potenza di elaborazione, la memoria e la larghezza di banda di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="5095f-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="5095f-374">Creare un account di archiviazione Premium nell'area di destinazione</span><span class="sxs-lookup"><span data-stu-id="5095f-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="5095f-375">Questo account verrà usato per la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="5095f-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="5095f-376">Tenere a portata di mano i dettagli della VM corrente, inclusi l'elenco di dischi e i BLOB VHD corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="5095f-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="5095f-377">Preparare l'applicazione per il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="5095f-377">Prepare your application for downtime.</span></span> <span data-ttu-id="5095f-378">Per eseguire una migrazione senza problemi, è necessario arrestare ogni elaborazione nel sistema corrente.</span><span class="sxs-lookup"><span data-stu-id="5095f-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="5095f-379">Solo a quel punto lo stato sarà coerente e sarà possibile eseguire la migrazione alla nuova piattaforma.</span><span class="sxs-lookup"><span data-stu-id="5095f-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="5095f-380">La durata del tempo di inattività dipenderà dalla quantità di dati nei dischi di cui eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-381">Se si sta creando una VM di Azure Resource Manager da un disco rigido virtuale specializzato, fare riferimento a [questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) per la distribuzione della macchina virtuale di Resource Manager tramite un disco esistente.</span><span class="sxs-lookup"><span data-stu-id="5095f-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="5095f-382">Registrazione del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="5095f-382">Register your VHD</span></span>
<span data-ttu-id="5095f-383">Per creare una VM dal disco rigido virtuale del sistema operativo o collegare un disco dati a una nuova VM, è necessario innanzitutto registrarlo.</span><span class="sxs-lookup"><span data-stu-id="5095f-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="5095f-384">Seguire la procedura riportata di seguito, a seconda dello scenario del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="5095f-385">Disco rigido virtuale del sistema operativo generalizzato per creare più istanze di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="5095f-386">Dopo che il disco rigido virtuale dell'immagine del sistema operativo viene caricato nell'account di archiviazione, registrarlo come **immagine macchina virtuale di Azure** , in modo che sia possibile usarlo per creare una o più istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5095f-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="5095f-387">Utilizzare i cmdlet PowerShell riportati di seguito per registrare il disco rigido virtuale come immagine del sistema operativo di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="5095f-388">Fornire l'URL completo del contenitore in cui è stato copiato il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="5095f-389">Copiare e salvare il nome di questa nuova immagine di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="5095f-390">Nell'esempio precedente è *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="5095f-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="5095f-391">Disco rigido virtuale di sistema operativo univoco per creare una singola istanza di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="5095f-392">Dopo aver caricato il disco rigido virtuale di sistema operativo univoco nell'account di archiviazione, registrarlo come **disco del sistema operativo Azure** in modo che sia possibile usarlo per creare un'istanza di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="5095f-393">Utilizzare i cmdlet PowerShell riportati di seguito per registrare il disco rigido virtuale come disco del sistema operativo di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="5095f-394">Fornire l'URL completo del contenitore in cui è stato copiato il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="5095f-395">Copiare e salvare il nome di questo nuovo disco di sistema operativo di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="5095f-396">Nell'esempio precedente è *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="5095f-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="5095f-397">Disco rigido virtuale del disco dati da collegare alle nuove istanze di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="5095f-398">Dopo avere caricato il disco rigido virtuale del disco dati nell'account di archiviazione, registrarlo come disco dati Azure in modo che possa essere collegato alla nuova istanza di VM di Azure serie DS, serie DSv2 o serie GS.</span><span class="sxs-lookup"><span data-stu-id="5095f-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="5095f-399">Utilizzare i cmdlet PowerShell riportati di seguito per registrare il disco rigido virtuale come disco dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="5095f-400">Fornire l'URL completo del contenitore in cui è stato copiato il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="5095f-401">Copiare e salvare il nome di questo nuovo disco dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="5095f-402">Nell'esempio precedente è *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="5095f-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="5095f-403">Creare una macchina virtuale che supporti Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="5095f-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="5095f-404">Una volta che l'immagine del sistema operativo o il disco del sistema operativo sono registrati, creare una nuova VM di Azure della serie DS, DSv2 o GS.</span><span class="sxs-lookup"><span data-stu-id="5095f-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="5095f-405">Si utilizzerà l'immagine del sistema operativo o il nome del disco del sistema operativo registrato.</span><span class="sxs-lookup"><span data-stu-id="5095f-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="5095f-406">Selezionare il tipo di macchina virtuale dal livello Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="5095f-407">Nell'esempio riportato di seguito viene usata la dimensione della macchina virtuale *Standard_DS2*.</span><span class="sxs-lookup"><span data-stu-id="5095f-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-408">Aggiornare le dimensioni del disco per assicurarsi che corrispondano alla capacità, ai requisiti di prestazione e alle dimensioni dei dischi di Azure disponibili.</span><span class="sxs-lookup"><span data-stu-id="5095f-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="5095f-409">Seguire i cmdlet di PowerShell dettagliati indicati di seguito per creare la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5095f-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="5095f-410">Innanzitutto, impostare i parametri comuni:</span><span class="sxs-lookup"><span data-stu-id="5095f-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="5095f-411">Innanzitutto, creare un servizio cloud in cui verranno ospitate le nuove VM.</span><span class="sxs-lookup"><span data-stu-id="5095f-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="5095f-412">In secondo luogo, a seconda dello scenario, creare l'istanza di VM di Azure dall'immagine del sistema operativo o dal disco del sistema operativo registrato.</span><span class="sxs-lookup"><span data-stu-id="5095f-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="5095f-413">Disco rigido virtuale del sistema operativo generalizzato per creare più istanze di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="5095f-414">Creare le nuove istanze di macchine virtuali di Azure serie DS utilizzando l’ **immagine del sistema operativo Azure** registrata.</span><span class="sxs-lookup"><span data-stu-id="5095f-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="5095f-415">Specificare questo nome immagine del sistema operativo nella configurazione della macchina virtuale quando si crea la nuova macchina virtuale come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5095f-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="5095f-416">Disco rigido virtuale di sistema operativo univoco per creare una singola istanza di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="5095f-417">Creare una nuova istanza di macchina virtuale di Azure serie DS utilizzando il **disco del sistema operativo Azure** registrato.</span><span class="sxs-lookup"><span data-stu-id="5095f-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="5095f-418">Specificare questo nome disco del sistema operativo nella configurazione della macchina virtuale quando si crea la nuova macchina virtuale come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5095f-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="5095f-419">Specificare altre informazioni di macchina virtuale di Azure, ad esempio, un servizio cloud, l’area, l’account di archiviazione, il set di disponibilità e i criteri di memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="5095f-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="5095f-420">Si noti che l'istanza di macchina virtuale deve essere collocata con il sistema operativo o con i dischi dati associati, in modo che il servizio cloud, l'area e l'account di archiviazione selezionati si trovino tutti nella stessa posizione dei dischi rigidi virtuali sottostanti di questi dischi.</span><span class="sxs-lookup"><span data-stu-id="5095f-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="5095f-421">Collegare il disco dati</span><span class="sxs-lookup"><span data-stu-id="5095f-421">Attach data disk</span></span>
<span data-ttu-id="5095f-422">Infine, se sono stati registrati i dischi rigidi virtuali del disco dati, collegarli alla nuova macchina virtuale che supporta Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="5095f-423">Utilizzare il seguente cmdlet PowerShell per collegare il disco dati alla nuova macchina virtuale e specificare i criteri di memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="5095f-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="5095f-424">Nell'esempio riportato di seguito il criterio di memorizzazione nella cache è impostato su *ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="5095f-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="5095f-425">È possibile che per supportare l'applicazione siano necessari passaggi specifici che non sono illustrati in questa guida.</span><span class="sxs-lookup"><span data-stu-id="5095f-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="5095f-426">Controllo e pianificazione del backup</span><span class="sxs-lookup"><span data-stu-id="5095f-426">Checking and plan backup</span></span>
<span data-ttu-id="5095f-427">Una volta che la nuova VM è operativa, accedervi con lo stesso ID di accesso e la stessa password della VM originale e verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="5095f-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="5095f-428">Tutte le impostazioni, inclusi i volumi con striping, dovrebbero essere presenti nella nuova VM.</span><span class="sxs-lookup"><span data-stu-id="5095f-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="5095f-429">L'ultimo passaggio è la pianificazione del backup e della manutenzione per la nuova VM in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="5095f-430"><a name="a-sample-migration-script"></a>Esempio di script di migrazione</span><span class="sxs-lookup"><span data-stu-id="5095f-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="5095f-431">Se è necessario eseguire la migrazione di più VM, sarà utile l'automazione con gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5095f-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="5095f-432">Di seguito è riportato un esempio di script che automatizza la migrazione di una VM.</span><span class="sxs-lookup"><span data-stu-id="5095f-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="5095f-433">Tenere presente che lo script seguente è solo un esempio e che sono state formulate alcune ipotesi sui dischi VM correnti.</span><span class="sxs-lookup"><span data-stu-id="5095f-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="5095f-434">Potrebbe essere necessario aggiornare lo script per farlo corrispondere allo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="5095f-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="5095f-435">Presupposti:</span><span class="sxs-lookup"><span data-stu-id="5095f-435">The assumptions are:</span></span>

* <span data-ttu-id="5095f-436">Si stanno creando macchine virtuali di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="5095f-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="5095f-437">I dischi del sistema operativo e i dischi dati di origine si trovano nello stesso account di archiviazione e nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="5095f-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="5095f-438">Se i dischi del sistema operativo e i dischi dati non sono nella stessa posizione, è possibile usare AzCopy o Azure PowerShell per copiare i dischi rigidi virtuali nei contenitori e negli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="5095f-439">Fare riferimento al passaggio precedente: [Copia del disco rigido virtuale con AzCopy o PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="5095f-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="5095f-440">In alternativa,è possibile modificare lo script per adattarlo al proprio scenario, ma è consigliabile usare AzCopy o PowerShell poiché è più facile e veloce.</span><span class="sxs-lookup"><span data-stu-id="5095f-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="5095f-441">Di seguito viene fornito lo script di automazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-441">The automation script is provided below.</span></span> <span data-ttu-id="5095f-442">Sostituire il testo con le informazioni necessarie e aggiornare lo script affinché corrisponda a uno scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="5095f-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5095f-443">L'uso dello script esistente non mantiene la configurazione di rete della macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="5095f-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="5095f-444">In questo caso, è necessario riconfigurare le impostazioni di rete nelle macchine virtuali migrate.</span><span class="sxs-lookup"><span data-stu-id="5095f-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="5095f-445"><a name="optimization"></a>Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="5095f-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="5095f-446">La configurazione VM corrente potrebbe essere personalizzata per favorirne il funzionamento con i dischi standard,</span><span class="sxs-lookup"><span data-stu-id="5095f-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="5095f-447">ad esempio, per migliorare le prestazioni usando più dischi in un volume con striping.</span><span class="sxs-lookup"><span data-stu-id="5095f-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="5095f-448">Ad esempio, invece di usare 4 dischi diversi in Archiviazione Premium, sarà possibile ottimizzare il costo con un solo disco.</span><span class="sxs-lookup"><span data-stu-id="5095f-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="5095f-449">Le ottimizzazioni di questo tipo devono essere gestite singolarmente e, dopo la migrazione, sono necessari passaggi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="5095f-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="5095f-450">Esiste anche la possibilità che questo processo non funzioni bene per i database e le applicazioni che dipendono dal layout del disco definito durante la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="5095f-451">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="5095f-451">Preparation</span></span>
1. <span data-ttu-id="5095f-452">Completare la migrazione semplice descritta nella sezione più sopra.</span><span class="sxs-lookup"><span data-stu-id="5095f-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="5095f-453">Le ottimizzazioni verranno eseguite nella nuova VM dopo la migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="5095f-454">Definire le dimensioni dei nuovi dischi necessarie per la configurazione ottimizzata.</span><span class="sxs-lookup"><span data-stu-id="5095f-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="5095f-455">Determinare il mapping dei dischi/volumi correnti alle specifiche dei nuovi dischi.</span><span class="sxs-lookup"><span data-stu-id="5095f-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="5095f-456">Passaggi di esecuzione</span><span class="sxs-lookup"><span data-stu-id="5095f-456">Execution steps</span></span>
1. <span data-ttu-id="5095f-457">Creare i nuovi dischi con le dimensioni corrette nella VM di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="5095f-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="5095f-458">Accedere alla VM e copiare i dati dal volume corrente al nuovo disco di cui viene eseguito il mapping a tale volume.</span><span class="sxs-lookup"><span data-stu-id="5095f-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="5095f-459">Effettuare questa operazione per tutti i volumi correnti di cui è necessario eseguire il mapping a un nuovo disco.</span><span class="sxs-lookup"><span data-stu-id="5095f-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="5095f-460">Modificare quindi le impostazioni dell'applicazione in modo da passare ai nuovi dischi e scollegare i vecchi volumi.</span><span class="sxs-lookup"><span data-stu-id="5095f-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="5095f-461">Per ottimizzare l'applicazione e migliorare le prestazioni del disco, fare riferimento a [Ottimizzazione delle prestazioni dell'applicazione](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="5095f-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="5095f-462">Migrazioni delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="5095f-462">Application migrations</span></span>
<span data-ttu-id="5095f-463">I database e altre applicazioni complesse potrebbero richiedere particolari passaggi in base a quanto definito dal provider dell'applicazione per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="5095f-464">Vedere la documentazione relativa a ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="5095f-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="5095f-465">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="5095f-465">E.g.</span></span> <span data-ttu-id="5095f-466">è possibile in genere eseguire la migrazione dei database con il backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="5095f-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5095f-467">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5095f-467">Next steps</span></span>
<span data-ttu-id="5095f-468">Controllare le risorse seguenti per scenari specifici per la migrazione di macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="5095f-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="5095f-469">Eseguire la migrazione di macchine virtuali di Azure tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5095f-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="5095f-470">Creare e caricare un disco rigido virtuale Windows Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="5095f-470">Create and upload a Windows Server VHD to Azure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="5095f-471">Creazione e caricamento di un disco rigido virtuale contenente il sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="5095f-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="5095f-472">Migrazione di macchine virtuali da Amazon AWS a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="5095f-473">Inoltre, controllare le seguenti risorse per altre informazioni su Archiviazione di Azure e sulle macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="5095f-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="5095f-474">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="5095f-475">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="5095f-476">Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5095f-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
