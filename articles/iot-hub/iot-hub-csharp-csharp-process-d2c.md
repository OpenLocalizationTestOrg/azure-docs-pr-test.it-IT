---
title: Elaborare messaggi da dispositivo a cloud dell'hub IoT di Azure usando i route (.NET) |Microsoft Docs
description: Come elaborare i messaggi da dispositivo a cloud dell'hub IoT usando le regole di routing e gli endpoint personalizzati per inviare i messaggi agli altri servizi di back-end.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="53a4b-103">Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route (.NET)</span><span class="sxs-lookup"><span data-stu-id="53a4b-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="53a4b-104">Questa esercitazione si basa sull'esercitazione [Introduzione a hub IoT].</span><span class="sxs-lookup"><span data-stu-id="53a4b-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="53a4b-105">L'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="53a4b-105">The tutorial:</span></span>

* <span data-ttu-id="53a4b-106">Illustra come usare le regole di routing per inviare i messaggi da dispositivo a cloud con un semplice metodo basato sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="53a4b-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="53a4b-107">Illustra come isolare i messaggi interattivi che richiedono un intervento immediato del back-end della soluzione per essere elaborati in seguito.</span><span class="sxs-lookup"><span data-stu-id="53a4b-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="53a4b-108">Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="53a4b-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="53a4b-109">Al contrario, i messaggi di punto dati, come ad esempio la telemetria di temperatura, vengono semplicemente inseriti in un motore di analisi.</span><span class="sxs-lookup"><span data-stu-id="53a4b-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="53a4b-110">Al termine di questa esercitazione vengono eseguite tre app di console .NET:</span><span class="sxs-lookup"><span data-stu-id="53a4b-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="53a4b-111">**SimulatedDevice**, una versione modificata dell'app creata nell'esercitazione [Introduzione a hub IoT], che invia messaggi di punti dati da dispositivo a cloud ogni secondo e messaggi interattivi da dispositivo a cloud ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="53a4b-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="53a4b-112">**ReadDeviceToCloudMessages** mostra i dati di telemetria non fondamentali inviati dall'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="53a4b-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="53a4b-113">**ReadCriticalQueue** rimuove i messaggi importanti inviati dall'app per dispositivi da una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="53a4b-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="53a4b-114">Questa coda è collegata all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="53a4b-115">L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="53a4b-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="53a4b-116">Per informazioni su come sostituire il dispositivo simulato in questa esercitazione con un dispositivo fisico, fare riferimento al [Centro per sviluppatori Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="53a4b-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="53a4b-117">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="53a4b-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="53a4b-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53a4b-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="53a4b-119">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="53a4b-119">An active Azure account.</span></span> <br/><span data-ttu-id="53a4b-120">Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="53a4b-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="53a4b-121">È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].</span><span class="sxs-lookup"><span data-stu-id="53a4b-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="53a4b-122">Inviare messaggi interattivi</span><span class="sxs-lookup"><span data-stu-id="53a4b-122">Send interactive messages</span></span>

