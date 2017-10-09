---
title: aaaBack backup dell'app in Azure
description: Informazioni su come backup toocreate delle App in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="58248-103">Eseguire il backup dell'app in Azure</span><span class="sxs-lookup"><span data-stu-id="58248-103">Back up your app in Azure</span></span>
<span data-ttu-id="58248-104">Hello eseguire il backup e ripristino di funzionalità in [Azure App Service](../app-service/app-service-value-prop-what-is.md) consente di creare con facilità backup app manualmente o in una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="58248-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="58248-105">È possibile ripristinare hello app tooa istantanea dello stato precedente la sovrascrittura app esistenti di hello o tooanother ripristino.</span><span class="sxs-lookup"><span data-stu-id="58248-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="58248-106">Per informazioni sul ripristino di un'app dal backup, vedere [Ripristinare un'app nel Servizio app di Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="58248-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="58248-107">Elementi di cui viene eseguito il backup</span><span class="sxs-lookup"><span data-stu-id="58248-107">What gets backed up</span></span>
<span data-ttu-id="58248-108">Servizio App può eseguire il backup seguenti hello informazioni tooan account di archiviazione Azure e di aver configurato il toouse app contenitore.</span><span class="sxs-lookup"><span data-stu-id="58248-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="58248-109">Configurazione dell'app</span><span class="sxs-lookup"><span data-stu-id="58248-109">App configuration</span></span>
* <span data-ttu-id="58248-110">Contenuto del file</span><span class="sxs-lookup"><span data-stu-id="58248-110">File content</span></span>
* <span data-ttu-id="58248-111">Database connesso tooyour app</span><span class="sxs-lookup"><span data-stu-id="58248-111">Database connected tooyour app</span></span>

