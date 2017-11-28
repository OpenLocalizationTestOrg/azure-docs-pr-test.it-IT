---
title: aggiornamento del firmware aaaDevice con l'IoT Hub Azure (.NET/nodo) | Documenti Microsoft
description: Come aggiornare la gestione dei dispositivi toouse su Azure IoT Hub tooinitiate un firmware del dispositivo. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che attiva l'aggiornamento del firmware hello.
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
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="b2fcf-104">Usare Gestione di dispositivi tooinitiate un aggiornamento del firmware del dispositivo (.NET/nodo)</span><span class="sxs-lookup"><span data-stu-id="b2fcf-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="b2fcf-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b2fcf-105">Introduction</span></span>
<span data-ttu-id="b2fcf-106">In hello [iniziare con la gestione dei dispositivi] [ lnk-dm-getstarted] esercitazione, si è visto come hello toouse [doppi dispositivo] [ lnk-devtwin] e [diretto metodi] [ lnk-c2dmethod] tooremotely primitive riavviare un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="b2fcf-107">Questa esercitazione viene utilizzato hello stesse primitive Hub IoT e Mostra come toodo un end-to-end simulato l'aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="b2fcf-108">Questo modello è usato nell'implementazione di aggiornamento del firmware hello per hello [esempio di implementazione dispositivo Pi Raspberry][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="b2fcf-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="b2fcf-109">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b2fcf-110">Creare un'applicazione console .NET che chiama hello firmwareUpdate dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="b2fcf-111">Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="b2fcf-112">Questo metodo avvia un processo a più fasi che attende l'immagine di firmware hello toodownload, scarica l'immagine del firmware hello e infine applica immagine del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="b2fcf-113">Durante ogni fase dell'aggiornamento hello hello dispositivo utilizza hello segnalato tooreport proprietà sullo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="b2fcf-114">Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):</span><span class="sxs-lookup"><span data-stu-id="b2fcf-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="b2fcf-115">**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza la risposta hello e periodicamente (ogni 500ms) consente di visualizzare hello aggiornato segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="b2fcf-116">**TriggerFWUpdate**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto firmwareUpdate, viene eseguito tramite un processo più stati di toosimulate un aggiornamento del firmware tra: in attesa per il download dell'immagine hello Download nuova immagine hello e infine l'applicazione hello image.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="b2fcf-117">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b2fcf-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b2fcf-119">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="b2fcf-120">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b2fcf-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-121">An active Azure account.</span></span> <span data-ttu-id="b2fcf-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="b2fcf-123">Seguire hello [iniziare con la gestione dei dispositivi](iot-hub-csharp-node-device-management-get-started.md) articolo toocreate l'hub IoT e ottenere la stringa di connessione IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="b2fcf-124">Attivare un aggiornamento del firmware remota sul dispositivo hello utilizzando un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="b2fcf-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="b2fcf-125">In questa sezione viene creata un'app console .NET (tramite C#) che avvia un aggiornamento del firmware remoto in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="b2fcf-126">utilizza dispositivo doppi query tooperiodically ottenere lo stato di hello dell'aggiornamento del firmware active hello app Hello utilizza un aggiornamento di hello tooinitiate dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="b2fcf-127">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="b2fcf-128">Progetto hello nome **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. <span data-ttu-id="b2fcf-130">In Esplora soluzioni fare doppio clic su hello **TriggerFWUpdate** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="b2fcf-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="b2fcf-131">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="b2fcf-132">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. <span data-ttu-id="b2fcf-134">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="b2fcf-135">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="b2fcf-136">Sostituire hello hello di più valori segnaposto con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello e hello Id del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="b2fcf-137">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="b2fcf-138">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-138">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="b2fcf-139">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="b2fcf-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="b2fcf-140">In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **TriggerFWUpdate** progetto **avviare**.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="b2fcf-141">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="b2fcf-142">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="b2fcf-142">Run hello apps</span></span>
<span data-ttu-id="b2fcf-143">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b2fcf-144">Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="b2fcf-145">In Visual Studio, fare clic su hello **TriggerFWUpdate** projectRun toohello c# app console, selezionare **Debug** e **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="b2fcf-146">Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Firmware aggiornato][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="b2fcf-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2fcf-148">Next steps</span></span>
<span data-ttu-id="b2fcf-149">In questa esercitazione, è stato utilizzato un tootrigger dirette del metodo remota aggiornamento del firmware su un dispositivo e hello utilizzato nel report di stato di hello toofollow le proprietà di aggiornamento del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="b2fcf-150">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b2fcf-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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