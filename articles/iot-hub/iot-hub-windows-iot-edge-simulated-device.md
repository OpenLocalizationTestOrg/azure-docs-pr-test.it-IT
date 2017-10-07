---
title: un dispositivo con Azure IoT Edge (Windows) aaaSimulate | Documenti Microsoft
description: Come toouse Azure IoT Edge in Windows toocreate un dispositivo simulato che invia dati di telemetria attraverso un hub IoT di Azure IoT Edge gateway tooan.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 6a2aeda0-696a-4732-90e1-595d2e2fadc6
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: ddbe85eb956e9934e80e2e80e09f77b24cf54856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a>Utilizzare i messaggi da dispositivo a cloud di Azure IoT Edge toosend con un dispositivo simulato (Windows)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Come toorun hello esempio

Hello **build.cmd** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository. Questo output include hello quattro IoT Edge moduli utilizzati in questo esempio.

Hello posizioni di script di compilazione di:

* **logger.dll** in hello **compilare\\moduli\\logger\\Debug** cartella.
* **iothub.dll** in hello **compilare\\moduli\\l'hub IOT\\Debug** cartella.
* **identità\_map.dll** in hello **compilare\\moduli\\identitymap\\Debug** cartella.
* **simulato\_device.dll** in hello **compilare\\moduli\\simulato\_dispositivo\\Debug** cartella.

Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON hello:

Hello simulato\_dispositivo\_cloud\_caricare\_esempio dura hello percorso tooa file di configurazione JSON come argomento della riga di comando. Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi\\simulato\_dispositivo\_cloud\_caricare\_esempio\\src\\ simulato\_dispositivo\_cloud\_caricare\_esempio\_win.json**. Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.

> [!NOTE]
> percorsi dei moduli Hello sono directory toohello relativo in cui hello simulato\_dispositivo\_cloud\_caricare\_sample.exe si trova. file di configurazione JSON di esempio Hello predefinite toowriting too'deviceCloudUploadGatewaylog.log' nella directory di lavoro corrente.

In un editor di testo aprire il file hello **esempi\\simulato\_dispositivo\_cloud\_caricare\_esempio\\src\\simulato\_dispositivo \_cloud\_caricare\_win.json** nella copia locale di hello **iot edge** repository. Questo file consente di configurare i moduli di Edge IoT hello nel gateway di esempio hello:

* Hello **l'hub IOT** modulo si connette tooyour IoT hub. Si configura l'hub IoT tooyour dati toosend. In particolare, il set di hello **IoTHubName** valore toohello nome dell'hub IoT e impostare hello **IoTHubSuffix** valore troppo**azure devices.net**. Set hello **trasporto** tooone valore di: **HTTP**, **AMQP**, o **MQTT**. Attualmente, solo **HTTP** condivide una connessione TCP per tutti i messaggi del dispositivo. Se si imposta il valore di hello troppo**AMQP**, o **MQTT**, gateway hello mantiene un tooIoT di connessione TCP di separato Hub per ogni dispositivo.
* Hello **mapping** modulo esegue il mapping di indirizzi MAC hello ID dispositivo simulato dispositivi tooyour Hub IoT. Assicurarsi che **deviceId** valori corrispondenza hello ID di hello due dispositivi di aver aggiunto l'hub IoT tooyour e tale hello **deviceKey** valori contengono chiavi hello i due dispositivi.
* Hello **BLE1** e **BLE2** moduli sono dispositivi hello simulato. Si noti come gli indirizzi MAC di modulo hello corrispondono agli indirizzi di hello in hello **mapping** modulo.
* Hello **Logger** modulo Registra il file di tooa attività gateway.
* Hello **percorso modulo** valori illustrati nell'esempio seguente hello sono directory toohello relativo in cui hello simulato\_dispositivo\_cloud\_caricare\_sample.exe si trova.
* Hello **collegamenti** matrice nella parte inferiore di hello del file JSON hello si connette hello **BLE1** e **BLE2** moduli toohello **mapping** modulo e hello **mapping** modulo toohello **l'hub IOT** modulo. Garantisce inoltre che tutti i messaggi vengono registrati da hello **Logger** modulo.

```json
{
    "modules" :
    [
      {
        "name": "IotHub",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\iothub\\Debug\\iothub.dll"
          }
          },
          "args": {
            "IoTHubName": "<<insert here IoTHubName>>",
            "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
            "Transport": "HTTP"
          }
        },
      {
        "name": "mapping",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\identitymap\\Debug\\identity_map.dll"
          }
          },
          "args": [
            {
              "macAddress": "01:01:01:01:01:01",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            },
            {
              "macAddress": "02:02:02:02:02:02",
              "deviceId": "<<insert here deviceId>>",
              "deviceKey": "<<insert here deviceKey>>"
            }
          ]
        },
      {
        "name": "BLE1",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "01:01:01:01:01:01"
          }
        },
      {
        "name": "BLE2",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\simulated_device\\Debug\\simulated_device.dll"
          }
          },
          "args": {
            "macAddress": "02:02:02:02:02:02"
          }
        },
      {
        "name": "Logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
          }
        },
        "args": {
          "filename": "deviceCloudUploadGatewaylog.log"
        }
      }
    ],
    "links" : [
        { "source" : "*", "sink" : "Logger" },
        { "source" : "BLE1", "sink" : "mapping" },
        { "source" : "BLE2", "sink" : "mapping" },
        { "source" : "mapping", "sink" : "IotHub" }
    ]
}
```

Salvare le modifiche apportate hello apportate toohello file di configurazione.

esempio hello toorun:

1. Al prompt dei comandi, passare toohello **compilare** cartella nella copia locale di hello **iot edge** repository.
2. Eseguire hello comando seguente:
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. È possibile utilizzare hello [Esplora dispositivo] [ lnk-device-explorer] o [l'hub IOT Esplora] [ lnk-iothub-explorer] strumento messaggi hello toomonitor che riceve l'hub IoT da hello gateway. Ad esempio, tramite l'hub IOT explorer è possibile monitorare i messaggi da dispositivo a cloud utilizzando hello comando seguente:

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Passaggi successivi

toogain conoscenze più avanzate di IoT Edge ed esperimento con alcuni esempi di codice, visitare hello esercitazioni per sviluppatori e risorse:

* [Inviare messaggi da dispositivo a cloud da un dispositivo fisico con IoT Edge][lnk-physical-device]
* [Azure IoT Edge][lnk-iot-edge]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Soluzione IoT da hello la messa a terra sicura][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md