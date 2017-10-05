---
title: Messaggi da cloud a dispositivo con l'hub IoT di Azure (.NET) | Documentazione Microsoft
description: Come inviare messaggi da cloud a dispositivo a un dispositivo da un hub IoT di Azure usando gli SDK di Azure IoT per .NET. Si modifica un'app per dispositivi per ricevere i messaggi diretti dal cloud al dispositivo e si modifica un'app back-end per inviare i messaggi diretti dal cloud al dispositivo.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="bfa94-104">Inviare messaggi dal cloud al dispositivo con Hub IoT (.NET)</span><span class="sxs-lookup"><span data-stu-id="bfa94-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="bfa94-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="bfa94-105">Introduction</span></span>
<span data-ttu-id="bfa94-106">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="bfa94-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="bfa94-107">L'esercitazione [Introduzione all'hub IoT di Azure] illustra come creare un hub IoT, effettuare il provisioning dell'identità di un dispositivo al suo interno e creare il codice di un'app per dispositivi che invia messaggi dal dispositivo al cloud.</span><span class="sxs-lookup"><span data-stu-id="bfa94-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="bfa94-108">Questa esercitazione si basa su [Introduzione all'hub IoT di Azure].</span><span class="sxs-lookup"><span data-stu-id="bfa94-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="bfa94-109">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bfa94-109">It shows you how to:</span></span>

* <span data-ttu-id="bfa94-110">Dal back-end della soluzione inviare messaggi da cloud a dispositivo a un singolo dispositivo tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bfa94-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="bfa94-111">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="bfa94-112">Dal back-end della soluzione richiedere l'acknowledgement di recapito (*feedback*) per i messaggi inviati a un dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bfa94-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="bfa94-113">Per altre informazioni sui messaggi da cloud a dispositivo, vedere la[Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="bfa94-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="bfa94-114">Al termine di questa esercitazione vengono eseguite due app console .NET:</span><span class="sxs-lookup"><span data-stu-id="bfa94-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="bfa94-115">**SimulatedDevice**, una versione modificata dell'app creata in [Introduzione all'hub IoT di Azure], che si connette all'hub IoT e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="bfa94-116">**SendCloudToDevice**, che invia un messaggio diretto dal cloud al dispositivo all'app per dispositivi tramite l'hub IoT e quindi riceve la conferma di recapito.</span><span class="sxs-lookup"><span data-stu-id="bfa94-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="bfa94-117">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi, tra cui C, Java e Javascript, tramite gli [SDK del dispositivo IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="bfa94-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="bfa94-118">Per istruzioni dettagliate su come connettere il dispositivo al codice dell'esercitazione e in generale all'hub IoT di Azure, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="bfa94-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="bfa94-119">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bfa94-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="bfa94-120">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bfa94-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="bfa94-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-121">An active Azure account.</span></span> <span data-ttu-id="bfa94-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bfa94-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="bfa94-123">Ricevere messaggi nell'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="bfa94-123">Receive messages in the device app</span></span>
<span data-ttu-id="bfa94-124">In questa sezione si modificherà l'app per dispositivi creata in [Introduzione all'hub IoT di Azure] per ricevere i messaggi diretti dal cloud al dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bfa94-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="bfa94-125">In Visual Studio, nel progetto **SimulatedDevice** aggiungere il seguente metodo alla classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="bfa94-126">Il metodo `ReceiveAsync` restituisce in modo asincrono il messaggio ricevuto nel momento in cui viene ricevuto dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="bfa94-127">Restituisce *null* dopo un periodo di timeout specificabile (in questo caso viene usato il valore predefinito di un minuto).</span><span class="sxs-lookup"><span data-stu-id="bfa94-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="bfa94-128">Quando l'app riceve un valore *Null*, deve rimanere in attesa di nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="bfa94-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="bfa94-129">Questo requisito è il motivo per la riga `if (receivedMessage == null) continue`.</span><span class="sxs-lookup"><span data-stu-id="bfa94-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="bfa94-130">La chiamata a `CompleteAsync()` notifica all'hub IoT che il messaggio è stato elaborato correttamente.</span><span class="sxs-lookup"><span data-stu-id="bfa94-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="bfa94-131">Il messaggio può essere rimosso dalla coda del dispositivo in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="bfa94-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="bfa94-132">Se si è verificato un evento che ha impedito all'app per dispositivo di completare l'elaborazione del messaggio, l'hub IoT lo recapita nuovamente.</span><span class="sxs-lookup"><span data-stu-id="bfa94-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="bfa94-133">È quindi importante che la logica di elaborazione del messaggio nell'app per dispositivo sia *idempotente*, in modo che la ricezione dello stesso messaggio più volte produca lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="bfa94-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="bfa94-134">Un'applicazione può anche abbandonare temporaneamente un messaggio e, di conseguenza, l'hub IoT mantiene il messaggio nella coda per un uso futuro.</span><span class="sxs-lookup"><span data-stu-id="bfa94-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="bfa94-135">In alternativa, l'applicazione può rifiutare un messaggio, rimuovendolo così definitivamente dalla coda.</span><span class="sxs-lookup"><span data-stu-id="bfa94-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="bfa94-136">Per altre informazioni sul ciclo di vita del messaggio da cloud a dispositivo, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="bfa94-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bfa94-137">Quando si usa HTTP invece di MQTT o AMQP come trasporto, il metodo `ReceiveAsync` verrà restituito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="bfa94-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="bfa94-138">Il modello supportato per i messaggi da cloud a dispositivo con HTTP è dispositivi collegati occasionalmente che controllano raramente la presenza di messaggi (a intervalli inferiori 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="bfa94-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="bfa94-139">La generazione di altre ricezioni HTTP comporta la limitazione delle richieste da parte dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bfa94-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="bfa94-140">Per altre informazioni sulle differenze tra il supporto di MQTT, AMQP e HTTP e sulla limitazione delle richieste dell'hub IoT, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="bfa94-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="bfa94-141">Aggiungere il metodo seguente al metodo **Main** immediatamente prima della riga `Console.ReadLine()`:</span><span class="sxs-lookup"><span data-stu-id="bfa94-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="bfa94-142">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="bfa94-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="bfa94-143">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="bfa94-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="bfa94-144">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="bfa94-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="bfa94-145">In questa sezione viene scritta un'app console di .NET che invia messaggi da cloud a dispositivo all'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bfa94-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="bfa94-146">Nella soluzione di Visual Studio corrente creare un progetto di applicazioni desktop in Visual C# usando il modello di progetto **Applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="bfa94-147">Denominare il progetto **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Nuovo progetto in Visual Studio][20]
2. <span data-ttu-id="bfa94-149">In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="bfa94-150">L'azione consente di visualizzare la finestra **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="bfa94-151">Cercare **Microsoft.Azure.Devices**, fare clic su **Installa** e quindi accettare le condizioni per l'uso.</span><span class="sxs-lookup"><span data-stu-id="bfa94-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="bfa94-152">Verrà quindi scaricato e installato il [pacchetto NuGet Azure IoT Service SDK] e verrà aggiunto un riferimento a tale pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bfa94-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="bfa94-153">Aggiungere l'istruzione `using` seguente all'inizio del file **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="bfa94-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="bfa94-154">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="bfa94-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="bfa94-155">Sostituire il valore del segnaposto con la stringa di connessione all'hub IoT da [Introduzione all'hub IoT di Azure]:</span><span class="sxs-lookup"><span data-stu-id="bfa94-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="bfa94-156">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="bfa94-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="bfa94-157">Questo metodo invia un nuovo messaggio da cloud a dispositivo al dispositivo con ID `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="bfa94-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="bfa94-158">Modificare questo parametro solo nel caso in cui sia stato modificato rispetto a quello usato in [Introduzione all'hub IoT di Azure].</span><span class="sxs-lookup"><span data-stu-id="bfa94-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="bfa94-159">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="bfa94-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="bfa94-160">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**. Selezionare **Progetti di avvio multipli**, quindi selezionare l'azione **Start** per **ReadDeviceToCloudMessages**, **SimulatedDevice** e **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="bfa94-161">Premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-161">Press **F5**.</span></span> <span data-ttu-id="bfa94-162">Devono avviarsi tutte e tre le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bfa94-162">All three applications should start.</span></span> <span data-ttu-id="bfa94-163">Selezionare la finestra **SendCloudToDevice** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="bfa94-164">Verrà visualizzato il messaggio ricevuto dall'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="bfa94-164">You should see the message being received by the device app.</span></span>
   
   ![Ricezione di un messaggio da parte dell'app][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="bfa94-166">Ricevere feedback di recapito</span><span class="sxs-lookup"><span data-stu-id="bfa94-166">Receive delivery feedback</span></span>
<span data-ttu-id="bfa94-167">È possibile richiedere la conferma della ricezione (o della scadenza) dall'hub IoT per ogni messaggio da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="bfa94-168">Questa opzione consente al back-end della soluzione di informare facilmente la logica di ripetizione o di compensazione.</span><span class="sxs-lookup"><span data-stu-id="bfa94-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="bfa94-169">Per altre informazioni sul feedback da cloud a dispositivo, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="bfa94-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="bfa94-170">In questa sezione viene modificata l'app **SendCloudToDevice** per richiedere feedback e riceverli dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bfa94-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="bfa94-171">In Visual Studio, nel progetto **SendCloudToDevice** aggiungere il seguente metodo alla classe **Programma**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="bfa94-172">Si noti che il modello di ricezione è identico a quello usato per ricevere messaggi da cloud a dispositivo dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="bfa94-173">Aggiungere il metodo seguente nel metodo **Main`serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` immediatamente dopo la riga** :</span><span class="sxs-lookup"><span data-stu-id="bfa94-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="bfa94-174">Per richiedere feedback del recapito del messaggio da cloud a dispositivo, è necessario specificare una proprietà nel metodo **SendCloudToDeviceMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="bfa94-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="bfa94-175">Aggiungere la riga seguente, subito dopo la riga `var commandMessage = new Message(...);` :</span><span class="sxs-lookup"><span data-stu-id="bfa94-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="bfa94-176">Premere **F5**per eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="bfa94-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="bfa94-177">Si dovrebbero avviare tutte e tre le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bfa94-177">You should see all three applications start.</span></span> <span data-ttu-id="bfa94-178">Selezionare la finestra **SendCloudToDevice** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="bfa94-179">Verrà visualizzata la ricezione del messaggio da parte dell'app per dispositivi e, dopo alcuni secondi, la ricezione del messaggio di feedback da parte dell'applicazione **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="bfa94-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Ricezione di un messaggio da parte dell'app][22]

> [!NOTE]
> <span data-ttu-id="bfa94-181">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="bfa94-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="bfa94-182">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="bfa94-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bfa94-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfa94-183">Next steps</span></span>
<span data-ttu-id="bfa94-184">In questa esercitazione è stato descritto come inviare e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bfa94-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="bfa94-185">Per avere degli esempi di soluzioni complete che utilizzano l'hub IoT, vedere la [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="bfa94-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="bfa94-186">Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="bfa94-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacchetto NuGet Azure IoT Service SDK]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md
[Introduzione all'hub IoT di Azure]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK del dispositivo IoT Azure]: iot-hub-devguide-sdks.md