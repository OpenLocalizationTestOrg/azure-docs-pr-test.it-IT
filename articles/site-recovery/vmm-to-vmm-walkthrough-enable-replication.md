---
title: sito secondario aaaEnable Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come replica tooenable per le macchine virtuali Hyper-V replica tooa sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="67aae-103">Passaggio 9: Consentire al sito secondario tooa replica per le macchine virtuali Hyper-V</span><span class="sxs-lookup"><span data-stu-id="67aae-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="67aae-104">Dopo aver impostato un criterio di replica, utilizzare questo articolo tooenable replica tooa sito secondario di System Center Virtual Machine Manager (VMM) per on-premise Hyper-V le macchine virtuali (VM), utilizzando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67aae-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="67aae-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="67aae-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="67aae-106">Selezionare le macchine virtuali tooreplicate</span><span class="sxs-lookup"><span data-stu-id="67aae-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="67aae-107">Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="67aae-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Abilitare la replica](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="67aae-109">In **origine**, selezionare il server VMM di hello e cloud in cui hello si trovano gli host Hyper-V da tooreplicate hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="67aae-110">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67aae-110">Then click **OK**.</span></span>

    ![Abilitare la replica](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="67aae-112">In **destinazione**, verificare il server VMM secondario di hello e cloud.</span><span class="sxs-lookup"><span data-stu-id="67aae-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="67aae-113">In **macchine virtuali**, selezionare le macchine virtuali hello desiderato tooprotect dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Abilitare la protezione delle macchine virtuali](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="67aae-115">È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** azione in **processi** > **i processi di ripristino del sito**.</span><span class="sxs-lookup"><span data-stu-id="67aae-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="67aae-116">Dopo aver hello **finalizzazione della protezione** processo viene completato, il completamento della replica iniziale hello e macchina virtuale di hello è pronta per il failover.</span><span class="sxs-lookup"><span data-stu-id="67aae-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="67aae-117">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="67aae-117">Note that:</span></span>

- <span data-ttu-id="67aae-118">È inoltre possibile abilitare la protezione per le macchine virtuali nella console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="67aae-119">Fare clic su **Abilita protezione** sulla barra degli strumenti hello in proprietà macchina virtuale hello > **Azure Site Recovery** scheda.</span><span class="sxs-lookup"><span data-stu-id="67aae-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="67aae-120">Dopo avere abilitato la replica, è possibile visualizzare le proprietà per hello VM in **elementi replicati**.</span><span class="sxs-lookup"><span data-stu-id="67aae-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="67aae-121">In hello **Essentials** dashboard, è possibile visualizzare informazioni sui criteri di replica hello per hello macchina virtuale e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="67aae-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="67aae-122">Per altri dettagli, fare clic su **Proprietà** .</span><span class="sxs-lookup"><span data-stu-id="67aae-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="67aae-123">Eseguire l'onboarding di VM esistenti</span><span class="sxs-lookup"><span data-stu-id="67aae-123">Onboard existing VMs</span></span>

<span data-ttu-id="67aae-124">Se in VMM sono presenti macchine virtuali replicate tramite la replica Hyper-V, è possibile caricarle per la replica in Azure Site Recovery nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="67aae-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="67aae-125">Assicurarsi che nel server hello Hyper-V ospita macchina virtuale esistente si trova nel cloud primario hello hello e tale server Hyper-V hello hosting hello macchina virtuale di replica si trova nel cloud secondario hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="67aae-126">Verificare che sia configurato un criterio di replica per i cloud VMM primario hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="67aae-127">Abilitare la replica per macchina virtuale primaria hello.</span><span class="sxs-lookup"><span data-stu-id="67aae-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="67aae-128">Azure Site Recovery e VMM assicurarsi che hello stesso host di replica e la macchina virtuale viene rilevato, Azure Site Recovery riutilizzerà e ristabilire la replica hello utilizzando le impostazioni specificate.</span><span class="sxs-lookup"><span data-stu-id="67aae-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="67aae-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67aae-129">Next steps</span></span>

<span data-ttu-id="67aae-130">Andare troppo[passaggio 10: eseguire un failover di test](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="67aae-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
