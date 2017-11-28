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
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="143b0-103">Utilizzare i messaggi da dispositivo a cloud di Azure IoT Edge toosend con un dispositivo simulato (Windows)</span><span class="sxs-lookup"><span data-stu-id="143b0-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="143b0-104">Come toorun hello esempio</span><span class="sxs-lookup"><span data-stu-id="143b0-104">How toorun hello sample</span></span>

<span data-ttu-id="143b0-105">Hello **build.cmd** script genera l'output di hello **compilare** cartella nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="143b0-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="143b0-106">Questo output include hello quattro IoT Edge moduli utilizzati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="143b0-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="143b0-107">Hello posizioni di script di compilazione di:</span><span class="sxs-lookup"><span data-stu-id="143b0-107">hello build script places the:</span></span>

* <span data-ttu-id="143b0-108">**logger.dll** in hello **compilare\\moduli\\logger\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="143b0-108">**logger.dll** in hello **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="143b0-109">**iothub.dll** in hello **compilare\\moduli\\l'hub IOT\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="143b0-109">**iothub.dll** in hello **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="143b0-110">**identità\_map.dll** in hello **compilare\\moduli\\identitymap\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="143b0-110">**identity\_map.dll** in hello **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="143b0-111">**simulato\_device.dll** in hello **compilare\\moduli\\simulato\_dispositivo\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="143b0-111">**simulated\_device.dll** in hello **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="143b0-112">Usare questi percorsi per hello **percorso modulo** valori come illustrato nel seguente file di impostazioni JSON hello:</span><span class="sxs-lookup"><span data-stu-id="143b0-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="143b0-113">Hello simulato\_dispositivo\_cloud\_caricare\_esempio dura hello percorso tooa file di configurazione JSON come argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="143b0-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="143b0-114">Hello file JSON di esempio seguente viene fornito nel repository SDK hello in **esempi\\simulato\_dispositivo\_cloud\_caricare\_esempio\\src\\ simulato\_dispositivo\_cloud\_caricare\_esempio\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="143b0-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="143b0-115">Questo funzionamento di file della configurazione come se non si modifica hello compilare hello tooplace script IoT Edge moduli o file eseguibili presenti in percorsi non predefiniti di esempio.</span><span class="sxs-lookup"><span data-stu-id="143b0-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="143b0-116">percorsi dei moduli Hello sono directory toohello relativo in cui hello simulato\_dispositivo\_cloud\_caricare\_sample.exe si trova.</span><span class="sxs-lookup"><span data-stu-id="143b0-116">hello module paths are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="143b0-117">file di configurazione JSON di esempio Hello predefinite toowriting too'deviceCloudUploadGatewaylog.log' nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="143b0-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="143b0-118">In un editor di testo aprire il file hello **esempi\\simulato\_dispositivo\_cloud\_caricare\_esempio\\src\\simulato\_dispositivo \_cloud\_caricare\_win.json** nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="143b0-118">In a text editor, open hello file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="143b0-119">Questo file consente di configurare i moduli di Edge IoT hello nel gateway di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="143b0-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="143b0-120">Hello **l'hub IOT** modulo si connette tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="143b0-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="143b0-121">Si configura l'hub IoT tooyour dati toosend.</span><span class="sxs-lookup"><span data-stu-id="143b0-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="143b0-122">In particolare, il set di hello **IoTHubName** valore toohello nome dell'hub IoT e impostare hello **IoTHubSuffix** valore troppo**azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="143b0-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="143b0-123">Set hello **trasporto** tooone valore di: **HTTP**, **AMQP**, o **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="143b0-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="143b0-124">Attualmente, solo **HTTP** condivide una connessione TCP per tutti i messaggi del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="143b0-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="143b0-125">Se si imposta il valore di hello troppo**AMQP**, o **MQTT**, gateway hello mantiene un tooIoT di connessione TCP di separato Hub per ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="143b0-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="143b0-126">Hello **mapping** modulo esegue il mapping di indirizzi MAC hello ID dispositivo simulato dispositivi tooyour Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="143b0-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="143b0-127">Assicurarsi che **deviceId** valori corrispondenza hello ID di hello due dispositivi di aver aggiunto l'hub IoT tooyour e tale hello **deviceKey** valori contengono chiavi hello i due dispositivi.</span><span class="sxs-lookup"><span data-stu-id="143b0-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="143b0-128">Hello **BLE1** e **BLE2** moduli sono dispositivi hello simulato.</span><span class="sxs-lookup"><span data-stu-id="143b0-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="143b0-129">Si noti come gli indirizzi MAC di modulo hello corrispondono agli indirizzi di hello in hello **mapping** modulo.</span><span class="sxs-lookup"><span data-stu-id="143b0-129">Note how hello module MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="143b0-130">Hello **Logger** modulo Registra il file di tooa attività gateway.</span><span class="sxs-lookup"><span data-stu-id="143b0-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="143b0-131">Hello **percorso modulo** valori illustrati nell'esempio seguente hello sono directory toohello relativo in cui hello simulato\_dispositivo\_cloud\_caricare\_sample.exe si trova.</span><span class="sxs-lookup"><span data-stu-id="143b0-131">hello **module path** values shown in hello following example are relative toohello directory where hello simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="143b0-132">Hello **collegamenti** matrice nella parte inferiore di hello del file JSON hello si connette hello **BLE1** e **BLE2** moduli toohello **mapping** modulo e hello **mapping** modulo toohello **l'hub IOT** modulo.</span><span class="sxs-lookup"><span data-stu-id="143b0-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="143b0-133">Garantisce inoltre che tutti i messaggi vengono registrati da hello **Logger** modulo.</span><span class="sxs-lookup"><span data-stu-id="143b0-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="143b0-134">Salvare le modifiche apportate hello apportate toohello file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="143b0-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="143b0-135">esempio hello toorun:</span><span class="sxs-lookup"><span data-stu-id="143b0-135">toorun hello sample:</span></span>

1. <span data-ttu-id="143b0-136">Al prompt dei comandi, passare toohello **compilare** cartella nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="143b0-136">At a command prompt, navigate toohello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
2. <span data-ttu-id="143b0-137">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="143b0-137">Run hello following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="143b0-138">È possibile utilizzare hello [Esplora dispositivo] [ lnk-device-explorer] o [l'hub IOT Esplora] [ lnk-iothub-explorer] strumento messaggi hello toomonitor che riceve l'hub IoT da hello gateway.</span><span class="sxs-lookup"><span data-stu-id="143b0-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="143b0-139">Ad esempio, tramite l'hub IOT explorer è possibile monitorare i messaggi da dispositivo a cloud utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="143b0-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="143b0-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="143b0-140">Next steps</span></span>

<span data-ttu-id="143b0-141">toogain conoscenze più avanzate di IoT Edge ed esperimento con alcuni esempi di codice, visitare hello esercitazioni per sviluppatori e risorse:</span><span class="sxs-lookup"><span data-stu-id="143b0-141">toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="143b0-142">[Inviare messaggi da dispositivo a cloud da un dispositivo fisico con IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="143b0-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="143b0-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="143b0-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="143b0-144">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="143b0-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="143b0-145">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="143b0-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="143b0-146">[Soluzione IoT da hello la messa a terra sicura][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="143b0-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md