<span data-ttu-id="58248-112">Hello seguenti soluzioni di database è supportato con funzionalità di backup:</span><span class="sxs-lookup"><span data-stu-id="58248-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="58248-113">Database SQL</span><span class="sxs-lookup"><span data-stu-id="58248-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="58248-114">Database di Azure per MySQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="58248-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="58248-115">Database di Azure per PostgreSQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="58248-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="58248-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="58248-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="58248-117">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="58248-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="58248-118">Ciascun backup è una copia offline completa dell'app, non un aggiornamento incrementale.</span><span class="sxs-lookup"><span data-stu-id="58248-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="58248-119">Requisiti e restrizioni</span><span class="sxs-lookup"><span data-stu-id="58248-119">Requirements and restrictions</span></span>
* <span data-ttu-id="58248-120">Hello eseguire il backup e ripristino funzionalità richiede hello toobe piano di servizio App in hello **Standard** livello o **Premium** livello.</span><span class="sxs-lookup"><span data-stu-id="58248-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="58248-121">Per ulteriori informazioni sulla scalabilità del toouse piano di servizio App un livello superiore, vedere [scalare in verticale un'app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="58248-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="58248-122">Il livello **Premium** consente un maggior numero di backup giornalieri rispetto al livello **Standard**.</span><span class="sxs-lookup"><span data-stu-id="58248-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="58248-123">È necessario un account di archiviazione di Azure e un contenitore in hello hello app che si desidera toobackup stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="58248-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="58248-124">Per ulteriori informazioni sugli account di archiviazione di Azure, vedere hello [collegamenti](#moreaboutstorage) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="58248-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="58248-125">I backup possono essere too10 GB di contenuto di applicazione e il database.</span><span class="sxs-lookup"><span data-stu-id="58248-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="58248-126">Se dimensioni hello del backup superano questo limite, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="58248-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="58248-127">Creare un backup manuale</span><span class="sxs-lookup"><span data-stu-id="58248-127">Create a manual backup</span></span>
1. <span data-ttu-id="58248-128">In hello [portale Azure](https://portal.azure.com), passare a pannello tooyour dell'app, selezionare **backup**.</span><span class="sxs-lookup"><span data-stu-id="58248-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="58248-129">Hello **backup** pannello verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="58248-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Pagina Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="58248-131">Se viene visualizzato il messaggio hello riportato di seguito, scegliere tooupgrade piano di servizio App prima di procedere con i backup.</span><span class="sxs-lookup"><span data-stu-id="58248-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="58248-132">Per altre informazioni, vedere [Scalare un'app Web in Servizio app di Azure](web-sites-scale.md) .</span><span class="sxs-lookup"><span data-stu-id="58248-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="58248-133">![Scelta dell'account di archiviazione](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="58248-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="58248-134">In hello **Backup** pannello, fare clic su **configura**
![fare clic su Configura.](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="58248-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="58248-135">In hello **la configurazione del Backup** pannello, fare clic su **archiviazione: non configurato** tooconfigure un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="58248-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Scegliere l'account di archiviazione][ChooseStorageAccount]
4. <span data-ttu-id="58248-137">Scegliere la destinazione del backup selezionando un **Account di archiviazione** e un **Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="58248-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="58248-138">account di archiviazione Hello devono appartenere toohello app hello si desidera ripristinare tooback stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="58248-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="58248-139">Se si desidera, è possibile creare un nuovo account di archiviazione o di un nuovo contenitore in pannelli dei rispettivi hello.</span><span class="sxs-lookup"><span data-stu-id="58248-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="58248-140">Al termine, fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="58248-140">When you're done, click **Select**.</span></span>
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="58248-142">In hello **la configurazione del Backup** blade che ancora viene lasciato aperto, è possibile configurare **Backup Database**, quindi selezionare i database di hello desiderate tooinclude nei backup hello (database SQL o MySQL), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="58248-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="58248-144">Per un database tooappear in questo elenco, la relativa stringa di connessione deve esistere in hello **le stringhe di connessione** sezione di hello **le impostazioni dell'applicazione** pannello per l'app.</span><span class="sxs-lookup"><span data-stu-id="58248-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="58248-145">In hello **la configurazione del Backup** pannello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="58248-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="58248-146">In hello **backup** pannello, fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="58248-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Pulsante BackUp Now][BackUpNow]
   
    <span data-ttu-id="58248-148">Viene visualizzato un messaggio di stato di avanzamento durante il processo di backup hello.</span><span class="sxs-lookup"><span data-stu-id="58248-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="58248-149">Dopo aver configurato l'account di archiviazione di hello e contenitore è possibile avviare un backup manuale in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="58248-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="58248-150">Configurazione dei backup automatici</span><span class="sxs-lookup"><span data-stu-id="58248-150">Configure automated backups</span></span>
1. <span data-ttu-id="58248-151">In hello **la configurazione del Backup** pannello, impostare **backup pianificati** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="58248-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Scegliere l'account di archiviazione](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="58248-153">Pianificazione del backup verranno visualizzate le opzioni, impostare **Backup pianificati** troppo**su**, quindi configurare la pianificazione del backup hello come desiderato e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="58248-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Abilitazione dei backup automatici][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="58248-155">Configurare backup parziali</span><span class="sxs-lookup"><span data-stu-id="58248-155">Configure Partial Backups</span></span>
<span data-ttu-id="58248-156">In alcuni casi non si desidera toobackup tutti gli elementi nella tua app.</span><span class="sxs-lookup"><span data-stu-id="58248-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="58248-157">Di seguito sono disponibili alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="58248-157">Here are a few examples:</span></span>

* <span data-ttu-id="58248-158">Si [configurano backup settimanali](web-sites-backup.md#configure-automated-backups) dell'app che contiene contenuto statico che non cambia mai, ad esempio immagini o post di blog precedenti.</span><span class="sxs-lookup"><span data-stu-id="58248-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="58248-159">L'app con oltre 10 GB di contenuto (quantità massima di hello che è possibile eseguire il backup in un momento).</span><span class="sxs-lookup"><span data-stu-id="58248-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="58248-160">Per evitare che i file di log toobackup hello.</span><span class="sxs-lookup"><span data-stu-id="58248-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="58248-161">I backup parziali permetterà di scegliere esattamente i file a cui si desidera toobackup.</span><span class="sxs-lookup"><span data-stu-id="58248-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="58248-162">Escludere file dal backup</span><span class="sxs-lookup"><span data-stu-id="58248-162">Exclude files from your backup</span></span>
<span data-ttu-id="58248-163">Si supponga di che avere un'applicazione che contiene i file di log e le immagini statiche che sono state backup una volta e non prevede toochange.</span><span class="sxs-lookup"><span data-stu-id="58248-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="58248-164">In questi casi è possibile escludere le cartelle e i file dall'archiviazione nei backup futuri.</span><span class="sxs-lookup"><span data-stu-id="58248-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="58248-165">tooexclude file e cartelle dal backup, creare un `_backup.filter` file hello `D:\home\site\wwwroot` cartella dell'app.</span><span class="sxs-lookup"><span data-stu-id="58248-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="58248-166">Specificare l'elenco di hello di file e cartelle che si desidera tooexclude in questo file.</span><span class="sxs-lookup"><span data-stu-id="58248-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="58248-167">Un modo semplice tooaccess dei file è toouse Kudu.</span><span class="sxs-lookup"><span data-stu-id="58248-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="58248-168">Fare clic su **strumenti avanzati -> Go** impostazione per il tooaccess app web Kudu.</span><span class="sxs-lookup"><span data-stu-id="58248-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Uso del portale con Kudu][kudu-portal]

<span data-ttu-id="58248-170">Identificare le cartelle di hello che si desidera tooexclude dal backup.</span><span class="sxs-lookup"><span data-stu-id="58248-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="58248-171">Ad esempio, si desidera toofilter hello evidenziato cartella out e file.</span><span class="sxs-lookup"><span data-stu-id="58248-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Cartella delle immagini][ImagesFolder]

<span data-ttu-id="58248-173">Creare un file denominato `_backup.filter` e inserire l'elenco di hello in precedenza nel file hello, ma rimuovere `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="58248-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="58248-174">Elencare una directory o un file per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="58248-174">List one directory or file per line.</span></span> <span data-ttu-id="58248-175">Pertanto, deve essere contenuto hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="58248-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="58248-176">Caricare `_backup.filter` file toohello `D:\home\site\wwwroot\` directory del tuo sito con [ftp](web-sites-deploy.md#ftp) o qualsiasi altro metodo.</span><span class="sxs-lookup"><span data-stu-id="58248-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="58248-177">Se si desidera, è possibile creare file hello direttamente utilizzando Kudu `DebugConsole` e inserire il contenuto di hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="58248-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="58248-178">Eseguire i backup hello stesso come si farebbe normalmente, [manualmente](#create-a-manual-backup) o [automaticamente](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="58248-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="58248-179">Ora, eventuali file e cartelle che vengono specificate in `_backup.filter` viene esclusa dal backup futuri di hello pianificata o avviato manualmente.</span><span class="sxs-lookup"><span data-stu-id="58248-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="58248-180">Ripristinare i backup parziali di hello del sito stesso modo di [ripristinare un backup regolare](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="58248-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="58248-181">il processo di ripristino Hello hello giusto.</span><span class="sxs-lookup"><span data-stu-id="58248-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="58248-182">Quando viene ripristinato un backup completo, tutto il contenuto nel sito hello viene sostituito con qualsiasi backup hello.</span><span class="sxs-lookup"><span data-stu-id="58248-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="58248-183">Se un file nel sito di hello, ma non nel backup hello verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="58248-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="58248-184">Tuttavia, quando viene ripristinato un backup parziale, qualsiasi contenuto che si trova in una delle directory hello disattivato o qualsiasi file disattivata, viene lasciato invariato.</span><span class="sxs-lookup"><span data-stu-id="58248-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="58248-185">Modalità di archiviazione dei backup</span><span class="sxs-lookup"><span data-stu-id="58248-185">How backups are stored</span></span>
<span data-ttu-id="58248-186">Dopo avere apportato uno o più backup per l'app, i backup hello sono visibili in hello **contenitori** blade di account di archiviazione e l'app.</span><span class="sxs-lookup"><span data-stu-id="58248-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="58248-187">Nell'account di archiviazione hello, ogni backup include un`.zip` file che contiene i dati di backup hello e un `.xml` file che contiene un manifesto di hello `.zip` il contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="58248-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="58248-188">È possibile decomprimere e individuare questi file se si desidera tooaccess i backup senza eseguire effettivamente un ripristino dell'app.</span><span class="sxs-lookup"><span data-stu-id="58248-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="58248-189">backup del database per l'applicazione hello Hello viene archiviato nella directory radice del file the.zip hello.</span><span class="sxs-lookup"><span data-stu-id="58248-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="58248-190">Per un database SQL può essere un file BACPAC (nessuna estensione di file) e può essere importato.</span><span class="sxs-lookup"><span data-stu-id="58248-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="58248-191">toocreate un database SQL in base a hello esportazione BACPAC, vedere [importare tooCreate un File BACPAC un nuovo Database utente](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="58248-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="58248-192">Modifica di qualsiasi file hello nel **websitebackups** contenitore può causare hello toobecome backup non valido e pertanto non ripristinabile.</span><span class="sxs-lookup"><span data-stu-id="58248-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="58248-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58248-193">Next Steps</span></span>
<span data-ttu-id="58248-194">Per informazioni sul ripristino di un'app da un backup, vedere [Ripristinare un'app nel Servizio app di Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="58248-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="58248-195">È possibile eseguire il backup e ripristinare le applicazioni di servizio App utilizzando API REST (vedere [usare REST toobackup e ripristino di App del servizio app](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="58248-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

