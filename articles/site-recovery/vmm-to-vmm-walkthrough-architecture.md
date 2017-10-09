---
title: architettura di hello aaaReview per il sito secondario con tooa di replica Hyper-V con Azure Site Recovery | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dell'architettura di hello per la replica delle macchine virtuali Hyper-V tooa secondario System Center VMM sito locale con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="7c9d1-103">Passaggio 1: Esaminare l'architettura di hello per il sito secondario di Hyper-V replica tooa</span><span class="sxs-lookup"><span data-stu-id="7c9d1-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="7c9d1-104">Questo articolo vengono descritti i componenti di hello e processi per la replica locale macchine virtuali di Hyper-V (VM) in cloud System Center Virtual Machine Manager (VMM), sito VMM secondario tooa utilizzando hello [Azure Site Recovery](site-recovery-overview.md)di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="7c9d1-105">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7c9d1-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="7c9d1-106">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="7c9d1-106">Architectural components</span></span>

<span data-ttu-id="7c9d1-107">Ecco cosa occorre per la replica del sito VMM secondario di macchine virtuali Hyper-V tooa.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="7c9d1-108">**Componente**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-108">**Component**</span></span> | <span data-ttu-id="7c9d1-109">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-109">**Location**</span></span> | <span data-ttu-id="7c9d1-110">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="7c9d1-111">**Azzurro**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-111">**Azure**</span></span> | <span data-ttu-id="7c9d1-112">Sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-112">Subscription in Azure.</span></span> | <span data-ttu-id="7c9d1-113">Creare un insieme di credenziali di servizi di ripristino in hello sottoscrizione di Azure, tooorchestrate e gestire la replica tra i percorsi di VMM.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="7c9d1-114">**Server VMM**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-114">**VMM server**</span></span> | <span data-ttu-id="7c9d1-115">È necessario avere a disposizione un percorso VMM primario e uno secondario.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="7c9d1-116">Si consiglia di un server VMM nel sito primario di hello e uno nel sito secondario hello</span><span class="sxs-lookup"><span data-stu-id="7c9d1-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="7c9d1-117">**Server Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-117">**Hyper-V server**</span></span> |  <span data-ttu-id="7c9d1-118">Uno o più server Hyper-V host nei cloud VMM primario e secondario di hello.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="7c9d1-119">Dati vengono replicati tra hello server primario e secondario Hyper-V host su hello LAN o VPN, utilizzando l'autenticazione Kerberos o certificati.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="7c9d1-120">**VM Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7c9d1-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="7c9d1-121">Nel server host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-121">On Hyper-V host server.</span></span> | <span data-ttu-id="7c9d1-122">server host di origine Hello deve avere almeno una macchina virtuale che si desidera tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="7c9d1-123">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="7c9d1-123">Replication process</span></span>

1. <span data-ttu-id="7c9d1-124">Impostare hello account Azure, creare un insieme di credenziali di servizi di ripristino e specificare gli elementi da tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="7c9d1-125">Configurare hello origine e destinazione le impostazioni di replica, che include l'installazione di hello Provider di Azure Site Recovery nel server VMM e agente di servizi di ripristino di Microsoft Azure hello in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="7c9d1-126">Creare un criterio di replica per l'origine hello cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="7c9d1-127">criteri di Hello sono applicato tooall macchine virtuali presenti negli host nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="7c9d1-128">Abilitare la replica per ogni VMM e viene eseguita la replica iniziale di una macchina virtuale in base alle impostazioni di hello che prescelto.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="7c9d1-129">Dopo la replica iniziale, viene avviata la replica delle modifiche differenziali.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="7c9d1-130">Le modifiche rilevate per un elemento vengono salvate in un file HRL.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Tooon tra più sedi locali](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="7c9d1-132">Processo di failover e failback</span><span class="sxs-lookup"><span data-stu-id="7c9d1-132">Failover and failback process</span></span>

1. <span data-ttu-id="7c9d1-133">È possibile eseguire un [failover](site-recovery-failover.md) pianificato o non pianificato tra siti locali.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="7c9d1-134">Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="7c9d1-135">È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="7c9d1-136">Se si esegue un failover non pianificato tooa sito secondario, dopo il failover delle macchine hello nella posizione secondaria hello non sono abilitati per la replica o di protezione.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="7c9d1-137">Se si esegue un failover pianificato, dopo il failover hello, le macchine in posizione secondaria hello sono protetti.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="7c9d1-138">Quindi, si esegue il commit hello failover toostart accesso hello del carico di lavoro dalla replica hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="7c9d1-139">Quando il sito primario è nuovamente disponibile, si avvia tooreplicate replica inversa da hello del sito secondario toohello primario.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="7c9d1-140">La replica inversa porta hello le macchine virtuali in uno stato protetto, ma Data Center secondario hello è ancora percorso attivo hello.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="7c9d1-141">sito primario di hello toomake nel percorso active hello, si avvia nuovamente un failover pianificato da tooprimary secondario, seguita da un'altra replica inversa.</span><span class="sxs-lookup"><span data-stu-id="7c9d1-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7c9d1-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c9d1-142">Next steps</span></span>

<span data-ttu-id="7c9d1-143">Andare troppo[passaggio 2: esaminare i prerequisiti di hello e le limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7c9d1-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
