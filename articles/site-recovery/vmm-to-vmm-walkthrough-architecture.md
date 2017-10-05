---
title: Esaminare l'architettura per la replica Hyper-V in un sito secondario con Azure Site Recovery | Microsoft Docs
description: Questo articolo offre una panoramica dell'architettura per la replica di macchine virtuali Hyper-V locali in un sito System Center VMM secondario con Azure Site Recovery.
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
ms.openlocfilehash: b78cd0d5a5395873afaddc8856004775f447e8ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="1f59d-103">Passaggio 1: Esaminare l'architettura per la replica Hyper-V in un sito secondario</span><span class="sxs-lookup"><span data-stu-id="1f59d-103">Step 1: Review the architecture for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="1f59d-104">Questo articolo descrive i componenti e i processi coinvolti durante la replica in un sito VMM secondario di macchine virtuali Hyper-V locali presenti in cloud System Center Virtual Machine Manager (VMM) tramite il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f59d-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM site using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="1f59d-105">Per inviare commenti è possibile usare la parte inferiore di questo articolo oppure il [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1f59d-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="1f59d-106">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="1f59d-106">Architectural components</span></span>

<span data-ttu-id="1f59d-107">Di seguito sono indicati i componenti necessari per la replica di macchine virtuali Hyper-V in un sito VMM secondario.</span><span class="sxs-lookup"><span data-stu-id="1f59d-107">Here's what you need for replicating Hyper-V VMs to a secondary VMM site.</span></span>

<span data-ttu-id="1f59d-108">**Componente**</span><span class="sxs-lookup"><span data-stu-id="1f59d-108">**Component**</span></span> | <span data-ttu-id="1f59d-109">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="1f59d-109">**Location**</span></span> | <span data-ttu-id="1f59d-110">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="1f59d-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="1f59d-111">**Azzurro**</span><span class="sxs-lookup"><span data-stu-id="1f59d-111">**Azure**</span></span> | <span data-ttu-id="1f59d-112">Sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1f59d-112">Subscription in Azure.</span></span> | <span data-ttu-id="1f59d-113">Creare un insieme di credenziali di Servizi di ripristino nella sottoscrizione di Azure per orchestrare e gestire la replica tra i percorsi VMM.</span><span class="sxs-lookup"><span data-stu-id="1f59d-113">You create a Recovery Services vault in the Azure subscription, to orchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="1f59d-114">**Server VMM**</span><span class="sxs-lookup"><span data-stu-id="1f59d-114">**VMM server**</span></span> | <span data-ttu-id="1f59d-115">È necessario avere a disposizione un percorso VMM primario e uno secondario.</span><span class="sxs-lookup"><span data-stu-id="1f59d-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="1f59d-116">È consigliabile distribuire un server VMM in un sito primario e uno nel sito secondario.</span><span class="sxs-lookup"><span data-stu-id="1f59d-116">We recommend a VMM server in the primary site, and one in the secondary site</span></span> 
<span data-ttu-id="1f59d-117">**Server Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1f59d-117">**Hyper-V server**</span></span> |  <span data-ttu-id="1f59d-118">Uno o più server host Hyper-V nei cloud VMM primario e secondario.</span><span class="sxs-lookup"><span data-stu-id="1f59d-118">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span> | <span data-ttu-id="1f59d-119">I dati vengono replicati tra il server host Hyper-V primario e secondario su LAN o VPN usando l'autenticazione Kerberos o del certificato.</span><span class="sxs-lookup"><span data-stu-id="1f59d-119">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="1f59d-120">**VM Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1f59d-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="1f59d-121">Nel server host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1f59d-121">On Hyper-V host server.</span></span> | <span data-ttu-id="1f59d-122">Il server host di origine deve avere almeno una VM che si vuole replicare.</span><span class="sxs-lookup"><span data-stu-id="1f59d-122">The source host server should have at least one VM that you want to replicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="1f59d-123">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="1f59d-123">Replication process</span></span>

