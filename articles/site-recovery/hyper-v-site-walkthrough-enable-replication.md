---
title: Abilitare la replica per le VM Hyper-V in Azure (senza System Center VMM) con Azure Site Recovery| Microsoft Docs
description: Vengono riepilogati i passaggi necessari per abilitare la replica delle VM Hyper-V in Azure usando il servizio Azure Site Recovery
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
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="af009-103">Passaggio 10: Abilitare la replica per le VM Hyper-V in Azure</span><span class="sxs-lookup"><span data-stu-id="af009-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="af009-104">Questo articolo illustra come abilitare la replica per le macchine virtuali Hyper-V locali (non gestite da System Center VMM) in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af009-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="af009-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="af009-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="af009-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="af009-106">Before you start</span></span>

<span data-ttu-id="af009-107">Prima di iniziare, verificare che l'account utente di Azure abbia le [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) necessarie per abilitare la replica di una nuova macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="af009-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="af009-108">Escludere dischi dalla replica</span><span class="sxs-lookup"><span data-stu-id="af009-108">Exclude disks from replication</span></span>

<span data-ttu-id="af009-109">Per impostazione predefinita, vengono replicati tutti i dischi in un computer.</span><span class="sxs-lookup"><span data-stu-id="af009-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="af009-110">È possibile escludere dischi dalla replica.</span><span class="sxs-lookup"><span data-stu-id="af009-110">You can exclude disks from replication.</span></span> <span data-ttu-id="af009-111">Ad esempio, è possibile evitare di replicare i dischi con dati temporanei o dati che vengono aggiornati ogni volta che un computer o un'applicazione viene riavviata, come pagefile.sys o tempdb di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af009-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="af009-112">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="af009-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="af009-113">Replicare le VM</span><span class="sxs-lookup"><span data-stu-id="af009-113">Replicate VMs</span></span>

<span data-ttu-id="af009-114">Abilitare la replica per le macchine virtuali nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="af009-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="af009-115">Fare clic su **Eseguire la replica dell'applicazione** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="af009-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="af009-116">Dopo avere configurato la replica per la prima volta, è possibile fare clic su **+Replica** per abilitare la replica per altri computer.</span><span class="sxs-lookup"><span data-stu-id="af009-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="af009-118">In **Origine** selezionare il sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="af009-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="af009-119">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af009-119">Then click **OK**.</span></span>
3. <span data-ttu-id="af009-120">In **Destinazione** selezionare la sottoscrizione dell'insieme di credenziali e il modello di failover da usare in Azure (modalità classica o Resource Manager) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="af009-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="af009-121">Selezionare l'account di archiviazione da usare.</span><span class="sxs-lookup"><span data-stu-id="af009-121">Select the storage account you want to use.</span></span> <span data-ttu-id="af009-122">Se non si dispone di un account da usare, è possibile [crearne uno](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="af009-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="af009-123">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af009-123">Then click **OK**.</span></span>
5. <span data-ttu-id="af009-124">Selezionare la rete di Azure e la subnet a cui dovranno connettersi le macchine virtuali di Azure create dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="af009-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="af009-125">Per applicare le impostazioni di rete a tutti i computer selezionati per la replica, selezionare **Configurare ora per le macchine virtuali selezionate**.</span><span class="sxs-lookup"><span data-stu-id="af009-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="af009-126">Scegliere **Configurare in seguito** per selezionare la rete di Azure per ogni computer.</span><span class="sxs-lookup"><span data-stu-id="af009-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="af009-127">Se non si dispone di una rete da usare, è possibile [crearne una](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="af009-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="af009-128">Selezionare una subnet, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="af009-128">Select a subnet if applicable.</span></span> <span data-ttu-id="af009-129">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af009-129">Then click **OK**.</span></span>

   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="af009-131">In **Macchine virtuali** > **Seleziona macchine virtuali** fare clic per selezionare tutte le macchine virtuali da replicare.</span><span class="sxs-lookup"><span data-stu-id="af009-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="af009-132">È possibile selezionare solo i computer per cui è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="af009-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="af009-133">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af009-133">Then click **OK**.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="af009-135">In **Proprietà** > **Configura proprietà**selezionare il sistema operativo per le VM selezionate e il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="af009-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="af009-136">Verificare che il nome della VM di Azure (nome di destinazione) sia conforme ai [requisiti per le macchine virtuali di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="af009-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="af009-137">Per impostazione predefinita, tutti i dischi della VM sono selezionati per la replica.</span><span class="sxs-lookup"><span data-stu-id="af009-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="af009-138">Deselezionare i dischi per escluderli.</span><span class="sxs-lookup"><span data-stu-id="af009-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="af009-139">Fare clic su **OK** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="af009-139">Click **OK** to save changes.</span></span> <span data-ttu-id="af009-140">È possibile impostare proprietà aggiuntive in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="af009-140">You can set additional properties later.</span></span>

    ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="af009-142">In **Impostazioni della replica** > **Configurare le impostazioni di replica** selezionare i criteri di replica da applicare per le VM protette.</span><span class="sxs-lookup"><span data-stu-id="af009-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="af009-143">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af009-143">Then click **OK**.</span></span> <span data-ttu-id="af009-144">È possibile modificare i criteri di replica in **Criteri di replica** > nome-criterio > **Modifica impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="af009-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="af009-145">Le modifiche applicate verranno usate per i computer di cui è già in corso la replica e per i nuovi computer.</span><span class="sxs-lookup"><span data-stu-id="af009-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Abilitare la replica](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="af009-147">È possibile tenere traccia dello stato del processo **Abilita protezione** in **Processi** > **Site Recovery jobs** (Processi di Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="af009-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="af009-148">Dopo l'esecuzione del processo **Finalizza protezione** la macchina virtuale è pronta per il failover.</span><span class="sxs-lookup"><span data-stu-id="af009-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af009-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af009-149">Next steps</span></span>


<span data-ttu-id="af009-150">Andare a [Passaggio 11: Eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="af009-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
