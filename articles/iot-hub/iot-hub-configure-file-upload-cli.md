---
title: Configurare l'upload del file nell'hub IoT usando l'interfaccia della riga di comando di Azure (az.py) | Microsoft Docs
description: Come configurare gli upload di file nell'hub IoT usando l'interfaccia della riga di comando della multipiattaforma di Azure 2.0 (az.py).
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="17058-103">Configurare gli upload dei file nell'hub IoT tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="17058-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="17058-104">Per usare la [funzionalità di caricamento di file nell'hub IoT][lnk-upload], è prima di tutto necessario associare un account di archiviazione di Azure all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17058-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="17058-105">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="17058-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="17058-106">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="17058-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="17058-107">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="17058-107">An active Azure account.</span></span> <span data-ttu-id="17058-108">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="17058-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="17058-109">[Interfaccia della riga di comando di Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="17058-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="17058-110">Un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="17058-110">An Azure IoT hub.</span></span> <span data-ttu-id="17058-111">Se non si dispone di un hub IoT, è possibile usare il `az iot hub create` [comando][lnk-cli-create-iothub] per crearne uno o il portale per [Creare un hub IoT][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="17058-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="17058-112">Un account dell'Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="17058-112">An Azure Storage account.</span></span> <span data-ttu-id="17058-113">Se non si dispone di un account di Archiviazione di Azure, è possibile usare l'[interfaccia della riga di comando di Azure 2.0 - Gestione degli account di archiviazione][lnk-manage-storage] per crearne uno o usare il portale per [Creare un account di archiviazione][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="17058-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="17058-114">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="17058-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="17058-115">Accedere al proprio account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="17058-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="17058-116">Al prompt dei comandi eseguire il [comando per l'accesso][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="17058-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="17058-117">Seguire le istruzioni per l'autenticazione tramite il codice e accedere all'account Azure con un Web browser.</span><span class="sxs-lookup"><span data-stu-id="17058-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="17058-118">Se si usano più sottoscrizioni di Azure, effettuando l'accesso ad Azure è possibile accedere a tutti gli account Azure associati alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="17058-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="17058-119">Usare il seguente [comando per elencare gli account Azure][lnk-az-account-command] che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="17058-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="17058-120">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per creare l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17058-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="17058-121">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="17058-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="17058-122">Recuperare i dettagli dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="17058-122">Retrieve your storage account details</span></span>

<span data-ttu-id="17058-123">I passaggi seguenti presuppongono che l'account di archiviazione sia stato creato tramite il modello di distribuzione di **Resource Manager** e non tramite quello **Classico**.</span><span class="sxs-lookup"><span data-stu-id="17058-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="17058-124">Per configurare i caricamenti dei file dai propri dispositivi, è necessario disporre della stringa di connessione di un account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="17058-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="17058-125">L'account di archiviazione deve trovarsi nella stessa sottoscrizione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17058-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="17058-126">È inoltre necessario il nome del contenitore BLOB nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17058-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="17058-127">Usare il comando seguente per recuperare le chiavi dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="17058-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="17058-128">Prendere nota del valore **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="17058-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="17058-129">sarà necessario nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="17058-129">You need it in the following steps.</span></span>

<span data-ttu-id="17058-130">Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:</span><span class="sxs-lookup"><span data-stu-id="17058-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="17058-131">Per elencare i contenitori BLOB esistenti nell'account di archiviazione, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="17058-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="17058-132">Per creare un contenitore BLOB nell'account di archiviazione, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="17058-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="17058-133">Caricamento di file</span><span class="sxs-lookup"><span data-stu-id="17058-133">File upload</span></span>

<span data-ttu-id="17058-134">È ora possibile configurare l'hub IoT per abilitare la [funzionalità di caricamento dei file][lnk-upload] usando i dettagli dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17058-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="17058-135">La configurazione richiede i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="17058-135">The configuration requires the following values:</span></span>

<span data-ttu-id="17058-136">**Contenitore di archiviazione**: un contenitore BLOB in un account di archiviazione di Azure nella sottoscrizione corrente da associare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17058-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="17058-137">Le informazioni necessarie sull'account di archiviazione sono state recuperate nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="17058-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="17058-138">L'hub IoT genera automaticamente URI di firma di accesso condiviso con autorizzazioni di scrittura per questo contenitore BLOB che possono essere usati dai dispositivi durante il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="17058-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="17058-139">**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="17058-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="17058-140">**SAS TTL**(TTL di firma di accesso condiviso): questa impostazione indica la durata degli URI di firma di accesso condiviso restituiti dal dispositivo tramite l’hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17058-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="17058-141">Il valore è un'ora per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="17058-141">Set to one hour by default.</span></span>

<span data-ttu-id="17058-142">**File notification settings default TTL**(TTL predefinito per le impostazioni di notifica dei file): durata di una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="17058-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="17058-143">Il valore è un giorno per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="17058-143">Set to one day by default.</span></span>

<span data-ttu-id="17058-144">**File notification maximum delivery count**(Numero massimo di recapiti per le notifiche dei file): numero di tentativi che verranno eseguiti dall'hub IoT per distribuire una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="17058-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="17058-145">Il valore è 10 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="17058-145">Set to 10 by default.</span></span>

<span data-ttu-id="17058-146">Usare i comandi dell'interfaccia della riga di comando di Azure per configurare le impostazioni di upload dei file nell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="17058-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="17058-147">In un uso di shell bash:</span><span class="sxs-lookup"><span data-stu-id="17058-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="17058-148">Nell'uso di un prompt dei comandi di Windows:</span><span class="sxs-lookup"><span data-stu-id="17058-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="17058-149">È possibile esaminare la configurazione di upload del file sull'hub IoT usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="17058-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="17058-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17058-150">Next steps</span></span>

<span data-ttu-id="17058-151">Per altre informazioni sulle funzionalità di caricamento dei file dell'hub IoT, vedere [Caricare file da un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="17058-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="17058-152">Per ulteriori informazioni sulla gestione dell'hub IoT di Azure, consultare questi collegamenti:</span><span class="sxs-lookup"><span data-stu-id="17058-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="17058-153">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="17058-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="17058-154">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="17058-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="17058-155">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="17058-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="17058-156">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="17058-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="17058-157">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="17058-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="17058-158">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="17058-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="17058-159">[Proteggere la soluzione IoT sin dall'inizio][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="17058-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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