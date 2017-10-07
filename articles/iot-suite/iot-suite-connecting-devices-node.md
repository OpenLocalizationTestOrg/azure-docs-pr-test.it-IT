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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata (Node.js)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Creare una soluzione di esempio di Node.js

Verificare che nel computer di sviluppo sia installato Node.js 0.11.5 o versione successiva. È possibile eseguire `node --version` alla versione di hello toocheck di hello riga di comando.

1. Nel computer di sviluppo creare una cartella denominata **RemoteMonitoring**. Esplorazione delle cartelle toothis nell'ambiente della riga di comando.

1. Esecuzione hello seguenti comandi toodownload e installare pacchetti hello necessari toocomplete hello app di esempio:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. In hello **RemoteMonitoring** cartella, creare un file denominato **remote_monitoring.js**. Aprire il file in un editor di testo.

1. In hello **remote_monitoring.js** file, aggiungere il seguente hello `require` istruzioni:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Aggiungere hello dopo le dichiarazioni delle variabili dopo hello `require` istruzioni. Sostituire i valori segnaposto hello [Id dispositivo] e [dispositivo Key] con i valori che si è preso nota per il dispositivo in hello remoto soluzione di monitoraggio. Utilizzare hello Hostname Hub IoT da hello soluzione dashboard tooreplace [hub IOT Name]. Ad esempio, se il nome host dell'hub IoT è **contoso.azure-devices.net**, sostituire [Nome IoTHub] con **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Aggiungere alcuni dati di telemetria di base di hello toodefine variabili seguenti:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Aggiungere hello risultati dell'operazione tooprint funzione helper seguenti:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Aggiungere hello i valori di dati di telemetria hello toorandomize toouse funzione helper seguenti:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Aggiungere hello seguente definizione per hello **DeviceInfo** dispositivo hello oggetto invia all'avvio:

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

1. Aggiungere hello seguente definizione per un doppio dispositivo hello segnalati valori. Questa definizione include le descrizioni dei metodi di hello diretti hello dispositivo supporta:

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

1. Aggiungere i seguenti hello toohandle funzione hello **riavviare** diretta chiamata al metodo:

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

1. Aggiungere i seguenti hello toohandle funzione hello **InitiateFirmwareUpdate** diretta chiamata al metodo. Questo metodo diretto utilizza un percorso di hello parametro toospecify di toodownload immagine di firmware hello e avvia hello in modo asincrono di aggiornamento del firmware sul dispositivo hello:

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

1. Aggiungere hello toocreate codice un'istanza del client seguenti:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Aggiungere hello seguente codice:

    * Aprire la connessione di hello.
    * Inviare hello **DeviceInfo** oggetto.
    * Impostare un gestore per le proprietà desiderate.
    * Inviare le proprietà segnalate.
    * Registra i gestori per i metodi di hello diretto.
    * Avviare l'invio dei dati di telemetria.

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

1. Salvare hello modifiche toohello **remote_monitoring.js** file.

1. Eseguire hello comando in un'applicazione di esempio hello toolaunch prompt dei comandi seguente:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
