---
title: Introduzione alla gestione dei dispositivi dell'hub IoT di Azure (.NET/Node) | Documentazione Microsoft
description: Come usare la gestione dei dispositivi dell'hub IoT di Azure per riavviare un dispositivo remoto. Usare Azure IoT SDK per dispositivi per Node.js per implementare un'app per dispositivo simulato che include un metodo diretto e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che richiama il metodo diretto.
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
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="2f9ed-104">Introduzione alla gestione dei dispositivi (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="2f9ed-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2f9ed-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2f9ed-106">Creare un hub IoT nel portale di Azure e un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2f9ed-107">Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="2f9ed-108">I metodi diretti vengono richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="2f9ed-109">Creare un'app console .NET che chiama il metodo diretto di riavvio nell'app per dispositivo simulato tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="2f9ed-110">Al termine dell'esercitazione saranno disponibili un'app per il dispositivo console Node.js e un'app back-end console .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="2f9ed-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="2f9ed-111">**dmpatterns_getstarted_device.js**, che si connette all'hub IoT con l'identità del dispositivo creata in precedenza, riceve un metodo diretto per il riavvio, simula un riavvio fisico e segnala il tempo impiegato per l'ultimo riavvio.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="2f9ed-112">**TriggerReboot**, che chiama un metodo diretto nell'app per dispositivo simulato, visualizza la risposta e le proprietà segnalate aggiornate.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="2f9ed-113">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2f9ed-114">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2f9ed-115">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2f9ed-116">[Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2f9ed-117">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-117">An active Azure account.</span></span> <span data-ttu-id="2f9ed-118">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="2f9ed-119">Attivare un riavvio remoto nel dispositivo con un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="2f9ed-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="2f9ed-120">In questa sezione viene creata un'app console .NET (tramite C#) che attiva un riavvio remoto su un dispositivo usando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="2f9ed-121">L'app esegue query sul dispositivo gemello per ottenere l'ora dell'ultimo riavvio per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="2f9ed-122">In Visual Studio aggiungere un progetto desktop classico di Windows Visual C# a una nuova soluzione usando il modello di progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="2f9ed-123">Verificare che la versione di .NET Framework sia 4.5.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="2f9ed-124">Assegnare al progetto il nome **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-124">Name the project **TriggerReboot**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

2. <span data-ttu-id="2f9ed-126">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **TriggerReboot** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="2f9ed-127">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="2f9ed-128">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
4. <span data-ttu-id="2f9ed-130">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="2f9ed-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="2f9ed-131">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="2f9ed-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="2f9ed-132">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente e il dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="2f9ed-133">Aggiungere il metodo seguente alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="2f9ed-134">Questo codice ottiene il dispositivo gemello per il dispositivo in fase di riavvio e restituisce le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="2f9ed-135">Aggiungere il metodo seguente alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="2f9ed-136">Il codice attiva il riavvio nel dispositivo usando un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="2f9ed-137">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="2f9ed-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="2f9ed-138">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2f9ed-139">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="2f9ed-139">Create a simulated device app</span></span>
<span data-ttu-id="2f9ed-140">Questa sezione consente di:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-140">In this section, you will</span></span>

* <span data-ttu-id="2f9ed-141">Creare un'app console Node.js che risponde a un metodo diretto chiamato dal cloud</span><span class="sxs-lookup"><span data-stu-id="2f9ed-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="2f9ed-142">Attivare un riavvio del dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="2f9ed-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="2f9ed-143">Usare le proprietà segnalate per abilitare le query nei dispositivi gemelli in modo da identificare i dispositivi e l'ora dell'ultimo riavvio</span><span class="sxs-lookup"><span data-stu-id="2f9ed-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="2f9ed-144">Creare una nuova cartella vuota denominata **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="2f9ed-145">Nella cartella **manageddevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="2f9ed-146">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2f9ed-147">Eseguire questo comando al prompt dei comandi nella cartella **manageddevice** per installare il pacchetto SDK per dispositivi **azure-iot-device** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2f9ed-148">Con un editor di testo creare un nuovo file **dmpatterns_getstarted_device.js** nella cartella **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="2f9ed-149">Aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_getstarted_device.js**:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2f9ed-150">Aggiungere una variabile **connectionString** e usarla per creare un'istanza **Client**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="2f9ed-151">Sostituire la stringa di connessione con la stringa di connessione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2f9ed-152">Aggiungere la funzione seguente per implementare il metodo diretto nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="2f9ed-152">Add the following function to implement the direct method on the device</span></span>
   
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
7. <span data-ttu-id="2f9ed-153">Aggiungere il codice seguente per aprire la connessione all'hub IoT e avviare il listener del metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="2f9ed-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="2f9ed-154">Salvare e chiudere il file **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="2f9ed-155">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2f9ed-156">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="2f9ed-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="2f9ed-157">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="2f9ed-157">Run the apps</span></span>
<span data-ttu-id="2f9ed-158">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="2f9ed-159">Al prompt dei comandi nella cartella **manageddevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="2f9ed-160">Eseguire l'app console C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="2f9ed-161">Fare clic con il pulsante destro del mouse sul progetto **TriggerReboot**, scegliere **Debug** e quindi selezionare **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="2f9ed-162">Nella console viene visualizzata la risposta del dispositivo al metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="2f9ed-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/