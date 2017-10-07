---
title: aaaGet avviato con l'IoT Hub Azure (nodo) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per Node.js. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Connessione hub IoT tooyour dispositivo simulato utilizzando nodo
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console Node.js:

* **CreateDeviceIdentity.js**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.
* **ReadDeviceToCloudMessages.js**, che consente di visualizzare dati di telemetria hello inviati dall'app dispositivo simulato.
* **SimulatedDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo utilizzando hello protocollo MQTT.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.
> 
> 

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

L'hub IoT è stato creato. È necessario hello nome host dell'IoT Hub e hello stringa di connessione IoT Hub che è necessario rest hello toocomplete di questa esercitazione.

## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo
In questa sezione si crea un'applicazione console Node.js che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT. Un dispositivo può connettersi solo hub tooIoT se dispone di una voce del Registro di sistema di hello identità. Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity]. Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.

1. Creare una nuova cartella vuota denominata **createdeviceidentity**. In hello **createdeviceidentity** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **createdeviceidentity** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK del servizio:
   
    ```
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un **CreateDeviceIdentity.js** file hello **createdeviceidentity** cartella.
4. Aggiungere il seguente hello `require` istruzione all'inizio di hello di hello **CreateDeviceIdentity.js** file:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Aggiungere i seguenti toohello codice hello **CreateDeviceIdentity.js** file e sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Aggiungere hello seguente codice toocreate una definizione di dispositivo nel Registro di sistema di hello identità nell'hub IoT. Questo codice crea un dispositivo se l'ID dispositivo hello non esiste nel Registro di sistema di hello identità, in caso contrario restituisce chiave hello del dispositivo esistente hello:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Salvare e chiudere il file **CreateDeviceIdentity.js** .
8. hello toorun **createdeviceidentity** applicazione, eseguire hello comando al prompt dei comandi di hello nella cartella createdeviceidentity hello seguente:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Prendere nota di hello **ID dispositivo** e **chiave dispositivo**. Questi valori è necessario in un secondo momento quando si crea un'applicazione che si connette tooIoT Hub come un dispositivo.

> [!NOTE]
> Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso. Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo. Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione. Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Ricezione di messaggi da dispositivo a cloud
In questa sezione si creerà un'app console di Node.js che legge i messaggi da dispositivo a cloud dall'hub IoT. Un hub IoT espone un [hub eventi][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread. cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata. Hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione viene illustrato come tooprocess dispositivo a cloud messaggi su larga scala. Hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione fornisce ulteriori informazioni su come tooprocess messaggi dagli hub eventi ed è applicabile toohello gli endpoint Hub IoT Hub eventi compatibile.

> [!NOTE]
> Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.
> 
> 

1. Creare una cartella vuota denominata **readdevicetocloudmessages**. In hello **readdevicetocloudmessages** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **readdevicetocloudmessages** cartella, eseguire hello successivo comando tooinstall hello **hub di eventi di azure** pacchetto:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Utilizzando un editor di testo, creare un **ReadDeviceToCloudMessages.js** file hello **readdevicetocloudmessages** cartella.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **ReadDeviceToCloudMessages.js** file:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Aggiungere hello seguente dichiarazione di variabile e sostituire il valore di segnaposto hello con stringa di connessione IoT Hub per l'hub hello:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Aggiungere i seguenti due funzioni della console di output toohello stampa hello:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Aggiungere i seguenti hello toocreate codice hello **EventHubClient**, aprire hello connessione tooyour IoT Hub e creare un ricevitore per ogni partizione. L'applicazione utilizza un filtro durante la creazione di un destinatario in modo che hello ricevitore legge solo i messaggi inviati tooIoT Hub dopo ricevitore hello viene avviata l'esecuzione. Questo filtro è utile in un ambiente di test in modo che solo hello set corrente di messaggi. In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello. Per ulteriori informazioni, vedere hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-process-d2c-tutorial] esercitazione:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Salvare e chiudere hello **ReadDeviceToCloudMessages.js** file.

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione si crea un'applicazione console Node. js che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.

1. Creare una cartella vuota denominata **simulateddevice**. In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un **SimulatedDevice.js** file hello **simulateddevice** cartella.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza. Sostituire **{youriothostname}** con nome hello dell'hub IoT hello creato hello *creare un IoT Hub* sezione. Sostituire **{yourdevicekey}** con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Aggiungere i seguenti output toodisplay funzione da un'applicazione hello hello:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Creare un callback e utilizzare hello **setInterval** funzione toosend un hub IoT tooyour di messaggi al secondo:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. Aprire hello connessione tooyour IoT Hub e avviare l'invio di messaggi:
   
    ```
    client.open(connectCallback);
    ```
9. Salvare e chiudere hello **SimulatedDevice.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi in hello **readdevicetocloudmessages** cartella, eseguire hello monitoraggio l'hub IoT toobegin di comando seguente:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Messaggi da dispositivo a cloud toomonitor di Node.js IoT Hub del servizio app][7]
2. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello toobegin comando invio hub IoT tooyour dati di telemetria seguenti:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Messaggi da dispositivo a cloud di Node.js IoT Hub dispositivo app toosend][8]
3. Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:
   
    ![Azure portale utilizzo riquadro mostra il numero di messaggi inviati tooIoT Hub][43]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT. È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello. 

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Connessione del dispositivo][lnk-connect-device]
* [Introduzione alla gestione dei dispositivi][lnk-device-management]
* [Introduzione ad Azure IoT Edge][lnk-iot-edge]

toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
