---
title: IoT Hub Azure aaaUse diretta metodi (.NET/nodo) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Usare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
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
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="6a475-104">Usare metodi diretti (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="6a475-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="6a475-105">In questa esercitazione verrà toodevelop .NET e un'applicazione console in Node.js:</span><span class="sxs-lookup"><span data-stu-id="6a475-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="6a475-106">**CallMethodOnDevice.sln**, un'app di back-end .NET, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="6a475-107">**SimulatedDevice.js**, un'app Node.js, che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="6a475-108">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="6a475-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="6a475-109">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="6a475-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="6a475-110">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6a475-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6a475-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6a475-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="6a475-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="6a475-112">An active Azure account.</span></span> <span data-ttu-id="6a475-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6a475-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6a475-114">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="6a475-114">Create a simulated device app</span></span>
<span data-ttu-id="6a475-115">In questa sezione si crea un'applicazione console Node. js che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.</span><span class="sxs-lookup"><span data-stu-id="6a475-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="6a475-116">Creare una nuova cartella vuota denominata **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="6a475-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="6a475-117">In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="6a475-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="6a475-118">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="6a475-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6a475-119">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** pacchetti:</span><span class="sxs-lookup"><span data-stu-id="6a475-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="6a475-120">Utilizzando un editor di testo, creare un file in hello **simulateddevice** cartella e denominarla **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="6a475-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="6a475-121">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="6a475-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="6a475-122">Aggiungere un **connectionString** variabile e usarlo toocreate un **DeviceClient** istanza.</span><span class="sxs-lookup"><span data-stu-id="6a475-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="6a475-123">Sostituire **{stringa di connessione dispositivo}** con stringa di connessione dispositivo hello generato nel hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="6a475-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="6a475-124">Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="6a475-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="6a475-125">Aprire l'hub IoT tooyour connessione hello e inizializzare listener per il metodo hello:</span><span class="sxs-lookup"><span data-stu-id="6a475-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="6a475-126">Salvare e chiudere hello **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="6a475-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="6a475-127">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="6a475-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6a475-128">Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="6a475-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="6a475-129">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="6a475-129">Call a direct method on a device</span></span>
<span data-ttu-id="6a475-130">In questa sezione si crea un'applicazione console .NET che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="6a475-131">In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="6a475-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="6a475-132">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6a475-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="6a475-133">Progetto hello nome **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="6a475-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. <span data-ttu-id="6a475-135">In Esplora soluzioni fare doppio clic su hello **CallMethodOnDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="6a475-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="6a475-136">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="6a475-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="6a475-137">Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="6a475-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Finestra Gestione pacchetti NuGet][11]

4. <span data-ttu-id="6a475-139">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="6a475-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="6a475-140">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="6a475-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="6a475-141">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="6a475-142">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="6a475-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="6a475-143">Questo metodo richiama un metodo diretto con nome `writeLine` su hello `myDeviceId` dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a475-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="6a475-144">Quindi, viene scritto risposta hello fornita dal dispositivo hello sulla console hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="6a475-145">Si noti come è possibile toospecify un valore di timeout per toorespond dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="6a475-146">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="6a475-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="6a475-147">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="6a475-147">Run hello applications</span></span>
<span data-ttu-id="6a475-148">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="6a475-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="6a475-149">In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **CallMethodOnDevice** progetto nel menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="6a475-150">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello in attesa di chiamate al metodo dall'IoT Hub toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6a475-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="6a475-151">Attendere tooopen dispositivo simulato hello:![][7]</span><span class="sxs-lookup"><span data-stu-id="6a475-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="6a475-152">Ora che il dispositivo hello è connesso e in attesa di chiamate al metodo, eseguire hello .NET **CallMethodOnDevice** metodo hello tooinvoke di app in app dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="6a475-153">Dovrebbe essere scritto nella console di hello risposta del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="6a475-154">dispositivo di Hello reagisce quindi il metodo toohello con la stampa questo messaggio:</span><span class="sxs-lookup"><span data-stu-id="6a475-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="6a475-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a475-155">Next steps</span></span>
<span data-ttu-id="6a475-156">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="6a475-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="6a475-157">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="6a475-158">È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="6a475-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="6a475-159">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="6a475-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="6a475-160">[Introduzione all'hub IoT]</span><span class="sxs-lookup"><span data-stu-id="6a475-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="6a475-161">[Pianificare processi in più dispositivi][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="6a475-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="6a475-162">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6a475-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md
