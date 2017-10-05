---
title: Eseguire un failover di test per la replica della macchina virtuale Hyper-V in un sito secondario con Azure Site Recovery | Microsoft Docs
description: Descrive come eseguire un failover di test per la replica della macchina virtuale Hyper-V in un sito System Center VMM secondario con Azure Site Recovery.
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
ms.openlocfilehash: 23d235d326273e7ec59feee6588a39f685401e52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="cda3c-103">Passaggio 10: Eseguire un failover di test per la replica Hyper-V in un sito secondario</span><span class="sxs-lookup"><span data-stu-id="cda3c-103">Step 10: Run a test failover for Hyper-V replication to a secondary site</span></span>


<span data-ttu-id="cda3c-104">Dopo aver abilitato la replica per le macchine virtuali Hyper-V con [Azure Site Recovery](site-recovery-overview.md), seguire quanto riportato in questo articolo per eseguire un failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article to run a test failover.</span></span> <span data-ttu-id="cda3c-105">Un failover di test verifica che la replica funzioni, senza alcuna conseguenza sull'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cda3c-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="cda3c-106">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cda3c-106">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="cda3c-107">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cda3c-107">Before you start</span></span>

- <span data-ttu-id="cda3c-108">Quando si attiva un failover di test è possibile specificare la rete a cui si connetteranno le macchine virtuali di replica di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-108">When you're triggering a test failover, you can specify the network to which the test replica VMs will connect.</span></span> <span data-ttu-id="cda3c-109">[Altre informazioni](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sulle opzioni di rete.</span><span class="sxs-lookup"><span data-stu-id="cda3c-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about the network options.</span></span>
- <span data-ttu-id="cda3c-110">È consigliabile non scegliere una rete selezionata durante il mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="cda3c-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="cda3c-111">Le istruzioni riportate in questo articolo descrivono come eseguire il failover di una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cda3c-111">The instructions in this article describe how to fail over a single VM.</span></span> <span data-ttu-id="cda3c-112">Consultare l'articolo relativo alla [creazione di piani di ripristino](site-recovery-create-recovery-plans.md) se si desidera eseguire il failover di più macchine virtuali contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="cda3c-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want to fail over multiple VMs together.</span></span>
- <span data-ttu-id="cda3c-113">Consultare l'articolo relativo alle [limitazioni per i failover di test](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="cda3c-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="cda3c-114">L'indirizzo IP assegnato a una macchina virtuale durante un failover di test corrisponde all'indirizzo IP che la macchina virtuale riceverebbe durante un failover pianificato o non pianificato, a condizione che l'indirizzo IP sia disponibile nella rete di failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-114">The IP address given to a VM during test failover is the same IP address that the VM would receive for a planned or unplanned failover (presuming that the IP address is available in the test failover network).</span></span> <span data-ttu-id="cda3c-115">Se l'indirizzo IP non è disponibile nella rete di failover di test, la macchina virtuale riceve un altro indirizzo IP disponibile in tale rete.</span><span class="sxs-lookup"><span data-stu-id="cda3c-115">If the IP address isn't available in the test failover network, the VM receives another IP address that is available in the test failover network.</span></span>
- <span data-ttu-id="cda3c-116">Se si desidera eseguire il failover di test nella rete di produzione per la convalida completa della macchina di connettività di rete end-to-end, si noti che:</span><span class="sxs-lookup"><span data-stu-id="cda3c-116">If you do want to do a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="cda3c-117">La macchina virtuale primaria deve essere arrestata quando si sta eseguendo il failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-117">The primary VM should be shut down when you're doing the test failover.</span></span> <span data-ttu-id="cda3c-118">In caso contrario si avranno due macchine virtuali con la stessa identità in esecuzione contemporaneamente sulla stessa rete.</span><span class="sxs-lookup"><span data-stu-id="cda3c-118">Otherwise, two VMs with the same identity will be running in the same network at the same time.</span></span> 
    - <span data-ttu-id="cda3c-119">Se si apportano modifiche alle macchine virtuali di test, tali modifiche andranno perdute durante la pulizia del failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-119">If you make changes to test VMs, those changes are lost when you clean up the test failover.</span></span> <span data-ttu-id="cda3c-120">Le modifiche non vengono replicate nella macchina virtuale primaria.</span><span class="sxs-lookup"><span data-stu-id="cda3c-120">These changes aren't replicated back to the primary VM.</span></span>
    - <span data-ttu-id="cda3c-121">Testare una rete di produzione comporta tempi di inattività per i carichi di lavoro della produzione.</span><span class="sxs-lookup"><span data-stu-id="cda3c-121">Testing a a production network leads to downtime for your production workloads.</span></span> <span data-ttu-id="cda3c-122">Chiedere agli utenti di non usare l'app quando l'analisi di ripristino di emergenza è in corso.</span><span class="sxs-lookup"><span data-stu-id="cda3c-122">Ask users not to use the app when the disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="cda3c-123">Eseguire un failover di test per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cda3c-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="cda3c-124">Per eseguire il failover di una macchina virtuale, in **Elementi replicati** fare clic sulla macchina virtuale e quindi su **Failover di test**.</span><span class="sxs-lookup"><span data-stu-id="cda3c-124">To fail over a single VM, in **Replicated Items**, click the VM > **Test Failover**.</span></span>
2. <span data-ttu-id="cda3c-125">In **Failover di test** specificare come le macchine virtuali di test dovranno essere connesse alle reti dopo il failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-125">In **Test Failover**, specify how test VMs will be connected to networks after the test failover.</span></span> 
3. <span data-ttu-id="cda3c-126">Fare clic su **OK** per iniziare il failover.</span><span class="sxs-lookup"><span data-stu-id="cda3c-126">Click **OK** to begin the failover.</span></span> <span data-ttu-id="cda3c-127">Tenere traccia dell'avanzamento sulla scheda **Processi** .</span><span class="sxs-lookup"><span data-stu-id="cda3c-127">Track progress on the **Jobs** tab.</span></span>
5. <span data-ttu-id="cda3c-128">Dopo il completamento del failover verificare che le macchine virtuali di test vengano avviate correttamente.</span><span class="sxs-lookup"><span data-stu-id="cda3c-128">After failover is complete, verify that the test VMs start successfully.</span></span>
6. <span data-ttu-id="cda3c-129">Al termine fare clic su **Cleanup test failover** (Pulizia failover di test) nel piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="cda3c-129">When you're done, click **Cleanup test failover** on the recovery plan.</span></span>
7. <span data-ttu-id="cda3c-130">Fare clic su **Note** per registrare e salvare eventuali osservazioni associate al failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-130">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="cda3c-131">Questa operazione elimina le macchine virtuali e le reti create durante il failover di test.</span><span class="sxs-lookup"><span data-stu-id="cda3c-131">This step deletes the virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cda3c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cda3c-132">Next steps</span></span>

<span data-ttu-id="cda3c-133">Dopo aver testato la distribuzione, leggere altre informazioni sugli altri tipi di [failover](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="cda3c-133">After you've tested the deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
