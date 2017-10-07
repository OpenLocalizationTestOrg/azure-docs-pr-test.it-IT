---
title: aaaConnect un dispositivo utilizzando Node.js | Documenti Microsoft
description: Viene descritto come tooconnect toohello un dispositivo Azure IoT Suite preconfigurato soluzione di monitoraggio remoto utilizzando un'applicazione scritta in Node.js.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="aba1c-103">Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Node.js)</span><span class="sxs-lookup"><span data-stu-id="aba1c-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="aba1c-104">Creare una soluzione di esempio di Node.js</span><span class="sxs-lookup"><span data-stu-id="aba1c-104">Create a node.js sample solution</span></span>

<span data-ttu-id="aba1c-105">Verificare che nel computer di sviluppo sia installato Node.js 0.11.5 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="aba1c-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="aba1c-106">È possibile eseguire `node --version` alla versione di hello toocheck di hello riga di comando.</span><span class="sxs-lookup"><span data-stu-id="aba1c-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="aba1c-107">Nel computer di sviluppo creare una cartella denominata **RemoteMonitoring**.</span><span class="sxs-lookup"><span data-stu-id="aba1c-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="aba1c-108">Esplorazione delle cartelle toothis nell'ambiente della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="aba1c-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="aba1c-109">Esecuzione hello seguenti comandi toodownload e installare pacchetti hello necessari toocomplete hello app di esempio:</span><span class="sxs-lookup"><span data-stu-id="aba1c-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="aba1c-110">In hello **RemoteMonitoring** cartella, creare un file denominato **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="aba1c-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="aba1c-111">Aprire il file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="aba1c-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="aba1c-112">In hello **remote_monitoring.js** file, aggiungere il seguente hello `require` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="aba1c-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="aba1c-113">Aggiungere hello dopo le dichiarazioni delle variabili dopo hello `require` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="aba1c-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="aba1c-114">Sostituire i valori segnaposto hello [Id dispositivo] e [dispositivo Key] con i valori che si è preso nota per il dispositivo in hello remoto soluzione di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="aba1c-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="aba1c-115">Utilizzare hello Hostname Hub IoT da hello soluzione dashboard tooreplace [hub IOT Name].</span><span class="sxs-lookup"><span data-stu-id="aba1c-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="aba1c-116">Ad esempio, se il nome host dell'hub IoT è **contoso.azure-devices.net**, sostituire [Nome IoTHub] con **contoso**:</span><span class="sxs-lookup"><span data-stu-id="aba1c-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="aba1c-117">Aggiungere alcuni dati di telemetria di base di hello toodefine variabili seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba1c-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="aba1c-118">Aggiungere hello risultati dell'operazione tooprint funzione helper seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba1c-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="aba1c-119">Aggiungere hello i valori di dati di telemetria hello toorandomize toouse funzione helper seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba1c-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="aba1c-120">Aggiungere hello seguente definizione per hello **DeviceInfo** dispositivo hello oggetto invia all'avvio:</span><span class="sxs-lookup"><span data-stu-id="aba1c-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="aba1c-121">Aggiungere hello seguente definizione per un doppio dispositivo hello segnalati valori.</span><span class="sxs-lookup"><span data-stu-id="aba1c-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="aba1c-122">Questa definizione include le descrizioni dei metodi di hello diretti hello dispositivo supporta:</span><span class="sxs-lookup"><span data-stu-id="aba1c-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="aba1c-123">Aggiungere i seguenti hello toohandle funzione hello **riavviare** diretta chiamata al metodo:</span><span class="sxs-lookup"><span data-stu-id="aba1c-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="aba1c-124">Aggiungere i seguenti hello toohandle funzione hello **InitiateFirmwareUpdate** diretta chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="aba1c-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="aba1c-125">Questo metodo diretto utilizza un percorso di hello parametro toospecify di toodownload immagine di firmware hello e avvia hello in modo asincrono di aggiornamento del firmware sul dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="aba1c-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="aba1c-126">Aggiungere hello toocreate codice un'istanza del client seguenti:</span><span class="sxs-lookup"><span data-stu-id="aba1c-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="aba1c-127">Aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="aba1c-127">Add hello following code to:</span></span>

    * <span data-ttu-id="aba1c-128">Aprire la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="aba1c-128">Open hello connection.</span></span>
    * <span data-ttu-id="aba1c-129">Inviare hello **DeviceInfo** oggetto.</span><span class="sxs-lookup"><span data-stu-id="aba1c-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="aba1c-130">Impostare un gestore per le proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="aba1c-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="aba1c-131">Inviare le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="aba1c-131">Send reported properties.</span></span>
    * <span data-ttu-id="aba1c-132">Registra i gestori per i metodi di hello diretto.</span><span class="sxs-lookup"><span data-stu-id="aba1c-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="aba1c-133">Avviare l'invio dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="aba1c-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="aba1c-134">Salvare hello modifiche toohello **remote_monitoring.js** file.</span><span class="sxs-lookup"><span data-stu-id="aba1c-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="aba1c-135">Eseguire hello comando in un'applicazione di esempio hello toolaunch prompt dei comandi seguente:</span><span class="sxs-lookup"><span data-stu-id="aba1c-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
