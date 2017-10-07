---
title: tooIoT di caricamento file aaaConfigure Hub utilizzando l'interfaccia CLI di Azure (az.py) | Documenti Microsoft
description: Come tooconfigure fileuploads tooAzure Hub IoT utilizzando hello multipiattaforma CLI di Azure 2.0 (az.py).
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Configurare gli upload dei file nell'hub IoT tramite l'interfaccia della riga di comando di Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub IoT. È possibile usare un account di archiviazione esistente o crearne uno nuovo.

toocomplete questa esercitazione, è necessario hello seguenti:

* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].
* Un hub IoT di Azure. Se non si dispone di un hub IoT, è possibile utilizzare hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate uno oppure utilizzare hello portale troppo [Crea un hub IoT] [file lnk-portale-hub].
* Un account dell'Archiviazione di Azure. Se non si dispone di un account di archiviazione di Azure, è possibile utilizzare hello [CLI di Azure 2.0 - gestire gli account di archiviazione] [ lnk-manage-storage] toocreate uno oppure utilizzare hello portale troppo[creare un account di archiviazione] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Accedere all'account Azure e impostarlo

Accedi tooyour account Azure e selezionare la sottoscrizione.

1. Al prompt dei comandi di hello, eseguire hello [comando login][lnk-login-command]:

    ```azurecli
    az login
    ```

    Seguire tooauthenticate istruzioni hello utilizzando codice hello e Accedi tooyour account Azure tramite un web browser.

1. Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello associato con le credenziali dell'account di Azure. Utilizzare la seguente hello [toolist comando hello account Azure] [ lnk-az-account-command] disponibile per toouse è:

    ```azurecli
    az account list
    ```

    Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT. È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Recuperare i dettagli dell'account di archiviazione

Hello passaggi seguenti si presuppone che la creazione dell'account di archiviazione utilizzando hello **Gestione risorse** modello di distribuzione e non hello **classico** modello di distribuzione.

Consente di caricare file tooconfigure dai dispositivi, è necessario stringa di connessione hello per un account di archiviazione di Azure. account di archiviazione Hello deve trovarsi in hello stessa sottoscrizione dell'hub IoT. È inoltre necessario nome hello di un contenitore blob nell'account di archiviazione hello. Utilizzare hello comando che segue tooretrieve le chiavi di account di archiviazione:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Prendere nota di hello **connectionString** valore. Non è presente hello alla procedura seguente.

Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:

* toolist hello blob i contenitori esistenti nell'account di archiviazione, usare hello comando seguente:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate un contenitore blob nell'account di archiviazione, utilizzare hello comando seguente:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Caricamento di file

È ora possibile configurare il tooenable hub IoT [funzionalità di caricamento del file] [ lnk-upload] utilizzando i dettagli dell'account di archiviazione.

configurazione di Hello richiede hello seguenti valori:

**Contenitore di archiviazione**: un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'hub IoT. Informazioni sull'account di archiviazione necessario hello nella precedente sezione hello recuperati. IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.

**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.

**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub. Tooone ora per impostazione predefinita.

**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere. Tooone giorno per impostazione predefinita.

**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello. Too10 per impostazione predefinita.

Utilizzare le impostazioni di caricamento file hello tooconfigure comandi CLI di Azure seguendo l'hub IoT hello:

In un uso di shell bash:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Nell'uso di un prompt dei comandi di Windows:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

È possibile consultare configurazione di caricamento file hello in IoT hub utilizzando hello comando seguente:

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create