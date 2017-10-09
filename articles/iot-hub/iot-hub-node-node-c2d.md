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
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="255f7-104">Inviare messaggi da cloud a dispositivo con l'hub IoT (Node)</span><span class="sxs-lookup"><span data-stu-id="255f7-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="255f7-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="255f7-105">Introduction</span></span>
<span data-ttu-id="255f7-106">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="255f7-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="255f7-107">Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app dispositivo simulato che invia messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="255f7-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="255f7-108">Questa esercitazione si basa su [iniziare con l'IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="255f7-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="255f7-109">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="255f7-109">It shows you how to:</span></span>

* <span data-ttu-id="255f7-110">Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="255f7-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="255f7-111">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255f7-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="255f7-112">Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="255f7-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="255f7-113">Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="255f7-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="255f7-114">Alla fine di hello di questa esercitazione, si esegue due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="255f7-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="255f7-115">**SimulatedDevice**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255f7-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="255f7-116">**SendCloudToDeviceMessage**, che invia un'app di dispositivo simulato toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.</span><span class="sxs-lookup"><span data-stu-id="255f7-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="255f7-117">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="255f7-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="255f7-118">Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="255f7-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="255f7-119">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="255f7-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="255f7-120">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="255f7-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="255f7-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="255f7-121">An active Azure account.</span></span> <span data-ttu-id="255f7-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="255f7-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="255f7-123">Ricezione di messaggi hello dispositivo simulato App</span><span class="sxs-lookup"><span data-stu-id="255f7-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="255f7-124">In questa sezione, si modifica hello dispositivo simulato app è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="255f7-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="255f7-125">Per aprire il file di SimulatedDevice.js hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="255f7-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="255f7-126">Modificare hello **connectCallback** funzione toohandle i messaggi inviati dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="255f7-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="255f7-127">In questo esempio, il dispositivo hello richiama sempre hello **completo** funzione toonotify IoT Hub che è stato elaborato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="255f7-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="255f7-128">La nuova versione di hello **connectCallback** funzione è simile al seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="255f7-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
   > <span data-ttu-id="255f7-129">Se si Usa HTTP invece di MQTT o AMQP come trasporto hello, hello **DeviceClient** istanza verifica la presenza di messaggi dall'IoT Hub raramente (meno di 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="255f7-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="255f7-130">Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="255f7-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="255f7-131">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="255f7-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="255f7-132">In questa sezione si crea un'applicazione console Node. js che invia messaggi da cloud a dispositivo toohello dispositivo simulato app.</span><span class="sxs-lookup"><span data-stu-id="255f7-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="255f7-133">È necessario hello ID dispositivo del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="255f7-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="255f7-134">È inoltre necessario hello stringa di connessione IoT Hub per l'hub che è possibile trovare nel hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="255f7-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="255f7-135">Creare una cartella vuota denominata **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="255f7-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="255f7-136">In hello **sendcloudtodevicemessage** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="255f7-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="255f7-137">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="255f7-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="255f7-138">Al prompt dei comandi in hello **sendcloudtodevicemessage** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="255f7-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="255f7-139">Utilizzando un editor di testo, creare un **SendCloudToDeviceMessage.js** file hello **sendcloudtodevicemessage** cartella.</span><span class="sxs-lookup"><span data-stu-id="255f7-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="255f7-140">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SendCloudToDeviceMessage.js** file:</span><span class="sxs-lookup"><span data-stu-id="255f7-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="255f7-141">Aggiungere hello seguente codice troppo**SendCloudToDeviceMessage.js** file.</span><span class="sxs-lookup"><span data-stu-id="255f7-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="255f7-142">Sostituire il valore di segnaposto hello "{iot hub stringa di connessione}" con la stringa di connessione IoT Hub hub hello è stato creato in hello hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="255f7-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="255f7-143">Sostituire i segnaposto hello "{id dispositivo}" con ID dispositivo hello del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione:</span><span class="sxs-lookup"><span data-stu-id="255f7-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="255f7-144">Aggiungere hello console toohello risultati di funzione tooprint operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="255f7-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="255f7-145">Aggiungere hello console toohello i messaggi di funzione tooprint recapito commenti e suggerimenti di seguito:</span><span class="sxs-lookup"><span data-stu-id="255f7-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="255f7-146">Aggiungere i seguenti hello toosend un dispositivo tooyour messaggio del codice e gestiscono il messaggio di commenti e suggerimenti hello quando il dispositivo hello invia un acknowledgement messaggio hello del cloud a dispositivo:</span><span class="sxs-lookup"><span data-stu-id="255f7-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
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
9. <span data-ttu-id="255f7-147">Salvare e chiudere il file **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="255f7-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="255f7-148">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="255f7-148">Run hello applications</span></span>
<span data-ttu-id="255f7-149">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="255f7-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="255f7-150">Al prompt dei comandi di hello in hello **simulateddevice** cartella, eseguire il seguente hello comandi toosend telemetria tooIoT Hub e toolisten per i messaggi da cloud a dispositivo:</span><span class="sxs-lookup"><span data-stu-id="255f7-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Eseguire app dispositivo simulato hello][img-simulated-device]
2. <span data-ttu-id="255f7-152">Al prompt dei comandi in hello **sendcloudtodevicemessage** cartella, eseguire hello successivo comando toosend un messaggio da cloud a dispositivo e attendere commenti e suggerimenti riconoscimento hello:</span><span class="sxs-lookup"><span data-stu-id="255f7-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Comando hello app toosend hello cloud a dispositivo][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="255f7-154">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="255f7-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="255f7-155">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="255f7-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="255f7-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="255f7-156">Next steps</span></span>
<span data-ttu-id="255f7-157">In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255f7-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="255f7-158">esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="255f7-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="255f7-159">toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="255f7-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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
