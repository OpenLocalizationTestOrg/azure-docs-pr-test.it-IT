---
title: Usare metodi diretti dell'Hub IoT di Azure (.NET/.NET) | Microsoft Docs
description: Come usare metodi diretti dell'Hub IoT di Azure. Si usa Azure IoT SDK per dispositivi per .NET per implementare un'app per dispositivi simulata che include un metodo diretto e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che richiama il metodo diretto.
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="77462-104">Usare metodi diretti (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="77462-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="77462-105">In questa esercitazione verranno sviluppate due app console .NET:</span><span class="sxs-lookup"><span data-stu-id="77462-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="77462-106">**CallMethodOnDevice**, un'app back-end .NET, che chiama un metodo nell'app per dispositivi simulata e visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="77462-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="77462-107">**SimulateDeviceMethods**, un'app console che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata in precedenza e risponde al metodo chiamato dal cloud.</span><span class="sxs-lookup"><span data-stu-id="77462-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="77462-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] offre informazioni sui vari Azure IoT SDK che è possibile usare per compilare applicazioni da eseguire nei dispositivi e il backend della soluzione.</span><span class="sxs-lookup"><span data-stu-id="77462-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="77462-109">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="77462-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="77462-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="77462-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="77462-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="77462-111">An active Azure account.</span></span> <span data-ttu-id="77462-112">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="77462-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="77462-113">Se invece si desidera creare l'identità del dispositivo a livello di codice, leggere la sezione corrispondente nell'articolo [Connettere il dispositivo simulato all'hub IoT tramite .NET][lnk-device-identity-csharp].</span><span class="sxs-lookup"><span data-stu-id="77462-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="77462-114">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="77462-114">Create a simulated device app</span></span>
<span data-ttu-id="77462-115">In questa sezione viene creata un'app console .NET che risponde a un metodo chiamato dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="77462-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="77462-116">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="77462-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="77462-117">Assegnare al progetto il nome **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="77462-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="77462-119">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **SimulateDeviceMethods**, quindi scegliere **Gestisci pacchetti NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="77462-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="77462-120">Nella finestra **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="77462-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="77462-121">Selezionare **Installa** per installare il pacchetto **microsoft.azure.devices.client** e accettare le condizioni d'uso.</span><span class="sxs-lookup"><span data-stu-id="77462-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="77462-122">Questa procedura scarica, installa e aggiunge un riferimento al pacchetto NuGet [Azure IoT SDK per dispositivi][lnk-nuget-client-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="77462-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. <span data-ttu-id="77462-124">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="77462-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="77462-125">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="77462-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="77462-126">Sostituire il valore del segnaposto con la stringa di connessione del dispositivo annotato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="77462-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="77462-127">Aggiungere quanto segue per implementare il metodo diretto nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="77462-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="77462-128">Infine aggiungere il codice seguente al metodo **Main** per aprire la connessione all'hub IoT e inizializzare il listener del metodo:</span><span class="sxs-lookup"><span data-stu-id="77462-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="77462-129">In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Imposta progetti di avvio...**.</span><span class="sxs-lookup"><span data-stu-id="77462-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="77462-130">Selezionare **Progetto di avvio singolo**, quindi selezionare il progetto **SimulateDeviceMethods** nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="77462-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="77462-131">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="77462-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="77462-132">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio i tentativi di connessione, come indicato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="77462-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="77462-133">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="77462-133">Call a direct method on a device</span></span>
<span data-ttu-id="77462-134">In questa sezione viene creata un'app console .NET che chiama un metodo nell'app per dispositivo simulato e quindi visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="77462-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="77462-135">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="77462-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="77462-136">Verificare che la versione di .NET Framework sia 4.5.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="77462-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="77462-137">Assegnare al progetto il nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="77462-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createserviceapp]
2. <span data-ttu-id="77462-139">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **CallMethodOnDevice** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="77462-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="77462-140">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="77462-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="77462-141">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="77462-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]

4. <span data-ttu-id="77462-143">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="77462-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="77462-144">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="77462-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="77462-145">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="77462-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="77462-146">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="77462-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="77462-147">Questo metodo richiama un metodo diretto con nome `writeLine` nel dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="77462-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="77462-148">Scrive quindi la risposta specificata dal dispositivo nella console.</span><span class="sxs-lookup"><span data-stu-id="77462-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="77462-149">Si noti che è possibile specificare un valore di timeout per la risposta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77462-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="77462-150">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="77462-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="77462-151">In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Imposta progetti di avvio...**.</span><span class="sxs-lookup"><span data-stu-id="77462-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="77462-152">Selezionare **Progetto di avvio singolo**, quindi selezionare il progetto **CallMethodOnDevice** nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="77462-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="77462-153">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="77462-153">Run the applications</span></span>
<span data-ttu-id="77462-154">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="77462-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="77462-155">Eseguire l'app per dispositivi .NET **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="77462-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="77462-156">Dovrebbe iniziare ad ascoltare le chiamate di metodo provenienti dall'IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="77462-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Esecuzione dell'app per dispositivi][img-deviceapprun]
1. <span data-ttu-id="77462-158">Quando il dispositivo è connesso e in attesa di chiamate del metodo, eseguire l'app .NET **CallMethodOnDevice** per richiamare il metodo nell'app per dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="77462-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="77462-159">La risposta del dispositivo dovrebbe essere scritta nella console.</span><span class="sxs-lookup"><span data-stu-id="77462-159">You should see the device response written in the console.</span></span>
   
    ![Esecuzione dell'app di servizio][img-serviceapprun]
1. <span data-ttu-id="77462-161">Il dispositivo risponde quindi al metodo stampando questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="77462-161">The device then reacts to the method by printing this message:</span></span>
   
    ![Metodo diretto chiamato sul dispositivo][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="77462-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77462-163">Next steps</span></span>
<span data-ttu-id="77462-164">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="77462-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="77462-165">Questa identità del dispositivo è stata usata per consentire all'app del dispositivo simulato di reagire ai metodi richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="77462-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="77462-166">È stata anche creata un'applicazione che richiama i metodi sul dispositivo e visualizza la risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77462-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="77462-167">Per altre informazioni sulle attività iniziali con l'hub IoT e per esplorare altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="77462-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="77462-168">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="77462-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="77462-169">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="77462-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="77462-170">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="77462-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="77462-171">[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="77462-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
