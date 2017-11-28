---
title: caricamento del file aaaUnderstand IoT Hub di Azure | Documenti Microsoft
description: "Guida per sviluppatori - funzionalità di caricamento file hello uso di IoT Hub toomanage caricamento di file da un contenitore di blob di archiviazione Azure tooan dispositivo."
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="8ea90-103">Caricare file con l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8ea90-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="8ea90-104">Come descritto in hello [gli endpoint IoT Hub] [ lnk-endpoints] articolo, un dispositivo può avviare un caricamento di file inviando una notifica tramite un endpoint che utilizzano il dispositivo (**/devices/ {deviceId} / file**).</span><span class="sxs-lookup"><span data-stu-id="8ea90-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="8ea90-105">Quando un dispositivo notifica IoT Hub che è stata completata un'operazione di caricamento, l'IoT Hub invia un messaggio di notifica di caricamento di file tramite hello **/messages/servicebound/filenotifications** endpoint servizio Web.</span><span class="sxs-lookup"><span data-stu-id="8ea90-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="8ea90-106">Anziché la mediazione dei messaggi tramite l'IoT Hub stesso, l'IoT Hub invece funge tooan un dispatcher associato l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ea90-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="8ea90-107">Un dispositivo richiede un token di archiviazione dall'IoT Hub che è specifico di toohello file hello intende tooupload.</span><span class="sxs-lookup"><span data-stu-id="8ea90-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="8ea90-108">dispositivo Hello utilizza URI SAS tooupload hello file toostorage hello e una volta completato il caricamento di hello dispositivo hello invia una notifica di completamento tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ea90-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="8ea90-109">IoT Hub controlla il caricamento di file hello è stato completato e quindi aggiunge un file caricamento notifica messaggio toohello orientati ai servizi file endpoint di notifica.</span><span class="sxs-lookup"><span data-stu-id="8ea90-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="8ea90-110">Prima di caricare un file tooIoT Hub, da un dispositivo, è necessario configurare l'hub da [associazione di una risorsa di archiviazione di Azure] [ lnk-associate-storage] tooit dell'account.</span><span class="sxs-lookup"><span data-stu-id="8ea90-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="8ea90-111">Il dispositivo può quindi [inizializzare un'operazione di caricamento] [ lnk-initialize] e quindi [notificare hub IoT] [ lnk-notify] quando viene completato il caricamento di hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="8ea90-112">Facoltativamente, quando un dispositivo notifica IoT Hub caricamento hello è stato completato, il servizio hello può generare un [messaggio di notifica][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="8ea90-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="8ea90-113">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="8ea90-113">When toouse</span></span>

<span data-ttu-id="8ea90-114">Utilizzare i file multimediali toosend caricamento di file e i batch di telemetria di grandi dimensioni caricato da dispositivi connessi in modo intermittente o la larghezza di banda toosave compresso.</span><span class="sxs-lookup"><span data-stu-id="8ea90-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="8ea90-115">Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] se in dubbio tra l'utilizzo di proprietà restituita, i messaggi da dispositivo a cloud o caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="8ea90-116">Associare un account di archiviazione di Azure all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8ea90-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="8ea90-117">la funzionalità di caricamento file hello toouse, è innanzitutto necessario collegare un toohello di account di archiviazione di Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ea90-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="8ea90-118">È possibile completare questa attività tramite hello [portale di Azure][lnk-management-portal], o a livello di programmazione tramite hello [il provider di risorse IoT Hub API REST] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="8ea90-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="8ea90-119">Dopo aver associato un account di archiviazione di Azure con l'IoT Hub, hello servizio restituisce un URI SAS tooa dispositivo quando il dispositivo hello avvia una richiesta di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea90-120">Hello [Azure IoT SDK] [ lnk-sdks] automaticamente il recupero di handle hello URI SAS, caricamento file hello e notifica l'IoT Hub di un caricamento completato.</span><span class="sxs-lookup"><span data-stu-id="8ea90-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="8ea90-121">Inizializzazione del caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="8ea90-121">Initialize a file upload</span></span>
<span data-ttu-id="8ea90-122">IoT Hub è un endpoint in modo specifico per i dispositivi toorequest un URI SAS per tooupload archiviazione un file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="8ea90-123">processo di caricamento file hello tooinitiate, hello dispositivo invia una richiesta POST troppo`{iot hub}.azure-devices.net/devices/{deviceId}/files` con hello corpo JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="8ea90-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="8ea90-124">IoT Hub restituisce hello dati, quale dispositivo hello utilizza file hello tooupload seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ea90-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="8ea90-125">Obsoleto: inizializzare un caricamento di file con un'operazione GET</span><span class="sxs-lookup"><span data-stu-id="8ea90-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="8ea90-126">Questa sezione vengono descritte le funzionalità deprecate come tooreceive un URI SAS dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ea90-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="8ea90-127">Metodo POST hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8ea90-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="8ea90-128">IoT Hub ha due file di toosupport endpoint REST caricare uno tooget hello URI SAS per l'archiviazione e hello altri hub IoT di hello toonotify di un caricamento completato.</span><span class="sxs-lookup"><span data-stu-id="8ea90-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="8ea90-129">Hello dispositivo avvia il processo di caricamento di hello file mediante l'invio di un hub IoT di toohello GET in `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="8ea90-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="8ea90-130">hub IoT Hello restituisce:</span><span class="sxs-lookup"><span data-stu-id="8ea90-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="8ea90-131">URI SAS toohello specifici file toobe caricato.</span><span class="sxs-lookup"><span data-stu-id="8ea90-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="8ea90-132">Toobe un ID di correlazione utilizzato una volta completato il caricamento di hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="8ea90-133">Notifica all'hub IoT del completamento del caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="8ea90-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="8ea90-134">dispositivo Hello è responsabile per il caricamento toostorage file hello tramite hello Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="8ea90-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="8ea90-135">Una volta completato il caricamento di hello, dispositivo hello invia una richiesta POST troppo`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con hello corpo JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="8ea90-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="8ea90-136">valore di Hello `isSuccess` è un valore Boolean che indica se il file hello è stato caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="8ea90-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="8ea90-137">codice di stato per Hello `statusCode` è lo stato di caricamento hello del toostorage file hello hello e hello `statusDescription` corrisponde toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="8ea90-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="8ea90-138">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="8ea90-138">Reference topics:</span></span>

<span data-ttu-id="8ea90-139">Hello argomenti di riferimento seguenti offrono ulteriori informazioni sul caricamento di file da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8ea90-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="8ea90-140">Notifiche di caricamento file</span><span class="sxs-lookup"><span data-stu-id="8ea90-140">File upload notifications</span></span>

<span data-ttu-id="8ea90-141">Facoltativamente, quando un dispositivo notifica IoT Hub che è stata completata un'operazione di caricamento, l'IoT Hub può generare un messaggio di notifica che contiene hello percorso di archiviazione e nome del file hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="8ea90-142">Come illustrato nella sezione [Endpoint][lnk-endpoints], , l'hub IoT recapita le notifiche di caricamento file sotto forma di messaggi tramite un endpoint per servizio (**/messages/servicebound/fileuploadnotifications**).</span><span class="sxs-lookup"><span data-stu-id="8ea90-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="8ea90-143">semantica di ricezione Hello per le notifiche di caricamento di file sono hello uguale a quello di messaggi da cloud a dispositivo e avere hello stesso [ciclo di vita del messaggio][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="8ea90-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="8ea90-144">Ogni messaggio recuperato dall'endpoint di notifica di caricamento file hello è un record JSON con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ea90-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="8ea90-145">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8ea90-145">Property</span></span> | <span data-ttu-id="8ea90-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ea90-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ea90-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="8ea90-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="8ea90-148">Timestamp che indica quando è stata creata la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="8ea90-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="8ea90-149">DeviceId</span></span> |<span data-ttu-id="8ea90-150">**DeviceId** del dispositivo hello cui caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="8ea90-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="8ea90-151">BlobUri</span></span> |<span data-ttu-id="8ea90-152">URI del file hello caricato.</span><span class="sxs-lookup"><span data-stu-id="8ea90-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="8ea90-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="8ea90-153">BlobName</span></span> |<span data-ttu-id="8ea90-154">Nome di hello caricamento file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="8ea90-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="8ea90-155">LastUpdatedTime</span></span> |<span data-ttu-id="8ea90-156">Timestamp che indica quando ultimo aggiornamento del file hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="8ea90-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="8ea90-157">BlobSizeInBytes</span></span> |<span data-ttu-id="8ea90-158">Dimensioni di hello caricamento file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="8ea90-159">**Esempio**.</span><span class="sxs-lookup"><span data-stu-id="8ea90-159">**Example**.</span></span> <span data-ttu-id="8ea90-160">Questo esempio viene illustrato come caricare di corpo hello di un file di messaggio di notifica.</span><span class="sxs-lookup"><span data-stu-id="8ea90-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="8ea90-161">Opzioni di configurazione per le notifiche di caricamento file</span><span class="sxs-lookup"><span data-stu-id="8ea90-161">File upload notification configuration options</span></span>

<span data-ttu-id="8ea90-162">Ogni hub IoT espone hello le opzioni di configurazione per le notifiche di caricamento di file seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ea90-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="8ea90-163">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8ea90-163">Property</span></span> | <span data-ttu-id="8ea90-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ea90-164">Description</span></span> | <span data-ttu-id="8ea90-165">Intervallo e valore predefinito</span><span class="sxs-lookup"><span data-stu-id="8ea90-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ea90-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="8ea90-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="8ea90-167">Controlla se le notifiche di caricamento di file vengono scritti endpoint delle notifiche di toohello file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="8ea90-168">Valore booleano.</span><span class="sxs-lookup"><span data-stu-id="8ea90-168">Bool.</span></span> <span data-ttu-id="8ea90-169">Predefinito: True.</span><span class="sxs-lookup"><span data-stu-id="8ea90-169">Default: True.</span></span> |
| <span data-ttu-id="8ea90-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="8ea90-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="8ea90-171">Durata (TTL) predefinita per le notifiche di caricamento file.</span><span class="sxs-lookup"><span data-stu-id="8ea90-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="8ea90-172">Intervallo ISO_8601 backup too48H (minimo 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="8ea90-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="8ea90-173">Predefinito: 1 ora.</span><span class="sxs-lookup"><span data-stu-id="8ea90-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="8ea90-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="8ea90-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="8ea90-175">Durata del blocco per la coda di notifiche di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="8ea90-176">too300 5 secondi (minimi 5 secondi).</span><span class="sxs-lookup"><span data-stu-id="8ea90-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="8ea90-177">Predefinito: 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="8ea90-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="8ea90-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="8ea90-179">Conteggio distribuzione massimo per il file hello caricare coda di notifica.</span><span class="sxs-lookup"><span data-stu-id="8ea90-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="8ea90-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="8ea90-180">1 too100.</span></span> <span data-ttu-id="8ea90-181">Predefinito: 100.</span><span class="sxs-lookup"><span data-stu-id="8ea90-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="8ea90-182">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="8ea90-182">Additional reference material</span></span>

<span data-ttu-id="8ea90-183">Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:</span><span class="sxs-lookup"><span data-stu-id="8ea90-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="8ea90-184">[Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.</span><span class="sxs-lookup"><span data-stu-id="8ea90-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="8ea90-185">[Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello e la limitazione di comportamenti che si applicano toohello servizio IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ea90-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="8ea90-186">[Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ea90-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="8ea90-187">[Il linguaggio di query di IoT Hub] [ lnk-query] descrive il linguaggio di query hello è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.</span><span class="sxs-lookup"><span data-stu-id="8ea90-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="8ea90-188">[Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="8ea90-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ea90-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ea90-189">Next steps</span></span>

<span data-ttu-id="8ea90-190">Ora si è appreso come tooupload file dai dispositivi gestiti mediante l'IoT Hub, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="8ea90-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="8ea90-191">[Gestire le identità dei dispositivi nell'hub IoT][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="8ea90-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="8ea90-192">[Controllo accesso tooIoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="8ea90-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="8ea90-193">[Utilizzare lo stato del dispositivo gemelli toosynchronize e configurazioni][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="8ea90-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="8ea90-194">[Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="8ea90-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="8ea90-195">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="8ea90-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="8ea90-196">Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="8ea90-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="8ea90-197">[File tooupload da dispositivi toohello di cloud con l'IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="8ea90-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
