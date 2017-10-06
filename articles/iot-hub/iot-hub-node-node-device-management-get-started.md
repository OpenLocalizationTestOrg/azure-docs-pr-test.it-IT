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
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="20215-104">Introduzione alla gestione dei dispositivi (Node)</span><span class="sxs-lookup"><span data-stu-id="20215-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="20215-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="20215-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="20215-106">Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="20215-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="20215-107">Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="20215-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="20215-108">Diretti metodi vengono richiamati dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="20215-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="20215-109">Creare un'applicazione console Node. js che chiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="20215-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="20215-110">Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="20215-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="20215-111">**dmpatterns_getstarted_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto di riavvio, simula riavviare il computer fisico e segnala il tempo di hello per ultimo riavvio hello.</span><span class="sxs-lookup"><span data-stu-id="20215-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="20215-112">**dmpatterns_getstarted_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza risposta hello e consente di visualizzare hello aggiornato segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="20215-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="20215-113">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="20215-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="20215-114">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="20215-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="20215-115">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="20215-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="20215-116">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="20215-116">An active Azure account.</span></span> <span data-ttu-id="20215-117">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="20215-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="20215-118">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="20215-118">Create a simulated device app</span></span>
<span data-ttu-id="20215-119">Questa sezione consente di:</span><span class="sxs-lookup"><span data-stu-id="20215-119">In this section, you will</span></span>

* <span data-ttu-id="20215-120">Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello</span><span class="sxs-lookup"><span data-stu-id="20215-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="20215-121">Attivare un riavvio del dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="20215-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="20215-122">Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato</span><span class="sxs-lookup"><span data-stu-id="20215-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="20215-123">Creare una cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="20215-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="20215-124">In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="20215-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="20215-125">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="20215-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="20215-126">Al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="20215-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="20215-127">Utilizzando un editor di testo, creare un **dmpatterns_getstarted_device.js** file hello **manageddevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="20215-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="20215-128">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_device.js** file:</span><span class="sxs-lookup"><span data-stu-id="20215-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="20215-129">Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="20215-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="20215-130">Sostituire la stringa di connessione hello con la stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="20215-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="20215-131">Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="20215-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="20215-132">Aprire l'hub IoT tooyour connessione hello e avviare il listener di un metodo diretto hello:</span><span class="sxs-lookup"><span data-stu-id="20215-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="20215-133">Salvare e chiudere hello **dmpatterns_getstarted_device.js** file.</span><span class="sxs-lookup"><span data-stu-id="20215-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="20215-134">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="20215-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="20215-135">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="20215-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="20215-136">Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="20215-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="20215-137">In questa sezione viene creata un'app console Node.js che attiva un riavvio remoto in un dispositivo usando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="20215-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="20215-138">app Hello utilizza hello toodiscover di query doppi dispositivo ora dell'ultimo riavvio del sistema per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="20215-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="20215-139">Creare una cartella vuota denominata **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="20215-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="20215-140">In hello **triggerrebootondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="20215-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="20215-141">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="20215-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="20215-142">Al prompt dei comandi in hello **triggerrebootondevice** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="20215-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="20215-143">Utilizzando un editor di testo, creare un **dmpatterns_getstarted_service.js** file hello **triggerrebootondevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="20215-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="20215-144">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="20215-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="20215-145">Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:</span><span class="sxs-lookup"><span data-stu-id="20215-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="20215-146">Aggiungere hello seguente funzione tooinvoke hello dispositivo metodo tooreboot hello dispositivo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="20215-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
7. <span data-ttu-id="20215-147">Aggiungere i seguenti hello funzionano tooquery per dispositivo hello e ottenere l'ora dell'ultimo riavvio hello:</span><span class="sxs-lookup"><span data-stu-id="20215-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
8. <span data-ttu-id="20215-148">Aggiungere hello seguendo le funzioni hello toocall di codice che attivano hello dirette del metodo di riavvio e query per hello riavviare ultima volta:</span><span class="sxs-lookup"><span data-stu-id="20215-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="20215-149">Salvare e chiudere hello **dmpatterns_getstarted_service.js** file.</span><span class="sxs-lookup"><span data-stu-id="20215-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="20215-150">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="20215-150">Run hello apps</span></span>
<span data-ttu-id="20215-151">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="20215-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="20215-152">Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="20215-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="20215-153">Al prompt dei comandi di hello in hello **triggerrebootondevice** cartella, eseguire hello successivo comando tootrigger hello remoto riavviare il computer ed eseguire query per hello toofind gemelli di hello dispositivo riavviare ultima volta.</span><span class="sxs-lookup"><span data-stu-id="20215-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="20215-154">Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="20215-154">You see hello device response toohello direct method in hello console.</span></span>

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
