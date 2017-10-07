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
# <a name="upload-files-with-iot-hub"></a>Caricare file con l'hub IoT

Come descritto in hello [gli endpoint IoT Hub] [ lnk-endpoints] articolo, un dispositivo può avviare un caricamento di file inviando una notifica tramite un endpoint che utilizzano il dispositivo (**/devices/ {deviceId} / file**). Quando un dispositivo notifica IoT Hub che è stata completata un'operazione di caricamento, l'IoT Hub invia un messaggio di notifica di caricamento di file tramite hello **/messages/servicebound/filenotifications** endpoint servizio Web.

Anziché la mediazione dei messaggi tramite l'IoT Hub stesso, l'IoT Hub invece funge tooan un dispatcher associato l'account di archiviazione di Azure. Un dispositivo richiede un token di archiviazione dall'IoT Hub che è specifico di toohello file hello intende tooupload. dispositivo Hello utilizza URI SAS tooupload hello file toostorage hello e una volta completato il caricamento di hello dispositivo hello invia una notifica di completamento tooIoT Hub. IoT Hub controlla il caricamento di file hello è stato completato e quindi aggiunge un file caricamento notifica messaggio toohello orientati ai servizi file endpoint di notifica.

Prima di caricare un file tooIoT Hub, da un dispositivo, è necessario configurare l'hub da [associazione di una risorsa di archiviazione di Azure] [ lnk-associate-storage] tooit dell'account.

Il dispositivo può quindi [inizializzare un'operazione di caricamento] [ lnk-initialize] e quindi [notificare hub IoT] [ lnk-notify] quando viene completato il caricamento di hello. Facoltativamente, quando un dispositivo notifica IoT Hub caricamento hello è stato completato, il servizio hello può generare un [messaggio di notifica][lnk-service-notification].

### <a name="when-toouse"></a>Quando toouse

Utilizzare i file multimediali toosend caricamento di file e i batch di telemetria di grandi dimensioni caricato da dispositivi connessi in modo intermittente o la larghezza di banda toosave compresso.

Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] se in dubbio tra l'utilizzo di proprietà restituita, i messaggi da dispositivo a cloud o caricamento del file.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Associare un account di archiviazione di Azure all'hub IoT

la funzionalità di caricamento file hello toouse, è innanzitutto necessario collegare un toohello di account di archiviazione di Azure IoT Hub. È possibile completare questa attività tramite hello [portale di Azure][lnk-management-portal], o a livello di programmazione tramite hello [il provider di risorse IoT Hub API REST] [ lnk-resource-provider-apis]. Dopo aver associato un account di archiviazione di Azure con l'IoT Hub, hello servizio restituisce un URI SAS tooa dispositivo quando il dispositivo hello avvia una richiesta di caricamento file.

> [!NOTE]
> Hello [Azure IoT SDK] [ lnk-sdks] automaticamente il recupero di handle hello URI SAS, caricamento file hello e notifica l'IoT Hub di un caricamento completato.


## <a name="initialize-a-file-upload"></a>Inizializzazione del caricamento di un file
IoT Hub è un endpoint in modo specifico per i dispositivi toorequest un URI SAS per tooupload archiviazione un file. processo di caricamento file hello tooinitiate, hello dispositivo invia una richiesta POST troppo`{iot hub}.azure-devices.net/devices/{deviceId}/files` con hello corpo JSON seguente:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IoT Hub restituisce hello dati, quale dispositivo hello utilizza file hello tooupload seguenti:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Obsoleto: inizializzare un caricamento di file con un'operazione GET

> [!NOTE]
> Questa sezione vengono descritte le funzionalità deprecate come tooreceive un URI SAS dall'IoT Hub. Metodo POST hello descritto in precedenza.

