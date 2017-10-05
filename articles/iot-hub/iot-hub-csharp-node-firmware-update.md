---
title: Aggiornamento firmware del dispositivo con l'hub IoT di Azure (.NET/Node) | Documentazione Microsoft
description: Come usare la gestione dei dispositivi nell'hub IoT di Azure per avviare un aggiornamento del firmware del dispositivo. Usare Azure IoT SDK per dispositivi per Node.js per implementare un'app per dispositivo simulato e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che attiva l'aggiornamento del firmware.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="eede1-104">Usare la gestione dei dispositivi per avviare un aggiornamento del firmware del dispositivo (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="eede1-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="eede1-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="eede1-105">Introduction</span></span>
<span data-ttu-id="eede1-106">Nell'esercitazione [Introduzione alla gestione dei dispositivi][lnk-dm-getstarted] è stato illustrato come usare il [dispositivo gemello][lnk-devtwin] e le primitive dei [metodi diretti][lnk-c2dmethod] per riavviare un dispositivo in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="eede1-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="eede1-107">Questa esercitazione usa le stesse primitive dell'hub IoT e illustra come eseguire un aggiornamento del firmware simulato completo.</span><span class="sxs-lookup"><span data-stu-id="eede1-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="eede1-108">Questo modello viene usato nell'implementazione dell'aggiornamento del firmware per l'[esempio di implementazione del dispositivo Raspberry Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="eede1-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="eede1-109">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="eede1-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="eede1-110">Creare un'app console .NET che chiama il metodo diretto firmwareUpdate nell'app per dispositivo simulato tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="eede1-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="eede1-111">Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="eede1-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="eede1-112">Questo metodo avvia un processo in più fasi che attende di scaricare l'immagine del firmware, quindi la scarica e infine la applica.</span><span class="sxs-lookup"><span data-stu-id="eede1-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="eede1-113">Durante l'esecuzione di ogni fase, il dispositivo usa le proprietà segnalate per aggiornare lo stato.</span><span class="sxs-lookup"><span data-stu-id="eede1-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="eede1-114">Al termine dell'esercitazione saranno disponibili un'app per il dispositivo console Node.js e un'app back-end console .NET (C#):</span><span class="sxs-lookup"><span data-stu-id="eede1-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="eede1-115">**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto nell'app per dispositivo simulato, visualizza la risposta e visualizza regolarmente (ogni 500 ms) le proprietà segnalate aggiornate.</span><span class="sxs-lookup"><span data-stu-id="eede1-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="eede1-116">**TriggerFWUpdate**, che connette all'hub IoT con l'identità del dispositivo creata prima, riceve un metodo diretto firmwareUpdate, esegue un processo in più stati per simulare un aggiornamento del firmware, inclusi l'attesa del download dell'immagine, il download della nuova immagine e infine l'applicazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="eede1-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="eede1-117">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eede1-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="eede1-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="eede1-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="eede1-119">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="eede1-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="eede1-120">[Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="eede1-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="eede1-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="eede1-121">An active Azure account.</span></span> <span data-ttu-id="eede1-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="eede1-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="eede1-123">Vedere l'articolo [Introduzione alla gestione dei dispositivi](iot-hub-csharp-node-device-management-get-started.md) per creare l'hub IoT e ottenere la stringa di connessione relativa.</span><span class="sxs-lookup"><span data-stu-id="eede1-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="eede1-124">Attivare un aggiornamento del firmware remoto nel dispositivo con un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="eede1-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="eede1-125">In questa sezione viene creata un'app console .NET (tramite C#) che avvia un aggiornamento del firmware remoto in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eede1-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="eede1-126">L'applicazione usa un metodo diretto per avviare l'aggiornamento e usa le query di dispositivo gemello per ottenere periodicamente lo stato di aggiornamento del firmware attivo.</span><span class="sxs-lookup"><span data-stu-id="eede1-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="eede1-127">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="eede1-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="eede1-128">Assegnare al progetto il nome **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="eede1-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. <span data-ttu-id="eede1-130">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **TriggerFWUpdate** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eede1-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="eede1-131">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="eede1-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="eede1-132">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="eede1-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="eede1-134">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="eede1-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="eede1-135">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="eede1-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="eede1-136">Sostituire il valore dei segnaposti multipli con la stringa di connessione dell'hub IoT creato nella sezione precedente e l'ID del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eede1-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="eede1-137">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="eede1-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="eede1-138">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="eede1-138">Add the following method to the **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="eede1-139">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="eede1-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="eede1-140">In Esplora soluzioni aprire **Imposta progetti di avvio** e assicurarsi che l'**azione** per il progetto **TriggerFWUpdate** sia impostata su **Avvio**.</span><span class="sxs-lookup"><span data-stu-id="eede1-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="eede1-141">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="eede1-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="eede1-142">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="eede1-142">Run the apps</span></span>
<span data-ttu-id="eede1-143">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="eede1-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="eede1-144">Al prompt dei comandi nella cartella **manageddevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="eede1-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="eede1-145">In Visual Studio, fare clic con il pulsante destro del mouse sul progetto **TriggerFWUpdate**. Eseguire l'app console C# quindi scegliere **Debug** e **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="eede1-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="eede1-146">Nella console viene visualizzata la risposta del dispositivo al metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="eede1-146">You see the device response to the direct method in the console.</span></span>

    ![Firmware aggiornato][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="eede1-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eede1-148">Next steps</span></span>
<span data-ttu-id="eede1-149">In questa esercitazione è stato usato un metodo diretto per attivare un aggiornamento del firmware remoto in un dispositivo e sono state usate le proprietà segnalate per conoscere lo stato del processo di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="eede1-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="eede1-150">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="eede1-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/