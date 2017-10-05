---
title: Messaggi da cloud a dispositivo con l'hub IoT di Azure (Node) | Microsoft Docs
description: Come inviare messaggi da cloud a dispositivo a un dispositivo da un hub IoT di Azure tramite Azure IoT SDK per Node. js. Modificare un'app per dispositivo simulato per ricevere messaggi da cloud a dispositivo e modificare un'app back-end per inviare i messaggi da cloud a dispositivo.
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
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="e8e6d-104">Inviare messaggi da cloud a dispositivo con l'hub IoT (Node)</span><span class="sxs-lookup"><span data-stu-id="e8e6d-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="e8e6d-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e8e6d-105">Introduction</span></span>
<span data-ttu-id="e8e6d-106">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="e8e6d-107">L'esercitazione [Introduzione all'hub IoT di Azure] illustra come creare un hub IoT, effettuare il provisioning dell'identità di un dispositivo al suo interno e creare il codice di un'app per dispositivo simulato che invia messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="e8e6d-108">Questa esercitazione si basa su [Introduzione all'hub IoT di Azure].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="e8e6d-109">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-109">It shows you how to:</span></span>

* <span data-ttu-id="e8e6d-110">Dal back-end della soluzione inviare messaggi da cloud a dispositivo a un singolo dispositivo tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="e8e6d-111">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="e8e6d-112">Dal back-end della soluzione richiedere l'acknowledgement di recapito (*feedback*) per i messaggi inviati a un dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="e8e6d-113">Per altre informazioni sui messaggi da cloud a dispositivo, vedere la[Guida per sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="e8e6d-114">Al termine di questa esercitazione, vengono eseguite due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="e8e6d-115">**SimulatedDevice**, una versione modificata dell'app creata in [Introduzione all'hub IoT di Azure], che si connette all'hub IoT e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="e8e6d-116">**SendCloudToDeviceMessage**, che invia un messaggio da cloud a dispositivo all'app per dispositivo simulato tramite l'hub IoT e riceve quindi l'acknowledgement di recapito.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="e8e6d-117">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="e8e6d-118">Per istruzioni dettagliate su come connettere il dispositivo al codice dell'esercitazione e in generale all'hub IoT di Azure, vedere il [Centro per sviluppatori Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="e8e6d-119">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e8e6d-120">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e8e6d-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-121">An active Azure account.</span></span> <span data-ttu-id="e8e6d-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="e8e6d-123">Ricevere messaggi nell'app per dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="e8e6d-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="e8e6d-124">In questa sezione si modificherà l'app per il dispositivo simulato creata in [Introduzione all'hub IoT di Azure] per ricevere i messaggi da cloud a dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="e8e6d-125">Con un editor di testo aprire il file SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="e8e6d-126">Modificare la funzione **connectCallback** per gestire i messaggi inviati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="e8e6d-127">In questo esempio il dispositivo richiama sempre la funzione **complete** per notificare all'hub IoT Hub che ha elaborato il messaggio.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="e8e6d-128">La nuova versione della funzione **connectCallback** è simile al frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
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
        // Create a message and send it to the IoT Hub every second
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
   > <span data-ttu-id="e8e6d-129">Se si usa HTTP/25 invece di MQTT o AMQP per il trasporto, l'istanza di **DeviceClient** controlla raramente i messaggi provenienti dall'hub IoT (meno di 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="e8e6d-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="e8e6d-130">Per altre informazioni sulle differenze tra il supporto di MQTT, AMQP e HTTP e sulla limitazione delle richieste dell'hub IoT, vedere [Guida per sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="e8e6d-131">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="e8e6d-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="e8e6d-132">In questa sezione si crea un'app console Node.js che invia messaggi da cloud a dispositivo all'app del dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="e8e6d-133">È necessario l'ID del dispositivo aggiunto nell'esercitazione [Introduzione all'hub IoT di Azure] .</span><span class="sxs-lookup"><span data-stu-id="e8e6d-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="e8e6d-134">È necessaria anche la stringa di connessione per l'hub IoT, disponibile nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="e8e6d-135">Creare una cartella vuota denominata **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="e8e6d-136">Nella cartella **sendcloudtodevicemessage** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="e8e6d-137">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="e8e6d-138">Eseguire questo comando al prompt dei comandi nella cartella **sendcloudtodevicemessage** per installare il pacchetto **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e8e6d-139">Con un editor di testo, creare un file **SendCloudToDeviceMessage.js** nella cartella **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="e8e6d-140">Aggiungere le istruzioni `require` seguenti all'inizio del file **SendCloudToDeviceMessage.js** :</span><span class="sxs-lookup"><span data-stu-id="e8e6d-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="e8e6d-141">Aggiungere il codice seguente al file **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="e8e6d-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="e8e6d-142">Sostituire il valore del segnaposto "{iot hub connection string}" con la stringa di connessione dell'hub IoT creato durante l'esercitazione [Introduzione all'hub IoT di Azure].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="e8e6d-143">Sostituire il segnaposto "{device id}" con l'ID del dispositivo aggiunto nell'esercitazione [Introduzione all'hub IoT di Azure]:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="e8e6d-144">Aggiungere la funzione seguente per stampare i risultati dell'operazione sulla console:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="e8e6d-145">Aggiungere la funzione seguente per stampare i messaggi di feedback del recapito sulla console:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="e8e6d-146">Aggiungere il codice seguente per inviare un messaggio al dispositivo e gestire il messaggio di feedback quando il dispositivo accetta il messaggio da cloud a dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="e8e6d-147">Salvare e chiudere il file **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="e8e6d-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="e8e6d-148">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="e8e6d-148">Run the applications</span></span>
<span data-ttu-id="e8e6d-149">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="e8e6d-150">Al prompt dei comandi nella cartella **simulateddevice** eseguire questo comando per inviare i dati di telemetria all'hub IoT e per rimanere in ascolto dei messaggi da cloud a dispositivo:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Eseguire un'app di dispositivo simulato][img-simulated-device]
2. <span data-ttu-id="e8e6d-152">A un prompt dei comandi nella cartella **sendcloudtodevicemessage** eseguire questo comando per inviare un messaggio da cloud a dispositivo e attendere il feedback di acknowledgment:</span><span class="sxs-lookup"><span data-stu-id="e8e6d-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Eseguire l'app per inviare il comando da cloud a dispositivo][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="e8e6d-154">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e8e6d-155">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="e8e6d-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="e8e6d-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8e6d-156">Next steps</span></span>
<span data-ttu-id="e8e6d-157">In questa esercitazione è stato descritto come inviare e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e8e6d-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="e8e6d-158">Per avere degli esempi di soluzioni complete che utilizzano l'hub IoT, vedere la [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="e8e6d-159">Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="e8e6d-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="e8e6d-160">[Introduzione all'hub IoT di Azure]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="e8e6d-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="e8e6d-161">[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="e8e6d-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="e8e6d-162">[Centro per sviluppatori Azure IoT]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="e8e6d-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="e8e6d-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="e8e6d-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="e8e6d-164">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="e8e6d-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="e8e6d-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="e8e6d-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
