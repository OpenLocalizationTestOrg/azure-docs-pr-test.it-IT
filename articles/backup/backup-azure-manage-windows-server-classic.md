---
title: Gestire i server e gli insiemi di credenziali di Backup di Azure con il modello di distribuzione classica di Azure | Microsoft Docs
description: Utilizzare questa esercitazione per imparare a gestire server e insieme di credenziali di Backup di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="749a8-103">Gestire server e insiemi di credenziali di Backup di Azure con il modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="749a8-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="749a8-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="749a8-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="749a8-105">Classico</span><span class="sxs-lookup"><span data-stu-id="749a8-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="749a8-106">In questo articolo è disponibile una panoramica delle attività di gestione dei backup disponibili tramite il portale di Azure classico e l'agente di Backup di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="749a8-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="749a8-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="749a8-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="749a8-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="749a8-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="749a8-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="749a8-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="749a8-110">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="749a8-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="749a8-111">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="749a8-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="749a8-112">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="749a8-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="749a8-113">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="749a8-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="749a8-114">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="749a8-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="749a8-115">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="749a8-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="749a8-116">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="749a8-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="749a8-117">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="749a8-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="749a8-118">Attività del portale di gestione</span><span class="sxs-lookup"><span data-stu-id="749a8-118">Management portal tasks</span></span>
1. <span data-ttu-id="749a8-119">Accedere al [portale di gestione](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="749a8-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="749a8-120">Fare clic su **Servizi di ripristino**, quindi fare clic sul nome dell'insieme di credenziali per il backup per visualizzare la relativa pagina Avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="749a8-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Servizi di ripristino](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="749a8-122">Selezionando le opzioni nella parte superiore della pagina avvio rapido, è possibile visualizzare le attività di gestione disponibili.</span><span class="sxs-lookup"><span data-stu-id="749a8-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Gestire le schede](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="749a8-124">Dashboard</span><span class="sxs-lookup"><span data-stu-id="749a8-124">Dashboard</span></span>
<span data-ttu-id="749a8-125">Fare clic su **Dashboard** per visualizzare la panoramica sull'utilizzo del server.</span><span class="sxs-lookup"><span data-stu-id="749a8-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="749a8-126">La **panoramica sull'utilizzo** include:</span><span class="sxs-lookup"><span data-stu-id="749a8-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="749a8-127">Il numero di istanze di Windows Server registrate nel cloud</span><span class="sxs-lookup"><span data-stu-id="749a8-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="749a8-128">Il numero di macchine virtuali di Azure protette nel cloud</span><span class="sxs-lookup"><span data-stu-id="749a8-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="749a8-129">Lo spazio di archiviazione totale usato in Azure</span><span class="sxs-lookup"><span data-stu-id="749a8-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="749a8-130">Lo stato dei processi recenti</span><span class="sxs-lookup"><span data-stu-id="749a8-130">The status of recent jobs</span></span>

<span data-ttu-id="749a8-131">Nella parte inferiore del dashboard è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="749a8-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="749a8-132">**Gestisci certificato** : se è stato usato un certificato per registrare il server, usare questa azione per aggiornare il certificato.</span><span class="sxs-lookup"><span data-stu-id="749a8-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="749a8-133">Se si usano le credenziali di insieme, non usare la funzionalità **Gestisci certificato**.</span><span class="sxs-lookup"><span data-stu-id="749a8-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="749a8-134">**Elimina** : elimina l'insieme di credenziali di backup corrente.</span><span class="sxs-lookup"><span data-stu-id="749a8-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="749a8-135">Se un insieme di credenziali per il backup non è più in uso, è possibile eliminarlo per liberare spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="749a8-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="749a8-136">**Elimina** eliminazione viene abilitata solo dopo l'eliminazione di tutti i server registrati dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="749a8-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="749a8-138">Elementi registrati</span><span class="sxs-lookup"><span data-stu-id="749a8-138">Registered items</span></span>
<span data-ttu-id="749a8-139">Fare clic su **Elementi registrati** per visualizzare i nomi dei server registrati nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="749a8-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="749a8-141">Il valore predefinito del filtro **Tipo** è Macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="749a8-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="749a8-142">Per visualizzare i nomi dei server registrati nell'insieme di credenziali, scegliere **Windows Server** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="749a8-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="749a8-143">Da questo punto è possibile eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="749a8-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="749a8-144">**Consenti ripetizione della registrazione**: quando questa opzione è selezionata per un server, è possibile usare la **Registrazione in linea** nell'agente di Backup di Microsoft Azure per registrare nuovamente il server con l'insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="749a8-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="749a8-145">La ri-registrazione di un server può essere necessaria per un errore nel certificato, oppure se è stato necessario ricreare il server.</span><span class="sxs-lookup"><span data-stu-id="749a8-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="749a8-146">**Eliminare** - Consente di eliminare un server dall'insieme di credenziali per il backup.</span><span class="sxs-lookup"><span data-stu-id="749a8-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="749a8-147">Tutti i dati archiviati associati al server verranno eliminati immediatamente.</span><span class="sxs-lookup"><span data-stu-id="749a8-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Attività di Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="749a8-149">Elementi protetti</span><span class="sxs-lookup"><span data-stu-id="749a8-149">Protected items</span></span>
<span data-ttu-id="749a8-150">Fare clic su **Elementi protetti** per visualizzare gli elementi di cui è stato eseguito il backup dai server.</span><span class="sxs-lookup"><span data-stu-id="749a8-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Elementi protetti](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="749a8-152">Configurare</span><span class="sxs-lookup"><span data-stu-id="749a8-152">Configure</span></span>
<span data-ttu-id="749a8-153">Nella scheda **Configura** è possibile selezionare l'opzione di ridondanza di archiviazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="749a8-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="749a8-154">È consigliabile selezionare l'opzione per la ridondanza dell'archiviazione subito dopo la creazione di un insieme di credenziali e prima che i computer vengano registrati nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="749a8-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="749a8-155">Dopo la registrazione di un elemento nell'insieme di credenziali, l'opzione di ridondanza di archiviazione è bloccata e non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="749a8-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configurare](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="749a8-157">Per altre informazioni sulla [ridondanza di archiviazione](../storage/common/storage-redundancy.md), vedere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="749a8-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="749a8-158">Attività dell'agente Backup di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="749a8-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="749a8-159">Console</span><span class="sxs-lookup"><span data-stu-id="749a8-159">Console</span></span>
<span data-ttu-id="749a8-160">Aprire l'**agente di Backup di Microsoft Azure**. Per trovarlo, cercare nel computer *Backup di Microsoft Azure*.</span><span class="sxs-lookup"><span data-stu-id="749a8-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente di Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="749a8-162">Dalle **Azioni** disponibili a destra della console dell'agente di backup è possibile eseguire le attività di gestione seguenti:</span><span class="sxs-lookup"><span data-stu-id="749a8-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="749a8-163">Registra server</span><span class="sxs-lookup"><span data-stu-id="749a8-163">Register Server</span></span>
* <span data-ttu-id="749a8-164">Pianificazione di un backup</span><span class="sxs-lookup"><span data-stu-id="749a8-164">Schedule Backup</span></span>
* <span data-ttu-id="749a8-165">Esegui backup</span><span class="sxs-lookup"><span data-stu-id="749a8-165">Back Up now</span></span>
* <span data-ttu-id="749a8-166">Modifica proprietà</span><span class="sxs-lookup"><span data-stu-id="749a8-166">Change Properties</span></span>

![Azioni della console dell'agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="749a8-168">Per **ripristinare i dati**, vedere [Ripristinare file da un computer che esegue Windows Server o un client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="749a8-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="749a8-169">Modificare un backup esistente</span><span class="sxs-lookup"><span data-stu-id="749a8-169">Modify an existing backup</span></span>
1. <span data-ttu-id="749a8-170">Nell'agente di Backup di Microsoft Azure fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="749a8-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="749a8-172">Nella **Pianificazione guidata backup** lasciare selezionata l'opzione **Modifica elementi o tempistica del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="749a8-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificare un backup pianificato](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="749a8-174">Per aggiungere o modificare elementi, nella schermata **Seleziona elementi per backup** fare clic su **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="749a8-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="749a8-175">In questa pagina della procedura guidata è anche possibile specificare le **Impostazioni di esclusione** .</span><span class="sxs-lookup"><span data-stu-id="749a8-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="749a8-176">Per escludere file o tipi di file, leggere la procedura per l'aggiunta di [impostazioni di esclusione](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="749a8-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="749a8-177">Selezionare i file e le cartelle di cui si vuole eseguire il backup e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="749a8-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Aggiungi elementi](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="749a8-179">Specificare la **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="749a8-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="749a8-180">È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.</span><span class="sxs-lookup"><span data-stu-id="749a8-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Specificare la pianificazione dei backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="749a8-182">Per informazioni dettagliate su come specificare la pianificazione del backup, vedere questo [articolo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="749a8-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="749a8-183">Selezionare i **criteri di conservazione** per la copia di backup e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="749a8-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Selezionare i criteri di conservazione](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="749a8-185">Nella schermata **Conferma** riesaminare le informazioni e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="749a8-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="749a8-186">Al termine della creazione della **pianificazione del backup** da parte della procedura guidata, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="749a8-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="749a8-187">Dopo aver modificato la protezione, è possibile verificare che i backup vengano attivati correttamente passando alla scheda **Processi** e assicurandosi che le modifiche siano presenti nei processi di backup.</span><span class="sxs-lookup"><span data-stu-id="749a8-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="749a8-188">Abilitare la limitazione della larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="749a8-188">Enable Network Throttling</span></span>
<span data-ttu-id="749a8-189">L'agente Backup di Azure offre la scheda Limitazione larghezza di banda rete che consente di controllare la modalità d'uso della larghezza di banda della rete durante il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="749a8-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="749a8-190">Questo controllo può essere utile se è necessario eseguire il backup dei dati durante l'orario di lavoro, ma senza che il processo di backup interferisca con il resto del traffico Internet.</span><span class="sxs-lookup"><span data-stu-id="749a8-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="749a8-191">La limitazione del trasferimento dati si applica alle attività di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="749a8-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="749a8-192">Per abilitare la limitazione della larghezza di banda della rete:</span><span class="sxs-lookup"><span data-stu-id="749a8-192">To enable throttling:</span></span>

1. <span data-ttu-id="749a8-193">Nell'**agente di Backup** fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="749a8-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="749a8-194">Selezionare la casella di controllo **Abilita la limitazione all'utilizzo della larghezza di banda Internet per le operazioni di backup** .</span><span class="sxs-lookup"><span data-stu-id="749a8-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="749a8-196">Dopo aver abilitato la limitazione, specificare la larghezza di banda consentita per il trasferimento dei dati di backup durante le **Ore lavorative** e le **Ore non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="749a8-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="749a8-197">I valori della larghezza di banda partono da 512 kilobyte al secondo (Kbps) e possono arrivare fino a 1023 megabyte al secondo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="749a8-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="749a8-198">È anche possibile definire l'inizio e la fine per **Ore lavorative**e i giorni della settimana da considerare come giorni lavorativi.</span><span class="sxs-lookup"><span data-stu-id="749a8-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="749a8-199">Le ore al di fuori delle ore lavorative specificate sono considerate non lavorative.</span><span class="sxs-lookup"><span data-stu-id="749a8-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="749a8-200">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="749a8-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="749a8-201">Impostazioni di esclusione</span><span class="sxs-lookup"><span data-stu-id="749a8-201">Exclusion settings</span></span>
1. <span data-ttu-id="749a8-202">Aprire l'**agente di Backup di Microsoft Azure**. Per trovarlo, cercare nel computer *Backup di Microsoft Azure*.</span><span class="sxs-lookup"><span data-stu-id="749a8-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Aprire l'agente di backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="749a8-204">Nell'agente di Backup di Microsoft Azure fare clic su **Pianifica backup**.</span><span class="sxs-lookup"><span data-stu-id="749a8-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="749a8-206">Nella Pianificazione guidata backup lasciare selezionata l'opzione **Modifica elementi o tempistica del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="749a8-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modificare una pianificazione](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="749a8-208">Fare clic su **Impostazioni di esclusione**.</span><span class="sxs-lookup"><span data-stu-id="749a8-208">Click **Exclusions Settings**.</span></span>

    ![Selezionare elementi da escludere](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="749a8-210">Fare clic su **Aggiungi esclusione**.</span><span class="sxs-lookup"><span data-stu-id="749a8-210">Click **Add Exclusion**.</span></span>

    ![Aggiungere esclusioni](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="749a8-212">Selezionare il percorso e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="749a8-212">Select the location and then, click **OK**.</span></span>

    ![Selezionare una posizione per l'esclusione](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="749a8-214">Aggiungere l'estensione di file nel campo **Tipo file** .</span><span class="sxs-lookup"><span data-stu-id="749a8-214">Add the file extension in the **File Type** field.</span></span>

    ![Escludere per tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="749a8-216">Aggiunta di un'estensione mp3</span><span class="sxs-lookup"><span data-stu-id="749a8-216">Adding an .mp3 extension</span></span>

    ![Esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="749a8-218">Per aggiungere un'altra estensione, fare clic su **Aggiungi esclusione** e immettere l'estensione di un altro tipo di file, aggiungendo un'estensione jpeg.</span><span class="sxs-lookup"><span data-stu-id="749a8-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Altro esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="749a8-220">Dopo aver aggiunto tutte le estensioni, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="749a8-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="749a8-221">Continuare con la Pianificazione guidata backup facendo clic su **Avanti** fino alla **pagina Conferma**, quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="749a8-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Conferma dell'esclusione](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="749a8-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="749a8-223">Next steps</span></span>
* [<span data-ttu-id="749a8-224">Ripristino di Windows Server o Windows Client da Azure</span><span class="sxs-lookup"><span data-stu-id="749a8-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="749a8-225">Per altre informazioni sul servizio Backup di Azure, vedere [Panoramica di Backup di Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="749a8-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="749a8-226">Visitare il [Forum su Backup di Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="749a8-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
