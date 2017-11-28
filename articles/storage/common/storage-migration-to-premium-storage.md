---
title: macchine virtuali di aaaMigrating tooAzure archiviazione Premium | Documenti Microsoft
description: Eseguire la migrazione del tooAzure macchine virtuali esistenti, archiviazione Premium. Archiviazione Premium offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con I/O intensivo in esecuzione su Macchine virtuali di Azure.
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
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="1d6b9-104">Migrazione tooAzure archiviazione Premium (dischi non gestite)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-105">Questo articolo viene illustrato come una macchina virtuale che utilizza dischi standard non gestito tooa macchina virtuale che utilizza toomigrate non gestito i dischi premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="1d6b9-106">È consigliabile usare dischi gestiti di Azure per nuove macchine virtuali e convertire i dischi di toomanaged precedente dischi non gestito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="1d6b9-107">Account archiviazione sottostante dei dischi handle hello gestiti in modo non è necessario.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="1d6b9-108">Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="1d6b9-109">Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con I/O intensivo.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="1d6b9-110">È possibile sfruttare la velocità di hello e le prestazioni di questi dischi eseguendo la migrazione tooAzure dischi di macchina virtuale dell'applicazione archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="1d6b9-111">scopo di Hello di questa guida è toohelp nuovi utenti di archiviazione di Azure Premium migliori preparare toomake una transizione graduale da loro tooPremium sistema corrente di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="1d6b9-112">Guida di Hello indirizzi tre componenti principali di hello in questo processo:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="1d6b9-113">Pianificare la migrazione di hello tooPremium archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="1d6b9-114">Preparare e copia dischi rigidi virtuali (VHD) tooPremium archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="1d6b9-115">Creare una macchina virtuale di Azure usando Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="1d6b9-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="1d6b9-116">È possibile eseguire la migrazione di macchine virtuali da altri tooAzure piattaforme archiviazione Premium o eseguire la migrazione di macchine virtuali di Azure esistente da archiviazione Standard tooPremium archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="1d6b9-117">Questa guida illustra i passaggi per entrambi i due scenari.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="1d6b9-118">Seguire i passaggi di hello specificati nella sezione appropriata di hello a seconda dello scenario.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-119">Una panoramica delle funzionalità e dei prezzi di Archiviazione Premium è disponibile in [Archiviazione Premium: archiviazione dalle prestazioni elevate per carichi di lavoro di macchine virtuali di Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="1d6b9-120">È consigliabile eseguire la migrazione di un disco di macchina virtuale che richiedono tooAzure IOPS elevata archiviazione Premium per ottenere prestazioni ottimali per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="1d6b9-121">Se il disco non richiede un numero elevato di IOPS, è possibile limitare i costi mantenendolo in Archiviazione Standard, che archivia i dati dei dischi delle macchine virtuali in unità disco rigido (HDD) invece che in unità SSD.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="1d6b9-122">Completare il processo di migrazione hello nella sua interezza richiedano azioni aggiuntive prima e dopo i passaggi di hello forniti in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="1d6b9-123">Ad esempio la configurazione di reti virtuali o gli endpoint o apportare modifiche al codice all'interno di un'applicazione hello stesso che potrebbero richiedere tempi di inattività dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="1d6b9-124">Queste azioni sono univoci tooeach applicazione e si dovrebbero essere completate insieme ai passaggi hello forniti in questo tooPremium completo della transizione di hello toomake Guida archiviazione più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="1d6b9-125"><a name="plan-the-migration-to-premium-storage"></a>Pianificare la migrazione di hello tooPremium archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="1d6b9-126">In questa sezione garantisce che sono pronti toofollow passaggi della migrazione hello in questo articolo e consente di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1d6b9-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d6b9-127">Prerequisites</span></span>
* <span data-ttu-id="1d6b9-128">È necessaria una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-128">You will need an Azure subscription.</span></span> <span data-ttu-id="1d6b9-129">Se non è disponibile, è possibile creare una sottoscrizione di [valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) di un mese oppure visitare [Prezzi di Azure](https://azure.microsoft.com/pricing/) per altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="1d6b9-130">tooexecute i cmdlet di PowerShell, è necessario il modulo di Microsoft Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="1d6b9-131">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per hello installare istruzioni sull'installazione e punto.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="1d6b9-132">Quando si pianifica toouse macchine virtuali di Azure in esecuzione in archiviazione Premium, è necessario toouse hello macchine virtuali in grado di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="1d6b9-133">Con le VM che supportano Archiviazione Premium è possibile usare dischi sia di Archiviazione Standard che di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="1d6b9-134">I dischi di archiviazione Premium saranno disponibili con più tipi di macchine Virtuali in hello future.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="1d6b9-135">Per altre informazioni su tutte le dimensioni e su tutti i tipi di dischi disponibili per le macchine virtuali di Azure, vedere [Dimensioni delle macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Dimensioni dei servizi cloud](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="1d6b9-136">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="1d6b9-136">Considerations</span></span>
<span data-ttu-id="1d6b9-137">Una macchina virtuale di Azure supporta collegamento di più dischi di archiviazione Premium in modo che le applicazioni possono esistere fino a too256 TB di spazio di archiviazione per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="1d6b9-138">Con Archiviazione Premium le applicazioni possono raggiungere 80.000 IOPS (operazioni di input/output al secondo) per ogni macchina virtuale e 2000 MB al secondo di velocità effettiva dei dischi per ogni macchina virtuale, con una latenza estremamente bassa per le operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="1d6b9-139">Sono disponibili diverse opzioni in termini di macchine virtuali e dischi.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="1d6b9-140">In questa sezione è toohelp si toofind un'opzione più adatta al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="1d6b9-141">Dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1d6b9-141">VM sizes</span></span>
<span data-ttu-id="1d6b9-142">sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1d6b9-143">Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="1d6b9-144">Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="1d6b9-145">Dimensione disco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-145">Disk sizes</span></span>
<span data-ttu-id="1d6b9-146">È possibile usare cinque tipi di dischi con la VM, ognuno con limiti di velocità effettiva e IOP specifici.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="1d6b9-147">Prendere in considerazione questi limiti quando scegliendo il tipo di disco hello per la macchina virtuale in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="1d6b9-148">Tipo di disco Premium</span><span class="sxs-lookup"><span data-stu-id="1d6b9-148">Premium Disks Type</span></span>  | <span data-ttu-id="1d6b9-149">P10</span><span class="sxs-lookup"><span data-stu-id="1d6b9-149">P10</span></span>   | <span data-ttu-id="1d6b9-150">P20</span><span class="sxs-lookup"><span data-stu-id="1d6b9-150">P20</span></span>   | <span data-ttu-id="1d6b9-151">P30</span><span class="sxs-lookup"><span data-stu-id="1d6b9-151">P30</span></span>            | <span data-ttu-id="1d6b9-152">P40</span><span class="sxs-lookup"><span data-stu-id="1d6b9-152">P40</span></span>            | <span data-ttu-id="1d6b9-153">P50</span><span class="sxs-lookup"><span data-stu-id="1d6b9-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="1d6b9-154">Dimensioni disco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-154">Disk size</span></span>           | <span data-ttu-id="1d6b9-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="1d6b9-155">128 GB</span></span>| <span data-ttu-id="1d6b9-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="1d6b9-156">512 GB</span></span>| <span data-ttu-id="1d6b9-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="1d6b9-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="1d6b9-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="1d6b9-160">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-160">IOPS per disk</span></span>       | <span data-ttu-id="1d6b9-161">500</span><span class="sxs-lookup"><span data-stu-id="1d6b9-161">500</span></span>   | <span data-ttu-id="1d6b9-162">2300</span><span class="sxs-lookup"><span data-stu-id="1d6b9-162">2300</span></span>  | <span data-ttu-id="1d6b9-163">5000</span><span class="sxs-lookup"><span data-stu-id="1d6b9-163">5000</span></span>           | <span data-ttu-id="1d6b9-164">7500</span><span class="sxs-lookup"><span data-stu-id="1d6b9-164">7500</span></span>           | <span data-ttu-id="1d6b9-165">7500</span><span class="sxs-lookup"><span data-stu-id="1d6b9-165">7500</span></span>           | 
| <span data-ttu-id="1d6b9-166">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-166">Throughput per disk</span></span> | <span data-ttu-id="1d6b9-167">100 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-167">100 MB per second</span></span> | <span data-ttu-id="1d6b9-168">150 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-168">150 MB per second</span></span> | <span data-ttu-id="1d6b9-169">200 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-169">200 MB per second</span></span> | <span data-ttu-id="1d6b9-170">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-170">250 MB per second</span></span> | <span data-ttu-id="1d6b9-171">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-171">250 MB per second</span></span> |

