---
title: aaaGet avviato con Azure IoT Hub (.NET) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per .NET. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="96a21-104">Connessione hub IoT tooyour dispositivo utilizzando .NET</span><span class="sxs-lookup"><span data-stu-id="96a21-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="96a21-105">Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console .NET:</span><span class="sxs-lookup"><span data-stu-id="96a21-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="96a21-106">**CreateDeviceIdentity**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="96a21-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="96a21-107">**ReadDeviceToCloudMessages**, che consente di visualizzare dati di telemetria hello inviati per l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="96a21-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="96a21-108">**SimulatedDevice**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo tramite protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="96a21-109">È possibile scaricare o clonare la soluzione di Visual Studio hello, che contiene tre app di hello da Github.</span><span class="sxs-lookup"><span data-stu-id="96a21-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="96a21-110">Per informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild toorun applicazioni nei dispositivi e il back-end di soluzione, vedere [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="96a21-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="96a21-111">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="96a21-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="96a21-112">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="96a21-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="96a21-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="96a21-113">An active Azure account.</span></span> <span data-ttu-id="96a21-114">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="96a21-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="96a21-115">È stato creato l'hub IoT e si dispone di nome host hello e stringa di connessione IoT Hub che è necessario rest hello toocomplete di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96a21-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="96a21-116">Ricezione di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="96a21-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="96a21-117">In questa sezione si crea un'app console di .NET che legge i messaggi da dispositivo a cloud dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96a21-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="96a21-118">Un hub IoT espone un [hub eventi di Azure][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread.</span><span class="sxs-lookup"><span data-stu-id="96a21-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="96a21-119">cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="96a21-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="96a21-120">toolearn come tooprocess dispositivo a cloud messaggi su larga scala, vedere hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96a21-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="96a21-121">Per ulteriori informazioni su come tooprocess messaggi dagli hub eventi, vedere hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96a21-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="96a21-122">(Questa esercitazione è applicabile toohello evento dell'Hub IoT Hub compatibile endpoint).</span><span class="sxs-lookup"><span data-stu-id="96a21-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="96a21-123">Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="96a21-124">In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="96a21-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="96a21-125">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="96a21-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="96a21-126">Progetto hello nome **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="96a21-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][10a]

2. <span data-ttu-id="96a21-128">In Esplora soluzioni fare doppio clic su hello **ReadDeviceToCloudMessages** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="96a21-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="96a21-129">In hello **Gestione pacchetti NuGet** finestra, cercare **Windowsazure**selezionare **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="96a21-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="96a21-130">Questa procedura Scarica, installa e aggiunge un riferimento troppo[Azure Service Bus][lnk-servicebus-nuget], con tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="96a21-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="96a21-131">Questo pacchetto consente endpoint hello applicazione tooconnect toohello Hub eventi compatibile con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96a21-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="96a21-132">Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="96a21-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="96a21-133">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="96a21-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="96a21-134">Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione "Creare un hub IoT" hello hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="96a21-135">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="96a21-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="96a21-136">Questo metodo utilizza un **EventHubReceiver** partizioni di ricezione di messaggi di istanza tooreceive da tutti hello IoT hub dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="96a21-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="96a21-137">Si noti come passare un `DateTime.Now` parametro quando si crea hello **EventHubReceiver** dell'oggetto, in modo che riceva solo i messaggi inviati dopo l'avvio.</span><span class="sxs-lookup"><span data-stu-id="96a21-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="96a21-138">Questo filtro è utile in un ambiente di test in modo da visualizzare il set corrente di hello dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="96a21-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="96a21-139">In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="96a21-140">Per ulteriori informazioni, vedere l'esercitazione hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="96a21-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="96a21-141">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="96a21-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="96a21-142">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="96a21-142">Create a device app</span></span>

<span data-ttu-id="96a21-143">In questa sezione si crea un'applicazione console .NET che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="96a21-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="96a21-144">In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="96a21-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="96a21-145">Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="96a21-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="96a21-146">Progetto hello nome **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="96a21-146">Name hello project **SimulatedDevice**.</span></span>

    ![Nuovo progetto desktop di Windows classico in Visual C#][10b]

2. <span data-ttu-id="96a21-148">In Esplora soluzioni fare doppio clic su hello **SimulatedDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="96a21-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="96a21-149">In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **Microsoft.Azure.Devices.Client**selezionare **installare** hello tooinstall **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="96a21-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="96a21-150">Questa procedura Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet SDK del dispositivo IoT di Azure] [ lnk-device-nuget] e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="96a21-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="96a21-151">Aggiungere il seguente hello `using` istruzione nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="96a21-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="96a21-152">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="96a21-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="96a21-153">Substitute `{iot hub hostname}` con nome host dell'hub IoT hello recuperato nella sezione "Creare un hub IoT" hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="96a21-154">Substitute `{device key}` con chiave dispositivo hello recuperato nella sezione "Creare un'identità del dispositivo" hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="96a21-155">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="96a21-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="96a21-156">Questo metodo invia un nuovo messaggio da dispositivo a cloud ogni secondo.</span><span class="sxs-lookup"><span data-stu-id="96a21-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="96a21-157">messaggio Hello contiene un oggetto JSON serializzato, con ID dispositivo hello e generato in modo casuale di numeri toosimulate un sensore di temperatura e un sensore umidità.</span><span class="sxs-lookup"><span data-stu-id="96a21-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="96a21-158">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="96a21-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="96a21-159">Per impostazione predefinita, hello **crea** metodo in un'app .NET Framework consente di creare un **DeviceClient** istanza che utilizza hello AMQP protocollo toocommunicate con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96a21-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="96a21-160">hello toouse protocollo MQTT o HTTP, utilizzare l'override di hello del hello **crea** metodo che consente di protocollo hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="96a21-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="96a21-161">UWP e PCL usano il protocollo HTTP hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="96a21-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="96a21-162">Se si utilizza il protocollo HTTP hello, è necessario aggiungere anche hello **webapi** hello di NuGet pacchetto tooyour progetto tooinclude **System.Net.Http.Formatting** dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="96a21-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="96a21-163">In questa esercitazione illustra i passaggi di hello toocreate un IoT Hub app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="96a21-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="96a21-164">È inoltre possibile utilizzare hello [servizio connesso per l'IoT Hub Azure] [ lnk-connected-service] tooyour dispositivo app di Visual Studio estensione tooadd hello codice necessario.</span><span class="sxs-lookup"><span data-stu-id="96a21-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="96a21-165">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="96a21-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="96a21-166">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="96a21-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="96a21-167">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="96a21-167">Run hello apps</span></span>

<span data-ttu-id="96a21-168">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="96a21-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="96a21-169">In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="96a21-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="96a21-170">Selezionare **più progetti di avvio**, quindi selezionare **avviare** come azione hello per entrambi hello **ReadDeviceToCloudMessages** e **SimulatedDevice** progetti.</span><span class="sxs-lookup"><span data-stu-id="96a21-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Proprietà del progetto di avvio][41]

2. <span data-ttu-id="96a21-172">Premere **F5** toostart entrambe le App in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="96a21-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="96a21-173">output della console da hello Hello **SimulatedDevice** messaggi hello di app Mostra l'app del dispositivo invia tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="96a21-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="96a21-174">output della console da hello Hello **ReadDeviceToCloudMessages** app Mostra messaggi hello che riceve l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96a21-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Output della console dalle app][42]

3. <span data-ttu-id="96a21-176">Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:</span><span class="sxs-lookup"><span data-stu-id="96a21-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Riquadro Utilizzo del portale di Azure][43]

## <a name="next-steps"></a><span data-ttu-id="96a21-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96a21-178">Next steps</span></span>

<span data-ttu-id="96a21-179">In questa esercitazione, è configurato un hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="96a21-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="96a21-180">È stato utilizzato questo dispositivo identità tooenable hello dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96a21-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="96a21-181">È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="96a21-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="96a21-182">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="96a21-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="96a21-183">[Connessione del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="96a21-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="96a21-184">[Introduzione alla gestione dei dispositivi][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="96a21-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="96a21-185">[Introduzione a IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="96a21-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="96a21-186">toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="96a21-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
