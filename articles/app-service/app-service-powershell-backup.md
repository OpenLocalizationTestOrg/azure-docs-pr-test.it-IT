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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Utilizzare PowerShell tooback e ripristino di App del servizio App
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [API REST](../app-service-web/websites-csm-backup.md)
> 
> 

Informazioni su come toouse Azure PowerShell tooback di backup e ripristino [App del servizio app](https://azure.microsoft.com/services/app-service/web/). Per altre informazioni sui backup delle app Web, inclusi i requisiti e le restrizioni, vedere [Eseguire il backup di un'app Web nel servizio app di Azure](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Prerequisiti
toouse PowerShell toomanage i backup di app, è necessario hello seguenti:

* **Un URL SAS** che consente la lettura e il contenitore di archiviazione di Azure tooan accesso in scrittura. Vedere [modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per una spiegazione di URL di firma di accesso condiviso. Vedere [Uso di Azure PowerShell con Archiviazione di Azure](../storage/common/storage-powershell-guide-full.md) per esempi sulla gestione di Archiviazione di Azure tramite PowerShell.
* **Una stringa di connessione di database** se si desidera tooback backup di un database con l'app web.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Come eseguire il backup cmdlet toogenerate toouse un URL SAS con hello web app
L'URL di firma di accesso condiviso può essere generato con PowerShell. Di seguito è riportato un esempio di come toogenerate che può essere utilizzato con i cmdlet di hello descritti in questo articolo.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Installare Azure PowerShell 1.3.2 o versioni successive
Per istruzioni sull'installazione e sull'uso di Azure PowerShell, vedere [Uso di Azure PowerShell con Azure Resource Manager](/powershell/azure/overview) .

## <a name="create-a-backup"></a>Creare un backup
Utilizzare toocreate cmdlet New-AzureRmWebAppBackup hello un backup di un'app web.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Viene creato un backup con un nome generato automaticamente. Se si desidera tooprovide un nome per il backup, usare parametro facoltativo di hello Nomebackup.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude un database nel backup hello, creare innanzitutto un'impostazione di backup del database utilizzando i cmdlet New-AzureRmWebAppDatabaseBackupSetting hello, quindi specificare tale impostazione in hello database parametro del cmdlet New-AzureRmWebAppBackup hello. il parametro database Hello accetta una matrice di impostazioni del database, consentendo tooback su più di un database.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Ottenere i backup
cmdlet Get-AzureRmWebAppBackupList Hello restituisce una matrice di tutti i backup per un'app web. È necessario fornire il nome di hello di hello web app e il relativo gruppo di risorse.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget un backup specifico, utilizzare il cmdlet Get-AzureRmWebAppBackup hello.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

È anche possibile inviare tramite pipe un oggetto applicazione web in uno dei cmdlet di gestione dei backup hello per praticità.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Pianificare backup automatici
È possibile pianificare i backup toohappen automaticamente a un intervallo specificato. tooconfigure una pianificazione di backup, utilizzare i cmdlet di hello AzureRmWebAppBackupConfiguration di modifica. Questo cmdlet accetta alcuni parametri:

* **Nome** : hello nome dell'app web hello.
* **ResourceGroupName** : hello nome della risorsa gruppo contenitore hello web app hello.
* **Slot** : facoltativo. nome Hello dello slot di hello web app.
* **StorageAccountUrl** -hello URL di firma di accesso condiviso per il contenitore di archiviazione di Azure hello utilizzato backup hello toostore.
* **FrequencyInterval** -valore numerico per la frequenza con cui hello i backup devono essere effettuati. Deve essere un intero positivo.
* **FrequencyUnit** -unità di tempo per la frequenza con cui hello i backup devono essere effettuati. Le opzioni disponibili sono Hour e Day.
* **RetentionPeriodInDays** - quanti giorni devono essere salvati i backup automatici di hello prima di essere eliminati automaticamente.
* **StartTime** : facoltativo. ora di Hello quando deve iniziare i backup automatici hello. I backup iniziano immediatamente se questo valore è Null. Deve essere un valore DateTime.
* **Databases** : facoltativo. Matrice di DatabaseBackupSettings per toobackup database hello.
* **KeepAtLeastOneBackup** : parametro facoltativo scambiato. Specificare questo se un backup deve essere mantenuto sempre in hello account di archiviazione, indipendentemente dal fatto che di risale è.

Ecco un esempio di come toouse questo cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello pianificazione di backup corrente, utilizzare Get-AzureRmWebAppBackupConfiguration hello cmdlet. Può essere utile per modificare una pianificazione già configurata.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Ripristinare un'app Web da un backup
toorestore un'app web da un backup, utilizzare cmdlet di hello AzureRmWebAppBackup di ripristino. toouse modo più semplice Hello questo cmdlet è in un oggetto backup recuperato dal cmdlet Get-AzureRmWebAppBackup hello o il cmdlet Get-AzureRmWebAppBackupList toopipe.

Dopo aver creato un oggetto di backup, è possibile inviare tramite pipe nel cmdlet Restore-AzureRmWebAppBackup hello. Specificare hello Sovrascrivi commutatore parametro tooindicate che si prevede di contenuto di hello toooverwrite dell'app web con contenuto di hello del backup hello. Se il backup di hello contiene i database, vengono ripristinati anche tali database.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Ecco un esempio di come toouse hello ripristino AzureRmWebAppBackup specificando tutti i parametri di hello.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Eliminazione di un backup
toodelete un backup, utilizzare il cmdlet Remove-AzureRmWebAppBackup hello. Questo rimuove backup hello dall'account di archiviazione. Specificare il nome dell'app, il gruppo di risorse e ID di hello hello backup si desidera toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

È anche possibile inviare tramite pipe un oggetto di backup in toodelete cmdlet Remove-AzureRmWebAppBackup hello è.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
