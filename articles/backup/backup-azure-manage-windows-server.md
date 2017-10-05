---
title: Gestire server e insiemi di credenziali di Servizi di ripristino di Azure | Microsoft Docs
description: Usare questa esercitazione per imparare a gestire server e insiemi di credenziali dei servizi di ripristino di Azure.
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
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="5a01b-103">Monitorare e gestire i server e gli insiemi di credenziali dei servizi di ripristino di Azure per i computer Windows</span><span class="sxs-lookup"><span data-stu-id="5a01b-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a01b-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="5a01b-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="5a01b-105">Classico</span><span class="sxs-lookup"><span data-stu-id="5a01b-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="5a01b-106">In questo articolo è disponibile una panoramica delle attività di gestione e monitoraggio dei backup disponibili tramite il portale di Azure e l'agente di Backup di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="5a01b-107">Questo articolo presuppone che sia già disponibile una sottoscrizione di Azure e che sia stato creato almeno un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="5a01b-108">Aprire un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="5a01b-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="5a01b-109">Il dashboard dell'insieme di credenziali di Servizi di ripristino visualizza i dettagli o attributi di un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="5a01b-110">Accedere al [portale di Azure](https://portal.azure.com/) usando la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="5a01b-111">Nel menu Hub fare clic su **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-111">On the Hub menu, click **More Services**.</span></span>

    ![Aprire l'elenco degli insiemi di credenziali di Servizi di ripristino](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="5a01b-113">Si vuole aprire un insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="5a01b-114">Nella finestra di dialogo, iniziare a digitare **Servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="5a01b-115">Non appena si inizia a digitare, l'elenco viene filtrato in base all'input.</span><span class="sxs-lookup"><span data-stu-id="5a01b-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="5a01b-116">Fare clic su **Insiemi di credenziali dei servizi di ripristino** per visualizzare l'elenco degli insiemi di credenziali di Servizi di ripristino presenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="5a01b-118">Verrà visualizzato l'elenco degli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-118">The list of Recovery Services vaults opens.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="5a01b-120">Nell'elenco degli insiemi di credenziali di Servizi di ripristino selezionare il nome dell'insieme da aprire.</span><span class="sxs-lookup"><span data-stu-id="5a01b-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="5a01b-121">Si apre il pannello del dashboard dell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![Dashboard dell'insieme di credenziali dei servizi di ripristino](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="5a01b-123">Dopo aver aperto l'insieme di credenziali di Servizi di ripristino, provare una delle attività di monitoraggio o gestione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="5a01b-124">Monitorare i processi di backup e gli avvisi</span><span class="sxs-lookup"><span data-stu-id="5a01b-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="5a01b-125">I processi e gli avvisi vengono monitorati dal dashboard dell'insieme di credenziali dei servizi di ripristino, dove vengono visualizzati:</span><span class="sxs-lookup"><span data-stu-id="5a01b-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="5a01b-126">Dettagli degli avvisi di backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-126">Backup alerts details</span></span>
* <span data-ttu-id="5a01b-127">File e cartelle, oltre alle macchine virtuali di Azure protette nel cloud</span><span class="sxs-lookup"><span data-stu-id="5a01b-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="5a01b-128">Spazio di archiviazione totale utilizzato in Azure</span><span class="sxs-lookup"><span data-stu-id="5a01b-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="5a01b-129">Stato dei processi di backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-129">Backup job status</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="5a01b-131">Fare clic sulle informazioni in ogni riquadro per aprire il pannello associato dove si gestiscono le attività correlate.</span><span class="sxs-lookup"><span data-stu-id="5a01b-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="5a01b-132">Nella parte superiore del dashboard:</span><span class="sxs-lookup"><span data-stu-id="5a01b-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="5a01b-133">Impostazioni: fornisce l'accesso alle attività di backup disponibili.</span><span class="sxs-lookup"><span data-stu-id="5a01b-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="5a01b-134">Backup: consente di eseguire il backup di nuovi file e cartelle (o VM di Azure) nell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="5a01b-135">Elimina: se un insieme di credenziali dei servizi di ripristino non è più in uso, è possibile eliminarlo per liberare spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="5a01b-136">L'opzione Elimina viene abilitata solo dopo l'eliminazione di tutti i server protetti dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="5a01b-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="5a01b-138">Avvisi per i backup con l'agente di Backup di Azure:</span><span class="sxs-lookup"><span data-stu-id="5a01b-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="5a01b-139">Livello avviso</span><span class="sxs-lookup"><span data-stu-id="5a01b-139">Alert Level</span></span> | <span data-ttu-id="5a01b-140">Avvisi inviati</span><span class="sxs-lookup"><span data-stu-id="5a01b-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="5a01b-141">Critico</span><span class="sxs-lookup"><span data-stu-id="5a01b-141">Critical</span></span> |<span data-ttu-id="5a01b-142">Errore di backup, errore di ripristino</span><span class="sxs-lookup"><span data-stu-id="5a01b-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="5a01b-143">Avviso</span><span class="sxs-lookup"><span data-stu-id="5a01b-143">Warning</span></span> |<span data-ttu-id="5a01b-144">Backup completato con avvisi (quando non viene eseguito il backup di meno di cento file a causa di problemi di danneggiamento e viene completato il backup di più di un milione di file)</span><span class="sxs-lookup"><span data-stu-id="5a01b-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="5a01b-145">Informazioni</span><span class="sxs-lookup"><span data-stu-id="5a01b-145">Informational</span></span> |<span data-ttu-id="5a01b-146">None</span><span class="sxs-lookup"><span data-stu-id="5a01b-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="5a01b-147">Gestire gli avvisi di backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-147">Manage Backup alerts</span></span>
<span data-ttu-id="5a01b-148">Fare clic sul riquadro **Avvisi di backup** per aprire il pannello **Avvisi di backup** e gestire gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5a01b-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Avvisi di backup](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="5a01b-150">Il riquadro Avvisi di backup mostra il numero di:</span><span class="sxs-lookup"><span data-stu-id="5a01b-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="5a01b-151">avvisi critici non risolti nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="5a01b-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="5a01b-152">avvertenze non risolte nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="5a01b-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="5a01b-153">Fare clic su ogni collegamento per passare al pannello **Avvisi di backup** con una visualizzazione filtrata di questi avvisi (critici o avvertenze).</span><span class="sxs-lookup"><span data-stu-id="5a01b-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="5a01b-154">Nel pannello Avvisi di backup è possibile:</span><span class="sxs-lookup"><span data-stu-id="5a01b-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="5a01b-155">Scegliere le informazioni appropriate da includere con gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5a01b-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Scegliere le colonne](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="5a01b-157">Filtrare gli avvisi per gravità, stato e ora di inizio/fine.</span><span class="sxs-lookup"><span data-stu-id="5a01b-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="5a01b-159">Configurare le notifiche in relazione a gravità, frequenza e destinatari, oltre ad attivare o disattivare gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5a01b-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="5a01b-161">Se si seleziona **Per ogni avviso** come frequenza per **Notifica**, nei messaggi di posta elettronica non vengono eseguiti raggruppamenti o riduzioni.</span><span class="sxs-lookup"><span data-stu-id="5a01b-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="5a01b-162">Ogni avviso restituisce 1 notifica.</span><span class="sxs-lookup"><span data-stu-id="5a01b-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="5a01b-163">Questa è l'impostazione predefinita e viene anche inviato immediatamente il messaggio di posta elettronica relativo alla risoluzione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="5a01b-164">Se si seleziona **Riepilogo orario** come frequenza per **Notifica**, viene inviato all'utente un messaggio di posta elettronica che informa che sono presenti nuovi avvisi non risolti generati nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="5a01b-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="5a01b-165">Allo scadere dell'ora viene inviato un messaggio di posta elettronica relativo alla risoluzione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="5a01b-166">Possono essere inviati avvisi per i livelli di gravità seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a01b-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="5a01b-167">Critico</span><span class="sxs-lookup"><span data-stu-id="5a01b-167">critical</span></span>
* <span data-ttu-id="5a01b-168">Avviso</span><span class="sxs-lookup"><span data-stu-id="5a01b-168">warning</span></span>
* <span data-ttu-id="5a01b-169">Informazioni</span><span class="sxs-lookup"><span data-stu-id="5a01b-169">information</span></span>

<span data-ttu-id="5a01b-170">Per disattivare l'avviso, usare il pulsante **Disattiva** nel pannello dei dettagli del processo.</span><span class="sxs-lookup"><span data-stu-id="5a01b-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="5a01b-171">Quando si fa clic su Disattiva, è possibile inserire note sulla risoluzione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="5a01b-172">Per scegliere le colonne da visualizzare nell'avviso, usare il pulsante **Scegli colonne** .</span><span class="sxs-lookup"><span data-stu-id="5a01b-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="5a01b-173">Nel pannello **Impostazioni** si gestiscono gli avvisi di backup selezionando **Monitoraggio e report > Avvisi ed eventi > Avvisi di backup** e quindi facendo clic su **Filtro** o su **Configura notifiche**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="5a01b-174">Gestire gli elementi di backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-174">Manage Backup items</span></span>
<span data-ttu-id="5a01b-175">Nel portale di gestione ora è disponibile la gestione dei backup locali.</span><span class="sxs-lookup"><span data-stu-id="5a01b-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="5a01b-176">Nella sezione Backup del dashboard il riquadro **Elementi di backup** indica il numero di elementi di backup protetti per l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="5a01b-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="5a01b-177">Fare clic su **File-cartelle** nel riquadro Elementi di backup.</span><span class="sxs-lookup"><span data-stu-id="5a01b-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Riquadro Elementi di backup](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="5a01b-179">Il pannello Elementi di backup si apre con il filtro impostato su File-cartella, dove è possibile vedere elencato ogni elemento di backup specifico.</span><span class="sxs-lookup"><span data-stu-id="5a01b-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Elementi di backup](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="5a01b-181">Se si seleziona un elemento di backup specifico nell'elenco, vengono visualizzati i dettagli più importanti dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="5a01b-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="5a01b-182">Nel pannello **Impostazioni** si gestiscono file e cartelle selezionando **Elementi protetti > Elementi di backup** e quindi scegliendo **File-Cartelle** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="5a01b-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="5a01b-184">Gestire i processi di backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-184">Manage Backup jobs</span></span>
<span data-ttu-id="5a01b-185">I processi di backup per i backup sia locali (quando il server locale esegue il backup in Azure) che di Azure sono visibili nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="5a01b-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="5a01b-186">Nella sezione Backup del dashboard il riquadro Processo di backup indica il numero di processi:</span><span class="sxs-lookup"><span data-stu-id="5a01b-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="5a01b-187">in corso</span><span class="sxs-lookup"><span data-stu-id="5a01b-187">in progress</span></span>
* <span data-ttu-id="5a01b-188">non riusciti nelle ultime 24 ore</span><span class="sxs-lookup"><span data-stu-id="5a01b-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="5a01b-189">Per gestire i processi di backup, fare clic sul riquadro **Processi di backup** per aprire il pannello Processi di backup.</span><span class="sxs-lookup"><span data-stu-id="5a01b-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="5a01b-191">Per modificare le informazioni disponibili nel pannello Processi di backup, usare il pulsante **Scegli colonne** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="5a01b-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="5a01b-192">Usare il pulsante **Filtro** per scegliere tra File e cartelle e Backup macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="5a01b-193">Se i file e le cartelle di cui è stato eseguito il backup non vengono visualizzati, fare clic sul pulsante **Filtro** nella parte superiore della pagina e scegliere **File e cartelle** dal menu Tipo di elemento.</span><span class="sxs-lookup"><span data-stu-id="5a01b-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="5a01b-194">Nel pannello **Impostazioni** si gestiscono i processi di Backup selezionando **Monitoraggio e report > Processi > Processi di backup** e quindi scegliendo **File-Cartelle** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="5a01b-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="5a01b-195">Monitorare l'utilizzo del backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-195">Monitor Backup usage</span></span>
<span data-ttu-id="5a01b-196">Nella sezione Backup del dashboard, il riquadro Utilizzo del backup indica lo spazio di archiviazione usato in Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="5a01b-197">L'utilizzo dello spazio di archiviazione viene fornito per:</span><span class="sxs-lookup"><span data-stu-id="5a01b-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="5a01b-198">Utilizzo dello spazio di archiviazione con ridondanza locale nel cloud associato all'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="5a01b-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="5a01b-199">Utilizzo dello spazio di archiviazione con ridondanza geografica nel cloud associato all'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="5a01b-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="5a01b-200">Gestire i server di produzione</span><span class="sxs-lookup"><span data-stu-id="5a01b-200">Manage your production servers</span></span>
<span data-ttu-id="5a01b-201">Per gestire i server di produzione, fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="5a01b-202">In Gestisci fare clic su **Infrastruttura di backup > Server di produzione**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="5a01b-203">Il pannello Server di produzione elenca tutti i server di produzione disponibili.</span><span class="sxs-lookup"><span data-stu-id="5a01b-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="5a01b-204">Fare clic su un server nell'elenco per aprire i dettagli del server.</span><span class="sxs-lookup"><span data-stu-id="5a01b-204">Click on a server in the list to open the server details.</span></span>

![Elementi protetti](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="5a01b-206">Aprire l'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="5a01b-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="5a01b-207">Aprire l'**agente di Backup di Microsoft Azure**. Per trovarlo, cercare nel computer *Backup di Microsoft Azure*.</span><span class="sxs-lookup"><span data-stu-id="5a01b-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="5a01b-209">Dalle **Azioni** disponibili a destra della console dell'agente di backup è possibile eseguire le attività di gestione seguenti:</span><span class="sxs-lookup"><span data-stu-id="5a01b-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="5a01b-210">Registra server</span><span class="sxs-lookup"><span data-stu-id="5a01b-210">Register Server</span></span>
* <span data-ttu-id="5a01b-211">Pianificazione di un backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-211">Schedule Backup</span></span>
* <span data-ttu-id="5a01b-212">Esegui backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-212">Back Up now</span></span>
* <span data-ttu-id="5a01b-213">Modifica proprietà</span><span class="sxs-lookup"><span data-stu-id="5a01b-213">Change Properties</span></span>

![Azioni della console dell'agente Backup di Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="5a01b-215">Per **ripristinare i dati**, vedere [Ripristinare file da un computer che esegue Windows Server o un client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="5a01b-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="5a01b-216">Modificare la pianificazione dei backup</span><span class="sxs-lookup"><span data-stu-id="5a01b-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="5a01b-217">Nell'agente di Backup di Microsoft Azure fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="5a01b-219">Nella **Pianificazione guidata backup** lasciare selezionata l'opzione **Modifica elementi o tempistica del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="5a01b-221">Per aggiungere o modificare elementi, nella schermata **Seleziona elementi per backup** fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="5a01b-222">In questa pagina della procedura guidata è anche possibile specificare le **Impostazioni di esclusione** .</span><span class="sxs-lookup"><span data-stu-id="5a01b-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="5a01b-223">Per escludere file o tipi di file, leggere la procedura per l'aggiunta di [impostazioni di esclusione](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="5a01b-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="5a01b-224">Selezionare i file e le cartelle di cui si vuole eseguire il backup e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="5a01b-226">Specificare la **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="5a01b-227">È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.</span><span class="sxs-lookup"><span data-stu-id="5a01b-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="5a01b-229">Per informazioni dettagliate su come specificare la pianificazione del backup, vedere questo [articolo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="5a01b-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="5a01b-230">Selezionare i **criteri di conservazione** per la copia di backup e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="5a01b-232">Nella schermata **Conferma** riesaminare le informazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="5a01b-233">Al termine della creazione della **pianificazione del backup** da parte della procedura guidata, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="5a01b-234">Dopo aver modificato la protezione, è possibile verificare che i backup vengano attivati correttamente passando alla scheda **Processi** e assicurandosi che le modifiche siano presenti nei processi di backup.</span><span class="sxs-lookup"><span data-stu-id="5a01b-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="5a01b-235">Abilitare la limitazione della larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="5a01b-235">Enable Network Throttling</span></span>

<span data-ttu-id="5a01b-236">L'agente Backup di Azure offre la scheda Limitazione larghezza di banda rete che consente di controllare la modalità d'uso della larghezza di banda della rete durante il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="5a01b-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="5a01b-237">Questo controllo può essere utile se è necessario eseguire il backup dei dati durante l'orario di lavoro, ma senza che il processo di backup interferisca con il resto del traffico Internet.</span><span class="sxs-lookup"><span data-stu-id="5a01b-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="5a01b-238">La limitazione del trasferimento dati si applica alle attività di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="5a01b-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="5a01b-239">Per abilitare la limitazione della larghezza di banda della rete:</span><span class="sxs-lookup"><span data-stu-id="5a01b-239">To enable throttling:</span></span>

1. <span data-ttu-id="5a01b-240">Nell'**agente di Backup** fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="5a01b-241">Nella scheda **Limitazione larghezza di banda rete selezionare **Abilita la limitazione all'utilizzo della larghezza di banda Internet per le operazioni di backup**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="5a01b-243">Dopo aver abilitato la limitazione, specificare la larghezza di banda consentita per il trasferimento dei dati di backup durante le **Ore lavorative** e le **Ore non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="5a01b-244">I valori della larghezza di banda partono da 512 kilobyte al secondo (Kbps) e possono arrivare fino a 1023 megabyte al secondo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="5a01b-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="5a01b-245">È anche possibile definire l'inizio e la fine per **Ore lavorative**e i giorni della settimana da considerare come giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="5a01b-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="5a01b-246">Le ore al di fuori delle ore lavorative specificate sono considerate non lavorative.</span><span class="sxs-lookup"><span data-stu-id="5a01b-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="5a01b-247">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="5a01b-248">Gestire le impostazioni di esclusione</span><span class="sxs-lookup"><span data-stu-id="5a01b-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="5a01b-249">Aprire l'**agente di Backup di Microsoft Azure**. Per trovarlo, cercare nel computer *Backup di Microsoft Azure*.</span><span class="sxs-lookup"><span data-stu-id="5a01b-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="5a01b-251">Nell'agente di Backup di Microsoft Azure fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="5a01b-253">Nella Pianificazione guidata backup lasciare selezionata l'opzione **Modifica elementi o tempistica del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="5a01b-255">Fare clic su **Impostazioni di esclusione**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-255">Click **Exclusions Settings**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="5a01b-257">Fare clic su **Aggiungi esclusione**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-257">Click **Add Exclusion**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="5a01b-259">Selezionare il percorso e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-259">Select the location and then, click **OK**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="5a01b-261">Aggiungere l'estensione di file nel campo **Tipo file** .</span><span class="sxs-lookup"><span data-stu-id="5a01b-261">Add the file extension in the **File Type** field.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="5a01b-263">Aggiunta di un'estensione mp3</span><span class="sxs-lookup"><span data-stu-id="5a01b-263">Adding an .mp3 extension</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="5a01b-265">Per aggiungere un'altra estensione, fare clic su **Aggiungi esclusione** e immettere l'estensione di un altro tipo di file, aggiungendo un'estensione jpeg.</span><span class="sxs-lookup"><span data-stu-id="5a01b-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="5a01b-267">Dopo aver aggiunto tutte le estensioni, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="5a01b-268">Continuare con la Pianificazione guidata backup facendo clic su **Avanti** fino alla **pagina Conferma**, quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="5a01b-270">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="5a01b-270">Frequently asked questions</span></span>
<span data-ttu-id="5a01b-271">**D1. Lo stato del processo di backup risulta completato nell'agente di Backup di Azure. Perché non è visibile immediatamente nel portale?**</span><span class="sxs-lookup"><span data-stu-id="5a01b-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="5a01b-272">R1.</span><span class="sxs-lookup"><span data-stu-id="5a01b-272">A1.</span></span> <span data-ttu-id="5a01b-273">C'è un ritardo massimo di 15 minuti tra lo stato del processo di backup visibile nell'agente di Backup di Azure e nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="5a01b-274">**D.2 Quando un processo di backup non riesce, quanto tempo passa prima che venga generato un avviso?**</span><span class="sxs-lookup"><span data-stu-id="5a01b-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="5a01b-275">R.2 Un avviso viene generato entro 20 minuti dall'errore di backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="5a01b-276">**D3. Esiste un caso in cui non viene inviato un messaggio di posta elettronica se le notifiche sono configurate?**</span><span class="sxs-lookup"><span data-stu-id="5a01b-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="5a01b-277">R3.</span><span class="sxs-lookup"><span data-stu-id="5a01b-277">A3.</span></span> <span data-ttu-id="5a01b-278">Di seguito sono indicati i casi in cui la notifica non verrà inviata per ridurre la frequenza degli avvisi:</span><span class="sxs-lookup"><span data-stu-id="5a01b-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="5a01b-279">Se le notifiche sono configurate su base oraria e un avviso viene generato e risolto entro l'ora</span><span class="sxs-lookup"><span data-stu-id="5a01b-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="5a01b-280">Il processo viene annullato.</span><span class="sxs-lookup"><span data-stu-id="5a01b-280">Job is canceled.</span></span>
* <span data-ttu-id="5a01b-281">Secondo processo di backup non riuscito perché è in corso il processo di backup originale.</span><span class="sxs-lookup"><span data-stu-id="5a01b-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="5a01b-282">Risoluzione dei problemi di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="5a01b-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="5a01b-283">**Problema:** i processi e/o gli avvisi generati dall'agente di Backup di Azure non vengono visualizzati nel portale.</span><span class="sxs-lookup"><span data-stu-id="5a01b-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="5a01b-284">**Procedura per la risoluzione del problema:** il processo, ```OBRecoveryServicesManagementAgent```, viene usato per inviare i dati dei processi e degli avvisi al servizio Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a01b-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="5a01b-285">A volte questo processo può risultare danneggiato o arrestato.</span><span class="sxs-lookup"><span data-stu-id="5a01b-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="5a01b-286">Per controllare se il processo si è arrestato, aprire **Gestione attività** e controllare se il processo ```OBRecoveryServicesManagementAgent``` è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5a01b-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="5a01b-287">Se il processo non è in esecuzione, aprire il **Pannello di controllo** e sfogliare l'elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="5a01b-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="5a01b-288">Avviare o riavviare **Agente di gestione di Servizi di ripristino di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a01b-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="5a01b-289">Per altre informazioni, sfogliare i log in:</span><span class="sxs-lookup"><span data-stu-id="5a01b-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="5a01b-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5a01b-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="5a01b-291">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a01b-291">Next steps</span></span>
* [<span data-ttu-id="5a01b-292">Ripristino di Windows Server o Windows Client da Azure</span><span class="sxs-lookup"><span data-stu-id="5a01b-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="5a01b-293">Per altre informazioni sul servizio Backup di Azure, vedere [Panoramica di Backup di Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="5a01b-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="5a01b-294">Visitare il [Forum su Backup di Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="5a01b-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
