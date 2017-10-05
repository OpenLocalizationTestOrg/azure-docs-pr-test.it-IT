---
title: Metodi diretti dell'Hub IoT di Azure (Node) | Documentazione Microsoft
description: Come usare metodi diretti dell'Hub IoT di Azure. Usare Azure IoT SDK per Node.js per implementare un'app per dispositivo simulato che include un metodo diretto e un'app di servizio che richiama il metodo diretto.
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="4b731-104">Usare i metodi diretti sul dispositivo IoT con Node. js</span><span class="sxs-lookup"><span data-stu-id="4b731-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="4b731-105">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="4b731-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="4b731-106">**CallMethodOnDevice.js**, che chiama un metodo nell'app per dispositivo simulato e visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="4b731-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="4b731-107">**SimulatedDevice.js**, che si connette all'hub IoT con l'identità del dispositivo creata in precedenza e risponde al metodo chiamato dal cloud.</span><span class="sxs-lookup"><span data-stu-id="4b731-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="4b731-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] offre informazioni sui vari Azure IoT SDK che è possibile usare per compilare applicazioni da eseguire nei dispositivi e il backend della soluzione.</span><span class="sxs-lookup"><span data-stu-id="4b731-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="4b731-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b731-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4b731-110">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="4b731-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4b731-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4b731-111">An active Azure account.</span></span> <span data-ttu-id="4b731-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4b731-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="4b731-113">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="4b731-113">Create a simulated device app</span></span>
<span data-ttu-id="4b731-114">In questa sezione viene creata un'applicazione console Node.js che risponde a un metodo chiamato dal cloud.</span><span class="sxs-lookup"><span data-stu-id="4b731-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="4b731-115">Creare una nuova cartella vuota denominata **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="4b731-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="4b731-116">Nella cartella **simulateddevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4b731-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4b731-117">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="4b731-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4b731-118">Eseguire questo comando al prompt dei comandi nella cartella **simulateddevice** per installare il pacchetto SDK per dispositivi **azure-iot-device** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="4b731-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="4b731-119">Con un editor di testo creare un nuovo file **SimulatedDevice.js** nella cartella **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="4b731-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="4b731-120">Aggiungere le istruzioni `require` seguenti all'inizio del file **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="4b731-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="4b731-121">Aggiungere una variabile **connectionString** e usarla per creare un'istanza di **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="4b731-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="4b731-122">Sostituire **{device connection string}** con la stringa di connessione del dispositivo generata nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="4b731-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="4b731-123">Aggiungere la funzione seguente per implementare il metodo nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4b731-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="4b731-124">Aprire la connessione all'hub IoT e inizializzare il listener del metodo:</span><span class="sxs-lookup"><span data-stu-id="4b731-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="4b731-125">Salvare e chiudere il file **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="4b731-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="4b731-126">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="4b731-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4b731-127">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio i tentativi di connessione, come indicato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="4b731-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="4b731-128">Chiamare un metodo su un dispositivo</span><span class="sxs-lookup"><span data-stu-id="4b731-128">Call a method on a device</span></span>
<span data-ttu-id="4b731-129">In questa sezione viene creata un'app console Node.js che chiama un metodo nell'app per dispositivo simulato e quindi visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="4b731-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="4b731-130">Creare una nuova cartella vuota denominata **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="4b731-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="4b731-131">Nella cartella **callmethodondevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="4b731-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="4b731-132">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="4b731-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4b731-133">Eseguire questo comando al prompt dei comandi nella cartella **callmethodondevice** per installare il pacchetto **azure-iothub**:</span><span class="sxs-lookup"><span data-stu-id="4b731-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="4b731-134">Usando un editor di testo creare un file **CallMethodOnDevice.js** nella cartella **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="4b731-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="4b731-135">Aggiungere le istruzioni `require` seguenti all'inizio del file **CallMethodOnDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="4b731-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="4b731-136">Aggiungere la dichiarazione di variabile seguente e sostituire il valore del segnaposto con la stringa di connessione per l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="4b731-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="4b731-137">Creare il client per aprire la connessione all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4b731-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="4b731-138">Aggiungere la funzione seguente per richiamare il metodo del dispositivo e stampare la risposta del dispositivo nella console:</span><span class="sxs-lookup"><span data-stu-id="4b731-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="4b731-139">Salvare e chiudere il file **CallMethodOnDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="4b731-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="4b731-140">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="4b731-140">Run the apps</span></span>
<span data-ttu-id="4b731-141">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="4b731-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="4b731-142">Eseguire questo comando al prompt dei comandi nella cartella **simulateddevice** per iniziare ad ascoltare le chiamate ai metodi dall'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="4b731-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="4b731-143">Al prompt dei comandi nella cartella **callmethodondevice** eseguire questo comando per iniziare a monitorare l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="4b731-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="4b731-144">Il dispositivo reagirà al metodo stampando il messaggio e l'applicazione che ha chiamato il metodo visualizzerà la risposta dal dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4b731-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="4b731-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b731-145">Next steps</span></span>
<span data-ttu-id="4b731-146">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4b731-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="4b731-147">Questa identità del dispositivo è stata usata per consentire all'app del dispositivo simulato di reagire ai metodi richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="4b731-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="4b731-148">È stata anche creata un'applicazione che richiama i metodi sul dispositivo e visualizza la risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4b731-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="4b731-149">Per altre informazioni sulle attività iniziali con l'hub IoT e per esplorare altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="4b731-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="4b731-150">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="4b731-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="4b731-151">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="4b731-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="4b731-152">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="4b731-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
