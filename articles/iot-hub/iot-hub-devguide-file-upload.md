---
title: Informazioni sul caricamento di file dell'hub IoT di Azure | Microsoft Docs
description: "Guida per gli sviluppatori: usare la funzionalità di caricamento di file dell'hub IoT per gestire il caricamento di file da un dispositivo a un contenitore BLOB di archiviazione di Azure."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="11465-103">Caricare file con l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="11465-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="11465-104">Come descritto nell'articolo [IoT Hub endpoints][lnk-endpoints] (Endpoint dell'hub IoT), un dispositivo può avviare il caricamento di un file inviando una notifica tramite un endpoint per il dispositivo (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="11465-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="11465-105">Quando un dispositivo notifica all'hub IoT il completamento di un caricamento, l'hub IoT invia un messaggio di notifica per il caricamento del file tramite l'endpoint per il servizio (**/messages/servicebound/filenotifications**).</span><span class="sxs-lookup"><span data-stu-id="11465-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="11465-106">I messaggi non vengono negoziati tramite l'hub IoT, che funge invece da strumento di recapito per un account di archiviazione di Azure associato.</span><span class="sxs-lookup"><span data-stu-id="11465-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="11465-107">Un dispositivo richiede dall'hub IoT un token di archiviazione specifico del file che intende caricare.</span><span class="sxs-lookup"><span data-stu-id="11465-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="11465-108">Il dispositivo usa l'URI di firma di accesso condiviso per caricare il file nella risorsa di archiviazione e al termine del caricamento invia una notifica di completamento all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11465-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="11465-109">L'hub IoT verifica che il completamento del file sia stato completato e quindi aggiunge un messaggio di notifica di caricamento file all'endpoint per il servizio per le notifiche relative ai file.</span><span class="sxs-lookup"><span data-stu-id="11465-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="11465-110">Prima di caricare un file in un hub IoT da un dispositivo, è necessario configurare l'hub [associando un account di archiviazione di Azure][lnk-associate-storage] all'hub.</span><span class="sxs-lookup"><span data-stu-id="11465-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="11465-111">Il dispositivo può quindi [inizializzare un'operazione di caricamento][lnk-initialize] e quindi [Inviare una notifica all'hub IoT][lnk-notify] al termine del caricamento.</span><span class="sxs-lookup"><span data-stu-id="11465-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="11465-112">Facoltativamente, quando un dispositivo comunica all'hub IoT che il caricamento è completo, il servizio può generare un [messaggio di notifica][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="11465-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="11465-113">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="11465-113">When to use</span></span>

<span data-ttu-id="11465-114">Usare il caricamento di file per inviare file multimediali e batch di telemetria di grandi dimensioni caricati da dispositivi con connessione intermittente o compressi per risparmiare la larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="11465-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="11465-115">Vedere [Device-to-cloud communication guidance][lnk-d2c-guidance] (Indicazioni sulla comunicazione da dispositivo a cloud) in caso di dubbi tra l'uso delle proprietà indicate, dei messaggi da dispositivo a cloud o del caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="11465-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="11465-116">Associare un account di archiviazione di Azure all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="11465-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="11465-117">Per usare la funzionalità di caricamento file, è prima necessario collegare un account di archiviazione di Azure all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11465-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="11465-118">Questa attività può essere completata nel [portale di Azure][lnk-management-portal] oppure a livello di codice con le [API REST del provider di risorse dell'hub IoT][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="11465-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="11465-119">Dopo l'associazione di un account di archiviazione di Azure all'hub IoT, quando un dispositivo avvia una richiesta di caricamento file il servizio restituisce al dispositivo un URI di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="11465-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="11465-120">Gli [Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure) gestiscono automaticamente il recupero dell'URI di firma di accesso condiviso, il caricamento del file e la notifica all'hub IoT del completamento del caricamento.</span><span class="sxs-lookup"><span data-stu-id="11465-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="11465-121">Inizializzazione del caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="11465-121">Initialize a file upload</span></span>
<span data-ttu-id="11465-122">L'hub IoT dispone di un endpoint dedicato in modo specifico ai dispositivi che consente di richiedere un URI di firma di accesso condiviso con cui l'archiviazione possa caricare un file.</span><span class="sxs-lookup"><span data-stu-id="11465-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="11465-123">Per avviare il processo di caricamento del file, il dispositivo invia una richiesta POST a `{iot hub}.azure-devices.net/devices/{deviceId}/files` con il corpo JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="11465-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="11465-124">L'hub IoT restituisce i dati seguenti, usati dal dispositivo per caricare il file:</span><span class="sxs-lookup"><span data-stu-id="11465-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="11465-125">Obsoleto: inizializzare un caricamento di file con un'operazione GET</span><span class="sxs-lookup"><span data-stu-id="11465-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="11465-126">In questa sezione viene descritta la funzionalità obsoleta per indicazioni su come ricevere un URI di firma di accesso condiviso dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11465-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="11465-127">Usare il metodo POST descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="11465-127">Use the POST method described previously.</span></span>

<span data-ttu-id="11465-128">Per supportare il caricamento di file, l'hub IoT usa due endpoint REST: uno per ottenere l'URI di firma di accesso condiviso per l'archiviazione e uno per la notifica all'hub IoT del completamento del caricamento.</span><span class="sxs-lookup"><span data-stu-id="11465-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="11465-129">Il dispositivo avvia il processo di caricamento file inviato una richiesta GET all'hub IoT in `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="11465-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="11465-130">L'hub IoT restituisce:</span><span class="sxs-lookup"><span data-stu-id="11465-130">The IoT hub returns:</span></span>

* <span data-ttu-id="11465-131">Un URI SAS specifico per il file da caricare.</span><span class="sxs-lookup"><span data-stu-id="11465-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="11465-132">Un ID di correlazione da utilizzare dopo il completamento del caricamento.</span><span class="sxs-lookup"><span data-stu-id="11465-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="11465-133">Notifica all'hub IoT del completamento del caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="11465-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="11465-134">Il dispositivo è responsabile del caricamento del file nella risorsa di archiviazione con Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="11465-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="11465-135">Al termine del caricamento, il dispositivo invia una richiesta POST a `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con il corpo JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="11465-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="11465-136">Il valore di `isSuccess` è un valore booleano che indica se il file è stato caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="11465-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="11465-137">Il codice di stato per `statusCode` è lo stato per il caricamento del file nell'archiviazione e `statusDescription` corrisponde a `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="11465-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="11465-138">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="11465-138">Reference topics:</span></span>

<span data-ttu-id="11465-139">Negli argomenti di riferimento seguenti vengono offerte altre informazioni sul caricamento dei file da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="11465-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="11465-140">Notifiche di caricamento file</span><span class="sxs-lookup"><span data-stu-id="11465-140">File upload notifications</span></span>

<span data-ttu-id="11465-141">Facoltativamente, quando un dispositivo notifica all'hub IoT il completamento di un caricamento, il servizio può generare un messaggio di notifica contenente il nome e la posizione di archiviazione del file.</span><span class="sxs-lookup"><span data-stu-id="11465-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="11465-142">Come illustrato nella sezione [Endpoint][lnk-endpoints], , l'hub IoT recapita le notifiche di caricamento file sotto forma di messaggi tramite un endpoint per servizio (**/messages/servicebound/fileuploadnotifications**).</span><span class="sxs-lookup"><span data-stu-id="11465-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="11465-143">La semantica di ricezione per le notifiche di caricamento file è uguale a quella dei messaggi da cloud a dispositivo e ha lo stesso [ciclo di vita dei messaggi][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="11465-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="11465-144">Ogni messaggio recuperato dall'endpoint delle notifiche di caricamento file è un record JSON con le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="11465-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="11465-145">Proprietà</span><span class="sxs-lookup"><span data-stu-id="11465-145">Property</span></span> | <span data-ttu-id="11465-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="11465-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11465-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="11465-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="11465-148">Timestamp che indica quando è stata creata la notifica.</span><span class="sxs-lookup"><span data-stu-id="11465-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="11465-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="11465-149">DeviceId</span></span> |<span data-ttu-id="11465-150">**DeviceId** del dispositivo che ha caricato il file.</span><span class="sxs-lookup"><span data-stu-id="11465-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="11465-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="11465-151">BlobUri</span></span> |<span data-ttu-id="11465-152">URI del file caricato.</span><span class="sxs-lookup"><span data-stu-id="11465-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="11465-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="11465-153">BlobName</span></span> |<span data-ttu-id="11465-154">Nome del file caricato.</span><span class="sxs-lookup"><span data-stu-id="11465-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="11465-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="11465-155">LastUpdatedTime</span></span> |<span data-ttu-id="11465-156">Timestamp che indica quando è stato eseguito l'ultimo aggiornamento del file.</span><span class="sxs-lookup"><span data-stu-id="11465-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="11465-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="11465-157">BlobSizeInBytes</span></span> |<span data-ttu-id="11465-158">Dimensioni del file caricato.</span><span class="sxs-lookup"><span data-stu-id="11465-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="11465-159">**Esempio**.</span><span class="sxs-lookup"><span data-stu-id="11465-159">**Example**.</span></span> <span data-ttu-id="11465-160">Questo esempio illustra il corpo di un messaggio di notifica di caricamento di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="11465-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="11465-161">Opzioni di configurazione per le notifiche di caricamento file</span><span class="sxs-lookup"><span data-stu-id="11465-161">File upload notification configuration options</span></span>

<span data-ttu-id="11465-162">Ogni hub IoT espone le opzioni di configurazione seguenti per le notifiche di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="11465-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="11465-163">Proprietà</span><span class="sxs-lookup"><span data-stu-id="11465-163">Property</span></span> | <span data-ttu-id="11465-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="11465-164">Description</span></span> | <span data-ttu-id="11465-165">Intervallo e valore predefinito</span><span class="sxs-lookup"><span data-stu-id="11465-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11465-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="11465-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="11465-167">Controlla se verranno scritte notifiche di caricamento file nell'endpoint per le notifiche relative ai file.</span><span class="sxs-lookup"><span data-stu-id="11465-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="11465-168">Valore booleano.</span><span class="sxs-lookup"><span data-stu-id="11465-168">Bool.</span></span> <span data-ttu-id="11465-169">Predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="11465-169">Default: True.</span></span> |
| <span data-ttu-id="11465-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="11465-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="11465-171">Durata (TTL) predefinita per le notifiche di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="11465-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="11465-172">Intervallo ISO_8601 fino a 48 ore (minimo 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="11465-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="11465-173">Predefinito: 1 ora.</span><span class="sxs-lookup"><span data-stu-id="11465-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="11465-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="11465-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="11465-175">Durata del blocco per la coda delle notifiche di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="11465-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="11465-176">Da 5 a 300 secondi (minimo 5 secondi).</span><span class="sxs-lookup"><span data-stu-id="11465-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="11465-177">Predefinito: 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="11465-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="11465-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="11465-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="11465-179">Numero massimo di recapiti per la coda delle notifiche di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="11465-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="11465-180">Da 1 a 100.</span><span class="sxs-lookup"><span data-stu-id="11465-180">1 to 100.</span></span> <span data-ttu-id="11465-181">Predefinito: 100.</span><span class="sxs-lookup"><span data-stu-id="11465-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="11465-182">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="11465-182">Additional reference material</span></span>

<span data-ttu-id="11465-183">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="11465-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="11465-184">[Endpoint dell'hub IoT][lnk-endpoints] illustra i diversi endpoint esposti da ogni hub IoT per operazioni della fase di esecuzione e di gestione.</span><span class="sxs-lookup"><span data-stu-id="11465-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="11465-185">[Quote e limitazioni][lnk-quotas] descrive le quote e i comportamenti di limitazione applicabili al servizio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11465-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="11465-186">[Azure IoT SDK per dispositivi e servizi][lnk-sdks] elenca gli SDK nei diversi linguaggi che è possibile usare quando si sviluppano app per dispositivi e servizi che interagiscono con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="11465-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="11465-187">[Linguaggio di query dell'hub IoT][lnk-query] descrive il linguaggio di query che è possibile usare per recuperare informazioni dall'hub IoT sui dispositivi gemelli e sui processi.</span><span class="sxs-lookup"><span data-stu-id="11465-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="11465-188">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt] offre altre informazioni sul supporto dell'hub IoT per il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="11465-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11465-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11465-189">Next steps</span></span>

<span data-ttu-id="11465-190">In questa esercitazione si è appreso come caricare i file dai dispositivi con l'hub IoT. Altri argomenti di interesse reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="11465-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="11465-191">[Gestire le identità dei dispositivi nell'hub IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="11465-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="11465-192">[Controllare l'accesso all'hub IoT][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="11465-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="11465-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins] (Usare dispositivi gemelli per sincronizzare lo stato e le configurazioni)</span><span class="sxs-lookup"><span data-stu-id="11465-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="11465-194">[Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="11465-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="11465-195">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="11465-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="11465-196">Per provare alcuni dei concetti descritti in questo articolo, può essere utile l'esercitazione seguente sull'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="11465-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="11465-197">[Come caricare file dai dispositivi al cloud con l'hub IoT][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="11465-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
