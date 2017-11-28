---
title: "aaaPlan capacità e scalabilità per la macchina virtuale Hyper-V replica (senza VMM) tooAzure con Azure Site Recovery | Documenti Microsoft"
description: "Utilizzare questa capacità tooplan articolo e la scala per la replica delle macchine virtuali Hyper-V tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a><span data-ttu-id="ac9c9-103">Passaggio 3: Pianificare la capacità e scalabilità per la replica Hyper-V tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac9c9-103">Step 3: Plan capacity and scaling for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="ac9c9-104">Utilizzare questo toofigure articolo pianificazione della capacità e scalabilità, la replica locale macchine virtuali Hyper-V (senza System Center VMM) tooAzure con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac9c9-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="ac9c9-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ac9c9-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="ac9c9-106">Come si inizia per pianificare la capacità?</span><span class="sxs-lookup"><span data-stu-id="ac9c9-106">How do I start capacity planning?</span></span>


<span data-ttu-id="ac9c9-107">Raccogliere informazioni sull'ambiente di replica e quindi pianificare la capacità di utilizzare queste informazioni, insieme alle considerazioni di hello evidenziato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="ac9c9-108">Raccogliere informazioni</span><span class="sxs-lookup"><span data-stu-id="ac9c9-108">Gather information</span></span>

1. <span data-ttu-id="ac9c9-109">Raccogliere informazioni sull'ambiente di replica, incluse le macchine virtuali, i dischi per ogni macchina virtuale e le risorse di archiviazione per ogni disco.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="ac9c9-110">Identificare la frequenza di modifica giornaliera (varianza) per i dati replicati.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="ac9c9-111">Scaricare hello [strumento la pianificazione della capacità di Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) frequenza di modifica tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="ac9c9-112">È consigliabile che eseguire questo strumento su un toocapture settimana medie.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="ac9c9-113">Calcolare la capacità</span><span class="sxs-lookup"><span data-stu-id="ac9c9-113">Figure out capacity</span></span>

<span data-ttu-id="ac9c9-114">In base alle informazioni di hello che la raccolta di dati, si esegue hello [strumento pianificazione della capacità di ripristino sito](http://aka.ms/asr-capacity-planner-excel) tooanalyze l'ambiente di origine e i carichi di lavoro, stimare le esigenze di larghezza di banda e risorse del server per il percorso di origine hello e hello risorse (macchine virtuali e archiviazione e così via), che è necessario che nel percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="ac9c9-115">È possibile eseguire lo strumento hello in due modi:</span><span class="sxs-lookup"><span data-stu-id="ac9c9-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="ac9c9-116">Pianificazione rapida: lo strumento hello in questa modalità le proiezioni di rete e server tooget in base a un numero medio di macchine virtuali, dischi, archiviazione e frequenza di modifica.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="ac9c9-117">Modalità di pianificazione: eseguire lo strumento hello in questa modalità e fornire i dettagli di ogni carico di lavoro a livello di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="ac9c9-118">Analizzare la compatibilità della macchina virtuale e ottenere le proiezioni di rete e server.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="ac9c9-119">Eseguire lo strumento hello:</span><span class="sxs-lookup"><span data-stu-id="ac9c9-119">Now run hello tool:</span></span>

1. <span data-ttu-id="ac9c9-120">Scaricare hello [strumento](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="ac9c9-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="ac9c9-121">pianificazione di hello toorun rapido, seguire [queste istruzioni](site-recovery-capacity-planner.md#run-the-quick-planner), scenario selezionare hello e **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="ac9c9-122">toorun hello planner dettagliato, attenersi alla [queste istruzioni](site-recovery-capacity-planner.md#run-the-detailed-planner), uno scenario selezionare hello e **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="ac9c9-123">Controllare la larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="ac9c9-123">Control network bandwidth</span></span>

<span data-ttu-id="ac9c9-124">Dopo aver calcolato hello di banda che richiesta, è necessario un paio di opzioni per la quantità di hello controllo della larghezza di banda utilizzata per la replica:</span><span class="sxs-lookup"><span data-stu-id="ac9c9-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="ac9c9-125">**Limitazione della larghezza di banda**: Hyper-V che vengono replicati tooAzure del traffico tramite uno specifico host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="ac9c9-126">È possibile limitare la larghezza di banda nel server host hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="ac9c9-127">**Influiscono sulla larghezza di banda**: È possibile influenzare la larghezza di banda hello utilizzata per la replica con un paio di chiavi del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="ac9c9-128">Limitare la larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="ac9c9-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="ac9c9-129">Aprire hello MMC di Backup di Microsoft Azure snap-nel server host Hyper-V di hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="ac9c9-130">Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="ac9c9-131">Nello snap-in hello fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="ac9c9-132">In hello **limitazione** scheda selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**e impostare i limiti di hello per lavoro e non lavorative ore.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="ac9c9-133">Valori validi sono compresi 512 Mbps di too102 Kbps al secondo.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Limitare la larghezza di banda](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="ac9c9-135">È inoltre possibile utilizzare hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) tooset limitazione delle richieste di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="ac9c9-136">Di seguito è riportato un esempio:</span><span class="sxs-lookup"><span data-stu-id="ac9c9-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="ac9c9-137">**Set-OBMachineSetting -NoThrottle** indica che non è necessaria alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="ac9c9-138">Influire sulla larghezza di banda di rete</span><span class="sxs-lookup"><span data-stu-id="ac9c9-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="ac9c9-139">Nel Registro di sistema hello passare troppo**Backup\Replication Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="ac9c9-140">il traffico di larghezza di banda hello tooinfluence su un disco di replica, modificare hello valore hello **UploadThreadsPerVM**, o creare la chiave di hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="ac9c9-141">larghezza di banda hello tooinfluence per il traffico di failback da Azure, modificare il valore di hello **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="ac9c9-142">valore predefinito di Hello è 4.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-142">hello default value is 4.</span></span> <span data-ttu-id="ac9c9-143">In una rete di "provisioning eccessivo", queste chiavi del Registro di sistema devono essere modificate dai valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="ac9c9-144">Hello massimo è 32.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-144">hello maximum is 32.</span></span> <span data-ttu-id="ac9c9-145">Monitorare il traffico toooptimize hello valore.</span><span class="sxs-lookup"><span data-stu-id="ac9c9-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac9c9-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac9c9-146">Next steps</span></span>

<span data-ttu-id="ac9c9-147">Andare troppo[passaggio 4: pianificare la rete](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="ac9c9-147">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
