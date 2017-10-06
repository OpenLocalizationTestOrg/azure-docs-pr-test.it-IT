---
title: IoT Hub aaaAzure diretta di metodi (nodo) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Utilizzare hello Azure IoT SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Usare i metodi diretti sul dispositivo IoT con Node. js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:

* **CallMethodOnDevice.js**, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.
* **SimulatedDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.
> 
> 

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione si crea un'applicazione console Node. js che risponde tooa metodo chiamato dal cloud hello.

1. Creare una nuova cartella vuota denominata **simulateddevice**. In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **SimulatedDevice.js** file hello **simulateddevice** cartella.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **DeviceClient** istanza. Sostituire **{stringa di connessione dispositivo}** con stringa di connessione dispositivo hello generato nel hello *creare un'identità del dispositivo* sezione:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Aggiungere hello seguente metodo di funzione tooimplement hello sul dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Aprire l'hub IoT tooyour connessione hello e avviare i listener per il metodo initialize hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Salvare e chiudere hello **SimulatedDevice.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Chiamare un metodo su un dispositivo
In questa sezione si crea un'applicazione console Node. js che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.

1. Creare una nuova cartella vuota denominata **callmethodondevice**. In hello **callmethodondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **callmethodondevice** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:
   
    ```
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un **CallMethodOnDevice.js** file hello **callmethodondevice** cartella.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **CallMethodOnDevice.js** file:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Aggiungere hello seguente dichiarazione di variabile e sostituire il valore di segnaposto hello con stringa di connessione IoT Hub per l'hub hello:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Creare l'hub IoT hello client tooopen hello connessione tooyour.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Aggiungere hello funzione tooinvoke hello (metodo) e stampa hello dispositivo risposta toohello console del dispositivo seguenti:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Salvare e chiudere hello **CallMethodOnDevice.js** file.

## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello in attesa di chiamate al metodo dall'IoT Hub toostart di comando seguente:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Al prompt dei comandi in hello **callmethodondevice** cartella, eseguire hello monitoraggio l'hub IoT toobegin di comando seguente:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Si noterà dispositivo hello reagire toohello metodo stampando messaggio hello e un'applicazione hello denominato risposta di hello visualizzazione metodo hello dal dispositivo hello:
   
    ![][9]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello. È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello. 

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Introduzione all'hub IoT]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md