<span data-ttu-id="53a4b-123">Modificare l'app per dispositivi creata nell'esercitazione [Introduzione a hub IoT] per inviare occasionalmente messaggi interattivi.</span><span class="sxs-lookup"><span data-stu-id="53a4b-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="53a4b-124">In Visual Studio, nel progetto **SimulatedDevice** sostituire il metodo `SendDeviceToCloudMessagesAsync` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="53a4b-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="53a4b-125">Con questo metodo La proprietà `"level": "critical"` verrà aggiunta in modo casuale ai messaggi inviati dal dispositivo, il quale simula un messaggio che richiede un intervento immediato del back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="53a4b-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="53a4b-126">L'app del dispositivo passa queste informazioni nelle proprietà del messaggio anziché nel corpo del messaggio, in modo che l'hub IoT possa indirizzare il messaggio alla destinazione messaggi appropriata.</span><span class="sxs-lookup"><span data-stu-id="53a4b-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="53a4b-127">È possibile usare le proprietà del messaggio per indirizzare i messaggi in diversi scenari, tra cui l'elaborazione del percorso a freddo, oltre all'esempio del percorso a caldo mostrato qui.</span><span class="sxs-lookup"><span data-stu-id="53a4b-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="53a4b-128">Per semplicità, questa esercitazione non implementa alcun criterio di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="53a4b-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="53a4b-129">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN relativo alla [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="53a4b-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="53a4b-130">Eseguire il routing dei messaggi a una coda nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="53a4b-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="53a4b-131">In questa sezione verrà illustrato come:</span><span class="sxs-lookup"><span data-stu-id="53a4b-131">In this section, you:</span></span>

* <span data-ttu-id="53a4b-132">Creare una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="53a4b-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="53a4b-133">Collegarla all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="53a4b-134">Configurare l'hub IoT per inviare messaggi alla coda in base alla presenza di una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="53a4b-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="53a4b-135">Per altre informazioni su come elaborare i messaggi dalle code del bus di servizio, vedere [Get started with queues][Service Bus queue] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="53a4b-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="53a4b-136">Creare una coda del bus di servizio, come descritto in [Get started with queues][Service Bus queue] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="53a4b-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="53a4b-137">La coda deve trovarsi nella stessa area e nella stessa sottoscrizione dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="53a4b-138">Prendere nota dello spazio dei nomi e del nome della coda.</span><span class="sxs-lookup"><span data-stu-id="53a4b-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53a4b-139">Nelle code e negli argomenti del bus di servizio usati come endpoint dell'hub IoT non devono essere abilitati le **sessioni** e il **rilevamento duplicati**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="53a4b-140">Se una di queste opzioni è abilitata, l'endpoint risulta **non raggiungibile** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="53a4b-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="53a4b-141">Nel Portale di Azure, aprire l'hub IoT e fare clic su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Endpoint in hub IoT][30]

3. <span data-ttu-id="53a4b-143">Nel pannello **Endpoint** fare clic su **Aggiungi** in alto per aggiungere la coda all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="53a4b-144">Denominare l'endpoint **CriticalQueue** e usare il menu a discesa per selezionare **Coda del bus di servizio**, lo spazio dei nomi del bus di servizio in cui si trova la coda e il nome della coda.</span><span class="sxs-lookup"><span data-stu-id="53a4b-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="53a4b-145">Al termine, fare clic su **Salva** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="53a4b-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![Aggiunta di un endpoint][31]
    
4. <span data-ttu-id="53a4b-147">Fare clic su **Route** nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="53a4b-148">Fare clic su **Aggiungi** nella parte superiore del pannello per creare una regola di routing che indirizzi i messaggi alla coda appena aggiunta.</span><span class="sxs-lookup"><span data-stu-id="53a4b-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="53a4b-149">Selezionare **DeviceTelemetry** come origine dei dati.</span><span class="sxs-lookup"><span data-stu-id="53a4b-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="53a4b-150">Immettere `level="critical"` come condizione, quindi scegliere la coda appena aggiunta come endpoint personalizzato, come endpoint della regola di routing.</span><span class="sxs-lookup"><span data-stu-id="53a4b-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="53a4b-151">Al termine, fare clic su **Salva** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="53a4b-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![Aggiunta di un route][32]
    
    <span data-ttu-id="53a4b-153">Assicurarsi che il route di fallback sia impostato su **ON**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="53a4b-154">Questo valore rappresenta la configurazione predefinita dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![Route di fallback][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="53a4b-156">Lettura dell'endpoint della coda</span><span class="sxs-lookup"><span data-stu-id="53a4b-156">Read from the queue endpoint</span></span>

<span data-ttu-id="53a4b-157">In questa sezione è possibile leggere i messaggi dell'endpoint della coda.</span><span class="sxs-lookup"><span data-stu-id="53a4b-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="53a4b-158">In Visual Studio aggiungere un progetto desktop di Windows classico in Visual C# usando il modello di progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="53a4b-159">Denominare il progetto **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="53a4b-160">In Esplora soluzioni fare clic con il tasto destro del mouse sul progetto **ReadCriticalQueue** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="53a4b-161">Viene visualizzata la finestra **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="53a4b-162">Cercare **WindowsAzure.ServiceBus**, fare clic su **Installa** e quindi accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="53a4b-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="53a4b-163">Viene quindi scaricato e installato il bus di servizio di Azure e viene aggiunto un riferimento ad esso, insieme alle relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="53a4b-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="53a4b-164">All'inizio del file **Program.cs** aggiungere le istruzioni **using** seguenti:</span><span class="sxs-lookup"><span data-stu-id="53a4b-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="53a4b-165">Aggiungere infine le righe seguenti al metodo **Main** .</span><span class="sxs-lookup"><span data-stu-id="53a4b-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="53a4b-166">Sostituire la stringa di connessione con le autorizzazioni **Ascolto** per la coda:</span><span class="sxs-lookup"><span data-stu-id="53a4b-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="53a4b-167">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="53a4b-167">Run the applications</span></span>
<span data-ttu-id="53a4b-168">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="53a4b-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="53a4b-169">In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="53a4b-170">Selezionare **Progetti di avvio multipli**, quindi selezionare **Avvio** come azione per i progetti **ReadDeviceToCloudMessages**, **SimulatedDevice** e **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="53a4b-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="53a4b-171">Premere **F5** per avviare le tre app console.</span><span class="sxs-lookup"><span data-stu-id="53a4b-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="53a4b-172">L'app **ReadDeviceToCloudMessages** include solo i messaggi non critici inviati dall'applicazione **SimulatedDevice**, mentre l'app **ReadCriticalQueue** include solo i messaggi critici.</span><span class="sxs-lookup"><span data-stu-id="53a4b-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Tre app console][50]

## <a name="next-steps"></a><span data-ttu-id="53a4b-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53a4b-174">Next steps</span></span>
<span data-ttu-id="53a4b-175">In questa esercitazione è stato descritto come inviare i messaggi da dispositivo a cloud in modo affidabile usando la funzionalità di routing dei messaggi dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="53a4b-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="53a4b-176">L'esercitazione [Come inviare messaggi da cloud a dispositivo con l'hub IoT][lnk-c2d] descrive le modalità di invio dei messaggi ai dispositivi dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="53a4b-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="53a4b-177">Per avere esempi di soluzioni complete che usano l'hub IoT, vedere [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="53a4b-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="53a4b-178">Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="53a4b-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="53a4b-179">Per ulteriori informazioni sul routing dei messaggi nell'hub IoT, vedere [Inviare e ricevere messaggi con l'hub IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="53a4b-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="53a4b-180">[Archiviazione di Azure]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="53a4b-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="53a4b-181">[bus di servizio di Azure]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="53a4b-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="53a4b-182">[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="53a4b-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="53a4b-183">[Introduzione a hub IoT]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="53a4b-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="53a4b-184">[Centro per sviluppatori Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="53a4b-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="53a4b-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="53a4b-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
