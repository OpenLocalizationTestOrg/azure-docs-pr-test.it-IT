---
title: aaaMigrate tooan una VM classico ARM gestiti disco VM | Documenti Microsoft
description: Eseguire la migrazione di una singola macchina virtuale di Azure dalla distribuzione classica hello tooManaged dischi nel modello di distribuzione di gestione risorse di hello del modello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="10de6-103">Eseguire la migrazione manuale di un tooa VM classico nuova ARM gestiti disco macchina virtuale dal disco rigido virtuale hello</span><span class="sxs-lookup"><span data-stu-id="10de6-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="10de6-104">Questa sezione viene spiegato si toomigrate le macchine virtuali di Azure esistente dal modello di distribuzione classica hello troppo[dischi gestiti](managed-disks-overview.md) nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="10de6-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="10de6-105">Pianificare la migrazione di hello di dischi tooManaged</span><span class="sxs-lookup"><span data-stu-id="10de6-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="10de6-106">In questa sezione contribuisce di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.</span><span class="sxs-lookup"><span data-stu-id="10de6-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="10de6-107">Percorso</span><span class="sxs-lookup"><span data-stu-id="10de6-107">Location</span></span>

<span data-ttu-id="10de6-108">Selezionare una posizione in cui Azure Managed Disks è disponibile.</span><span class="sxs-lookup"><span data-stu-id="10de6-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="10de6-109">Se si esegue la migrazione di dischi gestiti tooPremium, assicurarsi anche che l'archiviazione Premium è disponibile nell'area di hello in cui si intende toomigrate per.</span><span class="sxs-lookup"><span data-stu-id="10de6-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="10de6-110">Per informazioni aggiornate sulle località disponibili, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="10de6-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="10de6-111">Dimensioni delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="10de6-111">VM sizes</span></span>

<span data-ttu-id="10de6-112">Se si esegue la migrazione di dischi gestiti tooPremium, è pari a hello tooupdate hello VM tooPremium dimensioni in grado di archiviazione disponibile nell'area di hello macchina virtuale in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="10de6-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="10de6-113">Esaminare le dimensioni VM hello che sono in grado di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="10de6-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="10de6-114">sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="10de6-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="10de6-115">Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10de6-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="10de6-116">Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.</span><span class="sxs-lookup"><span data-stu-id="10de6-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="10de6-117">Dimensione disco</span><span class="sxs-lookup"><span data-stu-id="10de6-117">Disk sizes</span></span>

