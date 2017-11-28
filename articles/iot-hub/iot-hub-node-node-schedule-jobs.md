---
title: i processi di aaaSchedule con IoT Hub di Azure (nodo) | Documenti Microsoft
description: "Un IoT Hub Azure tooschedule come processo tooinvoke un metodo diretto su più dispositivi. Utilizzare hello Azure IoT SDK per Node.js tooimplement hello simulato dispositivo App e un processo del servizio app toorun hello."
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
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="8c237-104">Pianificare e trasmettere processi (Node)</span><span class="sxs-lookup"><span data-stu-id="8c237-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="8c237-105">IoT Hub Azure è un servizio completamente gestito che consente un toocreate app back-end e i processi di traccia di pianificare e aggiornare milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8c237-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="8c237-106">I processi possono essere utilizzati per hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="8c237-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="8c237-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="8c237-107">Update desired properties</span></span>
* <span data-ttu-id="8c237-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="8c237-108">Update tags</span></span>
* <span data-ttu-id="8c237-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="8c237-109">Invoke direct methods</span></span>

<span data-ttu-id="8c237-110">Concettualmente, un processo esegue il wrapping di una di queste azioni e tracce hello lo stato di avanzamento dell'esecuzione rispetto a un set di dispositivi, definito da una query di due dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8c237-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="8c237-111">Ad esempio, un'applicazione back-end può utilizzare tooinvoke un processo un metodo di riavvio su 10.000 dispositivi, specificato da una query di due dispositivi e pianificata in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8c237-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="8c237-112">L'applicazione può quindi avanzamento come ognuno di questi dispositivi di ricezione ed eseguire il metodo di riavvio hello.</span><span class="sxs-lookup"><span data-stu-id="8c237-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="8c237-113">Altre informazioni su queste funzionalità sono disponibili in questi articoli:</span><span class="sxs-lookup"><span data-stu-id="8c237-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="8c237-114">Proprietà e un doppio dispositivo: [introduzione gemelli dispositivo] [ lnk-get-started-twin] e [esercitazione: come dispositivo toouse doppio proprietà][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="8c237-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="8c237-115">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Metodi diretti][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="8c237-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="8c237-116">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="8c237-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8c237-117">Creare un'app dispositivo simulato che dispone di un metodo diretto, che consente di **lockDoor** che può essere chiamato da hello soluzione back-end.</span><span class="sxs-lookup"><span data-stu-id="8c237-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="8c237-118">Creare un'applicazione console in Node.js tale hello chiamate **lockDoor** dirette del metodo nell'app dispositivo simulato hello utilizzando un processo e gli aggiornamenti di hello desiderato utilizzando un processo di dispositivi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="8c237-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="8c237-119">Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="8c237-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="8c237-120">**simDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello e riceve un **lockDoor** metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="8c237-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="8c237-121">**scheduleJobService.js**, che chiama un metodo diretto in hello dispositivo simulato app e aggiornamento hello il dispositivo di proprietà di un doppio desiderate tramite un processo.</span><span class="sxs-lookup"><span data-stu-id="8c237-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="8c237-122">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c237-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8c237-123">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8c237-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="8c237-124">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="8c237-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8c237-125">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="8c237-125">An active Azure account.</span></span> <span data-ttu-id="8c237-126">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8c237-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8c237-127">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="8c237-127">Create a simulated device app</span></span>
<span data-ttu-id="8c237-128">In questa sezione si crea un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello, che attiva un riavvio del dispositivo simulato e utilizza hello segnalato proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato.</span><span class="sxs-lookup"><span data-stu-id="8c237-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="8c237-129">Creare una nuova cartella vuota chiamata **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="8c237-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="8c237-130">In hello **simDevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8c237-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="8c237-131">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="8c237-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8c237-132">Al prompt dei comandi in hello **simDevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **mqtt azure-iot-dispositivo** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="8c237-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="8c237-133">Utilizzando un editor di testo, creare un nuovo **simDevice.js** file hello **simDevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="8c237-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="8c237-134">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **simDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="8c237-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="8c237-135">Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="8c237-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="8c237-136">Aggiungere i seguenti hello toohandle funzione hello **lockDoor** metodo.</span><span class="sxs-lookup"><span data-stu-id="8c237-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="8c237-137">Aggiungere hello seguente gestore hello tooregister del codice per hello **lockDoor** metodo.</span><span class="sxs-lookup"><span data-stu-id="8c237-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="8c237-138">Salvare e chiudere hello **simDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="8c237-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="8c237-139">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="8c237-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8c237-140">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="8c237-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="8c237-141">Pianificare i processi per chiamare un metodo diretto e aggiornare le proprietà dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="8c237-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="8c237-142">In questa sezione si crea un'applicazione console Node. js che avvia un remoto **lockDoor** in un dispositivo utilizzando le proprietà di un diretto (metodo) e aggiornamento hello dispositivo doppi.</span><span class="sxs-lookup"><span data-stu-id="8c237-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="8c237-143">Creare una nuova cartella vuota chiamata **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="8c237-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="8c237-144">In hello **scheduleJobService** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8c237-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="8c237-145">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="8c237-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8c237-146">Al prompt dei comandi in hello **scheduleJobService** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="8c237-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="8c237-147">Utilizzando un editor di testo, creare un nuovo **scheduleJobService.js** file hello **scheduleJobService** cartella.</span><span class="sxs-lookup"><span data-stu-id="8c237-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="8c237-148">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="8c237-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="8c237-149">Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:</span><span class="sxs-lookup"><span data-stu-id="8c237-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="8c237-150">Aggiungere hello seguente una funzione che sarà utilizzato toomonitor hello esecuzione del processo di hello:</span><span class="sxs-lookup"><span data-stu-id="8c237-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
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
7. <span data-ttu-id="8c237-151">Aggiungere i seguenti processi di hello tooschedule codice che chiama il metodo di dispositivo hello hello:</span><span class="sxs-lookup"><span data-stu-id="8c237-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
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
8. <span data-ttu-id="8c237-152">Aggiungere hello gemelli di codice tooschedule hello processo tooupdate hello dispositivo seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c237-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
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
9. <span data-ttu-id="8c237-153">Salvare e chiudere hello **scheduleJobService.js** file.</span><span class="sxs-lookup"><span data-stu-id="8c237-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="8c237-154">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="8c237-154">Run hello applications</span></span>
<span data-ttu-id="8c237-155">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="8c237-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="8c237-156">Al prompt dei comandi di hello in hello **simDevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="8c237-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="8c237-157">Al prompt dei comandi di hello in hello **scheduleJobService** cartella, eseguire hello successivo comando tootrigger hello processi toolock hello porta e l'aggiornamento hello doppi</span><span class="sxs-lookup"><span data-stu-id="8c237-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="8c237-158">Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="8c237-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c237-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c237-159">Next steps</span></span>
<span data-ttu-id="8c237-160">In questa esercitazione è stato utilizzato un processo tooschedule un dispositivo tooa dirette del metodo e l'aggiornamento di hello delle proprietà del doppi dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8c237-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="8c237-161">toocontinue introduzione IoT Hub e modelli di gestione di dispositivi, ad esempio remoto tramite l'aggiornamento del firmware di hello air, vedere:</span><span class="sxs-lookup"><span data-stu-id="8c237-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="8c237-162">[Esercitazione: Come toodo un aggiornamento firmware][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="8c237-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="8c237-163">Introduzione a IoT Hub, toocontinue vedere [Introduzione a Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="8c237-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
