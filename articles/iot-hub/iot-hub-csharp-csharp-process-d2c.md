---
title: i messaggi da dispositivo a cloud di IoT Hub Azure aaaProcess mediante route (.Net) | Documenti Microsoft
description: Come i messaggi da dispositivo a cloud IoT Hub utilizzando le regole di routing e gli endpoint personalizzati toodispatch tooprocess messaggi tooother servizi di back-end.
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
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="9b10b-103">Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route (.NET)</span><span class="sxs-lookup"><span data-stu-id="9b10b-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="9b10b-104">In questa esercitazione si basa su hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9b10b-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="9b10b-105">esercitazione Hello:</span><span class="sxs-lookup"><span data-stu-id="9b10b-105">hello tutorial:</span></span>

* <span data-ttu-id="9b10b-106">Viene illustrato come toouse routing regole messaggi da dispositivo a cloud toodispatch in modo semplice e basata sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="9b10b-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="9b10b-107">Viene illustrato come messaggi interattivo tooisolate che richiedono un intervento immediato dalla soluzione hello back-end per un'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="9b10b-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="9b10b-108">Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="9b10b-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="9b10b-109">Al contrario, i messaggi di punto dati, come ad esempio la telemetria di temperatura, vengono semplicemente inseriti in un motore di analisi.</span><span class="sxs-lookup"><span data-stu-id="9b10b-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="9b10b-110">Alla fine di hello di questa esercitazione, si esegue tre applicazioni di console .NET:</span><span class="sxs-lookup"><span data-stu-id="9b10b-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="9b10b-111">**SimulatedDevice**, una versione modificata dell'applicazione hello creato in hello [iniziare con l'IoT Hub] esercitazione invia i messaggi da dispositivo a cloud punto dati ogni secondo e interattivo dispositivo a cloud messaggi ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="9b10b-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="9b10b-112">**ReadDeviceToCloudMessages** che consente di visualizzare hello non critici telemetria inviato per l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9b10b-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="9b10b-113">**ReadCriticalQueue** coda i messaggi critici di hello inviati per l'app del dispositivo da una coda del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="9b10b-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="9b10b-114">La coda è l'hub IoT toohello associata.</span><span class="sxs-lookup"><span data-stu-id="9b10b-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="9b10b-115">L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9b10b-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="9b10b-116">toolearn come tooreplace hello dispositivo simulato in questa esercitazione con un dispositivo fisico, vedere hello [Centro per sviluppatori di Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="9b10b-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="9b10b-117">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9b10b-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9b10b-118">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9b10b-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="9b10b-119">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9b10b-119">An active Azure account.</span></span> <br/><span data-ttu-id="9b10b-120">Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9b10b-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="9b10b-121">È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].</span><span class="sxs-lookup"><span data-stu-id="9b10b-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="9b10b-122">Inviare messaggi interattivi</span><span class="sxs-lookup"><span data-stu-id="9b10b-122">Send interactive messages</span></span>