IoT Hub ha due file di toosupport endpoint REST caricare uno tooget hello URI SAS per l'archiviazione e hello altri hub IoT di hello toonotify di un caricamento completato. Hello dispositivo avvia il processo di caricamento di hello file mediante l'invio di un hub IoT di toohello GET in `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. hub IoT Hello restituisce:

* URI SAS toohello specifici file toobe caricato.
* Toobe un ID di correlazione utilizzato una volta completato il caricamento di hello.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>Notifica all'hub IoT del completamento del caricamento di un file

dispositivo Hello è responsabile per il caricamento toostorage file hello tramite hello Azure Storage SDK. Una volta completato il caricamento di hello, dispositivo hello invia una richiesta POST troppo`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` con hello corpo JSON seguente:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

valore di Hello `isSuccess` è un valore Boolean che indica se il file hello è stato caricato correttamente. codice di stato per Hello `statusCode` è lo stato di caricamento hello del toostorage file hello hello e hello `statusDescription` corrisponde toohello `statusCode`.

## <a name="reference-topics"></a>Argomenti di riferimento:

Hello argomenti di riferimento seguenti offrono ulteriori informazioni sul caricamento di file da un dispositivo.

## <a name="file-upload-notifications"></a>Notifiche di caricamento file

Facoltativamente, quando un dispositivo notifica IoT Hub che è stata completata un'operazione di caricamento, l'IoT Hub può generare un messaggio di notifica che contiene hello percorso di archiviazione e nome del file hello.

Come illustrato nella sezione [Endpoint][lnk-endpoints], , l'hub IoT recapita le notifiche di caricamento file sotto forma di messaggi tramite un endpoint per servizio (**/messages/servicebound/fileuploadnotifications**). semantica di ricezione Hello per le notifiche di caricamento di file sono hello uguale a quello di messaggi da cloud a dispositivo e avere hello stesso [ciclo di vita del messaggio][lnk-lifecycle]. Ogni messaggio recuperato dall'endpoint di notifica di caricamento file hello è un record JSON con hello le proprietà seguenti:

| Proprietà | Descrizione |
| --- | --- |
| EnqueuedTimeUtc |Timestamp che indica quando è stata creata la notifica hello. |
| deviceId |**DeviceId** del dispositivo hello cui caricamento file hello. |
| BlobUri |URI del file hello caricato. |
| BlobName |Nome di hello caricamento file. |
| LastUpdatedTime |Timestamp che indica quando ultimo aggiornamento del file hello. |
| BlobSizeInBytes |Dimensioni di hello caricamento file. |

**Esempio**. Questo esempio viene illustrato come caricare di corpo hello di un file di messaggio di notifica.

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

## <a name="file-upload-notification-configuration-options"></a>Opzioni di configurazione per le notifiche di caricamento file

Ogni hub IoT espone hello le opzioni di configurazione per le notifiche di caricamento di file seguenti:

| Proprietà | Descrizione | Intervallo e valore predefinito |
| --- | --- | --- |
| **enableFileUploadNotifications** |Controlla se le notifiche di caricamento di file vengono scritti endpoint delle notifiche di toohello file. |Valore booleano. Predefinito: True. |
| **fileNotifications.ttlAsIso8601** |Durata (TTL) predefinita per le notifiche di caricamento file. |Intervallo ISO_8601 backup too48H (minimo 1 minuto). Predefinito: 1 ora. |
| **fileNotifications.lockDuration** |Durata del blocco per la coda di notifiche di caricamento file hello. |too300 5 secondi (minimi 5 secondi). Predefinito: 60 secondi. |
| **fileNotifications.maxDeliveryCount** |Conteggio distribuzione massimo per il file hello caricare coda di notifica. |1 too100. Predefinito: 100. |

## <a name="additional-reference-material"></a>Materiale di riferimento

Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* [Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* [Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello e la limitazione di comportamenti che si applicano toohello servizio IoT Hub.
* [Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* [Il linguaggio di query di IoT Hub] [ lnk-query] descrive il linguaggio di query hello è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.
* [Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi

Ora si è appreso come tooupload file dai dispositivi gestiti mediante l'IoT Hub, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:

* [Gestire le identità dei dispositivi nell'hub IoT][lnk-devguide-identities]
* [Controllo accesso tooIoT Hub][lnk-devguide-security]
* [Utilizzare lo stato del dispositivo gemelli toosynchronize e configurazioni][lnk-devguide-device-twins]
* [Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:

* [File tooupload da dispositivi toohello di cloud con l'IoT Hub][lnk-fileupload-tutorial]

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
