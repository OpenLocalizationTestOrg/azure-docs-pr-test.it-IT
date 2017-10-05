---
title: Introduzione alla gestione dei dispositivi dell'hub IoT di Azure (Node) | Documentazione Microsoft
description: Come usare la gestione dei dispositivi dell'hub IoT per riavviare un dispositivo remoto. Usare Azure IoT SDK per Node.js per implementare un'app per dispositivo simulato che include un metodo diretto e un'app di servizio che richiama il metodo diretto.
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="187ed-104">Introduzione alla gestione dei dispositivi (Node)</span><span class="sxs-lookup"><span data-stu-id="187ed-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="187ed-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="187ed-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="187ed-106">Creare un hub IoT nel portale di Azure e un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="187ed-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="187ed-107">Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="187ed-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="187ed-108">I metodi diretti vengono richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="187ed-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="187ed-109">Creare un'app console Node.js che chiama il metodo diretto di riavvio nell'app per dispositivo simulato tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="187ed-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="187ed-110">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="187ed-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="187ed-111">**dmpatterns_getstarted_device.js**, che si connette all'hub IoT con l'identità del dispositivo creata in precedenza, riceve un metodo diretto per il riavvio, simula un riavvio fisico e segnala il tempo impiegato per l'ultimo riavvio.</span><span class="sxs-lookup"><span data-stu-id="187ed-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="187ed-112">**dmpatterns_getstarted_service.js**, che chiama un metodo diretto nel dispositivo simulato, visualizza la risposta e le proprietà segnalate aggiornate.</span><span class="sxs-lookup"><span data-stu-id="187ed-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="187ed-113">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="187ed-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="187ed-114">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="187ed-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="187ed-115">[Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="187ed-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="187ed-116">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="187ed-116">An active Azure account.</span></span> <span data-ttu-id="187ed-117">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="187ed-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="187ed-118">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="187ed-118">Create a simulated device app</span></span>
<span data-ttu-id="187ed-119">Questa sezione consente di:</span><span class="sxs-lookup"><span data-stu-id="187ed-119">In this section, you will</span></span>

* <span data-ttu-id="187ed-120">Creare un'app console Node.js che risponde a un metodo diretto chiamato dal cloud</span><span class="sxs-lookup"><span data-stu-id="187ed-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="187ed-121">Attivare un riavvio del dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="187ed-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="187ed-122">Usare le proprietà segnalate per abilitare le query nei dispositivi gemelli in modo da identificare i dispositivi e l'ora dell'ultimo riavvio</span><span class="sxs-lookup"><span data-stu-id="187ed-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="187ed-123">Creare una cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="187ed-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="187ed-124">Nella cartella **manageddevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="187ed-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="187ed-125">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="187ed-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="187ed-126">Eseguire questo comando al prompt dei comandi nella cartella **manageddevice** per installare il pacchetto SDK per dispositivi **azure-iot-device** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="187ed-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="187ed-127">Con un editor di testo creare un file **dmpatterns_getstarted_device.js** nella cartella **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="187ed-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="187ed-128">Aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="187ed-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="187ed-129">Aggiungere una variabile **connectionString** e usarla per creare un'istanza **Client**.</span><span class="sxs-lookup"><span data-stu-id="187ed-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="187ed-130">Sostituire la stringa di connessione con la stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="187ed-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="187ed-131">Aggiungere la funzione seguente per implementare il metodo diretto nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="187ed-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="187ed-132">Aprire la connessione all'hub IoT e avviare il listener del metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="187ed-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="187ed-133">Salvare e chiudere il file **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="187ed-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="187ed-134">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="187ed-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="187ed-135">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="187ed-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="187ed-136">Attivare un riavvio remoto nel dispositivo con un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="187ed-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="187ed-137">In questa sezione viene creata un'app console Node.js che attiva un riavvio remoto in un dispositivo usando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="187ed-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="187ed-138">L'app esegue query nel dispositivo gemello per ottenere l'ora dell'ultimo riavvio del dispositivo in questione.</span><span class="sxs-lookup"><span data-stu-id="187ed-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="187ed-139">Creare una cartella vuota denominata **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="187ed-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="187ed-140">Nella cartella **triggerrebootondevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="187ed-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="187ed-141">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="187ed-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="187ed-142">Eseguire questo comando al prompt dei comandi nella cartella **triggerrebootondevice** per installare il pacchetto SDK per dispositivi **azure-iothub** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="187ed-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="187ed-143">Con un editor di testo creare un file **dmpatterns_getstarted_service.js** nella cartella **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="187ed-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="187ed-144">Aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="187ed-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="187ed-145">Aggiungere le dichiarazioni di variabile seguenti e sostituire i valori segnaposto:</span><span class="sxs-lookup"><span data-stu-id="187ed-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="187ed-146">Aggiungere la funzione seguente per richiamare il metodo per riavviare il dispositivo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="187ed-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="187ed-147">Aggiungere la funzione seguente per eseguire una query per il dispositivo e ottenere l'ora dell'ultimo riavvio:</span><span class="sxs-lookup"><span data-stu-id="187ed-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="187ed-148">Aggiungere il codice seguente per chiamare le funzioni che attivano il metodo diretto per il riavvio ed eseguire una query per ottenere l'ora dell'ultimo riavvio:</span><span class="sxs-lookup"><span data-stu-id="187ed-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="187ed-149">Salvare e chiudere il file **dmpatterns_getstarted_service.js**.</span><span class="sxs-lookup"><span data-stu-id="187ed-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="187ed-150">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="187ed-150">Run the apps</span></span>
<span data-ttu-id="187ed-151">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="187ed-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="187ed-152">Al prompt dei comandi nella cartella **manageddevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="187ed-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="187ed-153">Al prompt dei comandi nella cartella **triggerrebootondevice** eseguire questo comando per attivare il riavvio remoto e cercare il dispositivo gemello per trovare l'ora dell'ultimo riavvio.</span><span class="sxs-lookup"><span data-stu-id="187ed-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="187ed-154">Nella console viene visualizzata la risposta del dispositivo al metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="187ed-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
