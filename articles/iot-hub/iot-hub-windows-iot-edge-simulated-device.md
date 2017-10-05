---
title: Simulare un dispositivo con Azure IoT Edge (Windows) | Microsoft Docs
description: Come usare Azure IoT Edge in Windows per creare un dispositivo simulato che invia dati di telemetria attraverso un gateway Azure IoT Edge a un hub IoT.
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
ms.openlocfilehash: e7eb2931993daf3f0aecbd4a43d27ebd5adc10b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-iot-edge-to-send-device-to-cloud-messages-with-a-simulated-device-windows"></a><span data-ttu-id="3a608-103">Usare Azure IoT Edge per inviare messaggi da dispositivo a cloud con un dispositivo simulato (Windows)</span><span class="sxs-lookup"><span data-stu-id="3a608-103">Use Azure IoT Edge to send device-to-cloud messages with a simulated device (Windows)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="3a608-104">Per eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="3a608-104">How to run the sample</span></span>

<span data-ttu-id="3a608-105">Lo script **build.cmd** genera l'output nella cartella **build** nella copia locale dell'archivio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3a608-105">The **build.cmd** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="3a608-106">Questo output include i quattro moduli di IoT Edge usati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="3a608-106">This output includes the four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="3a608-107">Le posizioni dello script di compilazione sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a608-107">The build script places the:</span></span>

* <span data-ttu-id="3a608-108">**logger.dll** nella cartella **build\\modules\\logger\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3a608-108">**logger.dll** in the **build\\modules\\logger\\Debug** folder.</span></span>
* <span data-ttu-id="3a608-109">**iothub.dll** nella cartella **build\\modules\\iothub\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3a608-109">**iothub.dll** in the **build\\modules\\iothub\\Debug** folder.</span></span>
* <span data-ttu-id="3a608-110">**identity\_map.dll** nella cartella **build\\modules\\identitymap\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3a608-110">**identity\_map.dll** in the **build\\modules\\identitymap\\Debug** folder.</span></span>
* <span data-ttu-id="3a608-111">**simulated\_device.dll** nella cartella **build\\modules\\simulated\_device\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3a608-111">**simulated\_device.dll** in the **build\\modules\\simulated\_device\\Debug** folder.</span></span>

<span data-ttu-id="3a608-112">Usare questi percorsi per i valori **module path**, come illustrato nel file di impostazioni JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="3a608-112">Use these paths for the **module path** values as shown in the following JSON settings file:</span></span>

<span data-ttu-id="3a608-113">Il processo simulated\_device\_cloud\_upload\_sample accetta il percorso di un file di configurazione JSON come argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="3a608-113">The simulated\_device\_cloud\_upload\_sample process takes the path to a JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="3a608-114">Il file JSON di esempio seguente è disponibile nell'archivio SDK in **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="3a608-114">The following example JSON file is provided in the SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_win.json**.</span></span> <span data-ttu-id="3a608-115">Questo file di configurazione funziona così com'è, a meno che non si modifichi lo script di compilazione per inserire moduli di IoT Edge o file eseguibili di esempio in percorsi non predefiniti.</span><span class="sxs-lookup"><span data-stu-id="3a608-115">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="3a608-116">I percorsi dei moduli sono relativi alla directory in cui si trova il file simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="3a608-116">The module paths are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span> <span data-ttu-id="3a608-117">Per impostazione predefinita, il file di configurazione JSON di esempio prevede la scrittura del file "deviceCloudUploadGatewaylog.log" nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="3a608-117">The sample JSON configuration file defaults to writing to 'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="3a608-118">In un editor di testo aprire il file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** nella copia locale dell'archivio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3a608-118">In a text editor, open the file **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_win.json** in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="3a608-119">Questo file consente di configurare i moduli IoT Edge nel gateway di esempio:</span><span class="sxs-lookup"><span data-stu-id="3a608-119">This file configures the IoT Edge modules in the sample gateway:</span></span>

