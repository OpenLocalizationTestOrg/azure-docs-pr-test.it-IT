---
title: gli insiemi di credenziali e i server di servizi aaaManage Azure recovery | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come insiemi di credenziali di servizi di ripristino di Azure toomanage e server.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="b45b4-103">Monitorare e gestire i server e gli insiemi di credenziali dei servizi di ripristino di Azure per i computer Windows</span><span class="sxs-lookup"><span data-stu-id="b45b4-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b45b4-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="b45b4-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="b45b4-105">Classico</span><span class="sxs-lookup"><span data-stu-id="b45b4-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="b45b4-106">In questo articolo vengono fornite una panoramica di hello gestione e Monitoraggio attività di backup disponibili tramite hello Azure portal e hello Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="b45b4-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="b45b4-107">Questo articolo presuppone che sia già disponibile una sottoscrizione di Azure e che sia stato creato almeno un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="b45b4-108">Aprire un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="b45b4-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="b45b4-109">dashboard dell'insieme di credenziali di servizi di ripristino Hello è possibile visualizzare i dettagli di hello o attributi di un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="b45b4-110">Accedi toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b45b4-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="b45b4-111">Nel menu Hub hello, fare clic su **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-111">On hello Hub menu, click **More Services**.</span></span>

    ![Aprire l'elenco degli insiemi di credenziali di Servizi di ripristino](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="b45b4-113">Si desidera tooopen un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="b45b4-114">Nella finestra di dialogo hello inizia a digitare **servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="b45b4-115">Si inizia a digitare, elenco hello verrà filtrato in base all'input.</span><span class="sxs-lookup"><span data-stu-id="b45b4-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="b45b4-116">Fare clic su **insiemi di credenziali di servizi di ripristino** elenco hello toodisplay di servizi di ripristino di insiemi di credenziali nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b45b4-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="b45b4-118">verrà visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-118">hello list of Recovery Services vaults opens.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="b45b4-120">Dall'elenco di hello degli insiemi di credenziali, selezionare il nome di hello dell'archivio di servizi di ripristino si desidera tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="b45b4-121">verrà visualizzata la finestra di blade dashboard dell'insieme di credenziali di Hello servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![Dashboard dell'insieme di credenziali dei servizi di ripristino](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="b45b4-123">Ora che è stata aperta l'insieme di credenziali di servizi di ripristino hello, provare a eseguire una delle attività di monitoraggio o la gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="b45b4-124">Monitorare i processi di backup e gli avvisi</span><span class="sxs-lookup"><span data-stu-id="b45b4-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="b45b4-125">Monitorare i processi e avvisi da hello servizi di ripristino dell'insieme di credenziali dashboard, in cui vedere:</span><span class="sxs-lookup"><span data-stu-id="b45b4-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="b45b4-126">Dettagli degli avvisi di backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-126">Backup alerts details</span></span>
* <span data-ttu-id="b45b4-127">I file e cartelle, nonché macchine virtuali di Azure protette nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="b45b4-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="b45b4-128">Spazio di archiviazione totale utilizzato in Azure</span><span class="sxs-lookup"><span data-stu-id="b45b4-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="b45b4-129">Stato dei processi di backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-129">Backup job status</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="b45b4-131">Fare clic su informazioni hello in ognuno di questi riquadri aprirà blade di hello associata sarà possibile gestire le attività correlate.</span><span class="sxs-lookup"><span data-stu-id="b45b4-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="b45b4-132">Dall'alto hello di hello Dashboard:</span><span class="sxs-lookup"><span data-stu-id="b45b4-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="b45b4-133">Impostazioni: fornisce l'accesso alle attività di backup disponibili.</span><span class="sxs-lookup"><span data-stu-id="b45b4-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="b45b4-134">Insieme di credenziali di backup - consente il backup di nuovi file e cartelle (o macchine virtuali di Azure) toohello servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="b45b4-135">Delete - se l'insieme di credenziali dei servizi di un ripristino non è più utilizzato, è possibile eliminarla toofree spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b45b4-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="b45b4-136">Eliminazione è abilitata solo dopo aver eliminati tutti i server protetti dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="b45b4-138">Avvisi per i backup con l'agente di Backup di Azure:</span><span class="sxs-lookup"><span data-stu-id="b45b4-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="b45b4-139">Livello avviso</span><span class="sxs-lookup"><span data-stu-id="b45b4-139">Alert Level</span></span> | <span data-ttu-id="b45b4-140">Avvisi inviati</span><span class="sxs-lookup"><span data-stu-id="b45b4-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="b45b4-141">Critico</span><span class="sxs-lookup"><span data-stu-id="b45b4-141">Critical</span></span> |<span data-ttu-id="b45b4-142">Errore di backup, errore di ripristino</span><span class="sxs-lookup"><span data-stu-id="b45b4-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="b45b4-143">Avviso</span><span class="sxs-lookup"><span data-stu-id="b45b4-143">Warning</span></span> |<span data-ttu-id="b45b4-144">Backup completato con avvisi (quando meno di 100 file non sottoposti a backup a causa di problemi di toocorruption e più di un milione correttamente backup)</span><span class="sxs-lookup"><span data-stu-id="b45b4-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="b45b4-145">Informazioni</span><span class="sxs-lookup"><span data-stu-id="b45b4-145">Informational</span></span> |<span data-ttu-id="b45b4-146">None</span><span class="sxs-lookup"><span data-stu-id="b45b4-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="b45b4-147">Gestire gli avvisi di backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-147">Manage Backup alerts</span></span>
<span data-ttu-id="b45b4-148">Fare clic su hello **gli avvisi di Backup** riquadro tooopen hello **gli avvisi di Backup** blade e gestire gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b45b4-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Avvisi di backup](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="b45b4-150">gli avvisi di Backup Hello Mostra riquadro hello numero di:</span><span class="sxs-lookup"><span data-stu-id="b45b4-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="b45b4-151">avvisi critici non risolti nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="b45b4-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="b45b4-152">avvertenze non risolte nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="b45b4-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="b45b4-153">Facendo clic su ognuno di questi collegamenti accetta toohello **gli avvisi di Backup** pannello con una visualizzazione filtrata di questi avvisi (critici o avvisi).</span><span class="sxs-lookup"><span data-stu-id="b45b4-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="b45b4-154">Dal pannello hello gli avvisi di Backup è:</span><span class="sxs-lookup"><span data-stu-id="b45b4-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="b45b4-155">Scegliere hello informazioni appropriate tooinclude con gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b45b4-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Scegliere le colonne](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="b45b4-157">Filtrare gli avvisi per gravità, stato e ora di inizio/fine.</span><span class="sxs-lookup"><span data-stu-id="b45b4-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="b45b4-159">Configurare le notifiche in relazione a gravità, frequenza e destinatari, oltre ad attivare o disattivare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b45b4-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="b45b4-161">Se **per ogni avviso** sia selezionato come hello **notifica** frequenza viene eseguita alcuna raggruppamento o la riduzione di messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b45b4-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="b45b4-162">Ogni avviso restituisce 1 notifica.</span><span class="sxs-lookup"><span data-stu-id="b45b4-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="b45b4-163">Questo è l'impostazione predefinita hello e posta elettronica risoluzione hello viene inoltre inviato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="b45b4-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="b45b4-164">Se **Digest oraria** sia selezionato come hello **notifica** frequenza un messaggio di posta elettronica viene inviato utente toohello informa che non vi siano risolti nuovi avvisi generati in hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="b45b4-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="b45b4-165">Viene inviato un messaggio di posta elettronica risoluzione alla fine hello ora hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="b45b4-166">Gli avvisi possono essere inviati per hello seguenti livelli di gravità:</span><span class="sxs-lookup"><span data-stu-id="b45b4-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="b45b4-167">Critico</span><span class="sxs-lookup"><span data-stu-id="b45b4-167">critical</span></span>
* <span data-ttu-id="b45b4-168">Avviso</span><span class="sxs-lookup"><span data-stu-id="b45b4-168">warning</span></span>
* <span data-ttu-id="b45b4-169">Informazioni</span><span class="sxs-lookup"><span data-stu-id="b45b4-169">information</span></span>

<span data-ttu-id="b45b4-170">Disattivare l'avviso di hello con hello **disattiva** pulsante nel Pannello di dettagli processo hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="b45b4-171">Quando si fa clic su Disattiva, è possibile inserire note sulla risoluzione.</span><span class="sxs-lookup"><span data-stu-id="b45b4-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="b45b4-172">Si scelgono le colonne di hello desiderato tooappear nell'ambito dell'avviso hello con hello **scegliere le colonne** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b45b4-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="b45b4-173">Da hello **impostazioni** pannello, gestire gli avvisi di backup selezionando **monitoraggio e report > avvisi ed eventi > avvisi di Backup** e quindi fare clic su **filtro** o ** Configurare le notifiche**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="b45b4-174">Gestire gli elementi di backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-174">Manage Backup items</span></span>
<span data-ttu-id="b45b4-175">È ora disponibile nel portale di gestione di hello la gestione dei backup in locale.</span><span class="sxs-lookup"><span data-stu-id="b45b4-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="b45b4-176">Nella sezione Backup hello del dashboard hello hello **gli elementi di Backup** riquadro mostra il numero di hello degli elementi di backup protetto toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b45b4-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="b45b4-177">Fare clic su **File-cartelle** in hello riquadro gli elementi di Backup.</span><span class="sxs-lookup"><span data-stu-id="b45b4-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Riquadro Elementi di backup](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="b45b4-179">gli elementi di Backup Hello blade viene aperto con hello filtrare set tooFile-cartella in cui si verifica ogni backup specifico elemento elencati.</span><span class="sxs-lookup"><span data-stu-id="b45b4-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Elementi di backup](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="b45b4-181">Se si seleziona un elemento di backup specifico dall'elenco di hello, vedrai informazioni essenziali di hello per quell'elemento.</span><span class="sxs-lookup"><span data-stu-id="b45b4-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="b45b4-182">Da hello **impostazioni** pannello gestire file e cartelle selezionando **elementi protetti > Backup elementi** e quindi selezionando **File-cartelle** da hello menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="b45b4-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="b45b4-184">Gestire i processi di backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-184">Manage Backup jobs</span></span>
<span data-ttu-id="b45b4-185">I processi di backup per i backup di Azure e locale (quando è il server locale hello backup tooAzure) sono visibili nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="b45b4-186">Nella sezione di Backup del dashboard hello hello, riquadro di processo di Backup hello Mostra il numero di hello di processi:</span><span class="sxs-lookup"><span data-stu-id="b45b4-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="b45b4-187">in corso</span><span class="sxs-lookup"><span data-stu-id="b45b4-187">in progress</span></span>
* <span data-ttu-id="b45b4-188">non è riuscita in hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="b45b4-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="b45b4-189">toomanage processi di backup, fare clic su hello **i processi di Backup** riquadro, che apre il pannello di hello i processi di Backup.</span><span class="sxs-lookup"><span data-stu-id="b45b4-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="b45b4-191">Modificare le informazioni di hello disponibili nel Pannello di processi di Backup hello con hello **scegliere le colonne** pulsante nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="b45b4-192">Hello utilizzare **filtro** tooselect pulsante tra file e cartelle e i backup di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b45b4-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="b45b4-193">Se non viene visualizzato stato eseguito il backup dei file e cartelle, fare clic su **filtro** pulsante nella parte superiore di hello della pagina hello e selezionare **file e cartelle** dal menu di tipo di elemento hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="b45b4-194">Da hello **impostazioni** pannello, gestire i processi di backup selezionando **monitoraggio e report > processi > processi di Backup** e quindi selezionando **File-cartelle** elenco hello menu.</span><span class="sxs-lookup"><span data-stu-id="b45b4-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="b45b4-195">Monitorare l'utilizzo del backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-195">Monitor Backup usage</span></span>
<span data-ttu-id="b45b4-196">Nella sezione di Backup del dashboard hello hello, riquadro di utilizzo di Backup hello Mostra archiviazione hello utilizzato in Azure.</span><span class="sxs-lookup"><span data-stu-id="b45b4-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="b45b4-197">L'utilizzo dello spazio di archiviazione viene fornito per:</span><span class="sxs-lookup"><span data-stu-id="b45b4-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="b45b4-198">Utilizzo dell'archiviazione con ridondanza locale associato all'insieme di credenziali hello del cloud</span><span class="sxs-lookup"><span data-stu-id="b45b4-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="b45b4-199">Utilizzo di memoria di archiviazione con ridondanza geografica cloud associato all'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="b45b4-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="b45b4-200">Gestire i server di produzione</span><span class="sxs-lookup"><span data-stu-id="b45b4-200">Manage your production servers</span></span>
<span data-ttu-id="b45b4-201">Fare clic su server di produzione, toomanage **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="b45b4-202">In Gestisci fare clic su **Infrastruttura di backup > Server di produzione**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="b45b4-203">elenchi di blade Hello Server di produzione di tutti i server di produzione disponibili.</span><span class="sxs-lookup"><span data-stu-id="b45b4-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="b45b4-204">Fare clic su un server di dettagli del server hello tooopen elenco hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-204">Click on a server in hello list tooopen hello server details.</span></span>

![Elementi protetti](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="b45b4-206">Agente di Backup di Azure aprire hello</span><span class="sxs-lookup"><span data-stu-id="b45b4-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="b45b4-207">Aprire hello **Microsoft Azure Backup agent** (disponibili tramite la ricerca di computer per *Backup di Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="b45b4-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="b45b4-209">Da hello **azioni** disponibile all'indirizzo hello destra della console di agente di backup hello è eseguire hello seguenti attività di gestione:</span><span class="sxs-lookup"><span data-stu-id="b45b4-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="b45b4-210">Registra server</span><span class="sxs-lookup"><span data-stu-id="b45b4-210">Register Server</span></span>
* <span data-ttu-id="b45b4-211">Pianificazione di un backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-211">Schedule Backup</span></span>
* <span data-ttu-id="b45b4-212">Esegui backup</span><span class="sxs-lookup"><span data-stu-id="b45b4-212">Back Up now</span></span>
* <span data-ttu-id="b45b4-213">Modifica proprietà</span><span class="sxs-lookup"><span data-stu-id="b45b4-213">Change Properties</span></span>

![Azioni della console dell'agente Backup di Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="b45b4-215">troppo**Ripristina dati**, vedere [ripristinare i file tooa Windows server o computer client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="b45b4-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="b45b4-216">Modifica pianificazione backup hello</span><span class="sxs-lookup"><span data-stu-id="b45b4-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="b45b4-217">Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="b45b4-219">In hello **pianificazione guidata Backup** lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="b45b4-221">Se si desidera tooadd o modificare gli elementi, di hello **selezionare elementi tooBackup** fare clic su schermo **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="b45b4-222">È inoltre possibile impostare **impostazioni di esclusione** da questa pagina nella creazione guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="b45b4-223">Se si desidera che il file tooexclude o procedura hello per l'aggiunta di leggere i tipi di file [impostazioni di esclusione](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="b45b4-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="b45b4-224">Selezionare il file hello e le cartelle desidera ripristinare tooback e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="b45b4-226">Specificare hello **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="b45b4-227">È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.</span><span class="sxs-lookup"><span data-stu-id="b45b4-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="b45b4-229">Specifica la pianificazione del backup hello è illustrata in dettaglio in questo [articolo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="b45b4-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="b45b4-230">Seleziona hello **criteri di conservazione** copia di backup hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="b45b4-232">In hello **conferma** schermata hello rivedere le informazioni e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="b45b4-233">Al termine della creazione di hello guidata hello **pianificazione del backup**, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="b45b4-234">Dopo la modifica della protezione, è possibile verificare che i backup attivano correttamente da passare toohello **processi** scheda e conferma che le modifiche vengono riflesse nel hello i processi di backup.</span><span class="sxs-lookup"><span data-stu-id="b45b4-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="b45b4-235">Abilitare la limitazione della larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="b45b4-235">Enable Network Throttling</span></span>

<span data-ttu-id="b45b4-236">l'agente Azure Backup Hello fornisce una scheda di limitazione delle richieste che consente di toocontrol modalità di utilizzo della larghezza di banda di rete durante il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="b45b4-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="b45b4-237">Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico internet.</span><span class="sxs-lookup"><span data-stu-id="b45b4-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="b45b4-238">La limitazione delle richieste di dati trasferimento applica tooback backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="b45b4-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="b45b4-239">tooenable limitazione:</span><span class="sxs-lookup"><span data-stu-id="b45b4-239">tooenable throttling:</span></span>

1. <span data-ttu-id="b45b4-240">In hello **agente di Backup**, fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="b45b4-241">In hello * * limitazione scheda, selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="b45b4-243">Dopo aver abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="b45b4-244">i valori di larghezza di banda Hello iniziano da 512 kilobyte per secondo (Kbps) e possono aumentare fino a too1023 megabyte al secondo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="b45b4-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="b45b4-245">È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello vengono considerati lavoro giorni.</span><span class="sxs-lookup"><span data-stu-id="b45b4-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="b45b4-246">tempo di Hello di fuori di hello designato per le ore lavorative è ore non lavorative toobe considerate.</span><span class="sxs-lookup"><span data-stu-id="b45b4-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="b45b4-247">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="b45b4-248">Gestire le impostazioni di esclusione</span><span class="sxs-lookup"><span data-stu-id="b45b4-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="b45b4-249">Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="b45b4-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="b45b4-251">Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="b45b4-253">In Pianificazione guidata Backup hello lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="b45b4-255">Fare clic su **Impostazioni di esclusione**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-255">Click **Exclusions Settings**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="b45b4-257">Fare clic su **Aggiungi esclusione**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-257">Click **Add Exclusion**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="b45b4-259">Selezionare il percorso di hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-259">Select hello location and then, click **OK**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="b45b4-261">Aggiungere l'estensione del file hello in hello **tipo di File** campo.</span><span class="sxs-lookup"><span data-stu-id="b45b4-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="b45b4-263">Aggiunta di un'estensione mp3</span><span class="sxs-lookup"><span data-stu-id="b45b4-263">Adding an .mp3 extension</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="b45b4-265">tooadd un'altra estensione, fare clic su **Aggiunta esclusione** e immettere un'altra estensione del tipo di file (aggiunta di un'estensione JPEG).</span><span class="sxs-lookup"><span data-stu-id="b45b4-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="b45b4-267">Dopo aver aggiunto tutte le estensioni di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="b45b4-268">Continuare il processo hello pianificazione guidata Backup fare clic su **Avanti** finché hello **pagina di conferma**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="b45b4-270">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="b45b4-270">Frequently asked questions</span></span>
<span data-ttu-id="b45b4-271">**Q1. stato del processo di backup Hello indicato come completato nel hello agente Azure backup, perché non vengono riflesse immediatamente nel portale?**</span><span class="sxs-lookup"><span data-stu-id="b45b4-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="b45b4-272">R1.</span><span class="sxs-lookup"><span data-stu-id="b45b4-272">A1.</span></span> <span data-ttu-id="b45b4-273">Si è in ritardo massimo di 15 minuti tra lo stato del processo di backup hello applicata hello agente Azure backup e hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b45b4-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="b45b4-274">**Q.2 quando un processo di backup non riesce, quanto tempo occorre tooraise un avviso?**</span><span class="sxs-lookup"><span data-stu-id="b45b4-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="b45b4-275">All'interno di 20 minuti di hello Azure backup non riusciti, viene generato un avviso. 2.</span><span class="sxs-lookup"><span data-stu-id="b45b4-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="b45b4-276">**D3. Esiste un caso in cui non viene inviato un messaggio di posta elettronica se le notifiche sono configurate?**</span><span class="sxs-lookup"><span data-stu-id="b45b4-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="b45b4-277">R3.</span><span class="sxs-lookup"><span data-stu-id="b45b4-277">A3.</span></span> <span data-ttu-id="b45b4-278">Di seguito sono casi hello quando non verrà inviate notifiche hello nella frequenza degli avvisi hello tooreduce ordine:</span><span class="sxs-lookup"><span data-stu-id="b45b4-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="b45b4-279">Se le notifiche sono configurate ogni ora e un avviso viene generato e risolto entro ora hello</span><span class="sxs-lookup"><span data-stu-id="b45b4-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="b45b4-280">Il processo viene annullato.</span><span class="sxs-lookup"><span data-stu-id="b45b4-280">Job is canceled.</span></span>
* <span data-ttu-id="b45b4-281">Secondo processo di backup non riuscito perché è in corso il processo di backup originale.</span><span class="sxs-lookup"><span data-stu-id="b45b4-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="b45b4-282">Risoluzione dei problemi di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="b45b4-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="b45b4-283">**Problema:** processi e/o gli avvisi generati da agente Azure Backup hello non vengono visualizzati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b45b4-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="b45b4-284">**Risoluzione dei problemi:** hello processo ```OBRecoveryServicesManagementAgent```, invia hello processo e avviso dati toohello servizio Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="b45b4-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="b45b4-285">A volte questo processo può risultare danneggiato o arrestato.</span><span class="sxs-lookup"><span data-stu-id="b45b4-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="b45b4-286">il processo di hello tooverify non è in esecuzione, aprire **Task Manager** e verificare se hello ```OBRecoveryServicesManagementAgent``` processo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b45b4-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="b45b4-287">Supponendo che il processo di hello non è in esecuzione, aprire **Pannello di controllo** e visualizzare hello elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="b45b4-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="b45b4-288">Avviare o riavviare **Agente di gestione di Servizi di ripristino di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b45b4-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="b45b4-289">Per ulteriori informazioni, visitare registri hello:</span><span class="sxs-lookup"><span data-stu-id="b45b4-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="b45b4-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b45b4-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="b45b4-291">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b45b4-291">Next steps</span></span>
* [<span data-ttu-id="b45b4-292">Ripristino di Windows Server o Windows Client da Azure</span><span class="sxs-lookup"><span data-stu-id="b45b4-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="b45b4-293">toolearn ulteriori informazioni sui Backup di Azure, vedere [Cenni preliminari su Backup di Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="b45b4-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="b45b4-294">Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="b45b4-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
