---
title: "Pianificare la capacità e la scalabilità per la replica di VM Hyper-V (con VMM) in Azure con Azure Site Recovery | Microsoft Docs"
description: "Usare le istruzioni disponibili in questo articolo per pianificare la capacità e la scalabilità durante la replica di VM Hyper-V in cloud VMM in Azure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ab1dc21a829140f8cd2e57837d83a05b0d71bcdf
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="171a9-103">Passaggio 3: Pianificare la capacità e la scalabilità per la replica di Hyper-V in Azure (con VMM)</span><span class="sxs-lookup"><span data-stu-id="171a9-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="171a9-104">Dopo avere verificato i [prerequisiti per la distribuzione](vmm-to-azure-walkthrough-prerequisites.md), usare le istruzioni disponibili in questo articolo per configurare la pianificazione per la capacità e la scalabilità durante la replica di VM Hyper-V locali in cloud System Center Virtual Machine Manager (VMM) in Azure con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="171a9-104">After you've reviewed the [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="171a9-105">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="171a9-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="171a9-106">Come si inizia per pianificare la capacità?</span><span class="sxs-lookup"><span data-stu-id="171a9-106">How do I start capacity planning?</span></span>


<span data-ttu-id="171a9-107">Raccogliere informazioni sull'ambiente di replica e quindi pianificare la capacità usando i dati, insieme alle considerazioni illustrate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="171a9-107">You gather information about your replication environment, and then plan capacity using the data, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="171a9-108">Raccogliere informazioni</span><span class="sxs-lookup"><span data-stu-id="171a9-108">Gather information</span></span>

1. <span data-ttu-id="171a9-109">Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="171a9-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="171a9-110">Identificare la frequenza di modifica giornaliera (varianza) per i dati replicati.</span><span class="sxs-lookup"><span data-stu-id="171a9-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="171a9-111">Scaricare lo [strumento di pianificazione della capacità di Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) per ottenere la frequenza di modifica.</span><span class="sxs-lookup"><span data-stu-id="171a9-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="171a9-112">È consigliabile eseguire lo strumento nel corso di una settimana per acquisire le medie.</span><span class="sxs-lookup"><span data-stu-id="171a9-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="171a9-113">Calcolare la capacità</span><span class="sxs-lookup"><span data-stu-id="171a9-113">Figure out capacity</span></span>

<span data-ttu-id="171a9-114">In base alle informazioni raccolte, eseguire lo [strumento Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) per analizzare l'ambiente di origine e i carichi di lavoro e stimare le esigenze di larghezza di banda e le risorse server per la posizione di origine, oltre che le risorse (macchine virtuali, archiviazione e così via) necessarie nella posizione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="171a9-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="171a9-115">È possibile eseguire lo strumento nelle due modalità descritte di seguito:</span><span class="sxs-lookup"><span data-stu-id="171a9-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="171a9-116">Pianificazione rapida: eseguire lo strumento in questa modalità per ottenere le proiezioni di rete e server in base al numero medio di VM, dischi, archiviazione e frequenza di modifica.</span><span class="sxs-lookup"><span data-stu-id="171a9-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="171a9-117">Pianificazione dettagliata: eseguire lo strumento in questa modalità e specificare i dettagli di ogni carico di lavoro a livello di VM.</span><span class="sxs-lookup"><span data-stu-id="171a9-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="171a9-118">Analizzare la compatibilità della macchina virtuale e ottenere le proiezioni di rete e server.</span><span class="sxs-lookup"><span data-stu-id="171a9-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="171a9-119">Eseguire ora lo strumento:</span><span class="sxs-lookup"><span data-stu-id="171a9-119">Now run the tool:</span></span>

1. <span data-ttu-id="171a9-120">Scaricare lo [strumento](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="171a9-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="171a9-121">Per eseguire la pianificazione rapida, seguire [queste istruzioni](site-recovery-capacity-planner.md#run-the-quick-planner) e selezionare lo scenario **Da Hyper-V ad Azure**.</span><span class="sxs-lookup"><span data-stu-id="171a9-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="171a9-122">Per eseguire la pianificazione dettagliata, seguire [queste istruzioni](site-recovery-capacity-planner.md#run-the-detailed-planner) e selezionare lo scenario **Da Hyper-V ad Azure**.</span><span class="sxs-lookup"><span data-stu-id="171a9-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="171a9-123">Controllare la larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="171a9-123">Control network bandwidth</span></span>

<span data-ttu-id="171a9-124">Dopo aver calcolato la larghezza di banda necessaria, sono disponibili un paio di opzioni per controllare la quantità di larghezza di banda usata per la replica:</span><span class="sxs-lookup"><span data-stu-id="171a9-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="171a9-125">**Limitare la larghezza di banda**: il traffico Hyper-V che viene replicato in Azure passa per un host Hyper-V specifico.</span><span class="sxs-lookup"><span data-stu-id="171a9-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="171a9-126">È possibile limitare la larghezza di banda nel server host.</span><span class="sxs-lookup"><span data-stu-id="171a9-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="171a9-127">**Influire sulla larghezza di banda**: è possibile influire sulla larghezza di banda usata per la replica tramite un paio di chiavi del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="171a9-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="171a9-128">Limitare la larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="171a9-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="171a9-129">Aprire lo snap-in di MMC di Backup di Microsoft Azure nel server host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="171a9-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="171a9-130">Per impostazione predefinita, un collegamento a Backup di Microsoft Azure è disponibile sul desktop oppure in: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="171a9-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="171a9-131">Nello snap-in fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="171a9-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="171a9-132">Nella scheda **Limitazione larghezza di banda rete** selezionare **Abilita la limitazione all'uso della larghezza di banda Internet per le operazioni di backup** e impostare i limiti per le ore lavorative e non lavorative.</span><span class="sxs-lookup"><span data-stu-id="171a9-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="171a9-133">Gli intervalli validi sono compresi tra 512 Kbps e 102 Mbps al secondo.</span><span class="sxs-lookup"><span data-stu-id="171a9-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Limitare la larghezza di banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="171a9-135">È anche possibile usare il cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) per impostare la limitazione.</span><span class="sxs-lookup"><span data-stu-id="171a9-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="171a9-136">Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="171a9-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="171a9-137">**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="171a9-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="171a9-138">Influire sulla larghezza di banda di rete</span><span class="sxs-lookup"><span data-stu-id="171a9-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="171a9-139">Nel Registro di sistema passare a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="171a9-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="171a9-140">Per intervenire sul traffico della larghezza di banda in un disco di replica, modificare il valore di **UploadThreadsPerVM**oppure creare la chiave, se non esiste.</span><span class="sxs-lookup"><span data-stu-id="171a9-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="171a9-141">Per intervenire sulla larghezza di banda per il traffico di failback da Azure, modificare il valore di **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="171a9-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="171a9-142">Il valore predefinito è 4.</span><span class="sxs-lookup"><span data-stu-id="171a9-142">The default value is 4.</span></span> <span data-ttu-id="171a9-143">In una rete con provisioning eccessivo è necessario modificare i valori predefiniti di queste chiavi del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="171a9-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="171a9-144">Il valore massimo è 32.</span><span class="sxs-lookup"><span data-stu-id="171a9-144">The maximum is 32.</span></span> <span data-ttu-id="171a9-145">Monitorare il traffico per ottimizzare il valore.</span><span class="sxs-lookup"><span data-stu-id="171a9-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="171a9-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="171a9-146">Next steps</span></span>

<span data-ttu-id="171a9-147">Andare a [Passaggio 4: Pianificare la rete](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="171a9-147">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