* <span data-ttu-id="3a608-120">Il modulo **IoTHub** si connette all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3a608-120">The **IoTHub** module connects to your IoT hub.</span></span> <span data-ttu-id="3a608-121">È necessario configurarlo per l'invio di dati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3a608-121">You configure it to send data to your IoT hub.</span></span> <span data-ttu-id="3a608-122">In particolare, impostare il valore di **IoTHubName** sul nome dell'hub IoT e impostare il valore di **IoTHubSuffix** su **azure-devices.net**.</span><span class="sxs-lookup"><span data-stu-id="3a608-122">Specifically, set the **IoTHubName** value to the name of your IoT hub and set the **IoTHubSuffix** value to **azure-devices.net**.</span></span> <span data-ttu-id="3a608-123">Impostare il valore **Transport** su **HTTP**, **AMQP** o **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="3a608-123">Set the **Transport** value to one of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="3a608-124">Attualmente, solo **HTTP** condivide una connessione TCP per tutti i messaggi del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3a608-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="3a608-125">Se si imposta il valore su **AMQP** o **MQTT**, il gateway mantiene una connessione TCP separata all'hub IoT per ogni dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3a608-125">If you set the value to **AMQP**, or **MQTT**, the gateway maintains a separate TCP connection to IoT Hub for each device.</span></span>
* <span data-ttu-id="3a608-126">Il modulo **mapping** esegue il mapping degli indirizzi MAC dei dispositivi simulati sugli ID dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3a608-126">The **mapping** module maps the MAC addresses of your simulated devices to your IoT Hub device ids.</span></span> <span data-ttu-id="3a608-127">Assicurarsi che i valori di **deviceId** corrispondano agli ID dei due dispositivi aggiunti all'hub IoT e che i valori di **deviceKey** contengano le chiavi dei due dispositivi.</span><span class="sxs-lookup"><span data-stu-id="3a608-127">Make sure that **deviceId** values match the ids of the two devices you added to your IoT hub, and that the **deviceKey** values contain the keys of your two devices.</span></span>
* <span data-ttu-id="3a608-128">I moduli **BLE1** e **BLE2** sono i dispositivi simulati.</span><span class="sxs-lookup"><span data-stu-id="3a608-128">The **BLE1** and **BLE2** modules are the simulated devices.</span></span> <span data-ttu-id="3a608-129">Si noti come gli indirizzi del modulo MAC corrispondono a quelli nel modulo **mapping**.</span><span class="sxs-lookup"><span data-stu-id="3a608-129">Note how the module MAC addresses match the addresses in the **mapping** module.</span></span>
* <span data-ttu-id="3a608-130">Il modulo **Logger** registra l'attività del gateway in un file.</span><span class="sxs-lookup"><span data-stu-id="3a608-130">The **Logger** module logs your gateway activity to a file.</span></span>
* <span data-ttu-id="3a608-131">I valori **module path** illustrati nell'esempio seguente sono relativi alla directory in cui si trova il file simulated\_device\_cloud\_upload\_sample.exe.</span><span class="sxs-lookup"><span data-stu-id="3a608-131">The **module path** values shown in the following example are relative to the directory where the simulated\_device\_cloud\_upload\_sample.exe is located.</span></span>
* <span data-ttu-id="3a608-132">La matrice **links** nella parte inferiore del file JSON connette i moduli **BLE1** e **BLE2** al modulo **mapping** e il modulo **mapping** al modulo **IoTHub**.</span><span class="sxs-lookup"><span data-stu-id="3a608-132">The **links** array at the bottom of the JSON file connects the **BLE1** and **BLE2** modules to the **mapping** module, and the **mapping** module to the **IoTHub** module.</span></span> <span data-ttu-id="3a608-133">Inoltre, la matrice garantisce la registrazione di tutti i messaggi da parte del modulo **Logger** .</span><span class="sxs-lookup"><span data-stu-id="3a608-133">It also ensures that all messages are logged by the **Logger** module.</span></span>

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

<span data-ttu-id="3a608-134">Salvare le modifiche apportate al file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a608-134">Save the changes you made to the configuration file.</span></span>

<span data-ttu-id="3a608-135">Per eseguire l'esempio:</span><span class="sxs-lookup"><span data-stu-id="3a608-135">To run the sample:</span></span>

1. <span data-ttu-id="3a608-136">Al prompt dei comandi accedere alla cartella **build** della copia locale dell'archivio **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="3a608-136">At a command prompt, navigate to the **build** folder in your local copy of the **iot-edge** repository.</span></span>
2. <span data-ttu-id="3a608-137">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3a608-137">Run the following command:</span></span>
   
    ```cmd
    samples\simulated_device_cloud_upload\Debug\simulated_device_cloud_upload_sample.exe ..\samples\simulated_device_cloud_upload\src\simulated_device_cloud_upload_win.json
    ```
3. <span data-ttu-id="3a608-138">È possibile usare lo strumento [Esplora dispositivi][lnk-device-explorer] o [iothub-explorer][lnk-iothub-explorer] per monitorare i messaggi che l'hub IoT riceve dal gateway.</span><span class="sxs-lookup"><span data-stu-id="3a608-138">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to monitor the messages that IoT hub receives from the gateway.</span></span> <span data-ttu-id="3a608-139">Ad esempio, tramite iothub-explorer è possibile monitorare i messaggi da dispositivo a cloud usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3a608-139">For example, using iothub-explorer you can monitor device-to-cloud messages using the following command:</span></span>

    ```cmd
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="3a608-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a608-140">Next steps</span></span>

<span data-ttu-id="3a608-141">Per ottenere informazioni più avanzate su IoT Edge e provare alcuni esempi di codice, vedere le risorse e le esercitazioni per gli sviluppatori elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="3a608-141">To gain a more advanced understanding of IoT Edge and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="3a608-142">[Inviare messaggi da dispositivo a cloud da un dispositivo fisico con IoT Edge][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="3a608-142">[Send device-to-cloud messages from a physical device with IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="3a608-143">[Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="3a608-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="3a608-144">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="3a608-144">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3a608-145">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3a608-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3a608-146">[Proteggere la soluzione IoT sin dall'inizio][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="3a608-146">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md