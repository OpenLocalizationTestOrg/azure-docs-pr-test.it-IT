---
title: caricamento del file tooconfigure aaaUse hello Azure PowerShell | Documenti Microsoft
description: Come toouse hello Azure PowerShell cmdlet tooconfigure caricamenti di file di tooenable hub IoT da dispositivi connessi. Include informazioni sulla configurazione di account di archiviazione di Azure di destinazione hello.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Configurare i caricamenti dei file nell'hub IoT con PowerShell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub IoT. È possibile usare un account di archiviazione esistente o crearne uno nuovo.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Cmdlet di Azure PowerShell][lnk-powershell-install].
* Un hub IoT di Azure. Se non si dispone di un hub IoT, è possibile utilizzare hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate uno oppure utilizzare hello portale troppo[creare un hub IoT] [ lnk-portal-hub].
* Un account di archiviazione di Azure. Se non si dispone di un account di archiviazione di Azure, è possibile utilizzare hello [cmdlet di archiviazione di Azure PowerShell] [ lnk-powershell-storage] toocreate uno oppure utilizzare hello portale troppo[creare un account di archiviazione] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Accedere all'account Azure e impostarlo

Accedi tooyour account Azure e selezionare la sottoscrizione.

1. Al prompt dei comandi PowerShell hello, eseguire hello **accesso AzureRmAccount** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali. Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toomanage l'hub IoT. È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Recuperare i dettagli dell'account di archiviazione

Hello passaggi seguenti si presuppone che la creazione dell'account di archiviazione utilizzando hello **Gestione risorse** modello di distribuzione e non hello **classico** modello di distribuzione.

Consente di caricare file tooconfigure dai dispositivi, è necessario stringa di connessione hello per un account di archiviazione di Azure. account di archiviazione Hello deve trovarsi in hello stessa sottoscrizione dell'hub IoT. È inoltre necessario nome hello di un contenitore blob nell'account di archiviazione hello. Utilizzare hello comando che segue tooretrieve le chiavi di account di archiviazione:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Prendere nota di hello **key1** valore di chiave di account di archiviazione. Non è presente hello alla procedura seguente.

Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:

* toolist hello blob i contenitori esistenti nell'account di archiviazione, usare hello seguenti comandi:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate un contenitore blob nell'account di archiviazione, hello di utilizzare i comandi seguenti:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Configurare l'hub IoT

È ora possibile configurare il tooenable hub IoT [funzionalità di caricamento del file] [ lnk-upload] utilizzando i dettagli dell'account di archiviazione.

configurazione di Hello richiede hello seguenti valori:

**Contenitore di archiviazione**: un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'hub IoT. Informazioni sull'account di archiviazione necessario hello nella precedente sezione hello recuperati. IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.

**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.

**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub. Tooone ora per impostazione predefinita.

**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere. Tooone giorno per impostazione predefinita.

**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello. Too10 per impostazione predefinita.

Usare l'hub IoT seguendo le impostazioni di caricamento file hello tooconfigure cmdlet PowerShell hello:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sulle funzionalità di caricamento file hello dell'IoT Hub, vedere [caricare i file da un dispositivo][lnk-upload].

Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:

* [Gestire in blocco i dispositivi IoT][lnk-bulk]
* [Metriche di Hub IoT][lnk-metrics]
* [Monitoraggio delle operazioni][lnk-monitor]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]
* [Soluzione IoT da hello la messa a terra sicura][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md