---
title: i messaggi aaaCloud al dispositivo con Azure IoT Hub (nodo) | Documenti Microsoft
description: "La modalità toosend cloud a dispositivo dei messaggi tooa dispositivo da un hub IoT di Azure utilizzando hello Azure IoT SDK per Node.js. Per modificare i messaggi di cloud a dispositivo un dispositivo simulato app tooreceive e modificare un messaggio di cloud a dispositivo hello toosend app back-end."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Inviare messaggi da cloud a dispositivo con l'hub IoT (Node)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introduzione
L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app dispositivo simulato che invia messaggi da dispositivo a cloud.

Questa esercitazione si basa su [iniziare con l'IoT Hub]. Illustra le operazioni seguenti:

* Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.
* Ricevere messaggi da cloud a dispositivo in un dispositivo.
* Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.

Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].

Alla fine di hello di questa esercitazione, si esegue due applicazioni di console Node.js:

* **SimulatedDevice**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.
* **SendCloudToDeviceMessage**, che invia un'app di dispositivo simulato toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.

> [!NOTE]
> L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure. Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].
> 
> 

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Ricezione di messaggi hello dispositivo simulato App
In questa sezione, si modifica hello dispositivo simulato app è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.

1. Per aprire il file di SimulatedDevice.js hello, utilizzando un editor di testo.
2. Modificare hello **connectCallback** funzione toohandle i messaggi inviati dall'IoT Hub. In questo esempio, il dispositivo hello richiama sempre hello **completo** funzione toonotify IoT Hub che è stato elaborato il messaggio hello. La nuova versione di hello **connectCallback** funzione è simile al seguente frammento di codice hello:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > Se si Usa HTTP invece di MQTT o AMQP come trasporto hello, hello **DeviceClient** istanza verifica la presenza di messaggi dall'IoT Hub raramente (meno di 25 minuti). Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Inviare un messaggio da cloud a dispositivo
In questa sezione si crea un'applicazione console Node. js che invia messaggi da cloud a dispositivo toohello dispositivo simulato app. È necessario hello ID dispositivo del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione. È inoltre necessario hello stringa di connessione IoT Hub per l'hub che è possibile trovare nel hello [portale di Azure].

1. Creare una cartella vuota denominata **sendcloudtodevicemessage**. In hello **sendcloudtodevicemessage** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```shell
    npm init
    ```
2. Al prompt dei comandi in hello **sendcloudtodevicemessage** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un **SendCloudToDeviceMessage.js** file hello **sendcloudtodevicemessage** cartella.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SendCloudToDeviceMessage.js** file:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Aggiungere hello seguente codice troppo**SendCloudToDeviceMessage.js** file. Sostituire il valore di segnaposto hello "{iot hub stringa di connessione}" con la stringa di connessione IoT Hub hub hello è stato creato in hello hello [iniziare con l'IoT Hub] esercitazione. Sostituire i segnaposto hello "{id dispositivo}" con ID dispositivo hello del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Aggiungere hello console toohello risultati di funzione tooprint operazione seguente:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Aggiungere hello console toohello i messaggi di funzione tooprint recapito commenti e suggerimenti di seguito:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Aggiungere i seguenti hello toosend un dispositivo tooyour messaggio del codice e gestiscono il messaggio di commenti e suggerimenti hello quando il dispositivo hello invia un acknowledgement messaggio hello del cloud a dispositivo:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Salvare e chiudere il file **SendCloudToDeviceMessage.js** .

## <a name="run-hello-applications"></a>Eseguire applicazioni hello
Si è ora applicazioni hello toorun pronto.

1. Al prompt dei comandi di hello in hello **simulateddevice** cartella, eseguire il seguente hello comandi toosend telemetria tooIoT Hub e toolisten per i messaggi da cloud a dispositivo:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Eseguire app dispositivo simulato hello][img-simulated-device]
2. Al prompt dei comandi in hello **sendcloudtodevicemessage** cartella, eseguire hello successivo comando toosend un messaggio da cloud a dispositivo e attendere commenti e suggerimenti riconoscimento hello:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Comando hello app toosend hello cloud a dispositivo][img-send-command]
   
   > [!NOTE]
   > Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo. 

esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].

toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[iniziare con l'IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[Centro per sviluppatori di Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portale di Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
