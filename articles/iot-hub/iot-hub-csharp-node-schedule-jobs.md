---
title: Pianificare processi con l'hub IoT di Azure (.NET/Node) | Microsoft Docs
description: "Come pianificare un processo dell'hub IoT di Azure per richiamare un metodo diretto su più dispositivi. Usare Azure IoT SDK per dispositivi per Node.js per implementare app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che esegue il processo."
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
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="b4604-104">Pianificare e trasmettere processi (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="b4604-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="b4604-105">Usare l'hub IoT per pianificare e tenere traccia dei processi che aggiornano milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4604-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="b4604-106">Usare i processi per:</span><span class="sxs-lookup"><span data-stu-id="b4604-106">Use jobs to:</span></span>

* <span data-ttu-id="b4604-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="b4604-107">Update desired properties</span></span>
* <span data-ttu-id="b4604-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="b4604-108">Update tags</span></span>
* <span data-ttu-id="b4604-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="b4604-109">Invoke direct methods</span></span>

<span data-ttu-id="b4604-110">Un processo esegue il wrapping di una di queste azioni e tiene traccia dell'esecuzione rispetto a un set di dispositivi, definito da una query su dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="b4604-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="b4604-111">Ad esempio, un'applicazione back-end può usare un processo per chiamare un metodo diretto su 10.000 dispositivi che riavvia i dispositivi stessi.</span><span class="sxs-lookup"><span data-stu-id="b4604-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="b4604-112">È necessario specificare il set di dispositivi con una query di dispositivi gemelli e pianificare il processo in modo che venga eseguito in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b4604-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="b4604-113">L'applicazione può quindi tenere traccia dell'avanzamento mentre ognuno dei dispositivi riceve ed esegue il metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="b4604-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="b4604-114">Per altre informazioni su queste funzionalità, vedere:</span><span class="sxs-lookup"><span data-stu-id="b4604-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="b4604-115">Dispositivi gemelli e proprietà: [Introduzione ai dispositivi gemelli][lnk-get-started-twin] ed [Esercitazione: Come usare le proprietà dei dispositivi gemelli][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="b4604-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="b4604-116">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Usare metodi diretti][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="b4604-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="b4604-117">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="b4604-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b4604-118">Creare un'app per dispositivi che implementa un metodo diretto denominato **lockDoor** che può essere chiamato dall'app back-end.</span><span class="sxs-lookup"><span data-stu-id="b4604-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="b4604-119">L'app per dispositivi riceve anche le modifiche di proprietà desiderate dall'app back-end.</span><span class="sxs-lookup"><span data-stu-id="b4604-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="b4604-120">Creare un'app back-end che crea un processo per chiamare il metodo diretto **lockDoor** su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4604-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="b4604-121">Un altro processo invia gli aggiornamenti di proprietà desiderati a più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4604-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="b4604-122">Al termine dell'esercitazione saranno disponibili un'app per il dispositivo console Node.js e un'app back-end console .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="b4604-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="b4604-123">**simDevice.js** che si connette all'hub IoT, implementa il metodo diretto **lockDoor** e gestisce le modifiche di proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="b4604-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="b4604-124">**ScheduleJob** che usa i processi per chiamare il metodo diretto **lockDoor** e aggiornare le proprietà di dispositivi gemelli desiderate su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4604-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="b4604-125">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b4604-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b4604-126">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b4604-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b4604-127">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b4604-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="b4604-128">L'articolo [Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b4604-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b4604-129">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b4604-129">An active Azure account.</span></span> <span data-ttu-id="b4604-130">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b4604-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="b4604-131">Pianificare i processi per chiamare un metodo diretto e inviare gli aggiornamenti dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="b4604-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="b4604-132">In questa sezione si crea un'app console .NET (usando C#) che usa i processi per chiamare il metodo diretto **lockDoor** e inviare gli aggiornamenti di proprietà desiderati a più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4604-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="b4604-133">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="b4604-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="b4604-134">Assegnare al progetto il nome **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="b4604-134">Name the project **ScheduleJob**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. <span data-ttu-id="b4604-136">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **ScheduleJob** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b4604-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="b4604-137">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="b4604-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="b4604-138">Questa procedura scarica, installa e aggiunge un riferimento al pacchetto NuGet [Azure IoT SDK per servizi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b4604-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="b4604-140">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="b4604-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="b4604-141">Aggiungere l'istruzione `using` seguente se non è già presente nelle istruzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="b4604-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="b4604-142">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="b4604-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="b4604-143">Sostituire il segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="b4604-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="b4604-144">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="b4604-144">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="b4604-145">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="b4604-145">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="b4604-146">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="b4604-146">Add the following method to the **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="b4604-147">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="b4604-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="b4604-148">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che **Azione** per il progetto **ScheduleJob** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="b4604-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="b4604-149">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b4604-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b4604-150">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="b4604-150">Create a simulated device app</span></span>

<span data-ttu-id="b4604-151">In questa sezione si crea un'app console Node.js che risponde a un metodo diretto chiamato dal cloud, che attiva un riavvio del dispositivo simulato e usa le proprietà segnalate per abilitare le query del dispositivo gemello che consentono di identificare i dispositivi e di sapere quando sono stati riavviati l'ultima volta.</span><span class="sxs-lookup"><span data-stu-id="b4604-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="b4604-152">Creare una nuova cartella vuota chiamata **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="b4604-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="b4604-153">Nella cartella **simDevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b4604-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="b4604-154">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="b4604-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="b4604-155">Al prompt dei comandi nella cartella **simDevice** digitare il comando seguente per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="b4604-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="b4604-156">Con un editor di testo creare un nuovo file **simDevice.js** nella cartella **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="b4604-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="b4604-157">Aggiungere le istruzioni "require" seguenti all'inizio del file **simDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="b4604-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="b4604-158">Aggiungere una variabile **connectionString** e usarla per creare un'istanza **Client**.</span><span class="sxs-lookup"><span data-stu-id="b4604-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="b4604-159">Assicurarsi di sostituire i segnaposto con valori appropriati per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="b4604-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="b4604-160">Aggiungere la funzione seguente per gestire il metodo **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="b4604-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
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

1. <span data-ttu-id="b4604-161">Aggiungere il codice seguente per registrare il gestore per il metodo **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="b4604-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="b4604-162">Salvare e chiudere il file **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="b4604-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b4604-163">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="b4604-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b4604-164">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="b4604-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="b4604-165">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="b4604-165">Run the apps</span></span>

<span data-ttu-id="b4604-166">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="b4604-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="b4604-167">Al prompt dei comandi nella cartella **simDevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="b4604-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="b4604-168">Eseguire l'app console C# **ScheduleJob** facendo clic con il pulsante destro del mouse sul progetto **ScheduleJob**, quindi selezionando **Debug** e **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="b4604-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="b4604-169">L'output viene visualizzato sia dal dispositivo che dalle app back-end.</span><span class="sxs-lookup"><span data-stu-id="b4604-169">You see the output from both device and back-end apps.</span></span>

    ![Eseguire le app per pianificare i processi][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="b4604-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4604-171">Next steps</span></span>

<span data-ttu-id="b4604-172">In questa esercitazione è stato usato un processo per pianificare un metodo diretto in un dispositivo e aggiornare le proprietà di un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="b4604-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="b4604-173">Per altre informazioni sull'hub IoT e sui modelli di gestione dei dispositivi, ad esempio in modalità remota tramite l'aggiornamento del firmware air, vedere [Esercitazione: Come eseguire un aggiornamento del firmware][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="b4604-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="b4604-174">Per altre informazioni sulle attività iniziali con l'hub IoT, vedere [Getting started with IoT Edge][lnk-iot-edge] (Introduzione a IoT Edge).</span><span class="sxs-lookup"><span data-stu-id="b4604-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
