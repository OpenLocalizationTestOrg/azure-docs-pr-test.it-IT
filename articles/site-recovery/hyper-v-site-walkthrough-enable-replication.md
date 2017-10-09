---
title: la replica per le macchine virtuali Hyper-V replica tooAzure (senza System Center VMM) con Azure Site Recovery aaaEnable | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooenable tooAzure di replica è necessario per le macchine virtuali Hyper-V tramite il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="e1c7c-103">Passaggio 10: Abilitare la replica per le macchine virtuali Hyper-V replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="e1c7c-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="e1c7c-104">In questo articolo viene descritto come replica tooenable per locale macchine virtuali Hyper-V (non gestite da System Center VMM) tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="e1c7c-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e1c7c-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="e1c7c-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e1c7c-106">Before you start</span></span>

<span data-ttu-id="e1c7c-107">Prima di iniziare, assicurarsi che l'account utente di Azure è necessario hello [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="e1c7c-108">Escludere dischi dalla replica</span><span class="sxs-lookup"><span data-stu-id="e1c7c-108">Exclude disks from replication</span></span>

<span data-ttu-id="e1c7c-109">Per impostazione predefinita, vengono replicati tutti i dischi in un computer.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="e1c7c-110">È possibile escludere dischi dalla replica.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-110">You can exclude disks from replication.</span></span> <span data-ttu-id="e1c7c-111">Ad esempio non è possibile tooreplicate dischi con dati temporanei o dati che sono stato aggiornato ogni volta che un computer o applicazione viene riavviata (ad esempio pagefile.sys o tempdb di SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e1c7c-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="e1c7c-112">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="e1c7c-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="e1c7c-113">Replicare le VM</span><span class="sxs-lookup"><span data-stu-id="e1c7c-113">Replicate VMs</span></span>

<span data-ttu-id="e1c7c-114">Abilitare la replica per le macchine virtuali nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="e1c7c-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="e1c7c-115">Fare clic su **Eseguire la replica dell'applicazione** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="e1c7c-116">Dopo aver configurato la replica per hello prima volta, è possibile fare clic su **+ replicare** replica tooenable per computer aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="e1c7c-118">In **origine**, selezionare il sito hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="e1c7c-119">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-119">Then click **OK**.</span></span>
3. <span data-ttu-id="e1c7c-120">In **destinazione**, selezionare una sottoscrizione di insieme di credenziali hello e hello failover modello toouse in Azure (classica o risorsa management) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="e1c7c-121">Selezionare l'account di archiviazione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="e1c7c-122">Se non si dispone di un account a cui si vuole toouse, è possibile [crearlo](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e1c7c-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="e1c7c-123">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-123">Then click **OK**.</span></span>
5. <span data-ttu-id="e1c7c-124">Quando si crea il failover, si connetterà hello seleziona Azure toowhich rete e subnet macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="e1c7c-125">tooapply hello rete impostazioni tooall macchine si abilita per la replica, selezionare **Configura ora per macchine virtuali selezionate**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="e1c7c-126">Selezionare **configurare successivamente** tooselect hello Azure rete al computer.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="e1c7c-127">Se non si dispone di una rete a cui si desidera toouse, è possibile [crearlo](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="e1c7c-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="e1c7c-128">Selezionare una subnet, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-128">Select a subnet if applicable.</span></span> <span data-ttu-id="e1c7c-129">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-129">Then click **OK**.</span></span>

   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="e1c7c-131">In **macchine virtuali** > **selezionare le macchine virtuali**fare clic e selezionare ogni computer in cui si desidera tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="e1c7c-132">È possibile selezionare solo i computer per cui è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="e1c7c-133">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-133">Then click **OK**.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="e1c7c-135">In **proprietà** > **configurare proprietà**selezionare hello del sistema operativo per le macchine virtuali selezionata hello e hello disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="e1c7c-136">Verificare il nome di macchina virtuale di Azure hello (nome di destinazione) sia conforme ai [requisiti macchina virtuale di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="e1c7c-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="e1c7c-137">Per impostazione predefinita sono selezionati tutti i dischi di hello di hello VM per la replica.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="e1c7c-138">Cancella dischi tooexclude li.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="e1c7c-139">Fare clic su **OK** toosave modifiche.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="e1c7c-140">È possibile impostare proprietà aggiuntive in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-140">You can set additional properties later.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="e1c7c-142">In **le impostazioni di replica** > **configurare le impostazioni di replica**, selezionare i criteri di replica hello da tooapply per hello protetto le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="e1c7c-143">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-143">Then click **OK**.</span></span> <span data-ttu-id="e1c7c-144">È possibile modificare il criterio di replica hello in **criteri di replica** > criteri-name > **Modifica impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="e1c7c-145">Le modifiche applicate verranno usate per i computer di cui è già in corso la replica e per i nuovi computer.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="e1c7c-147">È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** processo **processi** > **i processi di ripristino del sito**.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="e1c7c-148">Dopo aver hello **finalizzazione della protezione** processo viene eseguito hello macchina è pronta per il failover.</span><span class="sxs-lookup"><span data-stu-id="e1c7c-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e1c7c-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1c7c-149">Next steps</span></span>


<span data-ttu-id="e1c7c-150">Andare troppo[passaggio 11: eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="e1c7c-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
