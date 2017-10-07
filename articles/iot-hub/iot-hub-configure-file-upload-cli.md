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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="b3436-103">Configurare gli upload dei file nell'hub IoT tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b3436-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="b3436-104">hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b3436-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="b3436-105">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="b3436-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="b3436-106">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3436-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b3436-107">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b3436-107">An active Azure account.</span></span> <span data-ttu-id="b3436-108">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b3436-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b3436-109">[Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="b3436-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="b3436-110">Un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-110">An Azure IoT hub.</span></span> <span data-ttu-id="b3436-111">Se non si dispone di un hub IoT, è possibile utilizzare hello `az iot hub create` [comando] [ lnk-cli-create-iothub] toocreate uno oppure utilizzare hello portale troppo [Crea un hub IoT] [file lnk-portale-hub].</span><span class="sxs-lookup"><span data-stu-id="b3436-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="b3436-112">Un account dell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-112">An Azure Storage account.</span></span> <span data-ttu-id="b3436-113">Se non si dispone di un account di archiviazione di Azure, è possibile utilizzare hello [CLI di Azure 2.0 - gestire gli account di archiviazione] [ lnk-manage-storage] toocreate uno oppure utilizzare hello portale troppo[creare un account di archiviazione] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="b3436-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="b3436-114">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="b3436-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="b3436-115">Accedi tooyour account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b3436-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="b3436-116">Al prompt dei comandi di hello, eseguire hello [comando login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="b3436-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="b3436-117">Seguire tooauthenticate istruzioni hello utilizzando codice hello e Accedi tooyour account Azure tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="b3436-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="b3436-118">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello associato con le credenziali dell'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="b3436-119">Utilizzare la seguente hello [toolist comando hello account Azure] [ lnk-az-account-command] disponibile per toouse è:</span><span class="sxs-lookup"><span data-stu-id="b3436-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="b3436-120">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toocreate l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b3436-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="b3436-121">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="b3436-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="b3436-122">Recuperare i dettagli dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b3436-122">Retrieve your storage account details</span></span>

<span data-ttu-id="b3436-123">Hello passaggi seguenti si presuppone che la creazione dell'account di archiviazione utilizzando hello **Gestione risorse** modello di distribuzione e non hello **classico** modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b3436-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="b3436-124">Consente di caricare file tooconfigure dai dispositivi, è necessario stringa di connessione hello per un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b3436-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="b3436-125">account di archiviazione Hello deve trovarsi in hello stessa sottoscrizione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b3436-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="b3436-126">È inoltre necessario nome hello di un contenitore blob nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b3436-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="b3436-127">Utilizzare hello comando che segue tooretrieve le chiavi di account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b3436-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="b3436-128">Prendere nota di hello **connectionString** valore.</span><span class="sxs-lookup"><span data-stu-id="b3436-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="b3436-129">Non è presente hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b3436-129">You need it in hello following steps.</span></span>

<span data-ttu-id="b3436-130">Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:</span><span class="sxs-lookup"><span data-stu-id="b3436-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="b3436-131">toolist hello blob i contenitori esistenti nell'account di archiviazione, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3436-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="b3436-132">toocreate un contenitore blob nell'account di archiviazione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3436-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="b3436-133">Caricamento di file</span><span class="sxs-lookup"><span data-stu-id="b3436-133">File upload</span></span>

<span data-ttu-id="b3436-134">È ora possibile configurare il tooenable hub IoT [funzionalità di caricamento del file] [ lnk-upload] utilizzando i dettagli dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b3436-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="b3436-135">configurazione di Hello richiede hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="b3436-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="b3436-136">**Contenitore di archiviazione**: un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b3436-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="b3436-137">Informazioni sull'account di archiviazione necessario hello nella precedente sezione hello recuperati.</span><span class="sxs-lookup"><span data-stu-id="b3436-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="b3436-138">IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="b3436-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="b3436-139">**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="b3436-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="b3436-140">**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3436-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="b3436-141">Tooone ora per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b3436-141">Set tooone hour by default.</span></span>

<span data-ttu-id="b3436-142">**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere.</span><span class="sxs-lookup"><span data-stu-id="b3436-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="b3436-143">Tooone giorno per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b3436-143">Set tooone day by default.</span></span>

<span data-ttu-id="b3436-144">**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="b3436-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="b3436-145">Too10 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b3436-145">Set too10 by default.</span></span>

<span data-ttu-id="b3436-146">Utilizzare le impostazioni di caricamento file hello tooconfigure comandi CLI di Azure seguendo l'hub IoT hello:</span><span class="sxs-lookup"><span data-stu-id="b3436-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="b3436-147">In un uso di shell bash:</span><span class="sxs-lookup"><span data-stu-id="b3436-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="b3436-148">Nell'uso di un prompt dei comandi di Windows:</span><span class="sxs-lookup"><span data-stu-id="b3436-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="b3436-149">È possibile consultare configurazione di caricamento file hello in IoT hub utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3436-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="b3436-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3436-150">Next steps</span></span>

<span data-ttu-id="b3436-151">Per ulteriori informazioni sulle funzionalità di caricamento file hello dell'IoT Hub, vedere [caricare i file da un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="b3436-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="b3436-152">Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b3436-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="b3436-153">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="b3436-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="b3436-154">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="b3436-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="b3436-155">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="b3436-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="b3436-156">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="b3436-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b3436-157">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b3436-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="b3436-158">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b3436-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="b3436-159">[Soluzione IoT da hello la messa a terra sicura][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="b3436-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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