1. <span data-ttu-id="1f59d-124">Configurare l'account Azure, creare un insieme di credenziali di Servizi di ripristino e specificare di cosa si vuole eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="1f59d-124">You set up the Azure account, create a Recovery Services vault, and specify what you want to replicate.</span></span>
2. <span data-ttu-id="1f59d-125">Configurare le impostazioni di replica di origine e di destinazione, inclusa l'installazione del provider di Azure Site Recovery nei server VMM, e l'agente di Servizi di ripristino di Microsoft Azure in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1f59d-125">You configure the source and target replication settings, which includes installing the Azure Site Recovery Provider on VMM servers, and the Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="1f59d-126">Creare criteri di replica per il cloud VMM di origine.</span><span class="sxs-lookup"><span data-stu-id="1f59d-126">You create a replication policy for the source VMM cloud.</span></span> <span data-ttu-id="1f59d-127">Il criterio viene applicato a tutte le VM negli host del cloud.</span><span class="sxs-lookup"><span data-stu-id="1f59d-127">The policy is applied to all VMs located on hosts in the cloud.</span></span>
4. <span data-ttu-id="1f59d-128">Abilitare la replica per ogni VMM. La replica iniziale di una macchina virtuale viene eseguita in base alle impostazioni scelte.</span><span class="sxs-lookup"><span data-stu-id="1f59d-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with the settings you choose.</span></span>
5. <span data-ttu-id="1f59d-129">Dopo la replica iniziale, viene avviata la replica delle modifiche differenziali.</span><span class="sxs-lookup"><span data-stu-id="1f59d-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="1f59d-130">Le modifiche rilevate per un elemento vengono salvate in un file HRL.</span><span class="sxs-lookup"><span data-stu-id="1f59d-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Da sito locale a sito locale](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="1f59d-132">Processo di failover e failback</span><span class="sxs-lookup"><span data-stu-id="1f59d-132">Failover and failback process</span></span>

1. <span data-ttu-id="1f59d-133">È possibile eseguire un [failover](site-recovery-failover.md) pianificato o non pianificato tra siti locali.</span><span class="sxs-lookup"><span data-stu-id="1f59d-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="1f59d-134">Se si esegue un failover pianificato, le macchine virtuali di origine vengono arrestate per assicurare che non si verifichino perdite di dati.</span><span class="sxs-lookup"><span data-stu-id="1f59d-134">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="1f59d-135">È possibile effettuare il failover di un solo computer o creare [piani di ripristino](site-recovery-create-recovery-plans.md) per orchestrare il failover di più computer.</span><span class="sxs-lookup"><span data-stu-id="1f59d-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="1f59d-136">Se si esegue un failover non pianificato in un sito secondario, dopo il failover i computer della posizione secondaria non sono abilitati per la protezione o la replica.</span><span class="sxs-lookup"><span data-stu-id="1f59d-136">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="1f59d-137">Se è stato eseguito un failover pianificato, dopo il failover i computer della posizione secondaria sono protetti.</span><span class="sxs-lookup"><span data-stu-id="1f59d-137">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="1f59d-138">Si esegue quindi il commit del failover per avviare l'accesso al carico di lavoro dalla VM di replica.</span><span class="sxs-lookup"><span data-stu-id="1f59d-138">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="1f59d-139">Quando il sito primario è nuovamente disponibile, si avvia la replica inversa dal sito secondario a quello primario.</span><span class="sxs-lookup"><span data-stu-id="1f59d-139">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="1f59d-140">La replica inversa porta le macchine virtuali in uno stato protetto, ma per il datacenter secondario resta la posizione attiva.</span><span class="sxs-lookup"><span data-stu-id="1f59d-140">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="1f59d-141">Per rendere di nuovo il sito primario la posizione attiva, occorre avviare un failover pianificato da sito secondario a primario, seguito da un'altra replica inversa.</span><span class="sxs-lookup"><span data-stu-id="1f59d-141">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1f59d-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f59d-142">Next steps</span></span>

<span data-ttu-id="1f59d-143">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="1f59d-143">Go to [Step 2: Review the prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
