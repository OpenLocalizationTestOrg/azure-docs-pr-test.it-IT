---
title: Usare metodi diretti dell'Hub IoT di Azure (.NET/Node) | Documentazione Microsoft
description: Come usare metodi diretti dell'Hub IoT di Azure. Si usa Azure IoT SDK per dispositivi per Node.js per implementare un'app per dispositivo simulato che include un metodo diretto e Azure IoT SDK per servizi per .NET per implementare un'app di servizio che richiama il metodo diretto.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="9512e-104">Usare metodi diretti (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="9512e-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="9512e-105">In questa esercitazione verrà sviluppata un'app console Node.js e .NET:</span><span class="sxs-lookup"><span data-stu-id="9512e-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="9512e-106">**CallMethodOnDevice.sln**, un'app back-end .NET, che chiama un metodo nell'app per dispositivo simulato e visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="9512e-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="9512e-107">**SimulatedDevice.js**, un'app Node.js che simula un dispositivo che si connette all'hub IoT con l'identità del dispositivo creata in precedenza e risponde al metodo chiamato dal cloud.</span><span class="sxs-lookup"><span data-stu-id="9512e-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="9512e-108">L'articolo [Azure IoT SDK][lnk-hub-sdks] offre informazioni sui vari Azure IoT SDK che è possibile usare per compilare applicazioni da eseguire nei dispositivi e il backend della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9512e-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="9512e-109">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="9512e-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="9512e-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9512e-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="9512e-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9512e-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="9512e-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9512e-112">An active Azure account.</span></span> <span data-ttu-id="9512e-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9512e-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="9512e-114">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="9512e-114">Create a simulated device app</span></span>
<span data-ttu-id="9512e-115">In questa sezione viene creata un'applicazione console Node.js che risponde a un metodo chiamato dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="9512e-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="9512e-116">Creare una nuova cartella vuota denominata **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="9512e-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="9512e-117">Nella cartella **simulateddevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9512e-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="9512e-118">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="9512e-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="9512e-119">Eseguire questo comando al prompt dei comandi nella cartella **simulateddevice** per installare i pacchetti **azure-iot-device** e **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="9512e-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="9512e-120">Con un editor di testo creare un file nella cartella **simulateddevice** e assegnargli il nome **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="9512e-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="9512e-121">Aggiungere le istruzioni `require` seguenti all'inizio del file **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="9512e-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="9512e-122">Aggiungere una variabile **connectionString** e usarla per creare un'istanza di **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="9512e-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="9512e-123">Sostituire **{device connection string}** con la stringa di connessione del dispositivo generata nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="9512e-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="9512e-124">Aggiungere la funzione seguente per implementare il metodo diretto nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9512e-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="9512e-125">Aprire la connessione all'hub IoT e inizializzare il listener del metodo:</span><span class="sxs-lookup"><span data-stu-id="9512e-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="9512e-126">Salvare e chiudere il file **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="9512e-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="9512e-127">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="9512e-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="9512e-128">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio i tentativi di connessione, come indicato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="9512e-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="9512e-129">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="9512e-129">Call a direct method on a device</span></span>
<span data-ttu-id="9512e-130">In questa sezione viene creata un'app console .NET che chiama un metodo nell'app per dispositivo simulato e quindi visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="9512e-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="9512e-131">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="9512e-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="9512e-132">Verificare che la versione di .NET Framework sia 4.5.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9512e-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="9512e-133">Assegnare al progetto il nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="9512e-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. <span data-ttu-id="9512e-135">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **CallMethodOnDevice** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9512e-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="9512e-136">Nella finestra **Gestione pacchetti NuGet** selezionare **Esplora**, cercare **microsoft.azure.devices**, selezionare **Installa** per installare il pacchetto **Microsoft.Azure.Devices** e accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="9512e-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="9512e-137">Questa procedura scarica, installa e aggiunge un riferimento al [pacchetto NuGet Azure IoT - SDK per dispositivi][lnk-nuget-service-sdk] e alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9512e-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][11]

4. <span data-ttu-id="9512e-139">Aggiungere le istruzione `using` seguenti all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="9512e-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="9512e-140">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="9512e-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="9512e-141">Sostituire il valore del segnaposto con la stringa di connessione dell'hub IoT creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="9512e-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="9512e-142">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="9512e-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="9512e-143">Questo metodo richiama un metodo diretto con nome `writeLine` nel dispositivo `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="9512e-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="9512e-144">Scrive quindi la risposta specificata dal dispositivo nella console.</span><span class="sxs-lookup"><span data-stu-id="9512e-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="9512e-145">Si noti che è possibile specificare un valore di timeout per la risposta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9512e-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="9512e-146">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="9512e-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="9512e-147">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="9512e-147">Run the applications</span></span>
<span data-ttu-id="9512e-148">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9512e-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="9512e-149">In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Imposta progetti di avvio...**.</span><span class="sxs-lookup"><span data-stu-id="9512e-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="9512e-150">Selezionare **Progetto di avvio singolo**, quindi selezionare il progetto **CallMethodOnDevice** nel menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="9512e-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="9512e-151">Eseguire questo comando al prompt dei comandi nella cartella **simulateddevice** per iniziare ad ascoltare le chiamate ai metodi dall'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="9512e-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="9512e-152">Attendere l'apertura del dispositivo simulato: ![][7]</span><span class="sxs-lookup"><span data-stu-id="9512e-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="9512e-153">Quando il dispositivo è connesso e in attesa di chiamate del metodo, eseguire l'app .NET **CallMethodOnDevice** per richiamare il metodo nell'app per dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="9512e-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="9512e-154">La risposta del dispositivo dovrebbe essere scritta nella console.</span><span class="sxs-lookup"><span data-stu-id="9512e-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="9512e-155">Il dispositivo risponde quindi al metodo stampando questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="9512e-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="9512e-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9512e-156">Next steps</span></span>
<span data-ttu-id="9512e-157">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9512e-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="9512e-158">Questa identità del dispositivo è stata usata per consentire all'app del dispositivo simulato di reagire ai metodi richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="9512e-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="9512e-159">È stata anche creata un'applicazione che richiama i metodi sul dispositivo e visualizza la risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9512e-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="9512e-160">Per altre informazioni sulle attività iniziali con l'hub IoT e per esplorare altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="9512e-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="9512e-161">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="9512e-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="9512e-162">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="9512e-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="9512e-163">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="9512e-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
<span data-ttu-id="9512e-164">[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="9512e-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
