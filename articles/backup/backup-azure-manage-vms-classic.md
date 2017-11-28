---
title: Gestire e monitorare i backup della macchina virtuale di Azure | Documentazione Microsoft
description: Informazioni su come gestire e monitorare i backup della macchina virtuale di Azure
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
ms.openlocfilehash: d876bb1759600fa29a26730bfa8b4ec19db1e442
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="27c24-103">Gestire i processi di Backup di Azure comuni e attivare gli avvisi nel portale classico</span><span class="sxs-lookup"><span data-stu-id="27c24-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27c24-104">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="27c24-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="27c24-105">Gestire i backup delle macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="27c24-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="27c24-106">In questo articolo vengono fornite informazioni sulle comuni attività di gestione e monitoraggio per le macchine virtuali modello classico protette in Azure.</span><span class="sxs-lookup"><span data-stu-id="27c24-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="27c24-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="27c24-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="27c24-108">Per informazioni dettagliate sull'utilizzo delle macchine virtuali con il modello di distribuzione classica, vedere [Preparare l'ambiente per il backup di macchine virtuali di Azure](backup-azure-vms-prepare.md) .</span><span class="sxs-lookup"><span data-stu-id="27c24-108">See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="27c24-109">A partire da marzo 2017, non è più possibile usare il portale classico per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-109">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="27c24-110">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="27c24-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="27c24-111">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="27c24-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="27c24-112">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="27c24-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="27c24-113">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="27c24-114">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="27c24-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="27c24-115">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="27c24-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="27c24-116">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="27c24-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="27c24-117">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="27c24-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="27c24-118">Gestire le macchine virtuali protette</span><span class="sxs-lookup"><span data-stu-id="27c24-118">Manage protected virtual machines</span></span>
<span data-ttu-id="27c24-119">Per gestire le macchine virtuali protette:</span><span class="sxs-lookup"><span data-stu-id="27c24-119">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="27c24-120">Per visualizzare e gestire le impostazioni di backup per una macchina virtuale, fare clic sulla scheda **Elementi protetti** .</span><span class="sxs-lookup"><span data-stu-id="27c24-120">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="27c24-121">Fare clic sul nome di un elemento protetto per visualizzare la scheda **Dettagli backup** contenente le informazioni sull'ultimo backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-121">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="27c24-123">Per visualizzare e gestire le impostazioni dei criteri di backup per una macchina virtuale fare clic sulla scheda **Criteri** .</span><span class="sxs-lookup"><span data-stu-id="27c24-123">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="27c24-125">Nella scheda **Criteri di backup** vengono visualizzati i criteri esistenti.</span><span class="sxs-lookup"><span data-stu-id="27c24-125">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="27c24-126">È possibile modificare i criteri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="27c24-126">You can modify as needed.</span></span> <span data-ttu-id="27c24-127">Se è necessario creare un nuovo criterio, fare clic su **Crea** nella pagina **Criteri**.</span><span class="sxs-lookup"><span data-stu-id="27c24-127">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="27c24-128">Si noti che un criterio può essere rimosso solo se non ha alcuna macchina virtuale associata.</span><span class="sxs-lookup"><span data-stu-id="27c24-128">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="27c24-130">È possibile ottenere altre informazioni sulle azioni o sullo stato di una macchina virtuale nella pagina **Processi** .</span><span class="sxs-lookup"><span data-stu-id="27c24-130">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="27c24-131">Fare clic su un processo nell'elenco per ottenere informazioni dettagliate oppure filtrare i processi per una macchina virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="27c24-131">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![Processi](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="27c24-133">Backup su richiesta di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="27c24-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="27c24-134">È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione.</span><span class="sxs-lookup"><span data-stu-id="27c24-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="27c24-135">Se il backup iniziale è in sospeso per la macchina virtuale, il backup su richiesta creerà una copia completa della macchina virtuale nell'insieme di credenziali di backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="27c24-135">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="27c24-136">Se il primo backup è stato completato, il backup su richiesta invierà all'insieme di credenziali di Backup di Azure solo le modifiche effettuate dopo il backup precedente.</span><span class="sxs-lookup"><span data-stu-id="27c24-136">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="27c24-137">Il periodo di conservazione dei dati di un backup su richiesta è impostato al valore specificato per la conservazione giornaliera nei criteri di conservazione corrispondenti alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-137">Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.</span></span>  
>
>

<span data-ttu-id="27c24-138">Per eseguire un backup su richiesta di una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="27c24-138">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="27c24-139">Passare alla pagina **Elementi protetti** e selezionare **Macchina virtuale di Azure** come **Tipo**, se non è già selezionata, quindi fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="27c24-139">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="27c24-141">Selezionare la macchina virtuale su cui si vuole eseguire un backup su richiesta e fare clic sul pulsante **Esegui backup ora** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="27c24-141">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![Esegui backup](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="27c24-143">Verrà creato un processo di backup nella macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="27c24-143">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="27c24-144">L'intervallo di conservazione del punto di ripristino creato tramite questo processo sarà uguale a quello specificato nei criteri associati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-144">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![Creazione del processo di backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="27c24-146">Per visualizzare i criteri associati a una macchina virtuale, eseguire il drill-down nella macchina virtuale nella pagina **Elementi protetti** e passare alla scheda dei criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-146">To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="27c24-147">Dopo la creazione del processo, è possibile fare clic sul pulsante **Visualizza processo** sulla barra degli strumenti per visualizzare il processo corrispondente nella pagina dei processi.</span><span class="sxs-lookup"><span data-stu-id="27c24-147">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![Processo di backup creato](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="27c24-149">Dopo il completamento corretto del processo, verrà creato un punto di ripristino che potrà essere usato per ripristinare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-149">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="27c24-150">Ciò incrementerà anche di 1 il valore della colonna del punto di ripristino nella pagina **Elementi protetti** .</span><span class="sxs-lookup"><span data-stu-id="27c24-150">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="27c24-151">Arrestare la protezione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="27c24-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="27c24-152">È possibile scegliere di arrestare i backup futuri di una macchina virtuale con le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="27c24-152">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="27c24-153">Mantenere i dati di backup associati alla macchina virtuale nell'insieme di credenziali di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="27c24-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="27c24-154">Eliminare i dati di backup associati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="27c24-155">Se si è scelto di conservare i dati di backup associati alla macchina virtuale, è possibile usarli per ripristinare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-155">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="27c24-156">Per i dettagli relativi ai prezzi per queste macchine virtuali, fare clic [qui](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="27c24-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="27c24-157">Per arrestare la protezione per una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="27c24-157">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="27c24-158">Passare alla pagina **Elementi protetti** e selezionare **Macchina virtuale di Azure** come tipo di filtro, se non è già selezionata, quindi fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="27c24-158">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="27c24-160">Selezionare la macchina virtuale e fare clic su **Arresta protezione** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="27c24-160">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="27c24-162">Per impostazione predefinita, il backup di Azure non elimina i dati di backup associati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-162">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="27c24-164">Per eliminare i dati di backup, selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="27c24-164">If you want to delete backup data, select the check box.</span></span>

    ![Casella di controllo](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="27c24-166">Selezionare un motivo per l'arresto del backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-166">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="27c24-167">Benché ciò sia facoltativo, specificando un motivo si consentirà a Backup di Azure di valutare i commenti e i suggerimenti e di assegnare priorità idonee agli scenari dei clienti.</span><span class="sxs-lookup"><span data-stu-id="27c24-167">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="27c24-168">Fare clic su **Invia** per inviare il processo **Arresta protezione**.</span><span class="sxs-lookup"><span data-stu-id="27c24-168">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="27c24-169">Fare clic su **Visualizza processo** per visualizzare il processo corrispondente nella pagina **Processi**.</span><span class="sxs-lookup"><span data-stu-id="27c24-169">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="27c24-171">Se non è stata selezionata l'opzione **Elimina i dati di backup associati** durante la procedura guidata **Arresta protezione**, dopo il completamento del processo lo stato della protezione verrà cambiato in **Protezione arrestata**.</span><span class="sxs-lookup"><span data-stu-id="27c24-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="27c24-172">I dati rimangono in Azure Backup finché non vengono eliminati esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="27c24-172">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="27c24-173">È comunque possibile eliminare i dati selezionando la macchina virtuale nella pagina **Elementi protetti** e facendo clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="27c24-173">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="27c24-175">Se è stata selezionata l'opzione **Elimina i dati di backup associati**, la macchina virtuale non sarà inclusa nella pagina **Elementi protetti**.</span><span class="sxs-lookup"><span data-stu-id="27c24-175">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="27c24-176">Riattivare la protezione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="27c24-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="27c24-177">Se non è stata selezionata l'opzione **Elimina i dati di backup associati** in **Arresta protezione**, sarà possibile riattivare la protezione della macchina virtuale eseguendo una procedura analoga al backup di macchine virtuali registrate.</span><span class="sxs-lookup"><span data-stu-id="27c24-177">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="27c24-178">Dopo la protezione, i dati di backup di questa macchina virtuale verranno conservati prima dell'arresto della protezione e verranno creati punti di ripristino dopo la riattivazione della protezione.</span><span class="sxs-lookup"><span data-stu-id="27c24-178">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="27c24-179">Dopo la riattivazione della protezione, lo stato di protezione della macchina virtuale verrà cambiato in **Protetto** se sono presenti punti di ripristino prima di **Arresta protezione**.</span><span class="sxs-lookup"><span data-stu-id="27c24-179">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![Protezione VM riattivata](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="27c24-181">Quando si riattiva la protezione della macchina virtuale, è possibile scegliere un criterio diverso rispetto ai criteri con cui la macchina virtuale è stata protetta inizialmente.</span><span class="sxs-lookup"><span data-stu-id="27c24-181">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="27c24-182">Annullare la registrazione di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="27c24-182">Unregister virtual machines</span></span>
<span data-ttu-id="27c24-183">Per rimuovere la macchina virtuale dall'insieme di credenziali per il backup:</span><span class="sxs-lookup"><span data-stu-id="27c24-183">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="27c24-184">Fare clic sul pulsante **ANNULLA REGISTRAZIONE** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="27c24-184">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![Disabilita protezione](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="27c24-186">Verrà visualizzata una notifica di tipo avviso popup nella parte inferiore della schermata di richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="27c24-186">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="27c24-187">Fare clic su **Sì** per continuare.</span><span class="sxs-lookup"><span data-stu-id="27c24-187">Click **YES** to continue.</span></span>

    ![Disabilita protezione](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="27c24-189">Eliminare i dati di backup</span><span class="sxs-lookup"><span data-stu-id="27c24-189">Delete Backup data</span></span>
<span data-ttu-id="27c24-190">È possibile eliminare i dati di backup associati a una macchina virtuale in due modi:</span><span class="sxs-lookup"><span data-stu-id="27c24-190">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="27c24-191">Durante il processo Arresta protezione</span><span class="sxs-lookup"><span data-stu-id="27c24-191">During Stop Protection Job</span></span>
* <span data-ttu-id="27c24-192">Dopo il completamento del processo Arresta protezione in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="27c24-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="27c24-193">Per eliminare i dati di backup in una macchina virtuale con stato *Protezione arrestata* dopo il completamento corretto di un processo **Arresta backup** :</span><span class="sxs-lookup"><span data-stu-id="27c24-193">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="27c24-194">Passare alla pagina **Elementi protetti** e selezionare **Macchina virtuale di Azure** come *Tipo*, quindi fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="27c24-194">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="27c24-196">Selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27c24-196">Select the virtual machine.</span></span> <span data-ttu-id="27c24-197">Lo stato della macchina virtuale sarà **Protezione arrestata** .</span><span class="sxs-lookup"><span data-stu-id="27c24-197">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="27c24-199">Fare clic sul pulsante **ELIMINA** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="27c24-199">Click the **DELETE** button at the bottom of the page.</span></span>

    ![Elimina backup](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="27c24-201">Nella procedura guidata **Elimina dati di backup** selezionare un motivo per l'eliminazione dei dati di backup (opzione consigliata) e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="27c24-201">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Elimina dati di backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="27c24-203">Verrà creato un processo per l'eliminazione dei dati di backup di una macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="27c24-203">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="27c24-204">Fare clic su **Visualizza processo** per visualizzare il processo corrispondente nella pagina Processi.</span><span class="sxs-lookup"><span data-stu-id="27c24-204">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![Eliminazione dei dati completata](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="27c24-206">Dopo il completamento del processo, la voce corrispondente alla macchina virtuale verrà rimossa dalla pagina **Elementi protetti** .</span><span class="sxs-lookup"><span data-stu-id="27c24-206">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="27c24-207">Dashboard</span><span class="sxs-lookup"><span data-stu-id="27c24-207">Dashboard</span></span>
<span data-ttu-id="27c24-208">Nella pagina **Dashboard** è possibile esaminare le informazioni sulle macchine virtuali di Azure, le relative risorse di archiviazione e i processi associati nelle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="27c24-208">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="27c24-209">È possibile visualizzare lo stato del backup ed eventuali errori di backup associati.</span><span class="sxs-lookup"><span data-stu-id="27c24-209">You can view backup status and any associated backup errors.</span></span>

![Dashboard](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="27c24-211">I valori nel dashboard vengono aggiornati ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="27c24-211">Values in the dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="27c24-212">Operazioni di controllo</span><span class="sxs-lookup"><span data-stu-id="27c24-212">Auditing Operations</span></span>
<span data-ttu-id="27c24-213">Backup di Azure consente di esaminare i "log operazioni" delle operazioni di backup attivate dal cliente, per vedere più facilmente e con esattezza quali operazioni di gestione sono state eseguite nell'insieme di credenziali per il backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-213">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="27c24-214">I log operazioni offrono un ottimo supporto per i controlli e le relazioni finali sulle operazioni di backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-214">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="27c24-215">Le operazioni seguenti vengono registrate nei log operazioni:</span><span class="sxs-lookup"><span data-stu-id="27c24-215">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="27c24-216">Registra</span><span class="sxs-lookup"><span data-stu-id="27c24-216">Register</span></span>
* <span data-ttu-id="27c24-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="27c24-217">Unregister</span></span>
* <span data-ttu-id="27c24-218">Configura protezione</span><span class="sxs-lookup"><span data-stu-id="27c24-218">Configure protection</span></span>
* <span data-ttu-id="27c24-219">Backup (sia backup pianificato che su richiesta tramite BackupNow)</span><span class="sxs-lookup"><span data-stu-id="27c24-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="27c24-220">Ripristino</span><span class="sxs-lookup"><span data-stu-id="27c24-220">Restore</span></span>
* <span data-ttu-id="27c24-221">Arresta protezione</span><span class="sxs-lookup"><span data-stu-id="27c24-221">Stop protection</span></span>
* <span data-ttu-id="27c24-222">Elimina dati di backup</span><span class="sxs-lookup"><span data-stu-id="27c24-222">Delete backup data</span></span>
* <span data-ttu-id="27c24-223">Aggiungi criteri</span><span class="sxs-lookup"><span data-stu-id="27c24-223">Add policy</span></span>
* <span data-ttu-id="27c24-224">Elimina criteri</span><span class="sxs-lookup"><span data-stu-id="27c24-224">Delete policy</span></span>
* <span data-ttu-id="27c24-225">Aggiorna criteri</span><span class="sxs-lookup"><span data-stu-id="27c24-225">Update policy</span></span>
* <span data-ttu-id="27c24-226">Annulla processo</span><span class="sxs-lookup"><span data-stu-id="27c24-226">Cancel job</span></span>

<span data-ttu-id="27c24-227">Per visualizzare i log operazioni corrispondenti all'insieme di credenziali per il backup:</span><span class="sxs-lookup"><span data-stu-id="27c24-227">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="27c24-228">Nel portale di Azure passare a **Servizi di gestione** e quindi fare clic sulla scheda **Log operazioni**.</span><span class="sxs-lookup"><span data-stu-id="27c24-228">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![Log delle operazioni](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="27c24-230">Nell'area dei filtri selezionare **Backup** come *Tipo*, specificare il nome dell'insieme di credenziali per il backup in *nome servizio* e fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="27c24-230">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro dei log operazioni](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="27c24-232">Nei log operazioni selezionare un'operazione qualsiasi e fare clic su **Dettagli** per visualizzare le informazioni corrispondenti a un'operazione.</span><span class="sxs-lookup"><span data-stu-id="27c24-232">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![Log operazioni: recupero dei dettagli](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="27c24-234">La procedura guidata **Dettagli** include informazioni su operazione attivate, ID processo, risorsa nella quale è stata attivata l'operazione e la relativa data di inizio.</span><span class="sxs-lookup"><span data-stu-id="27c24-234">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![Dettagli operazione](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="27c24-236">Notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="27c24-236">Alert notifications</span></span>
<span data-ttu-id="27c24-237">Nel portale è possibile ottenere notifiche di avviso personalizzate per i processi.</span><span class="sxs-lookup"><span data-stu-id="27c24-237">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="27c24-238">Questo risultato si ottiene definendo le regole di avviso basate su PowerShell negli eventi dei log operativi.</span><span class="sxs-lookup"><span data-stu-id="27c24-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="27c24-239">Si raccomanda di utilizzare *PowerShell 1.3.0 o versioni successive*.</span><span class="sxs-lookup"><span data-stu-id="27c24-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="27c24-240">Per definire una notifica di avviso personalizzata per gli errori di backup, ecco un comando di esempio:</span><span class="sxs-lookup"><span data-stu-id="27c24-240">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="27c24-241">**ResourceId**: è possibile ottenere queste informazioni dalla finestra popup Log operazioni come descritto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="27c24-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="27c24-242">ResourceUri nella finestra popup dei dettagli di un'operazione è il valore di ResourceId da fornire per questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27c24-242">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="27c24-243">**OperationName**: questa proprietà è in questo formato "Microsoft.Backup/backupvault/<EventName>" dove EventName può essere uno dei seguenti eventi: Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="27c24-243">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="27c24-244">**Status**: i valori supportati sono Started, Succeeded e Failed.</span><span class="sxs-lookup"><span data-stu-id="27c24-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="27c24-245">**ResourceGroup**: gruppo di risorse della risorsa in cui viene attivata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="27c24-245">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="27c24-246">È possibile ottenere queste informazioni dal valore di ResourceId.</span><span class="sxs-lookup"><span data-stu-id="27c24-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="27c24-247">Il valore tra i campi */resourceGroups/* e */providers/* nel valore ResourceId è il valore per ResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="27c24-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="27c24-248">**Name**: nome della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="27c24-248">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="27c24-249">**CustomEmail**: specificare l'indirizzo di posta elettronica personalizzato a cui dovrà essere inviata la notifica di avviso.</span><span class="sxs-lookup"><span data-stu-id="27c24-249">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="27c24-250">**SendToServiceOwners**: questa opzione invia la notifica di avviso a tutti gli amministratori e i coamministratori della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="27c24-250">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="27c24-251">Può essere usata nel cmdlet **New AzureRmAlertRuleEmail** .</span><span class="sxs-lookup"><span data-stu-id="27c24-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="27c24-252">Limitazioni per gli avvisi</span><span class="sxs-lookup"><span data-stu-id="27c24-252">Limitations on Alerts</span></span>
<span data-ttu-id="27c24-253">Gli avvisi basati su eventi sono soggetti alle limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="27c24-253">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="27c24-254">Gli avvisi vengono attivati in tutte le macchine virtuali nell'insieme di credenziali per il backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-254">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="27c24-255">Non è possibile personalizzare l'impostazione per ricevere avvisi per un set specifico di macchine virtuali in un insieme di credenziali per il backup.</span><span class="sxs-lookup"><span data-stu-id="27c24-255">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="27c24-256">Questa funzionalità è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="27c24-256">This feature is in Preview.</span></span> [<span data-ttu-id="27c24-257">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="27c24-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="27c24-258">Si riceveranno avvisi da "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="27c24-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="27c24-259">Attualmente non è possibile modificare il mittente del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="27c24-259">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27c24-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27c24-260">Next steps</span></span>
* [<span data-ttu-id="27c24-261">Ripristinare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="27c24-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
