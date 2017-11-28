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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="23112-104">Configurare i caricamenti dei file nell'hub IoT con PowerShell</span><span class="sxs-lookup"><span data-stu-id="23112-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="23112-105">hello toouse [funzionalità di caricamento del file nell'IoT Hub][lnk-upload], è innanzitutto necessario associare un account di archiviazione di Azure con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="23112-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="23112-106">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="23112-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="23112-107">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="23112-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="23112-108">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="23112-108">An active Azure account.</span></span> <span data-ttu-id="23112-109">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="23112-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="23112-110">[Cmdlet di Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="23112-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="23112-111">Un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="23112-111">An Azure IoT hub.</span></span> <span data-ttu-id="23112-112">Se non si dispone di un hub IoT, è possibile utilizzare hello [cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate uno oppure utilizzare hello portale troppo[creare un hub IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="23112-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="23112-113">Un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="23112-113">An Azure storage account.</span></span> <span data-ttu-id="23112-114">Se non si dispone di un account di archiviazione di Azure, è possibile utilizzare hello [cmdlet di archiviazione di Azure PowerShell] [ lnk-powershell-storage] toocreate uno oppure utilizzare hello portale troppo[creare un account di archiviazione] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="23112-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="23112-115">Accedere all'account Azure e impostarlo</span><span class="sxs-lookup"><span data-stu-id="23112-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="23112-116">Accedi tooyour account Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="23112-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="23112-117">Al prompt dei comandi PowerShell hello, eseguire hello **accesso AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="23112-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="23112-118">Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="23112-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="23112-119">Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:</span><span class="sxs-lookup"><span data-stu-id="23112-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="23112-120">Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toomanage l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="23112-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="23112-121">È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:</span><span class="sxs-lookup"><span data-stu-id="23112-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="23112-122">Recuperare i dettagli dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="23112-122">Retrieve your storage account details</span></span>

<span data-ttu-id="23112-123">Hello passaggi seguenti si presuppone che la creazione dell'account di archiviazione utilizzando hello **Gestione risorse** modello di distribuzione e non hello **classico** modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="23112-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="23112-124">Consente di caricare file tooconfigure dai dispositivi, è necessario stringa di connessione hello per un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="23112-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="23112-125">account di archiviazione Hello deve trovarsi in hello stessa sottoscrizione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="23112-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="23112-126">È inoltre necessario nome hello di un contenitore blob nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="23112-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="23112-127">Utilizzare hello comando che segue tooretrieve le chiavi di account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="23112-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="23112-128">Prendere nota di hello **key1** valore di chiave di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="23112-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="23112-129">Non è presente hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="23112-129">You need it in hello following steps.</span></span>

<span data-ttu-id="23112-130">Per i caricamenti dei file, è possibile usare un contenitore BLOB esistente oppure crearne uno nuovo:</span><span class="sxs-lookup"><span data-stu-id="23112-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="23112-131">toolist hello blob i contenitori esistenti nell'account di archiviazione, usare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="23112-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="23112-132">toocreate un contenitore blob nell'account di archiviazione, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="23112-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="23112-133">Configurare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="23112-133">Configure your IoT hub</span></span>

<span data-ttu-id="23112-134">È ora possibile configurare il tooenable hub IoT [funzionalità di caricamento del file] [ lnk-upload] utilizzando i dettagli dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="23112-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="23112-135">configurazione di Hello richiede hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="23112-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="23112-136">**Contenitore di archiviazione**: un contenitore blob in un account di archiviazione di Azure nel tooassociate sottoscrizione Azure corrente con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="23112-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="23112-137">Informazioni sull'account di archiviazione necessario hello nella precedente sezione hello recuperati.</span><span class="sxs-lookup"><span data-stu-id="23112-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="23112-138">IoT Hub genera automaticamente gli URI di firma di accesso condiviso con le autorizzazioni scrittura di toothis il contenitore blob per i dispositivi toouse durante il caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="23112-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="23112-139">**Receive notifications for uploaded files** (Ricezione di notifiche per i file caricati): abilitare o disabilitare le notifiche di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="23112-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="23112-140">**TTL SAS**: questa impostazione è hello time-to-live di hello SAS URI restituito toohello dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="23112-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="23112-141">Tooone ora per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="23112-141">Set tooone hour by default.</span></span>

<span data-ttu-id="23112-142">**Notifica di impostazioni predefinite di durata (TTL) del file**: hello time-to-live di una notifica di caricamento file prima di scadere.</span><span class="sxs-lookup"><span data-stu-id="23112-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="23112-143">Tooone giorno per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="23112-143">Set tooone day by default.</span></span>

<span data-ttu-id="23112-144">**Conteggio distribuzione massimo notifica file**: hello numero di volte in cui l'IoT Hub tentativi toodeliver una notifica di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="23112-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="23112-145">Too10 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="23112-145">Set too10 by default.</span></span>

<span data-ttu-id="23112-146">Usare l'hub IoT seguendo le impostazioni di caricamento file hello tooconfigure cmdlet PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="23112-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="23112-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23112-147">Next steps</span></span>

<span data-ttu-id="23112-148">Per ulteriori informazioni sulle funzionalità di caricamento file hello dell'IoT Hub, vedere [caricare i file da un dispositivo][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="23112-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="23112-149">Seguire questi toolearn collegamenti ulteriori informazioni sulla gestione di Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="23112-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="23112-150">[Gestire in blocco i dispositivi IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="23112-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="23112-151">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="23112-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="23112-152">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="23112-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="23112-153">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="23112-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="23112-154">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="23112-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="23112-155">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="23112-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="23112-156">[Soluzione IoT da hello la messa a terra sicura][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="23112-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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