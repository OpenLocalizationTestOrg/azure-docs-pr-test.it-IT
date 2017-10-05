---
title: Usare Azure PowerShell per configurare il caricamento dei file | Microsoft Docs
description: Come usare i cmdlet di Azure PowerShell per configurare l'hub IoT per abilitare i caricamenti di file da dispositivi connessi. Include informazioni sulla configurazione dell'account di archiviazione di Azure di destinazione.
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="ceede-104">Configurare i caricamenti dei file nell'hub IoT con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceede-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="ceede-105">Per usare la [funzionalità di caricamento di file nell'hub IoT][lnk-upload], è prima di tutto necessario associare un account di archiviazione di Azure all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ceede-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="ceede-106">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="ceede-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="ceede-107">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ceede-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ceede-108">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="ceede-108">An active Azure account.</span></span> <span data-ttu-id="ceede-109">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="ceede-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ceede-110">[Cmdlet di Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="ceede-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="ceede-111">Un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="ceede-111">An Azure IoT hub.</span></span> <span data-ttu-id="ceede-112">Se non si dispone di un hub IoT, è possibile usare il [cmdlet New-AzureRmIoTHub][lnk-powershell-iothub] o il portale per crearne uno: vedi [Creare un hub IoT][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="ceede-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="ceede-113">Un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ceede-113">An Azure storage account.</span></span> <span data-ttu-id="ceede-114">Se non si dispone di un account di Archiviazione di Azure, è possibile usare i [cmdlet PowerShell di Archiviazione di Azure][lnk-powershell-storage] per crearne uno o usare il portale per [creare un account di archiviazione][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="ceede-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="ceede-115">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="ceede-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="ceede-116">Accedere al proprio account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ceede-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="ceede-117">Nel prompt di PowerShell, usare il cmdlet **Login-AzureRmAccount**:</span><span class="sxs-lookup"><span data-stu-id="ceede-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="ceede-118">Se si usano più sottoscrizioni Azure e si esegue l'accesso ad Azure, è possibile accedere a tutte le sottoscrizioni di Azure associate alle credenziali.</span><span class="sxs-lookup"><span data-stu-id="ceede-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="ceede-119">Usare il comando seguente per elencare gli account Azure che è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="ceede-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="ceede-120">Usare il comando seguente per selezionare la sottoscrizione che si vuole usare per eseguire i comandi per gestire l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ceede-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="ceede-121">È possibile usare il nome o l'ID della sottoscrizione dall'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="ceede-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="ceede-122">Recuperare i dettagli dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ceede-122">Retrieve your storage account details</span></span>

<span data-ttu-id="ceede-123">I passaggi seguenti presuppongono che l'account di archiviazione sia stato creato tramite il modello di distribuzione di **Resource Manager** e non tramite quello **Classico**.</span><span class="sxs-lookup"><span data-stu-id="ceede-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="ceede-124">Per configurare i caricamenti dei file dai propri dispositivi, è necessario disporre della stringa di connessione di un account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ceede-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="ceede-125">L'account di archiviazione deve trovarsi nella stessa sottoscrizione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ceede-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="ceede-126">È inoltre necessario il nome del contenitore BLOB nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ceede-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="ceede-127">Usare il comando seguente per recuperare le chiavi dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="ceede-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="ceede-128">Prendere nota del valore della chiave dell'account di archiviazione **key1**.</span><span class="sxs-lookup"><span data-stu-id="ceede-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="ceede-129">sarà necessario nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="ceede-129">You need it in the following steps.</span></span>

<span data-ttu-id="ceede-130">Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:</span><span class="sxs-lookup"><span data-stu-id="ceede-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="ceede-131">Per elencare i contenitori BLOB esistente nell'account di archiviazione, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ceede-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="ceede-132">Per creare un contenitore BLOB nell'account di archiviazione, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ceede-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="ceede-133">Configurare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="ceede-133">Configure your IoT hub</span></span>

<span data-ttu-id="ceede-134">È ora possibile configurare l'hub IoT per abilitare la [funzionalità di caricamento dei file][lnk-upload] usando i dettagli dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ceede-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="ceede-135">La configurazione richiede i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="ceede-135">The configuration requires the following values:</span></span>

<span data-ttu-id="ceede-136">**Contenitore di archiviazione**: un contenitore BLOB in un account di archiviazione di Azure nella sottoscrizione corrente da associare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ceede-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="ceede-137">Le informazioni necessarie sull'account di archiviazione sono state recuperate nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ceede-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="ceede-138">L'hub IoT genera automaticamente URI di firma di accesso condiviso con autorizzazioni di scrittura per questo contenitore BLOB che possono essere usati dai dispositivi durante il caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="ceede-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="ceede-139">**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="ceede-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="ceede-140">**SAS TTL**(TTL di firma di accesso condiviso): questa impostazione indica la durata degli URI di firma di accesso condiviso restituiti dal dispositivo tramite l’hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ceede-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="ceede-141">Il valore è un'ora per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ceede-141">Set to one hour by default.</span></span>

<span data-ttu-id="ceede-142">**File notification settings default TTL**(TTL predefinito per le impostazioni di notifica dei file): durata di una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="ceede-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="ceede-143">Il valore è un giorno per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ceede-143">Set to one day by default.</span></span>

<span data-ttu-id="ceede-144">**File notification maximum delivery count**(Numero massimo di recapiti per le notifiche dei file): numero di tentativi che verranno eseguiti dall'hub IoT per distribuire una notifica di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="ceede-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="ceede-145">Il valore è 10 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ceede-145">Set to 10 by default.</span></span>

<span data-ttu-id="ceede-146">Usare il cmdlet PowerShell seguente per configurare le impostazioni di caricamento dei file nell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="ceede-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ceede-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ceede-147">Next steps</span></span>

<span data-ttu-id="ceede-148">Per altre informazioni sulle funzionalità di caricamento dei file dell'hub IoT, vedere [Caricare file da un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="ceede-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="ceede-149">Per ulteriori informazioni sulla gestione dell'hub IoT di Azure, consultare questi collegamenti:</span><span class="sxs-lookup"><span data-stu-id="ceede-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="ceede-150">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="ceede-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="ceede-151">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="ceede-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="ceede-152">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="ceede-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="ceede-153">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="ceede-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ceede-154">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ceede-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ceede-155">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ceede-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="ceede-156">[Proteggere la soluzione IoT sin dall'inizio][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="ceede-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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