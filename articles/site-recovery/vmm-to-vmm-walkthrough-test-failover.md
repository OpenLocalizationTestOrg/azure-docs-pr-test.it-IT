---
title: un failover di test per il sito secondario macchina virtuale Hyper-V replica tooa con Azure Site Recovery aaaRun | Documenti Microsoft
description: Viene descritto come un failover di test per la macchina virtuale Hyper-V replica tooa toorun sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="a79f9-103">Passaggio 10: Eseguire un failover di test per il sito secondario di Hyper-V replica tooa</span><span class="sxs-lookup"><span data-stu-id="a79f9-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="a79f9-104">Dopo aver abilitato la replica per le macchine virtuali Hyper-V (VM) con [Azure Site Recovery](site-recovery-overview.md), utilizzare questo toorun articolo un failover di test.</span><span class="sxs-lookup"><span data-stu-id="a79f9-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="a79f9-105">Un failover di test verifica che la replica funzioni, senza alcuna conseguenza sull'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a79f9-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="a79f9-106">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a79f9-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="a79f9-107">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a79f9-107">Before you start</span></span>

- <span data-ttu-id="a79f9-108">Quando si è attivato un failover di test, è possibile specificare hello rete toowhich hello replica di test che si connetteranno le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a79f9-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="a79f9-109">[Altre informazioni](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sulle opzioni di rete hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="a79f9-110">È consigliabile non scegliere una rete selezionata durante il mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="a79f9-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="a79f9-111">Hello istruzioni riportate in questo articolo viene descritto come toofail su una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a79f9-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="a79f9-112">Conoscenza [la creazione di piani di ripristino](site-recovery-create-recovery-plans.md) se si desidera toofail insieme in più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a79f9-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="a79f9-113">Consultare l'articolo relativo alle [limitazioni per i failover di test](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="a79f9-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="a79f9-114">indirizzo IP assegnato tooa VM durante il test failover Hello è hello stesso indirizzo IP che hello VM riceverebbe per un failover pianificato o non pianificato (presumendo che che l'indirizzo IP hello è disponibile in rete di failover di test hello).</span><span class="sxs-lookup"><span data-stu-id="a79f9-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="a79f9-115">Se l'indirizzo IP hello non è disponibile in rete di failover di test hello, hello VM riceve un altro indirizzo IP disponibile in rete di failover di test hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="a79f9-116">Se si desidera toodo un failover di test della rete di produzione, per la convalida completa della macchina di connettività di rete end-to-end, si noti che:</span><span class="sxs-lookup"><span data-stu-id="a79f9-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="a79f9-117">Hello che VM primaria devono essere arrestati quando si sta eseguendo il failover di test hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="a79f9-118">In caso contrario, due macchine virtuali con hello stessa identità verrà eseguito in hello stessa rete in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="a79f9-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="a79f9-119">Se si apportano modifiche di macchine virtuali tootest, tali modifiche vengono perse quando si pulizia hello failover di test.</span><span class="sxs-lookup"><span data-stu-id="a79f9-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="a79f9-120">Queste modifiche non vengono replicata toohello indietro VM primaria.</span><span class="sxs-lookup"><span data-stu-id="a79f9-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="a79f9-121">Test di una rete di produzione lead toodowntime per i carichi di lavoro di produzione.</span><span class="sxs-lookup"><span data-stu-id="a79f9-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="a79f9-122">Chiedere agli utenti non toouse hello app durante l'analisi di ripristino di emergenza hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="a79f9-123">Eseguire un failover di test per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a79f9-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="a79f9-124">toofail su una singola macchina virtuale, in **elementi replicati**, fare clic su hello VM > **Failover di Test**.</span><span class="sxs-lookup"><span data-stu-id="a79f9-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="a79f9-125">In **Test Failover**, specificare la modalità di macchine virtuali di test verranno connesse toonetworks dopo il failover di test di hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="a79f9-126">Fare clic su **OK** toobegin hello failover.</span><span class="sxs-lookup"><span data-stu-id="a79f9-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="a79f9-127">Avanzamento delle hello **processi** scheda.</span><span class="sxs-lookup"><span data-stu-id="a79f9-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="a79f9-128">Al termine del failover, verificare che avvia le macchine virtuali di test hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="a79f9-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="a79f9-129">Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="a79f9-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="a79f9-130">In **note**, registrare e salvare eventuali commenti associati hello test failover.</span><span class="sxs-lookup"><span data-stu-id="a79f9-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="a79f9-131">Questo passaggio Elimina hello le macchine virtuali e reti che sono state create durante il failover di test.</span><span class="sxs-lookup"><span data-stu-id="a79f9-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a79f9-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a79f9-132">Next steps</span></span>

<span data-ttu-id="a79f9-133">Dopo aver testato distribuzione hello, ulteriori informazioni su altri tipi di [failover](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="a79f9-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
