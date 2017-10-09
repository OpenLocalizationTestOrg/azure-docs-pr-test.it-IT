---
title: i processi di aaaSchedule con IoT Hub di Azure (.NET/nodo) | Documenti Microsoft
description: "Un IoT Hub Azure tooschedule come processo tooinvoke un metodo diretto su più dispositivi. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement hello simulato dispositivo App e servizi IoT di Azure SDK per .NET tooimplement un processo del servizio app toorun hello hello."
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
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="67ad4-104">Pianificare e trasmettere processi (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="67ad4-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="67ad4-105">Utilizzare i processi tooschedule e tenere traccia IoT Hub di Azure che aggiornano milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="67ad4-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="67ad4-106">Usare i processi per:</span><span class="sxs-lookup"><span data-stu-id="67ad4-106">Use jobs to:</span></span>

* <span data-ttu-id="67ad4-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="67ad4-107">Update desired properties</span></span>
* <span data-ttu-id="67ad4-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="67ad4-108">Update tags</span></span>
* <span data-ttu-id="67ad4-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="67ad4-109">Invoke direct methods</span></span>

<span data-ttu-id="67ad4-110">Un processo esegue il wrapping di una di queste azioni e le tracce hello esecuzione rispetto a un set di dispositivi che è definito da una query di due dispositivi.</span><span class="sxs-lookup"><span data-stu-id="67ad4-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="67ad4-111">Ad esempio, un'applicazione back-end è possibile utilizzare un tooinvoke processo un metodo diretto su 10.000 dispositivi che si riavvia dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="67ad4-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="67ad4-112">È necessario specifica il set di hello di dispositivi con una query di due dispositivi e pianificare toorun processo hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="67ad4-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="67ad4-113">avanzamento tiene traccia del processo Hello come tutti i dispositivi di hello di ricezione ed eseguire hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="67ad4-114">toolearn informazioni su ciascuna di queste funzionalità, vedere:</span><span class="sxs-lookup"><span data-stu-id="67ad4-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="67ad4-115">Proprietà e un doppio dispositivo: [introduzione gemelli dispositivo] [ lnk-get-started-twin] e [esercitazione: come dispositivo toouse doppio proprietà][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="67ad4-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="67ad4-116">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Usare metodi diretti][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="67ad4-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="67ad4-117">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="67ad4-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="67ad4-118">Creare un'app di dispositivo che implementa un metodo diretto denominato **lockDoor** che può essere chiamato da app back-end hello.</span><span class="sxs-lookup"><span data-stu-id="67ad4-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="67ad4-119">Hello dispositivo app riceve inoltre le modifiche alle proprietà desiderato dai hello back-end app.</span><span class="sxs-lookup"><span data-stu-id="67ad4-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="67ad4-120">Creare un'applicazione back-end che crea un hello toocall processo **lockDoor** metodo diretto su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="67ad4-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="67ad4-121">Un altro processo invia proprietà desiderata Aggiorna dispositivi toomultiple.</span><span class="sxs-lookup"><span data-stu-id="67ad4-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="67ad4-122">Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="67ad4-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="67ad4-123">**simDevice.js** che connette l'hub IoT tooyour, implementa hello **lockDoor** indirizzare lo si desidera metodo e gestisce le modifiche alle proprietà.</span><span class="sxs-lookup"><span data-stu-id="67ad4-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="67ad4-124">**ScheduleJob** che utilizza hello toocall processi **lockDoor** diretto (metodo) e aggiornamento hello dispositivo doppi desiderato proprietà su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="67ad4-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="67ad4-125">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="67ad4-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="67ad4-126">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="67ad4-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="67ad4-127">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="67ad4-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="67ad4-128">articolo Hello [preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="67ad4-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="67ad4-129">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-129">An active Azure account.</span></span> <span data-ttu-id="67ad4-130">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="67ad4-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="67ad4-131">Pianificare i processi per chiamare un metodo diretto e inviare gli aggiornamenti dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="67ad4-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="67ad4-132">In questa sezione si crea una .NET console app (usando c#) che utilizza hello toocall processi **lockDoor** metodo diretto e inviare proprietà desiderata Aggiorna dispositivi toomultiple.</span><span class="sxs-lookup"><span data-stu-id="67ad4-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="67ad4-133">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="67ad4-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="67ad4-134">Progetto hello nome **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="67ad4-134">Name hello project **ScheduleJob**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. <span data-ttu-id="67ad4-136">In Esplora soluzioni fare doppio clic su hello **ScheduleJob** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="67ad4-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="67ad4-137">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="67ad4-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="67ad4-138">Questo passaggio Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="67ad4-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="67ad4-140">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="67ad4-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="67ad4-141">Aggiungere il seguente hello `using` istruzione se non è già presente nelle istruzioni di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="67ad4-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="67ad4-142">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="67ad4-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="67ad4-143">Sostituire i segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="67ad4-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="67ad4-144">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="67ad4-144">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="67ad4-145">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="67ad4-145">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="67ad4-146">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="67ad4-146">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="67ad4-147">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="67ad4-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="67ad4-148">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **ScheduleJob** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="67ad4-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="67ad4-149">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="67ad4-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="67ad4-150">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="67ad4-150">Create a simulated device app</span></span>

<span data-ttu-id="67ad4-151">In questa sezione si crea un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello, che attiva un riavvio del dispositivo simulato e utilizza hello segnalato proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato.</span><span class="sxs-lookup"><span data-stu-id="67ad4-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="67ad4-152">Creare una nuova cartella vuota chiamata **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="67ad4-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="67ad4-153">In hello **simDevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="67ad4-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="67ad4-154">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="67ad4-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="67ad4-155">Al prompt dei comandi in hello **simDevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** pacchetti:</span><span class="sxs-lookup"><span data-stu-id="67ad4-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="67ad4-156">Utilizzando un editor di testo, creare un nuovo **simDevice.js** file hello **simDevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="67ad4-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="67ad4-157">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **simDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="67ad4-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="67ad4-158">Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="67ad4-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="67ad4-159">Verificare i segnaposto hello tooreplace che con il programma di installazione di valori tooyour appropriato.</span><span class="sxs-lookup"><span data-stu-id="67ad4-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="67ad4-160">Aggiungere i seguenti hello toohandle funzione hello **lockDoor** metodo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
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

1. <span data-ttu-id="67ad4-161">Aggiungere hello seguente gestore hello tooregister del codice per hello **lockDoor** metodo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="67ad4-162">Salvare e chiudere hello **simDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="67ad4-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="67ad4-163">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="67ad4-164">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="67ad4-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="67ad4-165">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="67ad4-165">Run hello apps</span></span>

<span data-ttu-id="67ad4-166">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="67ad4-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="67ad4-167">Al prompt dei comandi di hello in hello **simDevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="67ad4-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="67ad4-168">Applicazione console in esecuzione hello c# **ScheduleJob** facendo clic su hello **ScheduleJob** progetto, quindi selezionando **Debug** e **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="67ad4-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="67ad4-169">Viene visualizzato l'output di hello dal dispositivo e le applicazioni back-end.</span><span class="sxs-lookup"><span data-stu-id="67ad4-169">You see hello output from both device and back-end apps.</span></span>

    ![Eseguire app di hello tooschedule processi][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="67ad4-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67ad4-171">Next steps</span></span>

<span data-ttu-id="67ad4-172">In questa esercitazione è stato utilizzato un processo tooschedule un dispositivo tooa dirette del metodo e l'aggiornamento di hello delle proprietà del doppi dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="67ad4-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="67ad4-173">Guida introduttiva a modelli di gestione di IoT Hub e dispositivo, ad esempio remoto tramite l'aggiornamento del firmware di hello air, leggere toocontinue [esercitazione: come toodo un firmware aggiornare][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="67ad4-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="67ad4-174">Introduzione a IoT Hub, toocontinue vedere [Guida introduttiva a bordo IoT][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="67ad4-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
