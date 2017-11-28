---
title: IoT Hub Azure aaaUse diretta di metodi (.NET/.NET) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Usare il dispositivo di Azure IoT hello SDK per .NET tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="a6f84-104">Usare metodi diretti (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="a6f84-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="a6f84-105">In questa esercitazione, siamo corso toodevelop due applicazioni console .NET:</span><span class="sxs-lookup"><span data-stu-id="a6f84-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="a6f84-106">**CallMethodOnDevice**, un'applicazione back-end, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="a6f84-107">**SimulateDeviceMethods**, un'applicazione console che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f84-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="a6f84-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="a6f84-109">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="a6f84-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="a6f84-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a6f84-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a6f84-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a6f84-111">An active Azure account.</span></span> <span data-ttu-id="a6f84-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a6f84-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="a6f84-113">Se si desidera l'identità del dispositivo hello toocreate a livello di codice in alternativa, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo simulato utilizzando .NET] [ lnk-device-identity-csharp] articolo.</span><span class="sxs-lookup"><span data-stu-id="a6f84-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a6f84-114">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="a6f84-114">Create a simulated device app</span></span>
<span data-ttu-id="a6f84-115">In questa sezione si crea un'applicazione console .NET che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.</span><span class="sxs-lookup"><span data-stu-id="a6f84-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="a6f84-116">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a6f84-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a6f84-117">Progetto hello nome **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="a6f84-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="a6f84-119">In Esplora soluzioni fare doppio clic su hello **SimulateDeviceMethods** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a6f84-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a6f84-120">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="a6f84-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="a6f84-121">Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="a6f84-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="a6f84-122">Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a6f84-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="a6f84-124">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="a6f84-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="a6f84-125">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="a6f84-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a6f84-126">Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="a6f84-127">Aggiungere hello seguente tooimplement hello dirette del metodo nel dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="a6f84-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="a6f84-128">Infine, aggiungere hello seguente codice toohello **Main** metodo tooopen hello tooyour IoT hub e inizializzare hello metodo listener della connessione:</span><span class="sxs-lookup"><span data-stu-id="a6f84-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="a6f84-129">In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **SimulateDeviceMethods** progetto nel menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="a6f84-130">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="a6f84-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a6f84-131">Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="a6f84-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="a6f84-132">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="a6f84-132">Call a direct method on a device</span></span>
<span data-ttu-id="a6f84-133">In questa sezione si crea un'applicazione console .NET che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="a6f84-134">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a6f84-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a6f84-135">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a6f84-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="a6f84-136">Progetto hello nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="a6f84-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createserviceapp]
2. <span data-ttu-id="a6f84-138">In Esplora soluzioni fare doppio clic su hello **CallMethodOnDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="a6f84-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="a6f84-139">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="a6f84-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a6f84-140">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a6f84-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]

4. <span data-ttu-id="a6f84-142">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="a6f84-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="a6f84-143">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="a6f84-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a6f84-144">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="a6f84-145">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="a6f84-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="a6f84-146">Questo metodo richiama un metodo diretto con nome `writeLine` su hello `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a6f84-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="a6f84-147">Quindi, viene scritto risposta hello fornita dal dispositivo hello sulla console hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="a6f84-148">Si noti come è possibile toospecify un valore di timeout per toorespond dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="a6f84-149">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="a6f84-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="a6f84-150">In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **CallMethodOnDevice** progetto nel menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="a6f84-151">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="a6f84-151">Run hello applications</span></span>
<span data-ttu-id="a6f84-152">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="a6f84-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="a6f84-153">Eseguire app di dispositivo .NET hello **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="a6f84-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="a6f84-154">Dovrebbe iniziare ad ascoltare le chiamate di metodo provenienti dall'IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="a6f84-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Esecuzione dell'app per dispositivi][img-deviceapprun]
1. <span data-ttu-id="a6f84-156">Ora che il dispositivo hello è connesso e in attesa di chiamate al metodo, eseguire hello .NET **CallMethodOnDevice** metodo hello tooinvoke di app in app dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="a6f84-157">Dovrebbe essere scritto nella console di hello risposta del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-157">You should see hello device response written in hello console.</span></span>
   
    ![Esecuzione dell'app di servizio][img-serviceapprun]
1. <span data-ttu-id="a6f84-159">dispositivo di Hello reagisce quindi il metodo toohello con la stampa questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="a6f84-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Dirette del metodo richiamata sul dispositivo hello][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="a6f84-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6f84-161">Next steps</span></span>
<span data-ttu-id="a6f84-162">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="a6f84-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a6f84-163">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="a6f84-164">È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="a6f84-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="a6f84-165">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="a6f84-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="a6f84-166">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="a6f84-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="a6f84-167">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="a6f84-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="a6f84-168">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a6f84-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md