<span data-ttu-id="9b10b-123">Modificare hello app del dispositivo è stato creato in hello [iniziare con l'IoT Hub] toooccasionally esercitazione interattiva messaggi.</span><span class="sxs-lookup"><span data-stu-id="9b10b-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="9b10b-124">In Visual Studio, in hello **SimulatedDevice** del progetto, sostituire hello `SendDeviceToCloudMessagesAsync` metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="9b10b-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="9b10b-125">Questo metodo aggiunge in modo casuale proprietà hello `"level": "critical"` toomessages inviato dal dispositivo hello, che simula un messaggio che richiede un intervento immediato per hello soluzione back-end.</span><span class="sxs-lookup"><span data-stu-id="9b10b-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="9b10b-126">app per dispositivi Hello passare le informazioni nelle proprietà di messaggio hello, anziché nel corpo del messaggio hello, in modo che l'IoT Hub può instradare destinazione dei messaggi appropriata toohello messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="9b10b-127">È possibile utilizzare i messaggi tooroute di proprietà di messaggio per vari scenari, tra cui freddo-path, l'elaborazione, inoltre toohello hot-percorso riportato di seguito viene illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9b10b-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="9b10b-128">Per i migliori risultati hello di semplicità, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="9b10b-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="9b10b-129">Nel codice di produzione, è necessario implementare un criterio di ripetizione, ad esempio backoff esponenziale, come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="9b10b-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="9b10b-130">Coda di tooa route dei messaggi nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="9b10b-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="9b10b-131">In questa sezione verrà illustrato come:</span><span class="sxs-lookup"><span data-stu-id="9b10b-131">In this section, you:</span></span>

* <span data-ttu-id="9b10b-132">Creare una coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="9b10b-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="9b10b-133">La connessione hub IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="9b10b-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="9b10b-134">Configurare la coda IoT hub toosend messaggi toohello in base hello presenza di una proprietà nel messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="9b10b-135">Per ulteriori informazioni su come tooprocess messaggi dalle code del Bus di servizio, vedere [iniziare con le code][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="9b10b-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="9b10b-136">Creare una coda del bus di servizio, come descritto in [Get started with queues][Service Bus queue] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="9b10b-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="9b10b-137">deve essere coda Hello hello stessa sottoscrizione e area, come l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9b10b-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="9b10b-138">Prendere nota del nome dello spazio dei nomi e di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b10b-139">Nelle code e negli argomenti del bus di servizio usati come endpoint dell'hub IoT non devono essere abilitati le **sessioni** e il **rilevamento duplicati**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="9b10b-140">Se una di queste opzioni sono abilitata, l'endpoint di hello viene visualizzato come **non raggiungibile** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b10b-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="9b10b-141">In hello portale di Azure, aprire l'hub IoT e fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Endpoint in hub IoT][30]

3. <span data-ttu-id="9b10b-143">In hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooadd superiore dell'hub IoT tooyour di coda.</span><span class="sxs-lookup"><span data-stu-id="9b10b-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="9b10b-144">Endpoint hello nome **CriticalQueue** e utilizzare hello elenchi a discesa tooselect **coda di Service Bus**hello dello spazio dei nomi Service Bus in cui risiede la coda e nome della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="9b10b-145">Al termine, fare clic su **salvare** nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Aggiunta di un endpoint][31]
    
4. <span data-ttu-id="9b10b-147">Fare clic su **Route** nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9b10b-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="9b10b-148">Fare clic su **Aggiungi** nella parte superiore di hello di hello pannello toocreate una regola di routing che instrada i messaggi toohello coda è appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="9b10b-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="9b10b-149">Selezionare **DeviceTelemetry** come origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="9b10b-150">Immettere `level="critical"` come condizione hello e scegliere coda hello appena aggiunto come un endpoint personalizzato come hello endpoint regola di routing.</span><span class="sxs-lookup"><span data-stu-id="9b10b-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="9b10b-151">Al termine, fare clic su **salvare** nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Aggiunta di un route][32]
    
    <span data-ttu-id="9b10b-153">Assicurarsi di route fallback hello è troppo**ON**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="9b10b-154">Questo valore è hello predefinita per un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9b10b-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Route di fallback][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="9b10b-156">Lettura dall'endpoint di coda hello</span><span class="sxs-lookup"><span data-stu-id="9b10b-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="9b10b-157">In questa sezione, leggere i messaggi hello dall'endpoint di coda hello.</span><span class="sxs-lookup"><span data-stu-id="9b10b-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="9b10b-158">In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="9b10b-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="9b10b-159">Progetto hello nome **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="9b10b-160">In Esplora soluzioni fare doppio clic su hello **ReadCriticalQueue** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="9b10b-161">Questa operazione consente di visualizzare hello **Gestione pacchetti NuGet** finestra.</span><span class="sxs-lookup"><span data-stu-id="9b10b-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="9b10b-162">Cercare **Windowsazure**, fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="9b10b-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="9b10b-163">Questa operazione Scarica, installa e aggiunge un toohello riferimento Azure Service Bus, con tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9b10b-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="9b10b-164">Aggiungere il seguente hello **utilizzando** le istruzioni nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="9b10b-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="9b10b-165">Infine, aggiungere hello seguenti righe toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="9b10b-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="9b10b-166">Sostituire la stringa di connessione hello con **ascolto** le autorizzazioni per la coda hello:</span><span class="sxs-lookup"><span data-stu-id="9b10b-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
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

## <a name="run-hello-applications"></a><span data-ttu-id="9b10b-167">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="9b10b-167">Run hello applications</span></span>
<span data-ttu-id="9b10b-168">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="9b10b-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="9b10b-169">In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="9b10b-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="9b10b-170">Selezionare **più progetti di avvio**, quindi selezionare **avviare** come azione hello per hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **ReadCriticalQueue** progetti.</span><span class="sxs-lookup"><span data-stu-id="9b10b-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="9b10b-171">Premere **F5** toostart hello tre applicazioni console.</span><span class="sxs-lookup"><span data-stu-id="9b10b-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="9b10b-172">Hello **ReadDeviceToCloudMessages** app ha solo i messaggi non critici inviati dal hello **SimulatedDevice** applicazione e hello **ReadCriticalQueue** dispone solo di app messaggi critici.</span><span class="sxs-lookup"><span data-stu-id="9b10b-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Tre app console][50]

## <a name="next-steps"></a><span data-ttu-id="9b10b-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b10b-174">Next steps</span></span>
<span data-ttu-id="9b10b-175">In questa esercitazione è stato descritto come tooreliably inviare i messaggi da dispositivo a cloud tramite funzionalità di routing messaggi hello dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9b10b-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="9b10b-176">Hello [come toosend cloud a dispositivo messaggi con l'IoT Hub] [ lnk-c2d] viene illustrato come toosend messaggi dispositivi tooyour la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="9b10b-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="9b10b-177">esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="9b10b-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="9b10b-178">toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="9b10b-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="9b10b-179">toolearn informazioni su routing dei messaggi nell'IoT Hub, vedere [inviare e ricevere messaggi con l'IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="9b10b-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Archiviazione di Azure]: https://azure.microsoft.com/documentation/services/storage/
[bus di servizio di Azure]: https://azure.microsoft.com/documentation/services/service-bus/
[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[iniziare con l'IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro per sviluppatori di Azure IoT]: https://azure.microsoft.com/develop/iot
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
