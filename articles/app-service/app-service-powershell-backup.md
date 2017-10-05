---
title: Usare PowerShell per eseguire il backup e il ripristino di app del servizio app
description: Informazioni su come usare PowerShell per eseguire il backup e il ripristino di un'app nel servizio app di Azure
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="b2e18-103">Usare PowerShell per eseguire il backup e il ripristino di app del servizio app</span><span class="sxs-lookup"><span data-stu-id="b2e18-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2e18-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2e18-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="b2e18-105">API REST</span><span class="sxs-lookup"><span data-stu-id="b2e18-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="b2e18-106">Informazioni su come usare Azure PowerShell per eseguire il backup e il ripristino di [app del servizio app](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="b2e18-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="b2e18-107">Per altre informazioni sui backup delle app Web, inclusi i requisiti e le restrizioni, vedere [Eseguire il backup di un'app Web nel servizio app di Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b2e18-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2e18-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b2e18-108">Prerequisites</span></span>
<span data-ttu-id="b2e18-109">Per usare PowerShell per gestire i backup delle app, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b2e18-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="b2e18-110">**URL di firma di accesso condiviso** che consente l'accesso in lettura e scrittura a un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e18-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="b2e18-111">Per una spiegazione degli URL di firma di accesso condiviso, vedere [Conoscere il modello di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="b2e18-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="b2e18-112">Vedere [Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) per esempi sulla gestione di Archiviazione di Azure tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2e18-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="b2e18-113">**stringa di connessione del database** se si vuole eseguire il backup di un database insieme all'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="b2e18-114">Come generare un URL di firma di accesso condiviso da usare con i cmdlet di backup dell'app Web</span><span class="sxs-lookup"><span data-stu-id="b2e18-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="b2e18-115">L'URL di firma di accesso condiviso può essere generato con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2e18-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="b2e18-116">Di seguito è riportato un esempio su come generare un URL da usare con i cmdlet descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="b2e18-117">Installare Azure PowerShell 1.3.2 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="b2e18-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="b2e18-118">Per istruzioni sull'installazione e sull'uso di Azure PowerShell, vedere [Uso di Azure PowerShell con Azure Resource Manager](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="b2e18-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="b2e18-119">Creare un backup</span><span class="sxs-lookup"><span data-stu-id="b2e18-119">Create a backup</span></span>
<span data-ttu-id="b2e18-120">Usare il cmdlet New-AzureRmWebAppBackup per creare un backup di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="b2e18-121">Viene creato un backup con un nome generato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b2e18-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="b2e18-122">Se si vuole specificare un nome per il backup, usare il parametro facoltativo BackupName.</span><span class="sxs-lookup"><span data-stu-id="b2e18-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="b2e18-123">Per includere un database nel backup, creare prima di tutto un'impostazione di backup del database usando il cmdlet New-AzureRmWebAppDatabaseBackupSetting, quindi fornire tale informazione nel parametro Databases del cmdlet New-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="b2e18-124">Il parametro Databases accetta una matrice di impostazioni del database, consentendo di eseguire il backup di più database.</span><span class="sxs-lookup"><span data-stu-id="b2e18-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="b2e18-125">Ottenere i backup</span><span class="sxs-lookup"><span data-stu-id="b2e18-125">Get backups</span></span>
<span data-ttu-id="b2e18-126">Il cmdlet Get-AzureRmWebAppBackupList restituisce una matrice di backup per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="b2e18-127">È necessario specificare il nome dell'app Web e il rispettivo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b2e18-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="b2e18-128">Per ottenere un backup specifico, usare il cmdlet Get-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="b2e18-129">Per semplificare, è anche possibile inviare tramite pipe un oggetto app Web in uno dei cmdlet di gestione dei backup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="b2e18-130">Pianificare backup automatici</span><span class="sxs-lookup"><span data-stu-id="b2e18-130">Schedule automatic backups</span></span>
<span data-ttu-id="b2e18-131">È possibile pianificare i backup in modo che vengano eseguiti automaticamente a un intervallo specificato.</span><span class="sxs-lookup"><span data-stu-id="b2e18-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="b2e18-132">Per configurare una pianificazione di backup, usare il cmdlet Edit-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b2e18-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="b2e18-133">Questo cmdlet accetta alcuni parametri:</span><span class="sxs-lookup"><span data-stu-id="b2e18-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="b2e18-134">**Name** : nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="b2e18-135">**ResourceGroupName** : nome del gruppo di risorse che include l'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="b2e18-136">**Slot** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-136">**Slot** - Optional.</span></span> <span data-ttu-id="b2e18-137">Nome dello slot dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="b2e18-137">The name of the web app slot.</span></span>
* <span data-ttu-id="b2e18-138">**StorageAccountUrl** : URL di firma di accesso condiviso del contenitore di archiviazione di Azure usato per archiviare i backup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="b2e18-139">**FrequencyInterval** : valore numerico relativo alla frequenza con cui devono essere eseguiti i backup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="b2e18-140">Deve essere un intero positivo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-140">Must be a positive integer.</span></span>
* <span data-ttu-id="b2e18-141"><seg>
  **FrequencyUnit** : unità di tempo relativa alla frequenza con cui devono essere eseguiti i backup..</seg></span><span class="sxs-lookup"><span data-stu-id="b2e18-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="b2e18-142">Le opzioni disponibili sono Hour e Day.</span><span class="sxs-lookup"><span data-stu-id="b2e18-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="b2e18-143">**RetentionPeriodInDays** : giorni per cui è necessario conservare i backup automatici prima dell'eliminazione automatica.</span><span class="sxs-lookup"><span data-stu-id="b2e18-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="b2e18-144">**StartTime** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-144">**StartTime** - Optional.</span></span> <span data-ttu-id="b2e18-145">Ora in cui devono iniziare i backup automatici.</span><span class="sxs-lookup"><span data-stu-id="b2e18-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="b2e18-146">I backup iniziano immediatamente se questo valore è Null.</span><span class="sxs-lookup"><span data-stu-id="b2e18-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="b2e18-147">Deve essere un valore DateTime.</span><span class="sxs-lookup"><span data-stu-id="b2e18-147">Must be a DateTime.</span></span>
* <span data-ttu-id="b2e18-148">**Databases** : facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-148">**Databases** - Optional.</span></span> <span data-ttu-id="b2e18-149">Una matrice di DatabaseBackupSettings per i database da sottoporre a backup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="b2e18-150">**KeepAtLeastOneBackup** : parametro facoltativo scambiato.</span><span class="sxs-lookup"><span data-stu-id="b2e18-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="b2e18-151">Specificare questo valore se è necessario conservare sempre un backup nell'account di archiviazione, indipendentemente da quando è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b2e18-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="b2e18-152">Di seguito un esempio di uso del cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b2e18-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="b2e18-153">Per ottenere la pianificazione di backup corrente, usare il cmdlet Get-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b2e18-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="b2e18-154">Può essere utile per modificare una pianificazione già configurata.</span><span class="sxs-lookup"><span data-stu-id="b2e18-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="b2e18-155">Ripristinare un'app Web da un backup</span><span class="sxs-lookup"><span data-stu-id="b2e18-155">Restore a web app from a backup</span></span>
<span data-ttu-id="b2e18-156">Per ripristinare un'app Web da un backup, usare il cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="b2e18-157">Il modo più semplice per usare questo cmdlet consiste nell'inviare tramite pipe un oggetto backup recuperato dal cmdlet Get-AzureRmWebAppBackup o dal cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="b2e18-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="b2e18-158">Dopo avere ottenuto un oggetto backup, è possibile inviarlo tramite pipe nel cmdlet Restore-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="b2e18-159">Specificare il parametro opzionale Overwrite per indicare che si intende sovrascrivere i contenuti dell'app Web con i contenuti del backup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="b2e18-160">Se il backup contiene database, vengono ripristinati anche tali database.</span><span class="sxs-lookup"><span data-stu-id="b2e18-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="b2e18-161">Di seguito un esempio di uso del cmdlet Restore-AzureRmWebAppBackup con tutti i parametri specificati.</span><span class="sxs-lookup"><span data-stu-id="b2e18-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="b2e18-162">Eliminazione di un backup</span><span class="sxs-lookup"><span data-stu-id="b2e18-162">Delete a backup</span></span>
<span data-ttu-id="b2e18-163">Per eliminare un backup, usare il cmdlet Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="b2e18-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="b2e18-164">Il backup viene rimosso dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b2e18-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="b2e18-165">Specificare il nome dell'app, il rispettivo gruppo di risorse e l'ID del backup da eliminare.</span><span class="sxs-lookup"><span data-stu-id="b2e18-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="b2e18-166">È anche possibile inviare tramite pipe un oggetto backup al cmdlet Remove-AzureRmWebAppBackup per eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="b2e18-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
