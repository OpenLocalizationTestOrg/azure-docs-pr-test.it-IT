---
title: i backup di distribuzione di gestione risorse di macchina virtuale aaaManage | Documenti Microsoft
description: Informazioni su come toomanage e monitorare i backup distribuito Gestione risorse di macchina virtuale
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="3a6f6-103">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="3a6f6-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a6f6-104">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="3a6f6-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="3a6f6-105">Gestire i backup delle macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="3a6f6-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="3a6f6-106">In questo articolo vengono fornite indicazioni sulla gestione dei backup di macchine Virtuali e vengono illustrate le informazioni di avvisi di backup hello disponibili nel dashboard del portale hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="3a6f6-107">linee guida di Hello in questo articolo si applicano le macchine virtuali toousing con gli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="3a6f6-108">In questo articolo non viene illustrata la creazione di hello di macchine virtuali, né spiegano come tooprotect le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="3a6f6-109">Per una panoramica sulla protezione di macchine virtuali distribuite di gestione risorse di Azure in Azure con un insieme di credenziali di servizi di ripristino, vedere [innanzitutto: eseguire il backup di macchine virtuali tooa insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="3a6f6-110">Gestire gli insiemi di credenziali e le macchine virtuali protette</span><span class="sxs-lookup"><span data-stu-id="3a6f6-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="3a6f6-111">Nel portale di Azure hello, dashboard dell'insieme di credenziali di servizi di ripristino hello fornisce accesso tooinformation sull'inclusione di hello insieme di credenziali:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="3a6f6-112">Hello backup più recente dello snapshot, che è anche il punto di ripristino più recente di hello < br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="3a6f6-113">criteri di backup Hello < br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-113">hello backup policy <br\></span></span>
* <span data-ttu-id="3a6f6-114">Dimensioni totali di tutti gli snapshot di backup <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="3a6f6-115">numero di macchine virtuali che sono protetti con insieme di credenziali hello < br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="3a6f6-116">Molte attività di gestione con un backup della macchina virtuale iniziano con l'apertura di insieme di credenziali hello in dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="3a6f6-117">Tuttavia, poiché gli insiemi di credenziali possono essere utilizzati tooprotect tooview i dettagli relativi a una determinata macchina virtuale, aprire più elementi (o più macchine virtuali), dashboard di elemento di insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="3a6f6-118">Hello procedura riportata di seguito illustra come hello tooopen *dashboard dell'insieme di credenziali* e quindi continuare toohello *dashboard elemento dell'insieme di credenziali*.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="3a6f6-119">In entrambe le procedure che segnalano come tooadd hello insieme di credenziali e credenziali toohello elemento dashboard di Azure tramite hello Pin toodashboard comando sono disponibili "suggerimenti per la".</span><span class="sxs-lookup"><span data-stu-id="3a6f6-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="3a6f6-120">PIN toodashboard è una modalità di creazione di un insieme di credenziali di scelta rapida toohello o un elemento.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="3a6f6-121">È inoltre possibile eseguire comandi comuni da collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="3a6f6-122">Se si dispone di più dashboard e aprire pannelli, utilizzare il dispositivo di scorrimento di hello-blu scuro nella parte inferiore di hello di hello di tooslide finestra hello Azure dashboard e viceversa.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Visualizzazione completa con il dispositivo di scorrimento](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="3a6f6-124">Aprire un insieme di credenziali di servizi di ripristino nel dashboard di hello:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="3a6f6-125">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3a6f6-126">Nel menu Hub hello, fare clic su **Sfoglia** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="3a6f6-127">Si inizia a digitare, hello filtri di elenco in base all'input.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="3a6f6-128">Fare clic su **Insiemi di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-128">Click **Recovery Services vault**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="3a6f6-130">viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="3a6f6-131">Elenco di insiemi di credenziali dei Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="3a6f6-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="3a6f6-132">Se si aggiunge un toohello insieme di credenziali per il Dashboard di Azure, che insieme di credenziali è immediatamente accessibili quando si apre hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="3a6f6-133">un dashboard toohello insieme di credenziali, nell'elenco dell'insieme di credenziali hello toopin insieme di credenziali hello e scegliere **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="3a6f6-134">Hello elenco degli insiemi di credenziali, selezionare hello insieme di credenziali tooopen relativo dashboard.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="3a6f6-135">Quando si seleziona insieme di credenziali hello, dashboard dell'insieme di credenziali hello e hello **impostazioni** pannello aperto.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="3a6f6-136">Nella seguente immagine di hello, hello **Contoso insieme di credenziali** dashboard è quello evidenziato.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Aprire il dashboard dell'insieme di credenziali e il pannello Impostazioni](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="3a6f6-138">Aprire il dashboard di un elemento dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="3a6f6-138">Open a vault item dashboard</span></span>
<span data-ttu-id="3a6f6-139">Nella procedura precedente hello è aperto il dashboard di insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="3a6f6-140">dashboard di elemento dell'insieme di credenziali hello tooopen:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="3a6f6-141">Dashboard dell'insieme di credenziali hello in hello **elementi Backup** riquadro, fare clic su **macchine virtuali di Azure**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Aprire il riquadro Elementi di backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="3a6f6-143">Hello **gli elementi di Backup** blade sono elencati l'ultimo processo backup di hello per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="3a6f6-144">In questo esempio è presente una sola macchina virtuale, demovm-markgal, protetta da questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="3a6f6-146">Per facilitare l'accesso, è possibile aggiungere un toohello di elemento di insieme di credenziali del Dashboard di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="3a6f6-147">un elemento dell'insieme di credenziali, nell'elenco di elementi dell'insieme di credenziali di hello, elemento hello pulsante destro del mouse e scegliere toopin **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="3a6f6-148">In hello **elementi Backup** pannello, fare clic su elemento dashboard di hello elemento tooopen hello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="3a6f6-150">dashboard di elemento di insieme di credenziali Hello e il relativo **impostazioni** pannello aperto.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Dashboard degli elementi di backup con il pannello Impostazioni](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="3a6f6-152">Dal dashboard di elemento di insieme di credenziali hello, è possibile eseguire molte attività di gestione delle chiavi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="3a6f6-153">Modificare i criteri o creare nuovi criteri di backup<br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="3a6f6-154">Visualizzare i punti di ripristino e vedere il relativo stato di coerenza <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="3a6f6-155">Eseguire il backup su richiesta di una macchina virtuale <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="3a6f6-156">Arrestare la protezione delle macchine virtuali <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="3a6f6-157">Riprendere la protezione delle macchine virtuali <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="3a6f6-158">Eliminare i dati di un backup o un punto di ripristino <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="3a6f6-159">[ripristinare i dischi di backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="3a6f6-160">Per hello seguire le procedure seguenti, hello punto di partenza è dashboard elemento dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="3a6f6-161">Gestire i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="3a6f6-161">Manage backup policies</span></span>
1. <span data-ttu-id="3a6f6-162">In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **tutte le impostazioni** tooopen hello **impostazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="3a6f6-164">In hello **impostazioni** pannello, fare clic su **criteri di Backup** tooopen tale pannello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="3a6f6-165">Nel Pannello di hello, vengono visualizzati dettagli intervallo frequenza e conservazione dei backup hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="3a6f6-167">Da hello **scegliere Criteri di backup** menu:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="3a6f6-168">toochange criteri, selezionare un criterio diverso e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="3a6f6-169">nuovo criterio di Hello viene applicata immediatamente toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="3a6f6-170"><br\></span><span class="sxs-lookup"><span data-stu-id="3a6f6-170"><br\></span></span>
   * <span data-ttu-id="3a6f6-171">Selezionare un criterio, toocreate **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-171">toocreate a policy, select **Create New**.</span></span>

     ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="3a6f6-173">Per istruzioni sulla creazione di criteri di backup, vedere [Definizione di un criterio di backup](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="3a6f6-174">Durante la gestione dei criteri di backup, verificare che hello toofollow [consigliate](backup-azure-vms-introduction.md#best-practices) per ottimizzare le prestazioni di backup</span><span class="sxs-lookup"><span data-stu-id="3a6f6-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="3a6f6-175">Backup su richiesta di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3a6f6-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="3a6f6-176">È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="3a6f6-177">Se il backup iniziale hello è in sospeso, il backup su richiesta crea una copia completa della macchina virtuale hello in hello che insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="3a6f6-178">Se il backup iniziale di hello è completato, un backup su richiesta invierà le modifiche apportate dallo snapshot precedente hello, insieme di credenziali di servizi di ripristino toohello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="3a6f6-179">I backup successivi sono sempre incrementali.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="3a6f6-180">periodo di mantenimento Hello per un backup su richiesta è il valore di conservazione hello specificato per il punto di backup giornaliero hello nei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="3a6f6-181">Se non è selezionato alcun punto di backup giornaliero, viene utilizzato il punto di backup settimanale di hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="3a6f6-182">backup tootrigger una richiesta di una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="3a6f6-183">In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Backup ora**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="3a6f6-185">portale Hello assicura che si desidera toostart un processo di backup su richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="3a6f6-186">Fare clic su **Sì** toostart processo di backup hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-186">Click **Yes** toostart hello backup job.</span></span>

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="3a6f6-188">processo di backup Hello crea un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="3a6f6-189">periodo di mantenimento Hello hello del punto di ripristino è hello uguale al periodo di conservazione specificato nei criteri di hello associato a una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="3a6f6-190">stato di avanzamento hello tootrack per il processo di hello, nel dashboard dell'insieme di credenziali hello, fare clic su hello **i processi di Backup** riquadro.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="3a6f6-191">Arrestare la protezione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3a6f6-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="3a6f6-192">Se si sceglie toostop protezione di una macchina virtuale, viene chiesto se si desidera che i punti di ripristino hello tooretain.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="3a6f6-193">Esistono due modi toostop proteggono le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="3a6f6-194">interrompere tutti i processi di backup futuri ed eliminare tutti i punti di ripristino oppure</span><span class="sxs-lookup"><span data-stu-id="3a6f6-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="3a6f6-195">arrestare tutti i processi di backup futuri, ma lasciare hello punti di ripristino</span><span class="sxs-lookup"><span data-stu-id="3a6f6-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="3a6f6-196">È un costo associato lasciando hello punti di ripristino nel servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="3a6f6-197">Il vantaggio di hello di lasciare hello punti di ripristino è tuttavia che è possibile ripristinare una macchina virtuale hello in un secondo momento, se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="3a6f6-198">Per informazioni sul costo di hello di lasciare hello punti di ripristino, vedere hello [prezzi](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="3a6f6-199">Se si sceglie toodelete tutti i punti di ripristino, è possibile ripristinare una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="3a6f6-200">protezione toostop per una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="3a6f6-201">In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Interrompi backup**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Pulsante Arresta backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="3a6f6-203">verrà visualizzata la finestra di blade Interrompi Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-203">hello Stop Backup blade opens.</span></span>

    ![Pannello Arresta backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="3a6f6-205">In hello **Interrompi Backup** pannello, scegliere se tooretain o delete hello dati di backup.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="3a6f6-206">casella di Hello informazioni dettagliate sul prescelto.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-206">hello information box provides details about your choice.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="3a6f6-208">Se si sceglie di dati di backup hello tooretain, ignorare toostep 4.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="3a6f6-209">Se si sceglie toodelete dati di backup, verificare i processi di backup hello toostop desiderato e quindi eliminare i punti di ripristino hello - Nome hello del tipo di elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="3a6f6-211">Se non si è certi del nome dell'elemento hello, passare il mouse sul nome di hello punto esclamativo tooview hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="3a6f6-212">Inoltre, in nome hello dell'elemento di hello **Interrompi Backup** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="3a6f6-213">L'aggiunta di un **motivo** o **commento** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="3a6f6-214">processo di backup hello toostop per l'elemento corrente hello, fare clic su ![backup pulsante di arresto](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="3a6f6-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="3a6f6-215">Un messaggio di notifica consentono di conoscere i processi di backup hello siano stati arrestati.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="3a6f6-217">Riprendere la protezione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3a6f6-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="3a6f6-218">Se hello **Mantieni dati di Backup** opzione scelto durante la protezione per la macchina virtuale hello è stata arrestata, è possibile tooresume protezione.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="3a6f6-219">Se hello **Elimina dati di Backup** è stata scelta l'opzione, quindi non è possibile riprendere la protezione per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="3a6f6-220">protezione per la macchina virtuale hello tooresume</span><span class="sxs-lookup"><span data-stu-id="3a6f6-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="3a6f6-221">In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Riprendi backup**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Riprendere la protezione](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="3a6f6-223">Apre il pannello di criteri di Backup Hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a6f6-224">Quando si proteggono nuovamente macchina virtuale hello, è possibile scegliere un criterio diverso rispetto a criterio hello con cui è stato inizialmente protetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="3a6f6-225">Seguire i passaggi di hello in [gestire criteri di backup](backup-azure-manage-vms.md#manage-backup-policies) criteri hello tooassign per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="3a6f6-226">Una volta macchina virtuale toohello applicati criteri di backup hello, vedrai segue messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Macchina virtuale protetta correttamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="3a6f6-228">Eliminare i dati di backup</span><span class="sxs-lookup"><span data-stu-id="3a6f6-228">Delete Backup data</span></span>
<span data-ttu-id="3a6f6-229">È possibile eliminare i dati di backup hello associati a una macchina virtuale durante hello **Interrompi backup** processo, o in qualsiasi momento dopo hello processo di backup è stata completata.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="3a6f6-230">Potrebbe essere utile toowait giorni o settimane prima di eliminare i punti di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="3a6f6-231">A differenza di ripristino dei punti di ripristino, durante l'eliminazione di dati di backup, è possibile scegliere toodelete punti di ripristino specifico.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="3a6f6-232">Se si scelgono toodelete ai dati di backup, eliminare tutti i punti di ripristino associati a elementi hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="3a6f6-233">Hello procedura riportata di seguito si presuppone che il processo di Backup hello per la macchina virtuale hello è stato arrestato o disabilitato.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="3a6f6-234">Dopo aver disabilitato il processo di Backup di hello, hello **Riprendi backup** e **Elimina backup** opzioni sono disponibili nel dashboard di elemento di insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Pulsanti Riprendi ed Elimina](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="3a6f6-236">dati di backup in una macchina virtuale con hello toodelete *Backup disabilitato*:</span><span class="sxs-lookup"><span data-stu-id="3a6f6-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="3a6f6-237">In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Elimina backup**.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="3a6f6-239">Hello **Elimina dati di Backup** apre blade.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="3a6f6-241">Nome del tipo hello di hello elemento tooconfirm desiderato punti di ripristino toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="3a6f6-243">Se non si è certi del nome dell'elemento hello, passare il mouse sul nome di hello punto esclamativo tooview hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="3a6f6-244">Inoltre, in nome hello dell'elemento di hello **Elimina dati di Backup** nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="3a6f6-245">L'aggiunta di un **motivo** o **commento** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="3a6f6-246">Fare clic su dati di backup hello toodelete per l'elemento corrente hello, ![backup pulsante di arresto](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="3a6f6-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="3a6f6-247">Un messaggio di notifica consente di verificare i dati di backup hello sono stati eliminati.</span><span class="sxs-lookup"><span data-stu-id="3a6f6-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a6f6-248">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a6f6-248">Next steps</span></span>
<span data-ttu-id="3a6f6-249">Per informazioni su come ricreare una macchina virtuale da un punto di ripristino, vedere [Ripristinare macchine virtuali in Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="3a6f6-250">Per ulteriori informazioni sulla protezione di macchine virtuali, vedere [innanzitutto: eseguire il backup di macchine virtuali tooa insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="3a6f6-251">Per informazioni sul monitoraggio degli eventi, vedere [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Monitorare gli avvisi per i backup delle macchine virtuali di Azure).</span><span class="sxs-lookup"><span data-stu-id="3a6f6-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
