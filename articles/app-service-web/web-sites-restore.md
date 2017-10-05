---
title: Ripristinare un'app in Azure
description: Informazioni su come ripristinare l'app da un backup.
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="51c15-103">Ripristinare un'app in Azure</span><span class="sxs-lookup"><span data-stu-id="51c15-103">Restore an app in Azure</span></span>
<span data-ttu-id="51c15-104">Questo articolo illustra come ripristinare un'app nel [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) in precedenza sottoposta a un backup. Vedere [Eseguire il backup di un'app Web del Servizio app di Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="51c15-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="51c15-105">È possibile ripristinare su richiesta a uno stato precedente l'app con i relativi database collegati oppure creare una nuova app basata su uno dei backup dell'applicazione originale.</span><span class="sxs-lookup"><span data-stu-id="51c15-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="51c15-106">Servizio app di Azure supporta il backup e il ripristino dei seguenti database:</span><span class="sxs-lookup"><span data-stu-id="51c15-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="51c15-107">Database SQL</span><span class="sxs-lookup"><span data-stu-id="51c15-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="51c15-108">Database di Azure per MySQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="51c15-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="51c15-109">Database di Azure per PostgreSQL (anteprima)</span><span class="sxs-lookup"><span data-stu-id="51c15-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="51c15-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="51c15-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="51c15-111">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="51c15-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="51c15-112">Il ripristino da backup è disponibile per le app in esecuzione a livello **Standard** e **Premium**.</span><span class="sxs-lookup"><span data-stu-id="51c15-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="51c15-113">Per informazioni sul passaggio dell'app a un piano superiore, vedere [Scalare un'app Web in Servizio app di Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="51c15-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="51c15-114">Il livello **Premium** consente un maggior numero di backup giornalieri rispetto al livello **Standard**.</span><span class="sxs-lookup"><span data-stu-id="51c15-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="51c15-115">Ripristinare un'app da un backup esistente</span><span class="sxs-lookup"><span data-stu-id="51c15-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="51c15-116">Nel pannello **Impostazioni** dell'app nel Portale di Azure fare clic su **Backup** per visualizzare il pannello **Backup**.</span><span class="sxs-lookup"><span data-stu-id="51c15-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="51c15-117">Fare quindi clic su **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="51c15-117">Then click **Restore**.</span></span>
   
    ![Scegliere Ripristina][ChooseRestoreNow]
2. <span data-ttu-id="51c15-119">Nel pannello **Ripristina** , selezionare l'origine di backup.</span><span class="sxs-lookup"><span data-stu-id="51c15-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="51c15-120">L'opzione **Backup dell'app** mostra tutti i backup esistenti dell'app corrente, che possono essere facilmente selezionati.</span><span class="sxs-lookup"><span data-stu-id="51c15-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="51c15-121">L'opzione **Archiviazione** consente di selezionare qualsiasi file ZIP del backup da un account di archiviazione e un contenitore di Azure esistenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="51c15-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="51c15-122">Se si sta tentando di ripristinare un backup di un'altra app, usare l'opzione **Archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="51c15-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="51c15-123">Quindi, specificare la destinazione per il ripristino dell’app in **Destinazione di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="51c15-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="51c15-124">Se si sceglie **Sovrascrivi**, tutti i dati esistenti nell'app corrente verranno cancellati e sovrascritti.</span><span class="sxs-lookup"><span data-stu-id="51c15-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="51c15-125">Prima di scegliere **OK**, assicurarsi che sia esattamente ciò che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="51c15-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="51c15-126">È possibile selezionare **App esistente** per ripristinare il backup dell’app in un'altra applicazione nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="51c15-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="51c15-127">Prima di utilizzare questa opzione, deve già essere stata creata un'altra app nel gruppo di risorse con mirroring della configurazione del database in quello definito nel backup dell’app.</span><span class="sxs-lookup"><span data-stu-id="51c15-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="51c15-128">È anche possibile creare una **nuova** app in cui ripristinare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="51c15-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="51c15-129">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="51c15-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="51c15-130">Scaricare o eliminare un backup da un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="51c15-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="51c15-131">Dal pannello principale **Sfoglia** del portale di Azure selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="51c15-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="51c15-132">Verrà visualizzato un elenco degli account di archiviazione esistenti.</span><span class="sxs-lookup"><span data-stu-id="51c15-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="51c15-133">Selezionare l'account di archiviazione che contiene il backup che si intende scaricare o eliminare. Verrà visualizzato il pannello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="51c15-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="51c15-134">Nel pannello dell'account di archiviazione selezionare il contenitore desiderato.</span><span class="sxs-lookup"><span data-stu-id="51c15-134">In the storage account blade, select the container you want</span></span>
   
    ![Contenitori di visualizzazione][ViewContainers]
4. <span data-ttu-id="51c15-136">Selezionare il file di backup che si desidera scaricare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="51c15-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="51c15-138">Fare clic su **Scarica** o **Elimina** a seconda dell'azione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="51c15-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="51c15-139">Monitorare un'operazione di ripristino</span><span class="sxs-lookup"><span data-stu-id="51c15-139">Monitor a restore operation</span></span>
<span data-ttu-id="51c15-140">Per visualizzare i dettagli sul successo o sulla mancata riuscita dell'operazione di ripristino dell'app, passare al pannello **Log attività** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="51c15-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="51c15-141">Scorrere verso il basso per trovare l'operazione di ripristino desiderata e fare clic su di essa per selezionarla.</span><span class="sxs-lookup"><span data-stu-id="51c15-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="51c15-142">Nel pannello dei dettagli verranno visualizzate le informazioni disponibili correlate all'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51c15-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51c15-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51c15-143">Next Steps</span></span>
<span data-ttu-id="51c15-144">È possibile eseguire il backup e il ripristino delle applicazioni del servizio app usando l'API REST (vedere [Usare REST per eseguire il backup e il ripristino di app del servizio App](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="51c15-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