<span data-ttu-id="10de6-118">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="10de6-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="10de6-119">È possibile usare sette tipi di dischi gestiti della versione Premium con la macchina virtuale, ognuno con limiti IOP e di velocità effettiva specifici.</span><span class="sxs-lookup"><span data-stu-id="10de6-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="10de6-120">Considerare questi limiti quando si sceglie il tipo di disco Premium per la macchina virtuale hello in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.</span><span class="sxs-lookup"><span data-stu-id="10de6-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="10de6-121">Tipo di disco Premium</span><span class="sxs-lookup"><span data-stu-id="10de6-121">Premium Disks Type</span></span>  | <span data-ttu-id="10de6-122">P4</span><span class="sxs-lookup"><span data-stu-id="10de6-122">P4</span></span>    | <span data-ttu-id="10de6-123">P6</span><span class="sxs-lookup"><span data-stu-id="10de6-123">P6</span></span>    | <span data-ttu-id="10de6-124">P10</span><span class="sxs-lookup"><span data-stu-id="10de6-124">P10</span></span>   | <span data-ttu-id="10de6-125">P20</span><span class="sxs-lookup"><span data-stu-id="10de6-125">P20</span></span>   | <span data-ttu-id="10de6-126">P30</span><span class="sxs-lookup"><span data-stu-id="10de6-126">P30</span></span>   | <span data-ttu-id="10de6-127">P40</span><span class="sxs-lookup"><span data-stu-id="10de6-127">P40</span></span>   | <span data-ttu-id="10de6-128">P50</span><span class="sxs-lookup"><span data-stu-id="10de6-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="10de6-129">Dimensioni disco</span><span class="sxs-lookup"><span data-stu-id="10de6-129">Disk size</span></span>           | <span data-ttu-id="10de6-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-130">128 GB</span></span>| <span data-ttu-id="10de6-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-131">512 GB</span></span>| <span data-ttu-id="10de6-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-132">128 GB</span></span>| <span data-ttu-id="10de6-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-133">512 GB</span></span>            | <span data-ttu-id="10de6-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="10de6-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="10de6-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="10de6-137">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="10de6-137">IOPS per disk</span></span>       | <span data-ttu-id="10de6-138">120</span><span class="sxs-lookup"><span data-stu-id="10de6-138">120</span></span>   | <span data-ttu-id="10de6-139">240</span><span class="sxs-lookup"><span data-stu-id="10de6-139">240</span></span>   | <span data-ttu-id="10de6-140">500</span><span class="sxs-lookup"><span data-stu-id="10de6-140">500</span></span>   | <span data-ttu-id="10de6-141">2300</span><span class="sxs-lookup"><span data-stu-id="10de6-141">2300</span></span>              | <span data-ttu-id="10de6-142">5000</span><span class="sxs-lookup"><span data-stu-id="10de6-142">5000</span></span>              | <span data-ttu-id="10de6-143">7500</span><span class="sxs-lookup"><span data-stu-id="10de6-143">7500</span></span>              | <span data-ttu-id="10de6-144">7500</span><span class="sxs-lookup"><span data-stu-id="10de6-144">7500</span></span>              | 
| <span data-ttu-id="10de6-145">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="10de6-145">Throughput per disk</span></span> | <span data-ttu-id="10de6-146">25 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-146">25 MB per second</span></span>  | <span data-ttu-id="10de6-147">50 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-147">50 MB per second</span></span>  | <span data-ttu-id="10de6-148">100 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-148">100 MB per second</span></span> | <span data-ttu-id="10de6-149">150 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-149">150 MB per second</span></span> | <span data-ttu-id="10de6-150">200 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-150">200 MB per second</span></span> | <span data-ttu-id="10de6-151">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-151">250 MB per second</span></span> | <span data-ttu-id="10de6-152">250 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-152">250 MB per second</span></span> | 

