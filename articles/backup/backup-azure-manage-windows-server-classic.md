---
title: aaaManage insiemi di credenziali di Backup di Azure e i server Azure utilizzando il modello di distribuzione classica hello | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come insiemi di credenziali di Backup di Azure toomanage e server.
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
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="20450-103">Gestire gli insiemi di credenziali di Backup di Azure e i server utilizzando il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="20450-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20450-104">Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="20450-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="20450-105">Classico</span><span class="sxs-lookup"><span data-stu-id="20450-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="20450-106">In questo articolo sono disponibili una panoramica delle attività di gestione dei backup hello disponibili tramite hello portale di Azure classico e l'agente di Microsoft Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="20450-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20450-107">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="20450-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="20450-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="20450-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="20450-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="20450-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20450-110">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="20450-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="20450-111">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="20450-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="20450-112">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="20450-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="20450-113">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="20450-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="20450-114">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="20450-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="20450-115">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="20450-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="20450-116">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="20450-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="20450-117">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="20450-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="20450-118">Attività del portale di gestione</span><span class="sxs-lookup"><span data-stu-id="20450-118">Management portal tasks</span></span>
1. <span data-ttu-id="20450-119">Accedi toohello [portale di gestione](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="20450-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="20450-120">Fare clic su **servizi di ripristino**, quindi fare clic su nome hello della pagina di avvio rapido dell'insieme di credenziali backup tooview hello.</span><span class="sxs-lookup"><span data-stu-id="20450-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Servizi di ripristino](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="20450-122">Selezionando le opzioni di hello nella parte superiore di hello della pagina di avvio rapido di hello, è possibile visualizzare l'attività di gestione disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="20450-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Gestire le schede](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="20450-124">Dashboard</span><span class="sxs-lookup"><span data-stu-id="20450-124">Dashboard</span></span>
<span data-ttu-id="20450-125">Selezionare **Dashboard** panoramica sull'utilizzo di hello toosee per server hello.</span><span class="sxs-lookup"><span data-stu-id="20450-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="20450-126">Hello **panoramica sull'utilizzo** include:</span><span class="sxs-lookup"><span data-stu-id="20450-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="20450-127">numero di Hello di Windows Server registrate toocloud</span><span class="sxs-lookup"><span data-stu-id="20450-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="20450-128">numero di Hello macchine virtuali di Azure protette nel cloud</span><span class="sxs-lookup"><span data-stu-id="20450-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="20450-129">Hello spazio di archiviazione totale utilizzato in Azure</span><span class="sxs-lookup"><span data-stu-id="20450-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="20450-130">stato Hello di processi recenti</span><span class="sxs-lookup"><span data-stu-id="20450-130">hello status of recent jobs</span></span>

<span data-ttu-id="20450-131">Nella parte inferiore di hello di hello Dashboard è possibile eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="20450-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="20450-132">**Gestisci certificato** : se un certificato server hello tooregister usato, quindi usare questo certificato hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="20450-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="20450-133">Se si usano le credenziali di insieme, non usare la funzionalità **Gestisci certificato**.</span><span class="sxs-lookup"><span data-stu-id="20450-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="20450-134">**Eliminare** -eliminazioni hello corrente backup dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="20450-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="20450-135">Se non viene utilizzato un archivio di backup, è possibile eliminare toofree spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="20450-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="20450-136">**Eliminare** è abilitata solo dopo aver eliminati tutti i server registrati dall'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="20450-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="20450-138">Elementi registrati</span><span class="sxs-lookup"><span data-stu-id="20450-138">Registered items</span></span>
<span data-ttu-id="20450-139">Selezionare **elementi registrati** tooview i nomi di hello del server hello che sono registrati toothis insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="20450-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="20450-141">Hello **tipo** filtro predefinito tooAzure macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="20450-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="20450-142">Selezionare i nomi di hello tooview dei server hello di insieme di credenziali registrati toothis **Windows server** da hello menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="20450-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="20450-143">Da qui è possibile eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="20450-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="20450-144">**Ripetere la registrazione** : quando questa opzione è selezionata per un server è possibile utilizzare hello **registrazione guidata** hello in Microsoft Azure Backup agent tooregister hello server locale insieme di credenziali di backup hello una seconda volta .</span><span class="sxs-lookup"><span data-stu-id="20450-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="20450-145">Potrebbe essere necessario toore la registrazione a causa di errore tooan nel certificato hello oppure se un server di stato toobe ricompilato.</span><span class="sxs-lookup"><span data-stu-id="20450-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="20450-146">**Eliminare** -Elimina un server dall'insieme di credenziali backup hello.</span><span class="sxs-lookup"><span data-stu-id="20450-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="20450-147">Tutti i dati archiviato hello associati hello server vengono eliminati immediatamente.</span><span class="sxs-lookup"><span data-stu-id="20450-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Attività di Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="20450-149">Elementi protetti</span><span class="sxs-lookup"><span data-stu-id="20450-149">Protected items</span></span>
<span data-ttu-id="20450-150">Selezionare **elementi protetti** elementi hello tooview che sono stato eseguito il backup dai server hello.</span><span class="sxs-lookup"><span data-stu-id="20450-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Elementi protetti](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="20450-152">Configurare</span><span class="sxs-lookup"><span data-stu-id="20450-152">Configure</span></span>
<span data-ttu-id="20450-153">Da hello **configura** scheda è possibile selezionare l'opzione di ridondanza di archiviazione appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="20450-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="20450-154">Hello ora tooselect hello archiviazione ridondanza migliore è subito dopo la creazione di un insieme di credenziali e prima che tutti i computer siano registrati tooit.</span><span class="sxs-lookup"><span data-stu-id="20450-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="20450-155">Una volta un elemento dell'insieme di credenziali registrati toohello, opzione di ridondanza di archiviazione hello è bloccato e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="20450-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Configurare](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="20450-157">Per altre informazioni sulla [ridondanza di archiviazione](../storage/common/storage-redundancy.md), vedere questo articolo.</span><span class="sxs-lookup"><span data-stu-id="20450-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="20450-158">Attività dell'agente Backup di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="20450-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="20450-159">Console</span><span class="sxs-lookup"><span data-stu-id="20450-159">Console</span></span>
<span data-ttu-id="20450-160">Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="20450-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Agente di Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="20450-162">Da hello **azioni** disponibile all'indirizzo hello destra della console di agente di backup hello è possibile eseguire hello seguenti attività di gestione:</span><span class="sxs-lookup"><span data-stu-id="20450-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="20450-163">Registra server</span><span class="sxs-lookup"><span data-stu-id="20450-163">Register Server</span></span>
* <span data-ttu-id="20450-164">Pianificazione di un backup</span><span class="sxs-lookup"><span data-stu-id="20450-164">Schedule Backup</span></span>
* <span data-ttu-id="20450-165">Esegui backup</span><span class="sxs-lookup"><span data-stu-id="20450-165">Back Up now</span></span>
* <span data-ttu-id="20450-166">Modifica proprietà</span><span class="sxs-lookup"><span data-stu-id="20450-166">Change Properties</span></span>

![Azioni della console dell'agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="20450-168">troppo**Ripristina dati**, vedere [ripristinare i file tooa Windows server o computer client Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="20450-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="20450-169">Modificare un backup esistente</span><span class="sxs-lookup"><span data-stu-id="20450-169">Modify an existing backup</span></span>
1. <span data-ttu-id="20450-170">Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="20450-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="20450-172">In hello **pianificazione guidata Backup** lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="20450-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificare un backup pianificato](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="20450-174">Se si desidera tooadd o modificare gli elementi, di hello **selezionare elementi tooBackup** fare clic su schermo **Aggiungi elementi**.</span><span class="sxs-lookup"><span data-stu-id="20450-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="20450-175">È inoltre possibile impostare **impostazioni di esclusione** da questa pagina nella creazione guidata hello.</span><span class="sxs-lookup"><span data-stu-id="20450-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="20450-176">Se si desidera che il file tooexclude o procedura hello per l'aggiunta di leggere i tipi di file [impostazioni di esclusione](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="20450-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="20450-177">Selezionare il file hello e le cartelle desidera ripristinare tooback e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="20450-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Aggiungi elementi](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="20450-179">Specificare hello **pianificazione del backup** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="20450-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="20450-180">È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.</span><span class="sxs-lookup"><span data-stu-id="20450-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Specificare la pianificazione dei backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="20450-182">Specifica la pianificazione del backup hello è illustrata in dettaglio in questo [articolo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="20450-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="20450-183">Seleziona hello **criteri di conservazione** copia di backup hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="20450-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Selezionare i criteri di conservazione](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="20450-185">In hello **conferma** schermata hello rivedere le informazioni e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="20450-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="20450-186">Al termine della creazione di hello guidata hello **pianificazione del backup**, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="20450-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="20450-187">Dopo la modifica della protezione, è possibile verificare che i backup attivano correttamente da passare toohello **processi** scheda e conferma che le modifiche vengono riflesse nel hello i processi di backup.</span><span class="sxs-lookup"><span data-stu-id="20450-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="20450-188">Abilitare la limitazione della larghezza di banda della rete</span><span class="sxs-lookup"><span data-stu-id="20450-188">Enable Network Throttling</span></span>
<span data-ttu-id="20450-189">l'agente Azure Backup Hello fornisce una scheda di limitazione delle richieste che consente di toocontrol modalità di utilizzo della larghezza di banda di rete durante il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="20450-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="20450-190">Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico internet.</span><span class="sxs-lookup"><span data-stu-id="20450-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="20450-191">La limitazione delle richieste di dati trasferimento applica tooback backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="20450-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="20450-192">tooenable limitazione:</span><span class="sxs-lookup"><span data-stu-id="20450-192">tooenable throttling:</span></span>

1. <span data-ttu-id="20450-193">In hello **agente di Backup**, fare clic su **Modifica proprietà**.</span><span class="sxs-lookup"><span data-stu-id="20450-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="20450-194">Seleziona hello **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="20450-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="20450-196">Dopo aver abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.</span><span class="sxs-lookup"><span data-stu-id="20450-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="20450-197">i valori di larghezza di banda Hello iniziano da 512 kilobyte per secondo (Kbps) e possono aumentare fino a too1023 megabyte al secondo (Mbps).</span><span class="sxs-lookup"><span data-stu-id="20450-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="20450-198">È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello vengono considerati lavoro giorni.</span><span class="sxs-lookup"><span data-stu-id="20450-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="20450-199">tempo di Hello di fuori di hello designato per le ore lavorative è ore non lavorative toobe considerate.</span><span class="sxs-lookup"><span data-stu-id="20450-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="20450-200">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="20450-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="20450-201">Impostazioni di esclusione</span><span class="sxs-lookup"><span data-stu-id="20450-201">Exclusion settings</span></span>
1. <span data-ttu-id="20450-202">Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="20450-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Aprire l'agente di backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="20450-204">Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.</span><span class="sxs-lookup"><span data-stu-id="20450-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="20450-206">In Pianificazione guidata Backup hello lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="20450-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Modificare una pianificazione](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="20450-208">Fare clic su **Impostazioni di esclusione**.</span><span class="sxs-lookup"><span data-stu-id="20450-208">Click **Exclusions Settings**.</span></span>

    ![Selezionare gli elementi tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="20450-210">Fare clic su **Aggiungi esclusione**.</span><span class="sxs-lookup"><span data-stu-id="20450-210">Click **Add Exclusion**.</span></span>

    ![Aggiungere esclusioni](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="20450-212">Selezionare il percorso di hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="20450-212">Select hello location and then, click **OK**.</span></span>

    ![Selezionare una posizione per l'esclusione](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="20450-214">Aggiungere l'estensione del file hello in hello **tipo di File** campo.</span><span class="sxs-lookup"><span data-stu-id="20450-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Escludere per tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="20450-216">Aggiunta di un'estensione mp3</span><span class="sxs-lookup"><span data-stu-id="20450-216">Adding an .mp3 extension</span></span>

    ![Esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="20450-218">tooadd un'altra estensione, fare clic su **Aggiunta esclusione** e immettere un'altra estensione del tipo di file (aggiunta di un'estensione JPEG).</span><span class="sxs-lookup"><span data-stu-id="20450-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Altro esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="20450-220">Dopo aver aggiunto tutte le estensioni di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="20450-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="20450-221">Continuare il processo hello pianificazione guidata Backup fare clic su **Avanti** finché hello **pagina di conferma**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="20450-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Conferma dell'esclusione](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="20450-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20450-223">Next steps</span></span>
* [<span data-ttu-id="20450-224">Ripristino di Windows Server o Windows Client da Azure</span><span class="sxs-lookup"><span data-stu-id="20450-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="20450-225">toolearn ulteriori informazioni sui Backup di Azure, vedere [Cenni preliminari su Backup di Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="20450-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="20450-226">Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="20450-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
