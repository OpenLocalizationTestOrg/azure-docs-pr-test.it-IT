---
title: aaaGet avviato con la gestione dei dispositivi Azure IoT Hub (nodo) | Documenti Microsoft
description: "La modalità IoT Hub device management tooinitiate toouse un dispositivo remoto riavviare. Utilizzare hello IoT di Azure SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e un'applicazione di servizio che richiama metodo diretto hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Introduzione alla gestione dei dispositivi (Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Questa esercitazione illustra come:

* Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.
* Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo. Diretti metodi vengono richiamati dal cloud hello.
* Creare un'applicazione console Node. js che chiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.

Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:

**dmpatterns_getstarted_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto di riavvio, simula riavviare il computer fisico e segnala il tempo di hello per ultimo riavvio hello.

**dmpatterns_getstarted_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza risposta hello e consente di visualizzare hello aggiornato segnalati proprietà.

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.12.x o versione successiva. <br/>  [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
Questa sezione consente di:

* Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello
* Attivare un riavvio del dispositivo simulato
* Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato

1. Creare una cartella vuota denominata **manageddevice**.  In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un **dmpatterns_getstarted_device.js** file hello **manageddevice** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_device.js** file:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.  Sostituire la stringa di connessione hello con la stringa di connessione del dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Aprire l'hub IoT tooyour connessione hello e avviare il listener di un metodo diretto hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Salvare e chiudere hello **dmpatterns_getstarted_device.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto
In questa sezione viene creata un'app console Node.js che attiva un riavvio remoto in un dispositivo usando un metodo diretto. app Hello utilizza hello toodiscover di query doppi dispositivo ora dell'ultimo riavvio del sistema per il dispositivo.

1. Creare una cartella vuota denominata **triggerrebootondevice**.  In hello **triggerrebootondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **triggerrebootondevice** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt** pacchetto:
   
    ```
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un **dmpatterns_getstarted_service.js** file hello **triggerrebootondevice** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_service.js** file:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Aggiungere hello seguente funzione tooinvoke hello dispositivo metodo tooreboot hello dispositivo di destinazione:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Aggiungere i seguenti hello funzionano tooquery per dispositivo hello e ottenere l'ora dell'ultimo riavvio hello:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Aggiungere hello seguendo le funzioni hello toocall di codice che attivano hello dirette del metodo di riavvio e query per hello riavviare ultima volta:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Salvare e chiudere hello **dmpatterns_getstarted_service.js** file.

## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Al prompt dei comandi di hello in hello **triggerrebootondevice** cartella, eseguire hello successivo comando tootrigger hello remoto riavviare il computer ed eseguire query per hello toofind gemelli di hello dispositivo riavviare ultima volta.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
