---
title: aaaRestore un'app in Azure
description: Informazioni su come toorestore l'app da un backup.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="931dc-103">Ripristinare un'app in Azure</span><span class="sxs-lookup"><span data-stu-id="931dc-103">Restore an app in Azure</span></span>
<span data-ttu-id="931dc-104">In questo articolo illustra come toorestore un'app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) che in precedenza è stato eseguito il (vedere [eseguire il backup dell'app in Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="931dc-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="931dc-105">È possibile ripristinare l'app con lo stato precedente su richiesta tooa database collegati o creare una nuova app basata su uno dei backup dell'applicazione originale.</span><span class="sxs-lookup"><span data-stu-id="931dc-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="931dc-106">Servizio App di Azure supporta hello seguendo i database per il backup e ripristino:</span><span class="sxs-lookup"><span data-stu-id="931dc-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="931dc-107">Database SQL</span><span class="sxs-lookup"><span data-stu-id="931dc-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="931dc-108">Database di Azure per MySQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="931dc-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="931dc-109">Database di Azure per PostgreSQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="931dc-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="931dc-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="931dc-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="931dc-111">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="931dc-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="931dc-112">Ripristino da backup è disponibile tooapps in esecuzione in **Standard** e **Premium** livello.</span><span class="sxs-lookup"><span data-stu-id="931dc-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="931dc-113">Per informazioni sul passaggio dell'app a un piano superiore, vedere [Scalare un'app Web in Servizio app di Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="931dc-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="931dc-114">**Premium** livello consente un numero maggiore di toobe di backup giornaliera eseguita rispetto a **Standard** livello.</span><span class="sxs-lookup"><span data-stu-id="931dc-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="931dc-115">Ripristinare un'app da un backup esistente</span><span class="sxs-lookup"><span data-stu-id="931dc-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="931dc-116">In hello **impostazioni** fare clic su pannello dell'app nel portale di Azure, hello **backup** toodisplay hello **backup** blade.</span><span class="sxs-lookup"><span data-stu-id="931dc-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="931dc-117">Fare quindi clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="931dc-117">Then click **Restore**.</span></span>
   
    ![Scegliere Ripristina][ChooseRestoreNow]
2. <span data-ttu-id="931dc-119">In hello **ripristinare** blade, prima origine di backup selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="931dc-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="931dc-120">Hello **backup App** opzione Mostra tutti i backup esistenti dell'applicazione corrente hello di hello ed è possibile selezionare uno.</span><span class="sxs-lookup"><span data-stu-id="931dc-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="931dc-121">Hello **archiviazione** opzione consente di selezionare qualsiasi file ZIP di backup da qualsiasi account di archiviazione di Azure e un contenitore nella sottoscrizione esistente.</span><span class="sxs-lookup"><span data-stu-id="931dc-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="931dc-122">Se si sta tentando di toorestore un backup di un'altra app, utilizzare hello **archiviazione** opzione.</span><span class="sxs-lookup"><span data-stu-id="931dc-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="931dc-123">Quindi, specificare la destinazione hello per il ripristino dell'app hello in **destinazione di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="931dc-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="931dc-124">Se si sceglie **Sovrascrivi**, tutti i dati esistenti nell'app corrente verranno cancellati e sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="931dc-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="931dc-125">Prima di scegliere **OK**, verificare che sia esattamente ciò che si desidera toodo.</span><span class="sxs-lookup"><span data-stu-id="931dc-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="931dc-126">È possibile selezionare **App esistente** toorestore hello app tooanother backup in app hello nello stesso gruppo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="931dc-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="931dc-127">Prima di utilizzare questa opzione, è necessario avere già creato un'altra applicazione nel gruppo di risorse con il mirroring del database configurazione toohello quella definita nel backup app hello.</span><span class="sxs-lookup"><span data-stu-id="931dc-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="931dc-128">È inoltre possibile creare un **New** app toorestore il contenuto.</span><span class="sxs-lookup"><span data-stu-id="931dc-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="931dc-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="931dc-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="931dc-130">Scaricare o eliminare un backup da un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="931dc-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="931dc-131">Da hello principale **Sfoglia** pannello del portale di Azure selezionare hello **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="931dc-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="931dc-132">Verrà visualizzato un elenco degli account di archiviazione esistenti.</span><span class="sxs-lookup"><span data-stu-id="931dc-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="931dc-133">Selezionare l'account di archiviazione di hello contenente backup hello desiderato viene visualizzato un pannello toodownload o delete.hello hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="931dc-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="931dc-134">Nel Pannello di account di archiviazione hello, selezionare il contenitore di hello desiderato</span><span class="sxs-lookup"><span data-stu-id="931dc-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Contenitori di visualizzazione][ViewContainers]
4. <span data-ttu-id="931dc-136">Selezionare i file di backup si desidera toodownload o eliminare.</span><span class="sxs-lookup"><span data-stu-id="931dc-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="931dc-138">Fare clic su **scaricare** o **eliminare** a seconda di ciò che si desidera toodo.</span><span class="sxs-lookup"><span data-stu-id="931dc-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="931dc-139">Monitorare un'operazione di ripristino</span><span class="sxs-lookup"><span data-stu-id="931dc-139">Monitor a restore operation</span></span>
<span data-ttu-id="931dc-140">Dettagli toosee hello riuscita o meno dell'operazione di ripristino di app hello, passare toohello **Log attività** pannello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="931dc-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="931dc-141">Scorrere verso il basso toofind hello desiderato ripristino operazione e fare clic su tooselect.</span><span class="sxs-lookup"><span data-stu-id="931dc-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="931dc-142">Hello pannello Visualizza hello disponibili informazioni correlate toohello l'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="931dc-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="931dc-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="931dc-143">Next Steps</span></span>
<span data-ttu-id="931dc-144">È possibile eseguire il backup e ripristinare le applicazioni di servizio App utilizzando API REST (vedere [tooback REST di utilizzo di backup e ripristino di applicazioni di servizio App](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="931dc-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
