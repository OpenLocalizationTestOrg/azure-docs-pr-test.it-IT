---
title: aaaGet avviato con la gestione dei dispositivi Azure IoT Hub (.NET/nodo) | Documenti Microsoft
description: Come tooinitiate di gestione dispositivi Azure IoT Hub toouse un dispositivo remoto riavviare il computer. Usare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="d4d47-104">Introduzione alla gestione dei dispositivi (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="d4d47-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="d4d47-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="d4d47-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d4d47-106">Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d4d47-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="d4d47-107">Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="d4d47-108">Diretti metodi vengono richiamati dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d4d47-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="d4d47-109">Creare un'applicazione console .NET che chiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d4d47-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="d4d47-110">Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="d4d47-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="d4d47-111">**dmpatterns_getstarted_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto di riavvio, simula riavviare il computer fisico e segnala il tempo di hello per ultimo riavvio hello.</span><span class="sxs-lookup"><span data-stu-id="d4d47-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="d4d47-112">**TriggerReboot**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza risposta hello e consente di visualizzare hello aggiornato segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="d4d47-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="d4d47-113">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4d47-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d4d47-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d4d47-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d4d47-115">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d4d47-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="d4d47-116">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d4d47-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d4d47-117">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-117">An active Azure account.</span></span> <span data-ttu-id="d4d47-118">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d4d47-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="d4d47-119">Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="d4d47-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="d4d47-120">In questa sezione viene creata un'app console .NET (tramite C#) che attiva un riavvio remoto su un dispositivo usando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="d4d47-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="d4d47-121">app Hello utilizza hello toodiscover di query doppi dispositivo ora dell'ultimo riavvio del sistema per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="d4d47-122">In Visual Studio, aggiungere una nuova soluzione tooa progetto Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="d4d47-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d4d47-123">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d4d47-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d4d47-124">Progetto hello nome **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="d4d47-124">Name hello project **TriggerReboot**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

2. <span data-ttu-id="d4d47-126">In Esplora soluzioni fare doppio clic su hello **TriggerReboot** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d4d47-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="d4d47-127">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="d4d47-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d4d47-128">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d4d47-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
4. <span data-ttu-id="d4d47-130">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="d4d47-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="d4d47-131">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="d4d47-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d4d47-132">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello e dispositivo di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="d4d47-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="d4d47-133">Aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="d4d47-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="d4d47-134">Questo dispositivo gemelli di codice ottiene hello per il riavvio di dispositivo e l'output di hello hello segnalato proprietà.</span><span class="sxs-lookup"><span data-stu-id="d4d47-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="d4d47-135">Aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="d4d47-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="d4d47-136">Questo codice avvia il riavvio di hello sul dispositivo hello utilizzando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="d4d47-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="d4d47-137">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="d4d47-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="d4d47-138">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="d4d47-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d4d47-139">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="d4d47-139">Create a simulated device app</span></span>
<span data-ttu-id="d4d47-140">Questa sezione consente di:</span><span class="sxs-lookup"><span data-stu-id="d4d47-140">In this section, you will</span></span>

* <span data-ttu-id="d4d47-141">Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello</span><span class="sxs-lookup"><span data-stu-id="d4d47-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="d4d47-142">Attivare un riavvio del dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="d4d47-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="d4d47-143">Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato</span><span class="sxs-lookup"><span data-stu-id="d4d47-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="d4d47-144">Creare una nuova cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="d4d47-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="d4d47-145">In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="d4d47-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d4d47-146">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="d4d47-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d4d47-147">Al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="d4d47-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d4d47-148">Utilizzando un editor di testo, creare un nuovo **dmpatterns_getstarted_device.js** file hello **manageddevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="d4d47-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="d4d47-149">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_device.js** file:</span><span class="sxs-lookup"><span data-stu-id="d4d47-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="d4d47-150">Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="d4d47-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="d4d47-151">Sostituire la stringa di connessione hello con la stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="d4d47-152">Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="d4d47-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="d4d47-153">Aggiungere i seguenti hello l'hub IoT tooopen hello connessione tooyour del codice e avviare il listener di un metodo diretto hello:</span><span class="sxs-lookup"><span data-stu-id="d4d47-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="d4d47-154">Salvare e chiudere hello **dmpatterns_getstarted_device.js** file.</span><span class="sxs-lookup"><span data-stu-id="d4d47-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="d4d47-155">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d4d47-156">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d4d47-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="d4d47-157">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="d4d47-157">Run hello apps</span></span>
<span data-ttu-id="d4d47-158">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="d4d47-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d4d47-159">Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="d4d47-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="d4d47-160">Applicazione console in esecuzione hello c# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="d4d47-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="d4d47-161">Pulsante destro del mouse hello **TriggerReboot** progetto, selezionare **Debug**, quindi selezionare **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="d4d47-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="d4d47-162">Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="d4d47-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/