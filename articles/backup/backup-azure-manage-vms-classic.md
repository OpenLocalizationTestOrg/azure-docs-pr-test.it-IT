---
title: aaaManage e monitorare i backup di macchina virtuale di Azure | Documenti Microsoft
description: Informazioni su come toomanage e monitoraggio virtuale di Azure per una macchina backup
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="3117d-103">Gestire i processi di Backup di Azure comuni e attivare gli avvisi nel portale classico hello</span><span class="sxs-lookup"><span data-stu-id="3117d-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3117d-104">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="3117d-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="3117d-105">Gestire i backup delle macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="3117d-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="3117d-106">In questo articolo vengono fornite informazioni sulle comuni attività di gestione e monitoraggio per le macchine virtuali modello classico protette in Azure.</span><span class="sxs-lookup"><span data-stu-id="3117d-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="3117d-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3117d-108">Vedere [preparare tooback l'ambiente di macchine virtuali di Azure](backup-azure-vms-prepare.md) per informazioni dettagliate sull'utilizzo di distribuzione classica le macchine virtuali del modello.</span><span class="sxs-lookup"><span data-stu-id="3117d-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="3117d-109">A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.</span><span class="sxs-lookup"><span data-stu-id="3117d-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="3117d-110">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="3117d-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="3117d-111">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="3117d-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="3117d-112">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="3117d-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="3117d-113">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="3117d-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="3117d-114">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="3117d-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="3117d-115">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3117d-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="3117d-116">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="3117d-117">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3117d-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="3117d-118">Gestire le macchine virtuali protette</span><span class="sxs-lookup"><span data-stu-id="3117d-118">Manage protected virtual machines</span></span>
<span data-ttu-id="3117d-119">toomanage macchine virtuali protette:</span><span class="sxs-lookup"><span data-stu-id="3117d-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="3117d-120">tooview e gestire le impostazioni di backup per una macchina virtuale fare clic su hello **elementi protetti** scheda.</span><span class="sxs-lookup"><span data-stu-id="3117d-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="3117d-121">Fare clic sul nome hello di hello di toosee un elemento protetto **dettagli Backup** scheda, in cui vengono visualizzate informazioni sull'ultimo backup hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="3117d-123">tooview e gestire le impostazioni di criteri di backup per una macchina virtuale fare clic su hello **criteri** scheda.</span><span class="sxs-lookup"><span data-stu-id="3117d-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="3117d-125">Hello **criteri di Backup** scheda Mostra hello criterio esistente.</span><span class="sxs-lookup"><span data-stu-id="3117d-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="3117d-126">È possibile modificare i criteri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="3117d-126">You can modify as needed.</span></span> <span data-ttu-id="3117d-127">Se è necessario un nuovo criterio toocreate fare clic su **crea** su hello **criteri** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="3117d-128">Si noti che se si desidera tooremove un criterio non deve contenere tutte le macchine virtuali è associate.</span><span class="sxs-lookup"><span data-stu-id="3117d-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="3117d-130">È possibile ottenere ulteriori informazioni sulle azioni o lo stato per una macchina virtuale in hello **processi** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="3117d-131">Fare clic su un processo in hello elenco tooget ulteriori dettagli, o filtrare i processi per una macchina virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="3117d-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Processi](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="3117d-133">Backup su richiesta di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3117d-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="3117d-134">È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione.</span><span class="sxs-lookup"><span data-stu-id="3117d-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="3117d-135">Se il backup iniziale hello è in sospeso per la macchina virtuale hello, backup su richiesta verrà creata una copia completa della macchina virtuale hello nell'insieme di credenziali di backup Azure.</span><span class="sxs-lookup"><span data-stu-id="3117d-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="3117d-136">Se il primo backup viene completato, verrà di backup su richiesta solo le modifiche di trasmissione da un precedente backup tooAzure backup insieme di credenziali ad esempio, è sempre incrementale.</span><span class="sxs-lookup"><span data-stu-id="3117d-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="3117d-137">Periodo di mantenimento di un backup su richiesta è impostato un valore tooretention specificato per la conservazione giornaliera nel criterio di backup corrispondente toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3117d-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="3117d-138">backup tootake una richiesta di una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3117d-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="3117d-139">Passare toohello **elementi protetti** pagina e selezionare **macchina virtuale di Azure** come **tipo** (se non è già selezionata) e fare clic su **selezionare**pulsante.</span><span class="sxs-lookup"><span data-stu-id="3117d-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="3117d-141">Selezionare hello e della macchina virtuale in cui desidera che una richiesta tootake backup fare clic su **Esegui Backup ora** pulsante nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Esegui backup](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="3117d-143">Verrà creato un processo di backup sulla macchina virtuale hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="3117d-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="3117d-144">Mantenimento del punto di ripristino creato tramite il processo sarà corrisponde a quello specificato nel criterio hello associata a una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Creazione del processo di backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="3117d-146">criteri di hello tooview associato a una macchina virtuale, drill down in macchina virtuale in hello **elementi protetti** pagina e la scheda Criteri toobackup passare.</span><span class="sxs-lookup"><span data-stu-id="3117d-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="3117d-147">Una volta creato il processo di hello, è possibile fare clic su **Visualizza processo** pulsante di tipo avviso popup hello barra toosee processo corrispondente di hello nella pagina dei processi hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Processo di backup creato](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="3117d-149">Dopo il completamento del processo di hello, verrà creato un punto di ripristino che è possibile utilizzare macchina virtuale di toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="3117d-150">Questo valore colonna punto di ripristino hello anche incrementa di 1 in **elementi protetti** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="3117d-151">Arrestare la protezione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3117d-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="3117d-152">È possibile scegliere toostop nei backup futuri hello di una macchina virtuale con hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3117d-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="3117d-153">Mantenere i dati di backup associati alla macchina virtuale nell'insieme di credenziali di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="3117d-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="3117d-154">Eliminare i dati di backup associati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3117d-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="3117d-155">Se sono stati selezionati i dati di backup tooretain associati alla macchina virtuale, è possibile utilizzare la macchina virtuale hello dati di backup toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="3117d-156">Per i dettagli relativi ai prezzi per queste macchine virtuali, fare clic [qui](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="3117d-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="3117d-157">protezione tooStop per una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3117d-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="3117d-158">Passare troppo**elementi protetti** pagina e selezionare **macchina virtuale di Azure** come tipo di filtro hello (se non è già selezionata) e fare clic su **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3117d-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="3117d-160">Selezionare la macchina virtuale di hello e fare clic su **Arresta protezione dati** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="3117d-162">Per impostazione predefinita, Azure Backup non elimina i dati di backup hello associati alla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="3117d-164">Se si desiderano toodelete dati di backup, selezionare la casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Casella di controllo](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="3117d-166">Selezionare un motivo per l'interruzione del backup hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="3117d-167">Mentre questo è facoltativo, fornire un motivo verrà Guida toowork di Backup di Azure ai suggerimenti hello e assegnare priorità agli scenari cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="3117d-168">Fare clic su **Invia** hello toosubmit pulsante **arrestare la protezione dati** processo.</span><span class="sxs-lookup"><span data-stu-id="3117d-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="3117d-169">Fare clic su **Visualizza processo** toosee hello processo hello corrispondente in **processi** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="3117d-171">Se non è stato selezionato **Elimina dati di backup associati** opzione durante **Arresta protezione dati** procedura guidata, quindi registra il completamento del processo, la protezione stato diventa troppo**protezione interrotta**.</span><span class="sxs-lookup"><span data-stu-id="3117d-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="3117d-172">dati Hello rimangono con Backup di Azure finché viene eliminato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="3117d-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="3117d-173">È sempre possibile eliminare dati hello selezionando una macchina virtuale hello in hello **elementi protetti** pagina e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="3117d-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="3117d-175">Se si è scelto di hello **Elimina dati di backup associati** opzione, hello macchina virtuale non far parte di hello **elementi protetti** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="3117d-176">Riattivare la protezione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3117d-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="3117d-177">Se non è stato selezionato hello **Elimina dati di backup associati** opzione **Arresta protezione dati**, è possibile proteggere nuovamente macchina virtuale hello seguendo toobacking simile passaggi di hello backup registrato virtuale macchine.</span><span class="sxs-lookup"><span data-stu-id="3117d-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="3117d-178">Una volta protetto, la macchina virtuale sarà protetto in modo i dati di backup conservati toostop precedente e punti di ripristino creato dopo riproteggere.</span><span class="sxs-lookup"><span data-stu-id="3117d-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="3117d-179">Dopo aver riproteggere, lo stato di protezione della macchina virtuale hello verrà modificato troppo**Protected** se non esistono punti di ripristino precedenti troppo**Arresta protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="3117d-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Protezione VM riattivata](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="3117d-181">Quando si proteggono nuovamente macchina virtuale hello, è possibile scegliere un criterio diverso rispetto a criterio hello con cui è stato inizialmente protetto macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3117d-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="3117d-182">Annullare la registrazione di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3117d-182">Unregister virtual machines</span></span>
<span data-ttu-id="3117d-183">Se si desidera una macchina virtuale di hello tooremove dall'insieme di credenziali backup hello:</span><span class="sxs-lookup"><span data-stu-id="3117d-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="3117d-184">Fare clic su hello **UNREGISTER** pulsante nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Disabilita protezione](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="3117d-186">Viene visualizzata una notifica di tipo avviso popup nella parte inferiore di hello della schermata Ciao richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="3117d-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="3117d-187">Fare clic su **Sì** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="3117d-187">Click **YES** toocontinue.</span></span>

    ![Disabilita protezione](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="3117d-189">Eliminare i dati di backup</span><span class="sxs-lookup"><span data-stu-id="3117d-189">Delete Backup data</span></span>
<span data-ttu-id="3117d-190">È possibile eliminare i dati di backup hello associati a una macchina virtuale, ovvero:</span><span class="sxs-lookup"><span data-stu-id="3117d-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="3117d-191">Durante il processo Arresta protezione</span><span class="sxs-lookup"><span data-stu-id="3117d-191">During Stop Protection Job</span></span>
* <span data-ttu-id="3117d-192">Dopo il completamento del processo Arresta protezione in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3117d-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="3117d-193">toodelete i dati di backup in una macchina virtuale, ovvero in hello *protezione interrotta* stato post corretto completamento di un **Interrompi Backup** processo:</span><span class="sxs-lookup"><span data-stu-id="3117d-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="3117d-194">Passare toohello **elementi protetti** pagina e selezionare **macchina virtuale di Azure** come *tipo* e fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3117d-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="3117d-196">Selezionare una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-196">Select hello virtual machine.</span></span> <span data-ttu-id="3117d-197">macchina virtuale di Hello sarà **protezione interrotta** stato.</span><span class="sxs-lookup"><span data-stu-id="3117d-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="3117d-199">Fare clic su hello **eliminare** pulsante nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Elimina backup](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="3117d-201">In hello **Elimina dati di backup** procedura guidata, selezionare un motivo per l'eliminazione di dati di backup (scelta consigliati) e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="3117d-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Elimina dati di backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="3117d-203">Verrà creato un processo toodelete backup di dati della macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="3117d-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="3117d-204">Fare clic su **Visualizza processo** toosee processo corrispondente nella pagina processi.</span><span class="sxs-lookup"><span data-stu-id="3117d-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Eliminazione dei dati completata](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="3117d-206">Una volta completato il processo di hello, hello voce verrà rimosso dalla macchina virtuale corrispondente con toohello **gli elementi protetti** pagina.</span><span class="sxs-lookup"><span data-stu-id="3117d-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="3117d-207">Dashboard</span><span class="sxs-lookup"><span data-stu-id="3117d-207">Dashboard</span></span>
<span data-ttu-id="3117d-208">In hello **Dashboard** pagina è possibile esaminare le informazioni sulle macchine virtuali di Azure, i relativi archiviazione e i processi associati ad essi nel hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="3117d-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="3117d-209">È possibile visualizzare lo stato del backup ed eventuali errori di backup associati.</span><span class="sxs-lookup"><span data-stu-id="3117d-209">You can view backup status and any associated backup errors.</span></span>

![Dashboard](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="3117d-211">I valori nel dashboard di hello vengono aggiornati una volta ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="3117d-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="3117d-212">Operazioni di controllo</span><span class="sxs-lookup"><span data-stu-id="3117d-212">Auditing Operations</span></span>
<span data-ttu-id="3117d-213">Backup di Azure offre la revisione di hello "operazione i log" di operazioni di backup attivati dal cliente hello rende facile toosee esattamente quali operazioni di gestione sono state eseguite sul insieme di credenziali backup hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="3117d-214">Registri operazioni abilitare grande finale e il supporto per operazioni di backup hello di controllo.</span><span class="sxs-lookup"><span data-stu-id="3117d-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="3117d-215">Hello dopo le operazioni viene registrata nei log operazioni:</span><span class="sxs-lookup"><span data-stu-id="3117d-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="3117d-216">Registra</span><span class="sxs-lookup"><span data-stu-id="3117d-216">Register</span></span>
* <span data-ttu-id="3117d-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="3117d-217">Unregister</span></span>
* <span data-ttu-id="3117d-218">Configura protezione</span><span class="sxs-lookup"><span data-stu-id="3117d-218">Configure protection</span></span>
* <span data-ttu-id="3117d-219">Backup (sia backup pianificato che su richiesta tramite BackupNow)</span><span class="sxs-lookup"><span data-stu-id="3117d-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="3117d-220">Ripristino</span><span class="sxs-lookup"><span data-stu-id="3117d-220">Restore</span></span>
* <span data-ttu-id="3117d-221">Arresta protezione</span><span class="sxs-lookup"><span data-stu-id="3117d-221">Stop protection</span></span>
* <span data-ttu-id="3117d-222">Elimina dati di backup</span><span class="sxs-lookup"><span data-stu-id="3117d-222">Delete backup data</span></span>
* <span data-ttu-id="3117d-223">Aggiungi criteri</span><span class="sxs-lookup"><span data-stu-id="3117d-223">Add policy</span></span>
* <span data-ttu-id="3117d-224">Elimina criteri</span><span class="sxs-lookup"><span data-stu-id="3117d-224">Delete policy</span></span>
* <span data-ttu-id="3117d-225">Aggiorna criteri</span><span class="sxs-lookup"><span data-stu-id="3117d-225">Update policy</span></span>
* <span data-ttu-id="3117d-226">Annulla processo</span><span class="sxs-lookup"><span data-stu-id="3117d-226">Cancel job</span></span>

<span data-ttu-id="3117d-227">operazione tooview registra l'insieme di credenziali backup tooa corrispondente:</span><span class="sxs-lookup"><span data-stu-id="3117d-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="3117d-228">Passare troppo**servizi di gestione** nel portale di Azure, quindi fare clic su hello **registri operazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="3117d-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Log delle operazioni](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="3117d-230">Nei filtri di hello selezionare **Backup** come *tipo* e specificare il nome dell'insieme di credenziali backup hello in *nome servizio* e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="3117d-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro dei log operazioni](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="3117d-232">Nei registri operazioni hello, selezionare qualsiasi operazione e fare clic su **dettagli** toosee dettagli operazione tooan corrispondente.</span><span class="sxs-lookup"><span data-stu-id="3117d-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Log operazioni: recupero dei dettagli](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="3117d-234">Hello **guidata dettagli** contiene informazioni sull'operazione hello attivato, il processo, Id di risorsa in cui viene attivata, questa operazione e ora di inizio dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Dettagli operazione](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="3117d-236">Notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="3117d-236">Alert notifications</span></span>
<span data-ttu-id="3117d-237">È possibile ottenere le notifiche di avviso personalizzate per i processi di hello nel portale.</span><span class="sxs-lookup"><span data-stu-id="3117d-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="3117d-238">Questo risultato si ottiene definendo le regole di avviso basate su PowerShell negli eventi dei log operativi.</span><span class="sxs-lookup"><span data-stu-id="3117d-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="3117d-239">Si raccomanda di utilizzare *PowerShell 1.3.0 o versioni successive*.</span><span class="sxs-lookup"><span data-stu-id="3117d-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="3117d-240">toodefine tooalert una notifica personalizzata per gli errori di backup, un comando di esempio sarà simile:</span><span class="sxs-lookup"><span data-stu-id="3117d-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="3117d-241">**ResourceId**: è possibile ottenere queste informazioni dalla finestra popup Log operazioni come descritto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="3117d-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="3117d-242">Nella finestra popup di dettagli di un'operazione ResourceUri è hello ResourceId toobe fornito per questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3117d-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="3117d-243">**OperationName**: trattarsi del formato hello "Microsoft.Backup/backupvault/<EventName>" dove EventName è uno di registrare, annullare la registrazione, ConfigureProtection, Backup, ripristino, StopProtection, DeleteBackupData, UpdateProtectionPolicy CreateProtectionPolicy, DeleteProtectionPolicy,</span><span class="sxs-lookup"><span data-stu-id="3117d-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="3117d-244">**Status**: i valori supportati sono Started, Succeeded e Failed.</span><span class="sxs-lookup"><span data-stu-id="3117d-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="3117d-245">**Gruppo di risorse**: gruppo di risorse della risorsa hello in cui viene attivata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="3117d-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="3117d-246">È possibile ottenere queste informazioni dal valore di ResourceId.</span><span class="sxs-lookup"><span data-stu-id="3117d-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="3117d-247">Valore compreso tra i campi */ResourceGroups /* e */providers/* in ResourceId corrisponde al valore hello per gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3117d-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="3117d-248">**Nome**: nome della regola di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="3117d-249">**CustomEmail**: specificare toowhich indirizzo di posta elettronica personalizzati hello toosend notifica di avviso</span><span class="sxs-lookup"><span data-stu-id="3117d-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="3117d-250">**SendToServiceOwners**: questa opzione Invia gli amministratori tooall notifica di avviso e i coamministratori della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="3117d-251">Può essere usata nel cmdlet **New AzureRmAlertRuleEmail** .</span><span class="sxs-lookup"><span data-stu-id="3117d-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="3117d-252">Limitazioni per gli avvisi</span><span class="sxs-lookup"><span data-stu-id="3117d-252">Limitations on Alerts</span></span>
<span data-ttu-id="3117d-253">Avvisi basati su eventi sono sottoposti toohello limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3117d-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="3117d-254">Gli avvisi vengono attivati in tutte le macchine virtuali nell'insieme di credenziali backup hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="3117d-255">Non è possibile personalizzare il tooget gli avvisi per un set specifico di macchine virtuali in un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="3117d-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="3117d-256">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="3117d-256">This feature is in Preview.</span></span> [<span data-ttu-id="3117d-257">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="3117d-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="3117d-258">Si riceveranno avvisi da "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="3117d-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="3117d-259">Attualmente non è possibile modificare il mittente di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="3117d-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3117d-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3117d-260">Next steps</span></span>
* [<span data-ttu-id="3117d-261">Ripristinare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3117d-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
