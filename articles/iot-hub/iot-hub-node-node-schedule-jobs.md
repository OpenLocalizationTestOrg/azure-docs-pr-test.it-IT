---
title: Pianificare processi con l'hub IoT di Azure (Node) | Microsoft Docs
description: "Come pianificare un processo dell'hub IoT di Azure per richiamare un metodo diretto su più dispositivi. Usare Azure IoT SDK per Node.js per implementare le app per dispositivi simulati e un'app di servizio per eseguire il processo."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 42e594dc6a8a8be619b5652bf8e44cf883650489
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="684bf-104">Pianificare e trasmettere processi (Node)</span><span class="sxs-lookup"><span data-stu-id="684bf-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="684bf-105">L'hub IoT di Azure è un servizio completamente gestito che consente a un'app back-end di creare e tenere traccia dei processi che pianificano e aggiornano milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="684bf-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="684bf-106">I processi possono essere usati per le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="684bf-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="684bf-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="684bf-107">Update desired properties</span></span>
* <span data-ttu-id="684bf-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="684bf-108">Update tags</span></span>
* <span data-ttu-id="684bf-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="684bf-109">Invoke direct methods</span></span>

<span data-ttu-id="684bf-110">Concettualmente, un processo esegue il wrapping di una di queste azioni e tiene traccia dell'avanzamento dell'esecuzione rispetto a un set di dispositivi, definito da una query di dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="684bf-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="684bf-111">Grazie a un processo, ad esempio, un'app back-end può richiamare un metodo di riavvio in 10.000 dispositivi, specificato da una query di dispositivi gemelli e pianificato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="684bf-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="684bf-112">L'applicazione può quindi tenere traccia dell'avanzamento mentre ognuno dei dispositivi riceve ed esegue il metodo di riavvio.</span><span class="sxs-lookup"><span data-stu-id="684bf-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="684bf-113">Altre informazioni su queste funzionalità sono disponibili in questi articoli:</span><span class="sxs-lookup"><span data-stu-id="684bf-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="684bf-114">Dispositivi gemelli e proprietà: [Introduzione ai dispositivi gemelli][lnk-get-started-twin] ed [Esercitazione: Come usare le proprietà dei dispositivi gemelli][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="684bf-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="684bf-115">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Metodi diretti][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="684bf-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="684bf-116">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="684bf-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="684bf-117">Creare un'app per dispositivo simulato con un metodo diretto che abilita il metodo diretto **lockDoor** che può essere chiamato dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="684bf-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="684bf-118">Creare un'app console Node.js che chiama il metodo diretto **lockDoor** nell'app per dispositivo simulato tramite un processo e aggiorna le proprietà desiderate tramite un processo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="684bf-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="684bf-119">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="684bf-119">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="684bf-120">**simDevice.js**, che si connette all'hub IoT con l'identità del dispositivo e riceve un metodo diretto **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="684bf-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="684bf-121">**scheduleJobService.js**, che chiama un metodo diretto nell'app per dispositivo simulato e aggiorna le proprietà desiderate di un dispositivo gemello tramite un processo.</span><span class="sxs-lookup"><span data-stu-id="684bf-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="684bf-122">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="684bf-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="684bf-123">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="684bf-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="684bf-124">[Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="684bf-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="684bf-125">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="684bf-125">An active Azure account.</span></span> <span data-ttu-id="684bf-126">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="684bf-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="684bf-127">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="684bf-127">Create a simulated device app</span></span>
<span data-ttu-id="684bf-128">In questa sezione si crea un'app console Node.js che risponde a un metodo diretto chiamato dal cloud, che attiva un riavvio del dispositivo simulato e usa le proprietà segnalate per abilitare le query del dispositivo gemello che consentono di identificare i dispositivi e di sapere quando sono stati riavviati l'ultima volta.</span><span class="sxs-lookup"><span data-stu-id="684bf-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="684bf-129">Creare una nuova cartella vuota chiamata **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="684bf-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="684bf-130">Nella cartella **simDevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="684bf-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="684bf-131">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="684bf-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="684bf-132">Eseguire questo comando al prompt dei comandi nella cartella **simDevice** per installare il pacchetto SDK per dispositivi **azure-iot-device** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="684bf-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="684bf-133">Con un editor di testo creare un nuovo file **simDevice.js** nella cartella **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="684bf-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="684bf-134">Aggiungere le istruzioni "require" seguenti all'inizio del file **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="684bf-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="684bf-135">Aggiungere una variabile **connectionString** e usarla per creare un'istanza **Client**.</span><span class="sxs-lookup"><span data-stu-id="684bf-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="684bf-136">Aggiungere la funzione seguente per gestire il metodo **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="684bf-136">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="684bf-137">Aggiungere il codice seguente per registrare il gestore per il metodo **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="684bf-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="684bf-138">Salvare e chiudere il file **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="684bf-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="684bf-139">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="684bf-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="684bf-140">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="684bf-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="684bf-141">Pianificare i processi per chiamare un metodo diretto e aggiornare le proprietà dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="684bf-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="684bf-142">In questa sezione si creerà un'app console Node.js che avvia un **lockDoor** remoto su un dispositivo usando un metodo diretto e verranno aggiornate le proprietà del dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="684bf-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="684bf-143">Creare una nuova cartella vuota chiamata **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="684bf-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="684bf-144">Nella cartella **scheduleJobService** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="684bf-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="684bf-145">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="684bf-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="684bf-146">Eseguire questo comando al prompt dei comandi nella cartella **scheduleJobService** per installare il pacchetto SDK per dispositivi **azure-iothub** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="684bf-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="684bf-147">Usando un editor di testo, creare un nuovo file **scheduleJobService.js** nella cartella **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="684bf-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="684bf-148">Aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_gscheduleJobServiceetstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="684bf-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="684bf-149">Aggiungere le dichiarazioni di variabile seguenti e sostituire i valori segnaposto:</span><span class="sxs-lookup"><span data-stu-id="684bf-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="684bf-150">Aggiungere la funzione seguente che verrà usata per monitorare l'esecuzione del processo:</span><span class="sxs-lookup"><span data-stu-id="684bf-150">Add the following function that will be used to monitor the execution of the job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="684bf-151">Aggiungere il codice seguente per pianificare il processo che chiama il metodo del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="684bf-151">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="684bf-152">Aggiungere il codice seguente per pianificare il processo che aggiorna il dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="684bf-152">Add the following code to schedule the job to update the device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="684bf-153">Salvare e chiudere il file **scheduleJobService.js**.</span><span class="sxs-lookup"><span data-stu-id="684bf-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="684bf-154">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="684bf-154">Run the applications</span></span>
<span data-ttu-id="684bf-155">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="684bf-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="684bf-156">Al prompt dei comandi nella cartella **simDevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="684bf-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="684bf-157">Eseguire il comando riportato di seguito al prompt dei comandi nella cartella **scheduleJobService** per attivare i processi per bloccare la porta e aggiornare il dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="684bf-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="684bf-158">Nella console viene visualizzata la risposta del dispositivo al metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="684bf-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="684bf-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="684bf-159">Next steps</span></span>
<span data-ttu-id="684bf-160">In questa esercitazione è stato usato un processo per pianificare un metodo diretto in un dispositivo e aggiornare le proprietà di un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="684bf-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="684bf-161">Per altre informazioni sull'hub IoT e sui modelli di gestione dei dispositivi, ad esempio in modalità remota tramite l'aggiornamento del firmware air, vedere:</span><span class="sxs-lookup"><span data-stu-id="684bf-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="684bf-162">[Esercitazione: Come eseguire un aggiornamento del firmware][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="684bf-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="684bf-163">Per altre informazioni sulle attività iniziali con l'hub IoT, vedere [Introduzione a IoT Edge di Azure][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="684bf-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