<span data-ttu-id="1d6b9-172">A seconda del carico di lavoro, determinare se per la macchina virtuale in uso sono necessari dischi dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="1d6b9-173">È possibile collegare più dati persistenti dischi tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="1d6b9-174">Se necessario, è possibile eseguire lo striping tra hello dischi tooincrease hello capacità e prestazioni del volume hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="1d6b9-175">Per altre informazioni sullo striping del disco, vedere [qui](storage-premium-storage-performance.md#disk-striping). Se si esegue lo striping di dischi dati di Archiviazione Premium con [Spazi di archiviazione][4], è consigliabile configurare una colonna per ogni disco usato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="1d6b9-176">In caso contrario, hello complessivo delle prestazioni del volume con striping hello potrebbero essere inferiore al previsto a causa di toouneven distribuzione del traffico tra dischi hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="1d6b9-177">Per le macchine virtuali Linux è possibile utilizzare hello *mdadm* tooachieve utilità hello stesso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="1d6b9-178">Per informazioni dettagliate, vedere l'articolo sulla [configurazione del RAID software in Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="1d6b9-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="1d6b9-179">Obiettivi di scalabilità per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-179">Storage account scalability targets</span></span>
<span data-ttu-id="1d6b9-180">Account di archiviazione Premium sono hello seguenti obiettivi di scalabilità in aggiunta toohello [Azure obiettivi di scalabilità e prestazioni](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="1d6b9-181">Se i requisiti dell'applicazione superano obiettivi di scalabilità hello di un singolo account di archiviazione, compilare l'applicazione toouse più account di archiviazione e partizionare i dati in tali account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="1d6b9-182">Capacità account totale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-182">Total Account Capacity</span></span> | <span data-ttu-id="1d6b9-183">Larghezza di banda totale per un account di archiviazione con ridondanza locale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d6b9-184">Capacità disco : 35 TB</span><span class="sxs-lookup"><span data-stu-id="1d6b9-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="1d6b9-185">Capacità snapshot: 10 TB</span><span class="sxs-lookup"><span data-stu-id="1d6b9-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="1d6b9-186">Backup too50 Gigabit al secondo in entrata e in uscita</span><span class="sxs-lookup"><span data-stu-id="1d6b9-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="1d6b9-187">Per ulteriori informazioni sulle specifiche di archiviazione Premium di hello, estrarre [obiettivi di scalabilità e prestazioni quando si utilizza l'archiviazione Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="1d6b9-188">Criteri di memorizzazione nella cache su disco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-188">Disk caching policy</span></span>
<span data-ttu-id="1d6b9-189">Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="1d6b9-190">Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="1d6b9-191">Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="1d6b9-192">le impostazioni della cache di Hello per i dischi di dati esistente possono essere aggiornate mediante [portale Azure](https://portal.azure.com) o hello *- HostCaching* parametro di hello *Set-AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="1d6b9-193">Percorso</span><span class="sxs-lookup"><span data-stu-id="1d6b9-193">Location</span></span>
<span data-ttu-id="1d6b9-194">Selezionare una posizione in cui è disponibile il servizio Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="1d6b9-195">Per informazioni aggiornate sulle località disponibili, vedere [Prodotti in base all'area](https://azure.microsoft.com/regions/#services) .</span><span class="sxs-lookup"><span data-stu-id="1d6b9-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="1d6b9-196">Le macchine virtuali presenti in hello stessa area, come account di archiviazione che archivi hello dischi per hello VM offrirà prestazioni migliori rispetto a se si trovano in aree separate hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="1d6b9-197">Altre impostazioni di configurazione delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="1d6b9-198">Quando si crea una macchina virtuale di Azure, sarà richiesto tooconfigure determinate impostazioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="1d6b9-199">Tenere presente che alcune impostazioni sono fisse per la durata di hello di hello macchina virtuale, mentre è possibile modificare o aggiungere altri utenti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="1d6b9-200">Esaminare queste impostazioni di configurazione della macchina virtuale di Azure e assicurarsi che questi siano configurati in modo appropriato toomatch i requisiti del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="1d6b9-201">Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-201">Optimization</span></span>
<span data-ttu-id="1d6b9-202">L'articolo [Archiviazione Premium di Azure: progettata per prestazioni elevate](storage-premium-storage-performance.md) fornisce indicazioni per lo sviluppo di applicazioni a prestazioni elevate mediante l'Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="1d6b9-203">È possibile seguire le linee guida hello combinate con prestazioni migliori procedure consigliate applicabile tootechnologies utilizzati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="1d6b9-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparare e copiare i dischi rigidi virtuali (VHD) tooPremium archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="1d6b9-205">Hello seguente sezione vengono fornite linee guida per la preparazione di dischi rigidi virtuali dalla macchina virtuale e copia di dischi rigidi virtuali tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="1d6b9-206">Scenario 1: "in corso la migrazione tooAzure macchine virtuali di Azure esistente archiviazione Premium."</span><span class="sxs-lookup"><span data-stu-id="1d6b9-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="1d6b9-207">Scenario 2: "in corso la migrazione macchine virtuali da altri tooAzure piattaforme archiviazione Premium."</span><span class="sxs-lookup"><span data-stu-id="1d6b9-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="1d6b9-208">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d6b9-208">Prerequisites</span></span>
<span data-ttu-id="1d6b9-209">hello tooprepare dischi rigidi virtuali per la migrazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="1d6b9-210">Una sottoscrizione di Azure, un account di archiviazione e un contenitore di archiviazione account toowhich è possibile copiare il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="1d6b9-211">Si noti che l'account di archiviazione di destinazione hello può essere un account Standard o Premium archiviazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="1d6b9-212">Un hello toogeneralize strumento disco rigido virtuale se si prevede di toocreate più istanze di macchina virtuale da esso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="1d6b9-213">Ad esempio, sysprep per Windows o virt-sysprep per Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="1d6b9-214">Un strumento tooupload hello VHD file toohello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="1d6b9-215">Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) o utilizzare un [Esplora archivi Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="1d6b9-216">Questa guida viene descritto come copiare il disco rigido virtuale utilizzando lo strumento AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-217">Se si sceglie l'opzione copia sincrono con AzCopy, per ottenere prestazioni ottimali, copiare il disco rigido virtuale eseguendo uno di questi strumenti da una macchina virtuale di Azure in hello stessa regione dell'account di archiviazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="1d6b9-218">Se si copia un disco rigido virtuale da una macchina virtuale di Azure in un'area diversa, le prestazioni potrebbero essere più lente.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="1d6b9-219">Per copiare una grande quantità di dati in larghezza di banda limitata, prendere in considerazione [tramite servizio di importazione/esportazione di Azure hello, dati tootransfer tooBlob archiviazione](../storage-import-export-service.md); in questo modo si tootransfer i dati dal disco rigido shipping unità tooan Azure Data Center.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="1d6b9-220">È possibile utilizzare importazione/esportazione di Azure servizio toocopy dati tooa account di archiviazione standard solo hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="1d6b9-221">Una volta hello dati nell'account di archiviazione standard, è possibile utilizzare entrambi hello [API di copia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) o account di archiviazione di AzCopy tootransfer hello dati tooyour premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="1d6b9-222">Notare che Microsoft Azure supporta solo file di disco rigido virtuale a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="1d6b9-223">I file VHDX o i dischi rigidi virtuali dinamici non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="1d6b9-224">Se si dispone di un disco rigido virtuale dinamico, è possibile convertirlo toofixed dimensioni utilizzando hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="1d6b9-225"><a name="scenario1"></a>Scenario 1: "in corso la migrazione tooAzure macchine virtuali di Azure esistente archiviazione Premium."</span><span class="sxs-lookup"><span data-stu-id="1d6b9-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="1d6b9-226">Se si esegue la migrazione di macchine virtuali di Azure, hello arresta macchina virtuale esistente preparare i dischi rigidi virtuali per ogni tipo di hello del disco rigido virtuale desiderata e quindi copiare hello VHD con AzCopy o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="1d6b9-227">Hello VM deve toobe completamente verso il basso toomigrate uno stato pulito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="1d6b9-228">Sarà presente un tempo di inattività fino al completamento della migrazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="1d6b9-229">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-229">Step 1.</span></span> <span data-ttu-id="1d6b9-230">Preparare i dischi rigidi virtuali per la migrazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="1d6b9-231">Se si esegue la migrazione tooPremium macchine virtuali di Azure esistente archiviazione, potrebbe essere il disco rigido virtuale:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="1d6b9-232">Un'immagine del sistema operativo generalizzata</span><span class="sxs-lookup"><span data-stu-id="1d6b9-232">A generalized operating system image</span></span>
* <span data-ttu-id="1d6b9-233">Un disco di sistema operativo univoco</span><span class="sxs-lookup"><span data-stu-id="1d6b9-233">A unique operating system disk</span></span>
* <span data-ttu-id="1d6b9-234">Un disco dati</span><span class="sxs-lookup"><span data-stu-id="1d6b9-234">A data disk</span></span>

<span data-ttu-id="1d6b9-235">Di seguito vengono illustrati tre scenari per la preparazione dei dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="1d6b9-236">Utilizzare un toocreate disco rigido virtuale del sistema operativo generalizzato più istanze di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="1d6b9-237">Se si siano caricando un disco rigido virtuale che verrà utilizzato toocreate più istanze di macchina virtuale di Azure generiche, è innanzitutto necessario generalizzare VHD utilizzando un'utilità sysprep.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="1d6b9-238">Si applica tooa disco rigido virtuale che si trova in locale o nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="1d6b9-239">Sysprep consente di rimuove le informazioni specifiche del computer hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d6b9-240">Eseguire un'istantanea o il backup della macchina virtuale prima di generalizzarla.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="1d6b9-241">Interrompe e deallocare hello VM istanza in esecuzione sysprep.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="1d6b9-242">Attenersi alla procedura riportata di seguito toosysprep un disco rigido virtuale del sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="1d6b9-243">Si noti che esegue il comando di Sysprep hello richiederà tooshut macchina virtuale hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="1d6b9-244">Per altre informazioni su Sysprep, vedere la [panoramica di Sysprep](http://technet.microsoft.com/library/hh825209.aspx) oppure il [materiale di riferimento tecnico di Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="1d6b9-245">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="1d6b9-246">Immettere hello seguente tooopen comando Sysprep:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="1d6b9-247">Selezionare sistema immettere Out-of-Box configurazione guidata, casella di controllo selezionare hello Generalize hello System Preparation Tool, selezionare **arresto**, quindi fare clic su **OK**, come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="1d6b9-248">Sysprep verrà generalizzare hello del sistema operativo e arresta il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="1d6b9-249">Per una VM Ubuntu, utilizzare virt sysprep tooachieve hello stesso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="1d6b9-250">Vedere [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="1d6b9-251">Vedere anche alcune open source di hello [il Provisioning di Server Linux software](http://www.cyberciti.biz/tips/server-provisioning-software.html) per altri sistemi operativi Linux.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="1d6b9-252">Utilizzare un toocreate disco rigido virtuale del sistema operativo univoco di una singola istanza di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="1d6b9-253">Se si dispone di un'applicazione in esecuzione nella macchina virtuale che richiede dati specifici di hello macchina hello, non generalizzare hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="1d6b9-254">Un disco rigido virtuale generalizzato non può essere utilizzato toocreate un'unica istanza di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="1d6b9-255">Ad esempio, se si dispone di Controller di dominio sul disco rigido virtuale, l'esecuzione di sysprep lo renderà inefficace come controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="1d6b9-256">Esaminare le applicazioni di hello nella macchina virtuale e hello impatto dell'esecuzione di sysprep su di essi prima della generalizzazione hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="1d6b9-257">Registrare un disco rigido virtuale di dischi dati</span><span class="sxs-lookup"><span data-stu-id="1d6b9-257">Register data disk VHD</span></span>
<span data-ttu-id="1d6b9-258">Se dispone di dischi di dati in Azure toobe eseguita la migrazione, è necessario assicurarsi che macchine virtuali di hello che utilizzano questi dati vengono arrestati i dischi.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="1d6b9-259">Seguire i passaggi hello descritti di seguito toocopy VHD tooAzure archiviazione Premium e registrarlo come disco dati di provisioning.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="1d6b9-260">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-260">Step 2.</span></span> <span data-ttu-id="1d6b9-261">Creare hello destinazione per il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="1d6b9-262">Creare un account di archiviazione per mantenere i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="1d6b9-263">Considerare i seguenti punti quando si pianifica dove hello toostore i dischi rigidi virtuali:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="1d6b9-264">destinazione Hello account di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="1d6b9-265">posizione dell'account di archiviazione Hello deve essere uguale a archiviazione Premium macchine virtuali di Azure in grado di supportare verrà creato nella fase finale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="1d6b9-266">È possibile copiare il nuovo account di archiviazione tooa o hello toouse piano stesso account di archiviazione in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="1d6b9-267">Copiare e salvare una chiave di account di archiviazione hello hello destinazione dell'account di archiviazione per la fase successiva hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="1d6b9-268">Per i dischi dati, è possibile scegliere tookeep alcuni dischi dati in un account di archiviazione standard (ad esempio, i dischi che dispongono di archiviazione di dispositivo di raffreddamento), ma è fortemente consigliabile spostare tutti i dati per l'archiviazione premium toouse del carico di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="1d6b9-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="1d6b9-270">Copia del disco rigido virtuale con AzCopy o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6b9-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="1d6b9-271">Il percorso del contenitore e l'account tooprocess chiave una di queste due opzioni di archiviazione, sarà necessario toofind.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="1d6b9-272">Il percorso del contenitore e la chiave dell'account di archiviazione sono reperibili in **Portale di Azure** > **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="1d6b9-273">URL del contenitore Hello sarà ad esempio "https://myaccount.blob.core.windows.net/mycontainer/".</span><span class="sxs-lookup"><span data-stu-id="1d6b9-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="1d6b9-274">Opzione 1: copia di un disco rigido virtuale con AzCopy (copia asincrona)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="1d6b9-275">Utilizza AzCopy, è possibile caricare hello VHD su hello Internet.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="1d6b9-276">A seconda delle dimensioni di hello di hello dischi rigidi virtuali, l'operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="1d6b9-277">Quando si utilizza questa opzione, ricordare limiti di ingresso/uscita account di archiviazione di toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="1d6b9-278">Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="1d6b9-279">Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="1d6b9-280">Aprire Azure PowerShell e passare toohello cartella in cui è installato AzCopy.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="1d6b9-281">Comando che segue di hello utilizzare file di disco rigido virtuale toocopy hello "Origine" troppo "Destination".</span><span class="sxs-lookup"><span data-stu-id="1d6b9-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="1d6b9-282">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="1d6b9-283">Ecco le descrizioni dei parametri di hello utilizzati nel comando AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="1d6b9-284">**/ Origine:  *&lt;origine&gt;:***  percorso della cartella di hello o URL del contenitore dell'archiviazione che contiene hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="1d6b9-285">**/ SourceKey:  *&lt;chiave dell'account origine&gt;:***  chiave account di archiviazione dell'account di archiviazione di origine hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="1d6b9-286">**/ Dest:  *&lt;destinazione&gt;:***  toocopy URL contenitore di archiviazione hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="1d6b9-287">**/ DestKey:  *&lt;chiave dell'account dest&gt;:***  chiave account di archiviazione dell'account di archiviazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="1d6b9-288">**/ Modello:  *&lt;nome file&gt;:***  specifica il nome di file di hello di hello toocopy di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="1d6b9-289">Per informazioni dettagliate sull'uso di AzCopy strumento, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="1d6b9-290">Opzione 2: copia di un disco rigido virtuale con PowerShell (copia sincronizzata)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="1d6b9-291">È inoltre possibile copiare i file VHD hello utilizzando il cmdlet di PowerShell hello AzureStorageBlobCopy di inizio.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="1d6b9-292">Utilizzare hello comando seguente in Azure PowerShell toocopy disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="1d6b9-293">Sostituire i valori hello in <> con valori corrispondenti dall'account di archiviazione di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="1d6b9-294">toouse questo comando, è necessario disporre di un contenitore chiamato VHD nell'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="1d6b9-295">Se il contenitore di hello non esiste, crearlo prima di eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="1d6b9-296">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="1d6b9-297"><a name="scenario2"></a>Scenario 2: "in corso la migrazione macchine virtuali da altri tooAzure piattaforme archiviazione Premium."</span><span class="sxs-lookup"><span data-stu-id="1d6b9-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="1d6b9-298">Se si esegue la migrazione di disco rigido virtuale da tooAzure di archiviazione Cloud non Azure, è prima necessario esportare directory locale tooa di hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="1d6b9-299">Percorso di origine completo hello di disco rigido virtuale in cui è archiviato utile la directory locale hello e utilizzando quindi tooupload AzCopy è tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="1d6b9-300">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-300">Step 1.</span></span> <span data-ttu-id="1d6b9-301">Esportare la directory locale tooa di disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="1d6b9-302">Copia di un disco rigido virtuale da AWS</span><span class="sxs-lookup"><span data-stu-id="1d6b9-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="1d6b9-303">Se si utilizza AWS, esportare hello EC2 istanza tooa disco rigido virtuale in un bucket S3 Amazon.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="1d6b9-304">Seguire i passaggi di hello descritti nella documentazione di Amazon per lo strumento dell'interfaccia della riga di comando (CLI) di esportazione Amazon EC2 istanze tooinstall hello Amazon EC2 hello ed eseguire i file VHD hello comando create-istanza--attività di esportazione tooexport hello EC2 istanza tooa.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="1d6b9-305">Toouse assicurarsi di essere **VHD** per immagine disco hello &#95; &#95; Variabile formato quando si esegue hello **creare-istanza--attività di esportazione** comando.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="1d6b9-306">file disco rigido virtuale esportato Hello viene salvato nel bucket S3 Amazon hello che scelto durante il processo.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="1d6b9-307">Scaricare i file VHD hello da bucket S3 hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="1d6b9-308">File VHD hello selezionare, quindi **azioni** > **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="1d6b9-309">Copia di un disco rigido virtuale da altri cloud non Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="1d6b9-310">Se si esegue la migrazione di disco rigido virtuale da tooAzure di archiviazione Cloud non Azure, è prima necessario esportare directory locale tooa di hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="1d6b9-311">Copiare hello percorso di origine completo della directory locale di hello in cui sono archiviati i file VHD.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="1d6b9-312">Copia di un disco rigido virtuale da locale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="1d6b9-313">Se si esegue la migrazione di disco rigido virtuale da un ambiente locale, è necessario il percorso di origine completo hello in cui sono archiviati i file VHD.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="1d6b9-314">percorso di origine Hello potrebbe essere una condivisione di file o percorso del server.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="1d6b9-315">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-315">Step 2.</span></span> <span data-ttu-id="1d6b9-316">Creare hello destinazione per il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="1d6b9-317">Creare un account di archiviazione per mantenere i dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="1d6b9-318">Considerare i seguenti punti quando si pianifica dove hello toostore i dischi rigidi virtuali:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="1d6b9-319">account di archiviazione di destinazione Hello potrebbe essere archiviazione standard o premium in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="1d6b9-320">area dell'account di archiviazione Hello deve corrispondere all'archiviazione Premium macchine virtuali di Azure in grado di supportare verrà creato in fase di hello finale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="1d6b9-321">È possibile copiare il nuovo account di archiviazione tooa o hello toouse piano stesso account di archiviazione in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="1d6b9-322">Copiare e salvare una chiave di account di archiviazione hello hello destinazione dell'account di archiviazione per la fase successiva hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="1d6b9-323">È fortemente consigliabile spostare tutti i dati per l'archiviazione premium toouse del carico di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="1d6b9-324">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-324">Step 3.</span></span> <span data-ttu-id="1d6b9-325">Caricare hello VHD tooAzure archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="1d6b9-326">Dopo avere creato il disco rigido virtuale nella directory locale hello, è possibile utilizzare AzCopy o AzurePowerShell tooupload hello VHD file tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="1d6b9-327">Di seguito sono fornite entrambe le opzioni:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="1d6b9-328">Opzione 1: Utilizzo di file con estensione vhd di Azure PowerShell Add-AzureVhd tooupload hello</span><span class="sxs-lookup"><span data-stu-id="1d6b9-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="1d6b9-329">Un esempio <Uri> potrebbe essere ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="1d6b9-330">Un esempio <FileInfo> potrebbe essere ***"C:\path\to\upload.vhd"***.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="1d6b9-331">Opzione 2: Utilizzo di file con estensione vhd hello tooupload AzCopy</span><span class="sxs-lookup"><span data-stu-id="1d6b9-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="1d6b9-332">Utilizza AzCopy, è possibile caricare hello VHD su hello Internet.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="1d6b9-333">A seconda delle dimensioni di hello di hello dischi rigidi virtuali, l'operazione potrebbe richiedere tempo.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="1d6b9-334">Quando si utilizza questa opzione, ricordare limiti di ingresso/uscita account di archiviazione di toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="1d6b9-335">Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="1d6b9-336">Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="1d6b9-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="1d6b9-337">Aprire Azure PowerShell e passare toohello cartella in cui è installato AzCopy.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="1d6b9-338">Comando che segue di hello utilizzare file di disco rigido virtuale toocopy hello "Origine" troppo "Destination".</span><span class="sxs-lookup"><span data-stu-id="1d6b9-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="1d6b9-339">Esempio:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="1d6b9-340">Ecco le descrizioni dei parametri di hello utilizzati nel comando AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="1d6b9-341">**/ Origine:  *&lt;origine&gt;:***  percorso della cartella di hello o URL del contenitore dell'archiviazione che contiene hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="1d6b9-342">**/ SourceKey:  *&lt;chiave dell'account origine&gt;:***  chiave account di archiviazione dell'account di archiviazione di origine hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="1d6b9-343">**/ Dest:  *&lt;destinazione&gt;:***  toocopy URL contenitore di archiviazione hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="1d6b9-344">**/ DestKey:  *&lt;chiave dell'account dest&gt;:***  chiave account di archiviazione dell'account di archiviazione di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="1d6b9-345">**/ BlobType: pagina:** specifica tale destinazione hello è un blob di pagine.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="1d6b9-346">**/ Modello:  *&lt;nome file&gt;:***  specifica il nome di file di hello di hello toocopy di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="1d6b9-347">Per informazioni dettagliate sull'uso di AzCopy strumento, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="1d6b9-348">Altre opzioni per il caricamento di un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="1d6b9-349">È inoltre possibile caricare un account di archiviazione tooyour disco rigido virtuale utilizzando uno dei hello seguente indica:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="1d6b9-350">API Copy Blob di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="1d6b9-351">Caricamento di BLOB in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="1d6b9-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="1d6b9-352">Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="1d6b9-353">È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="1d6b9-354">È possibile utilizzare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) ora hello tooestimate dall'unità di dimensioni e il trasferimento di dati.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="1d6b9-355">Importazione/esportazione può essere utilizzato l'account di archiviazione standard tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="1d6b9-356">Sarà necessario toocopy dall'account di archiviazione toopremium archiviazione standard usando uno strumento come AzCopy.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="1d6b9-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Creare macchine virtuali di Azure tramite Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="1d6b9-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="1d6b9-358">Dopo aver hello VHD caricato o copiato toohello desiderato account di archiviazione, seguire le istruzioni hello questo hello tooregister sezione VHD come immagine del sistema operativo o il disco del sistema operativo a seconda dello scenario e quindi creare un'istanza di macchina virtuale da esso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="1d6b9-359">disco dati Hello disco rigido virtuale può essere collegato toohello macchina virtuale dopo averla creata.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="1d6b9-360">Un esempio di script di migrazione viene fornito alla fine di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="1d6b9-361">Si tratta di uno script semplificato, che non corrisponde a tutti gli scenari.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="1d6b9-362">Potrebbe essere necessario tooupdate hello script toomatch con il proprio scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="1d6b9-363">toosee se questo script si applica tooyour scenario, vedere di seguito [Script di migrazione di un esempio](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="1d6b9-364">Elenco di controllo</span><span class="sxs-lookup"><span data-stu-id="1d6b9-364">Checklist</span></span>
1. <span data-ttu-id="1d6b9-365">Attendere fino a quando tutti i dischi rigidi Virtuali hello copia è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="1d6b9-366">Verificare che l'archiviazione Premium è disponibile nell'area di hello a che esegue la migrazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="1d6b9-367">Decidere hello nuova serie di macchine Virtuali che verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="1d6b9-368">Deve essere uno spazio di archiviazione Premium in grado di supportare e hello dimensioni devono essere a seconda della disponibilità di hello in area hello e in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="1d6b9-369">Decidere hello esatta dimensioni delle macchine Virtuali che si utilizzerà.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="1d6b9-370">Dimensioni della macchina virtuale devono numero di hello toobe toosupport sufficiente di dischi dati che si dispone.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="1d6b9-371">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="1d6b9-371">E.g.</span></span> <span data-ttu-id="1d6b9-372">Se si dispone di 4 dischi dati, hello macchina virtuale deve disporre di 2 o più core.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="1d6b9-373">Considerare anche la potenza di elaborazione, la memoria e la larghezza di banda di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="1d6b9-374">Creare un account di archiviazione Premium nell'area di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="1d6b9-375">Si tratta di account hello che verrà utilizzato per hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="1d6b9-376">Dispone di hello corrente VM informazioni utili, tra cui hello elenco di dischi e i BLOB VHD corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="1d6b9-377">Preparare l'applicazione per il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-377">Prepare your application for downtime.</span></span> <span data-ttu-id="1d6b9-378">toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="1d6b9-379">Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="1d6b9-380">Durata inattività dipenderà hello quantità di dati in toomigrate dischi hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-381">Se si sta creando una VM di Azure Resource Manager da un disco specializzato di disco rigido virtuale, fare riferimento troppo[questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) per la distribuzione di VM Resource Manager utilizzando un disco esistente.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="1d6b9-382">Registrazione del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6b9-382">Register your VHD</span></span>
<span data-ttu-id="1d6b9-383">una macchina virtuale dal disco rigido virtuale del sistema operativo o un tooa disco dati tooattach toocreate nuova macchina virtuale, è necessario prima registrarli.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="1d6b9-384">Seguire la procedura riportata di seguito, a seconda dello scenario del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="1d6b9-385">Generalizzato toocreate disco rigido virtuale del sistema operativo più istanze di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="1d6b9-386">Dopo aver generalizzato immagine del sistema operativo è di disco rigido virtuale caricato toohello account di archiviazione, registrarlo come un **immagine di macchina virtuale di Azure** in modo che è possibile creare uno o più istanze di macchina virtuale da esso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="1d6b9-387">Utilizzare il disco rigido virtuale di hello tooregister i cmdlet di PowerShell seguente come un'immagine del sistema operativo VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="1d6b9-388">Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="1d6b9-389">Copiare e salvare il nome di hello di questa nuova immagine di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="1d6b9-390">Nell'esempio hello sopra, è *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="1d6b9-391">Toocreate disco rigido virtuale del sistema operativo univoco una singola istanza di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="1d6b9-392">Dopo aver hello univoco disco rigido virtuale del sistema operativo è caricato toohello archiviazione conto, registrarlo come un **disco del sistema operativo Azure** in modo che è possibile creare un'istanza di macchina virtuale da esso.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="1d6b9-393">Utilizzare queste tooregister i cmdlet di PowerShell il disco rigido virtuale come disco del sistema operativo Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="1d6b9-394">Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="1d6b9-395">Copiare e salvare il nome di hello del nuovo disco del sistema operativo Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="1d6b9-396">Nell'esempio hello sopra, è *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="1d6b9-397">Toobe di disco rigido virtuale del disco dati collegato toonew delle istanze di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="1d6b9-398">Una volta hello disco dati è di disco rigido virtuale caricato toostorage account, registrarlo come un disco dati di Azure in modo che possa essere allegato tooyour nuova serie DS, DSv2 serie o istanza di macchina virtuale di Azure serie GS.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="1d6b9-399">Utilizzare queste tooregister i cmdlet di PowerShell il disco rigido virtuale come un disco dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="1d6b9-400">Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="1d6b9-401">Copiare e salvare il nome di hello di questo nuovo disco dati di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="1d6b9-402">Nell'esempio hello sopra, è *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="1d6b9-403">Creare una macchina virtuale che supporti Archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="1d6b9-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="1d6b9-404">Una volta hello immagine del sistema operativo o disco del sistema operativo sono registrati, creare una nuova serie DS, DSv2-series o GS-series VM.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="1d6b9-405">Si utilizzerà immagine del sistema operativo hello o nome del disco del sistema operativo è stato registrato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="1d6b9-406">Selezionare il tipo di macchina virtuale hello dal livello di archiviazione Premium hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="1d6b9-407">Nell'esempio seguente, usiamo hello *Standard_DS2* dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-408">Aggiornare hello disco dimensioni toomake verificarne che la corrispondenza, la capacità e requisiti di prestazioni e le dimensioni di hello disponibile su disco di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="1d6b9-409">Cmdlet di PowerShell seguente hello dettagliate sotto toocreate hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="1d6b9-410">Innanzitutto, impostare i parametri comuni di hello:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="1d6b9-411">Innanzitutto, creare un servizio cloud in cui verranno ospitate le nuove VM.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="1d6b9-412">Successivamente, a seconda dello scenario, creare hello macchina virtuale di Azure da hello immagine del sistema operativo o disco del sistema operativo che è stato registrato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="1d6b9-413">Generalizzato toocreate disco rigido virtuale del sistema operativo più istanze di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="1d6b9-414">Creare uno o più nuove macchine Virtuali di Azure serie DS istanze utilizzando hello di hello **immagine del sistema operativo Azure** registrato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="1d6b9-415">Questo nome di immagine del sistema operativo specificato nella configurazione della macchina virtuale hello durante la creazione nuova macchina virtuale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="1d6b9-416">Toocreate disco rigido virtuale del sistema operativo univoco una singola istanza di macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="1d6b9-417">Creare una nuova istanza VM Azure serie DS utilizzando hello **disco del sistema operativo Azure** registrato.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="1d6b9-418">Specificare il nome del disco del sistema operativo nella configurazione della macchina virtuale hello durante la creazione di hello nuova macchina virtuale, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="1d6b9-419">Specificare altre informazioni di macchina virtuale di Azure, ad esempio, un servizio cloud, l’area, l’account di archiviazione, il set di disponibilità e i criteri di memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="1d6b9-420">Si noti che istanza hello della macchina virtuale deve essere condiviso con sistema operativo associato o dischi dati, pertanto l'account di servizio, area e di archiviazione cloud hello selezionato deve essere hello stesso percorso hello sottostante dischi rigidi virtuali di questi dischi.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="1d6b9-421">Collegare il disco dati</span><span class="sxs-lookup"><span data-stu-id="1d6b9-421">Attach data disk</span></span>
<span data-ttu-id="1d6b9-422">Infine, se sono state registrate dati su disco di dischi rigidi virtuali, collegarli toohello nuova VM di Azure in grado di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="1d6b9-423">Utilizzare le seguenti PowerShell cmdlet tooattach dati disco toohello nuova macchina virtuale e specificare i criteri di memorizzazione nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="1d6b9-424">Nell'esempio riportato di seguito hello criteri di memorizzazione nella cache è troppo*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="1d6b9-425">Potrebbero essere presenti ulteriori passaggi necessari toosupport l'applicazione che non rientrano in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="1d6b9-426">Controllo e pianificazione del backup</span><span class="sxs-lookup"><span data-stu-id="1d6b9-426">Checking and plan backup</span></span>
<span data-ttu-id="1d6b9-427">Una volta hello nuova macchina virtuale è in esecuzione, l'accesso tramite hello stesso id di accesso e password come hello macchina virtuale originale e verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="1d6b9-428">Tutte le impostazioni di hello, inclusi i volumi con striping hello, può essere incluso in hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="1d6b9-429">ultimo passaggio Hello è tooplan pianificazione di backup e manutenzione per la nuova macchina virtuale in base alle esigenze dell'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="1d6b9-430"><a name="a-sample-migration-script"></a>Esempio di script di migrazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="1d6b9-431">Se si dispone di più macchine virtuali toomigrate, saranno utili automazione tramite gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="1d6b9-432">Di seguito è uno script di esempio che consente di automatizzare la migrazione di hello di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="1d6b9-433">Si noti che gli script seguente è solo un esempio e sono presenti alcuni presupposti presenti sui dischi di macchina virtuale correnti hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="1d6b9-434">Potrebbe essere necessario tooupdate hello script toomatch con il proprio scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="1d6b9-435">presupposti Hello sono:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-435">hello assumptions are:</span></span>

* <span data-ttu-id="1d6b9-436">Si stanno creando macchine virtuali di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="1d6b9-437">I dischi del sistema operativo e i dischi dati di origine si trovano nello stesso account di archiviazione e nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="1d6b9-438">Se i dischi del sistema operativo e i dischi di dati non sono nello stesso hello inserito, è possibile usare AzCopy o Azure PowerShell toocopy dischi rigidi virtuali tramite gli account di archiviazione e i contenitori.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="1d6b9-439">Fare riferimento passaggio precedente toohello: [copia dei dischi rigidi Virtuali con PowerShell o di AzCopy](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="1d6b9-440">Modifica questa toomeet script lo scenario è un'altra scelta, ma è consigliabile usare AzCopy o PowerShell in quanto è più facile e veloce.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="1d6b9-441">script di automazione Hello di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-441">hello automation script is provided below.</span></span> <span data-ttu-id="1d6b9-442">Sostituire il testo con le informazioni necessarie e aggiornare hello script toomatch con il proprio scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b9-443">Utilizzando uno script esistente hello non mantiene la configurazione di rete hello dell'origine di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="1d6b9-444">È necessario toore-config le impostazioni di rete hello in macchine virtuali migrate.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="1d6b9-445"><a name="optimization"></a>Ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="1d6b9-446">Configurazione della macchina virtuale corrente può essere personalizzata in modo specifico toowork anche con dischi Standard.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="1d6b9-447">Ad esempio, tooincrease hello delle prestazioni con numero di dischi in un volume con striping.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="1d6b9-448">Anziché 4 dischi separatamente in archiviazione Premium, ad esempio, potrebbe essere il costo di hello toooptimize in grado di con un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="1d6b9-449">Le ottimizzazioni come questo toobe necessità gestito sul caso per caso e richiedono istruzioni personalizzate dopo la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="1d6b9-450">Inoltre, si noti che questo processo potrebbe non funzionare bene per i database e applicazioni che dipendono dal layout del disco hello definita nel programma di installazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="1d6b9-451">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="1d6b9-451">Preparation</span></span>
1. <span data-ttu-id="1d6b9-452">Hello completo migrazione semplice, come descritto in hello precedente sezione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="1d6b9-453">Verranno eseguite le ottimizzazioni su hello nuova macchina virtuale dopo la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="1d6b9-454">Definire dimensioni disco nuovo hello richiesto hello con ottimizzazione per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="1d6b9-455">Determinare il mapping di hello dischi o volumi toohello nuovo disco specifiche correnti.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="1d6b9-456">Passaggi di esecuzione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-456">Execution steps</span></span>
1. <span data-ttu-id="1d6b9-457">Creare hello nuovi dischi con dimensioni corrette di hello in hello macchina virtuale di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="1d6b9-458">Account di accesso toohello macchina virtuale e copia hello i dati da hello corrente toohello nuovo disco del volume che esegue il mapping toothat volume.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="1d6b9-459">Questa operazione per tutti i volumi corrente hello necessarie toomap tooa nuovo disco.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="1d6b9-460">Successivamente, modificare hello applicazione impostazioni tooswitch toohello nuovi dischi e volumi hello scollegare.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="1d6b9-461">Per l'ottimizzazione di un'applicazione hello per migliorare le prestazioni del disco, fare riferimento troppo[ottimizzazione delle prestazioni dell'applicazione](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="1d6b9-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="1d6b9-462">Migrazioni delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="1d6b9-462">Application migrations</span></span>
<span data-ttu-id="1d6b9-463">I database e altre applicazioni complesse potrebbero essere necessari passaggi speciali come definito dal provider dell'applicazione hello per la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="1d6b9-464">Consultare la documentazione dell'applicazione toorespective.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="1d6b9-465">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="1d6b9-465">E.g.</span></span> <span data-ttu-id="1d6b9-466">è possibile in genere eseguire la migrazione dei database con il backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d6b9-467">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d6b9-467">Next steps</span></span>
<span data-ttu-id="1d6b9-468">Vedere hello risorse per scenari specifici per la migrazione di macchine virtuale seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="1d6b9-469">Eseguire la migrazione di macchine virtuali di Azure tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1d6b9-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="1d6b9-470">Creare e caricare tooAzure un disco rigido virtuale di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1d6b9-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="1d6b9-471">Creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux</span><span class="sxs-lookup"><span data-stu-id="1d6b9-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="1d6b9-472">Migrazione di macchine virtuali da Amazon AWS tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="1d6b9-473">Vedere anche hello seguenti risorse toolearn ulteriori informazioni sull'archiviazione di Azure e macchine virtuali di Azure:</span><span class="sxs-lookup"><span data-stu-id="1d6b9-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="1d6b9-474">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="1d6b9-475">Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="1d6b9-476">Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1d6b9-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
