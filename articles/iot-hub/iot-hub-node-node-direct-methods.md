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
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="6997b-104">Usare i metodi diretti sul dispositivo IoT con Node. js</span><span class="sxs-lookup"><span data-stu-id="6997b-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="6997b-105">Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="6997b-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="6997b-106">**CallMethodOnDevice.js**, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="6997b-107">**SimulatedDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="6997b-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="6997b-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="6997b-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6997b-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6997b-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6997b-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="6997b-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="6997b-111">An active Azure account.</span></span> <span data-ttu-id="6997b-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6997b-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6997b-113">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="6997b-113">Create a simulated device app</span></span>
<span data-ttu-id="6997b-114">In questa sezione si crea un'applicazione console Node. js che risponde tooa metodo chiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="6997b-115">Creare una nuova cartella vuota denominata **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="6997b-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="6997b-116">In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="6997b-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="6997b-117">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6997b-118">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6997b-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="6997b-119">Utilizzando un editor di testo, creare un nuovo **SimulatedDevice.js** file hello **simulateddevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="6997b-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="6997b-120">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="6997b-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="6997b-121">Aggiungere un **connectionString** variabile e usarlo toocreate un **DeviceClient** istanza.</span><span class="sxs-lookup"><span data-stu-id="6997b-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="6997b-122">Sostituire **{stringa di connessione dispositivo}** con stringa di connessione dispositivo hello generato nel hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="6997b-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="6997b-123">Aggiungere hello seguente metodo di funzione tooimplement hello sul dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
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
7. <span data-ttu-id="6997b-124">Aprire l'hub IoT tooyour connessione hello e avviare i listener per il metodo initialize hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="6997b-125">Salvare e chiudere hello **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="6997b-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="6997b-126">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="6997b-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6997b-127">Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="6997b-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="6997b-128">Chiamare un metodo su un dispositivo</span><span class="sxs-lookup"><span data-stu-id="6997b-128">Call a method on a device</span></span>
<span data-ttu-id="6997b-129">In questa sezione si crea un'applicazione console Node. js che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="6997b-130">Creare una nuova cartella vuota denominata **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="6997b-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="6997b-131">In hello **callmethodondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="6997b-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="6997b-132">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6997b-133">Al prompt dei comandi in hello **callmethodondevice** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6997b-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="6997b-134">Utilizzando un editor di testo, creare un **CallMethodOnDevice.js** file hello **callmethodondevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="6997b-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="6997b-135">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **CallMethodOnDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="6997b-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="6997b-136">Aggiungere hello seguente dichiarazione di variabile e sostituire il valore di segnaposto hello con stringa di connessione IoT Hub per l'hub hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="6997b-137">Creare l'hub IoT hello client tooopen hello connessione tooyour.</span><span class="sxs-lookup"><span data-stu-id="6997b-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="6997b-138">Aggiungere hello funzione tooinvoke hello (metodo) e stampa hello dispositivo risposta toohello console del dispositivo seguenti:</span><span class="sxs-lookup"><span data-stu-id="6997b-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
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
8. <span data-ttu-id="6997b-139">Salvare e chiudere hello **CallMethodOnDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="6997b-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="6997b-140">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="6997b-140">Run hello apps</span></span>
<span data-ttu-id="6997b-141">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="6997b-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="6997b-142">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello in attesa di chiamate al metodo dall'IoT Hub toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6997b-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="6997b-143">Al prompt dei comandi in hello **callmethodondevice** cartella, eseguire hello monitoraggio l'hub IoT toobegin di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6997b-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="6997b-144">Si noterà dispositivo hello reagire toohello metodo stampando messaggio hello e un'applicazione hello denominato risposta di hello visualizzazione metodo hello dal dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="6997b-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="6997b-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6997b-145">Next steps</span></span>
<span data-ttu-id="6997b-146">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="6997b-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="6997b-147">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="6997b-148">È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6997b-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="6997b-149">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="6997b-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="6997b-150">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="6997b-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="6997b-151">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="6997b-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="6997b-152">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6997b-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