<span data-ttu-id="10de6-153">**Managed Disks Standard**</span><span class="sxs-lookup"><span data-stu-id="10de6-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="10de6-154">Esistono sette tipi di dischi gestiti della versione Standard che possono essere usati con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10de6-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="10de6-155">Si differenziano per capacità ma presentano gli stessi limiti IOP e di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="10de6-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="10de6-156">Scegliere il tipo di hello di dischi gestiti Standard in base alle esigenze di capacità hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10de6-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="10de6-157">Tipo di disco Standard</span><span class="sxs-lookup"><span data-stu-id="10de6-157">Standard Disk Type</span></span>  | <span data-ttu-id="10de6-158">S4</span><span class="sxs-lookup"><span data-stu-id="10de6-158">S4</span></span>               | <span data-ttu-id="10de6-159">S6</span><span class="sxs-lookup"><span data-stu-id="10de6-159">S6</span></span>               | <span data-ttu-id="10de6-160">S10</span><span class="sxs-lookup"><span data-stu-id="10de6-160">S10</span></span>              | <span data-ttu-id="10de6-161">S20</span><span class="sxs-lookup"><span data-stu-id="10de6-161">S20</span></span>              | <span data-ttu-id="10de6-162">S30</span><span class="sxs-lookup"><span data-stu-id="10de6-162">S30</span></span>              | <span data-ttu-id="10de6-163">S40</span><span class="sxs-lookup"><span data-stu-id="10de6-163">S40</span></span>              | <span data-ttu-id="10de6-164">S50</span><span class="sxs-lookup"><span data-stu-id="10de6-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="10de6-165">Dimensioni disco</span><span class="sxs-lookup"><span data-stu-id="10de6-165">Disk size</span></span>           | <span data-ttu-id="10de6-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-166">30 GB</span></span>            | <span data-ttu-id="10de6-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-167">64 GB</span></span>            | <span data-ttu-id="10de6-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-168">128 GB</span></span>           | <span data-ttu-id="10de6-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="10de6-169">512 GB</span></span>           | <span data-ttu-id="10de6-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="10de6-171">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="10de6-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="10de6-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="10de6-173">IOPS per disco</span><span class="sxs-lookup"><span data-stu-id="10de6-173">IOPS per disk</span></span>       | <span data-ttu-id="10de6-174">500</span><span class="sxs-lookup"><span data-stu-id="10de6-174">500</span></span>              | <span data-ttu-id="10de6-175">500</span><span class="sxs-lookup"><span data-stu-id="10de6-175">500</span></span>              | <span data-ttu-id="10de6-176">500</span><span class="sxs-lookup"><span data-stu-id="10de6-176">500</span></span>              | <span data-ttu-id="10de6-177">500</span><span class="sxs-lookup"><span data-stu-id="10de6-177">500</span></span>              | <span data-ttu-id="10de6-178">500</span><span class="sxs-lookup"><span data-stu-id="10de6-178">500</span></span>              | <span data-ttu-id="10de6-179">500</span><span class="sxs-lookup"><span data-stu-id="10de6-179">500</span></span>             | <span data-ttu-id="10de6-180">500</span><span class="sxs-lookup"><span data-stu-id="10de6-180">500</span></span>              | 
| <span data-ttu-id="10de6-181">Velocità effettiva per disco</span><span class="sxs-lookup"><span data-stu-id="10de6-181">Throughput per disk</span></span> | <span data-ttu-id="10de6-182">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-182">60 MB per second</span></span> | <span data-ttu-id="10de6-183">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-183">60 MB per second</span></span> | <span data-ttu-id="10de6-184">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-184">60 MB per second</span></span> | <span data-ttu-id="10de6-185">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-185">60 MB per second</span></span> | <span data-ttu-id="10de6-186">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-186">60 MB per second</span></span> | <span data-ttu-id="10de6-187">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-187">60 MB per second</span></span> | <span data-ttu-id="10de6-188">60 MB al secondo</span><span class="sxs-lookup"><span data-stu-id="10de6-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="10de6-189">Criteri di memorizzazione nella cache su disco</span><span class="sxs-lookup"><span data-stu-id="10de6-189">Disk caching policy</span></span> 

<span data-ttu-id="10de6-190">**Managed Disks Premium**</span><span class="sxs-lookup"><span data-stu-id="10de6-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="10de6-191">Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10de6-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="10de6-192">Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10de6-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="10de6-193">Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="10de6-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="10de6-194">Prezzi</span><span class="sxs-lookup"><span data-stu-id="10de6-194">Pricing</span></span>

