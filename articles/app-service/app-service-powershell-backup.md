---
title: aaaUse PowerShell tooback di backup e ripristino di applicazioni di servizio App
description: Informazioni su come toouse PowerShell tooback di backup e ripristino di un'app in Azure App Service
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="072c5-103">Utilizzare PowerShell tooback e ripristino di App del servizio App</span><span class="sxs-lookup"><span data-stu-id="072c5-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="072c5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="072c5-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="072c5-105">API REST</span><span class="sxs-lookup"><span data-stu-id="072c5-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="072c5-106">Informazioni su come toouse Azure PowerShell tooback di backup e ripristino [App del servizio app](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="072c5-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="072c5-107">Per altre informazioni sui backup delle app Web, inclusi i requisiti e le restrizioni, vedere [Eseguire il backup di un'app Web nel servizio app di Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="072c5-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="072c5-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="072c5-108">Prerequisites</span></span>
<span data-ttu-id="072c5-109">toouse PowerShell toomanage i backup di app, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="072c5-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="072c5-110">**Un URL SAS** che consente la lettura e il contenitore di archiviazione di Azure tooan accesso in scrittura.</span><span class="sxs-lookup"><span data-stu-id="072c5-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="072c5-111">Vedere [modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per una spiegazione di URL di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="072c5-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="072c5-112">Vedere [Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) per esempi sulla gestione di Archiviazione di Azure tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="072c5-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="072c5-113">**Una stringa di connessione di database** se si desidera tooback backup di un database con l'app web.</span><span class="sxs-lookup"><span data-stu-id="072c5-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="072c5-114">Come eseguire il backup cmdlet toogenerate toouse un URL SAS con hello web app</span><span class="sxs-lookup"><span data-stu-id="072c5-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="072c5-115">L'URL di firma di accesso condiviso può essere generato con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="072c5-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="072c5-116">Di seguito è riportato un esempio di come toogenerate che può essere utilizzato con i cmdlet di hello descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="072c5-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="072c5-117">Installare Azure PowerShell 1.3.2 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="072c5-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="072c5-118">Per istruzioni sull'installazione e sull'uso di Azure PowerShell, vedere [Uso di Azure PowerShell con Azure Resource Manager](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="072c5-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="072c5-119">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="072c5-119">Create a backup</span></span>
<span data-ttu-id="072c5-120">Utilizzare toocreate cmdlet New-AzureRmWebAppBackup hello un backup di un'app web.</span><span class="sxs-lookup"><span data-stu-id="072c5-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="072c5-121">Viene creato un backup con un nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="072c5-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="072c5-122">Se si desidera tooprovide un nome per il backup, usare parametro facoltativo di hello Nomebackup.</span><span class="sxs-lookup"><span data-stu-id="072c5-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="072c5-123">tooinclude un database nel backup hello, creare innanzitutto un'impostazione di backup del database utilizzando i cmdlet New-AzureRmWebAppDatabaseBackupSetting hello, quindi specificare tale impostazione in hello database parametro del cmdlet New-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="072c5-124">il parametro database Hello accetta una matrice di impostazioni del database, consentendo tooback su più di un database.</span><span class="sxs-lookup"><span data-stu-id="072c5-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="072c5-125">Ottenere i backup</span><span class="sxs-lookup"><span data-stu-id="072c5-125">Get backups</span></span>
<span data-ttu-id="072c5-126">cmdlet Get-AzureRmWebAppBackupList Hello restituisce una matrice di tutti i backup per un'app web.</span><span class="sxs-lookup"><span data-stu-id="072c5-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="072c5-127">È necessario fornire il nome di hello di hello web app e il relativo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="072c5-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="072c5-128">tooget un backup specifico, utilizzare il cmdlet Get-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="072c5-129">È anche possibile inviare tramite pipe un oggetto applicazione web in uno dei cmdlet di gestione dei backup hello per praticità.</span><span class="sxs-lookup"><span data-stu-id="072c5-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="072c5-130">Pianificare backup automatici</span><span class="sxs-lookup"><span data-stu-id="072c5-130">Schedule automatic backups</span></span>
<span data-ttu-id="072c5-131">È possibile pianificare i backup toohappen automaticamente a un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="072c5-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="072c5-132">tooconfigure una pianificazione di backup, utilizzare i cmdlet di hello AzureRmWebAppBackupConfiguration di modifica.</span><span class="sxs-lookup"><span data-stu-id="072c5-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="072c5-133">Questo cmdlet accetta alcuni parametri:</span><span class="sxs-lookup"><span data-stu-id="072c5-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="072c5-134">**Nome** : hello nome dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="072c5-135">**ResourceGroupName** : hello nome della risorsa gruppo contenitore hello web app hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="072c5-136">**Slot** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="072c5-136">**Slot** - Optional.</span></span> <span data-ttu-id="072c5-137">nome Hello dello slot di hello web app.</span><span class="sxs-lookup"><span data-stu-id="072c5-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="072c5-138">**StorageAccountUrl** -hello URL di firma di accesso condiviso per il contenitore di archiviazione di Azure hello utilizzato backup hello toostore.</span><span class="sxs-lookup"><span data-stu-id="072c5-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="072c5-139">**FrequencyInterval** -valore numerico per la frequenza con cui hello i backup devono essere effettuati.</span><span class="sxs-lookup"><span data-stu-id="072c5-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="072c5-140">Deve essere un intero positivo.</span><span class="sxs-lookup"><span data-stu-id="072c5-140">Must be a positive integer.</span></span>
* <span data-ttu-id="072c5-141">**FrequencyUnit** -unità di tempo per la frequenza con cui hello i backup devono essere effettuati.</span><span class="sxs-lookup"><span data-stu-id="072c5-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="072c5-142">Le opzioni disponibili sono Hour e Day.</span><span class="sxs-lookup"><span data-stu-id="072c5-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="072c5-143">**RetentionPeriodInDays** - quanti giorni devono essere salvati i backup automatici di hello prima di essere eliminati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="072c5-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="072c5-144">**StartTime** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="072c5-144">**StartTime** - Optional.</span></span> <span data-ttu-id="072c5-145">ora di Hello quando deve iniziare i backup automatici hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="072c5-146">I backup iniziano immediatamente se questo valore è Null.</span><span class="sxs-lookup"><span data-stu-id="072c5-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="072c5-147">Deve essere un valore DateTime.</span><span class="sxs-lookup"><span data-stu-id="072c5-147">Must be a DateTime.</span></span>
* <span data-ttu-id="072c5-148">**Databases** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="072c5-148">**Databases** - Optional.</span></span> <span data-ttu-id="072c5-149">Matrice di DatabaseBackupSettings per toobackup database hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="072c5-150">**KeepAtLeastOneBackup** : parametro facoltativo scambiato.</span><span class="sxs-lookup"><span data-stu-id="072c5-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="072c5-151">Specificare questo se un backup deve essere mantenuto sempre in hello account di archiviazione, indipendentemente dal fatto che di risale è.</span><span class="sxs-lookup"><span data-stu-id="072c5-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="072c5-152">Ecco un esempio di come toouse questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="072c5-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="072c5-153">tooget hello pianificazione di backup corrente, utilizzare Get-AzureRmWebAppBackupConfiguration hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="072c5-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="072c5-154">Può essere utile per modificare una pianificazione già configurata.</span><span class="sxs-lookup"><span data-stu-id="072c5-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="072c5-155">Ripristinare un'app Web da un backup</span><span class="sxs-lookup"><span data-stu-id="072c5-155">Restore a web app from a backup</span></span>
<span data-ttu-id="072c5-156">toorestore un'app web da un backup, utilizzare cmdlet di hello AzureRmWebAppBackup di ripristino.</span><span class="sxs-lookup"><span data-stu-id="072c5-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="072c5-157">toouse modo più semplice Hello questo cmdlet è in un oggetto backup recuperato dal cmdlet Get-AzureRmWebAppBackup hello o il cmdlet Get-AzureRmWebAppBackupList toopipe.</span><span class="sxs-lookup"><span data-stu-id="072c5-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="072c5-158">Dopo aver creato un oggetto di backup, è possibile inviare tramite pipe nel cmdlet Restore-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="072c5-159">Specificare hello Sovrascrivi commutatore parametro tooindicate che si prevede di contenuto di hello toooverwrite dell'app web con contenuto di hello del backup hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="072c5-160">Se il backup di hello contiene i database, vengono ripristinati anche tali database.</span><span class="sxs-lookup"><span data-stu-id="072c5-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="072c5-161">Ecco un esempio di come toouse hello ripristino AzureRmWebAppBackup specificando tutti i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="072c5-162">Eliminazione di un backup</span><span class="sxs-lookup"><span data-stu-id="072c5-162">Delete a backup</span></span>
<span data-ttu-id="072c5-163">toodelete un backup, utilizzare il cmdlet Remove-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="072c5-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="072c5-164">Questo rimuove backup hello dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="072c5-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="072c5-165">Specificare il nome dell'app, il gruppo di risorse e ID di hello hello backup si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="072c5-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="072c5-166">È anche possibile inviare tramite pipe un oggetto di backup in toodelete cmdlet Remove-AzureRmWebAppBackup hello è.</span><span class="sxs-lookup"><span data-stu-id="072c5-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