<span data-ttu-id="10de6-195">Hello revisione [prezzi per i dischi gestiti](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="10de6-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="10de6-196">Prezzi di dischi gestiti Premium è identico a hello i dischi Premium non gestito.</span><span class="sxs-lookup"><span data-stu-id="10de6-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="10de6-197">Tuttavia, il prezzo della versione Standard dei dischi gestiti è diverso da quello della versione Standard dei dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="10de6-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="10de6-198">Elenco di controllo</span><span class="sxs-lookup"><span data-stu-id="10de6-198">Checklist</span></span>

1.  <span data-ttu-id="10de6-199">Se si esegue la migrazione di dischi gestiti tooPremium, verificare che sia disponibile nell'area di hello a che esegue la migrazione.</span><span class="sxs-lookup"><span data-stu-id="10de6-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="10de6-200">Decidere hello nuova serie di macchine Virtuali che verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="10de6-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="10de6-201">Se si esegue la migrazione di dischi gestiti tooPremium deve essere uno spazio di archiviazione Premium in grado di supportare.</span><span class="sxs-lookup"><span data-stu-id="10de6-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="10de6-202">Decidere hello VM dimensioni esatte si utilizzerà che sono disponibili nell'area di hello a che esegue la migrazione.</span><span class="sxs-lookup"><span data-stu-id="10de6-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="10de6-203">Dimensioni della macchina virtuale devono numero di hello toobe toosupport sufficiente di dischi dati che si dispone.</span><span class="sxs-lookup"><span data-stu-id="10de6-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="10de6-204">Ad esempio, se si dispone di quattro dischi di dati, hello VM deve disporre di due o più core.</span><span class="sxs-lookup"><span data-stu-id="10de6-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="10de6-205">Considerare anche la potenza di elaborazione, la memoria e la larghezza di banda di rete necessarie.</span><span class="sxs-lookup"><span data-stu-id="10de6-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="10de6-206">Dispone di hello corrente VM informazioni utili, tra cui hello elenco di dischi e i BLOB VHD corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="10de6-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="10de6-207">Preparare l'applicazione per il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="10de6-207">Prepare your application for downtime.</span></span> <span data-ttu-id="10de6-208">toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello.</span><span class="sxs-lookup"><span data-stu-id="10de6-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="10de6-209">Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma.</span><span class="sxs-lookup"><span data-stu-id="10de6-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="10de6-210">Durata di tempo di inattività dipende dalla quantità di hello dei dati in toomigrate dischi hello.</span><span class="sxs-lookup"><span data-stu-id="10de6-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="10de6-211">Eseguire la migrazione di hello VM</span><span class="sxs-lookup"><span data-stu-id="10de6-211">Migrate hello VM</span></span>

<span data-ttu-id="10de6-212">Preparare l'applicazione per il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="10de6-212">Prepare your application for downtime.</span></span> <span data-ttu-id="10de6-213">toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello.</span><span class="sxs-lookup"><span data-stu-id="10de6-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="10de6-214">Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma.</span><span class="sxs-lookup"><span data-stu-id="10de6-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="10de6-215">Durata di tempo di inattività dipende dalla quantità hello di dati in toomigrate dischi hello.</span><span class="sxs-lookup"><span data-stu-id="10de6-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="10de6-216">Innanzitutto, impostare i parametri comuni di hello:</span><span class="sxs-lookup"><span data-stu-id="10de6-216">First, set hello common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="10de6-217">Creare un disco del sistema operativo gestito utilizzando hello disco rigido virtuale da hello classic macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10de6-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="10de6-218">Assicurarsi di aver fornito hello completare l'URI di hello parametro toohello $osVhdUri disco rigido virtuale del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="10de6-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="10de6-219">Per **-AccountType**, immettere **PremiumLRS** o **StandardLRS** in base al tipo di dischi (Premium o Standard) verso cui si sta eseguendo la migrazione.</span><span class="sxs-lookup"><span data-stu-id="10de6-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="10de6-220">Collegare toohello disco del sistema operativo hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10de6-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="10de6-221">Creare un disco dati gestiti da file di disco rigido virtuale dati hello e aggiungerlo toohello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10de6-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="10de6-222">Creare hello nuova macchina virtuale impostando public IP, la rete virtuale e scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="10de6-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="10de6-223">Potrebbero essere presenti ulteriori passaggi necessari toosupport l'applicazione che non rientrano in questa Guida.</span><span class="sxs-lookup"><span data-stu-id="10de6-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="10de6-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10de6-224">Next steps</span></span>

- <span data-ttu-id="10de6-225">Connessione macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="10de6-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="10de6-226">Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10de6-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

