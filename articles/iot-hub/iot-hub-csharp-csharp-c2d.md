---
title: i messaggi aaaCloud al dispositivo con Azure IoT Hub (.NET) | Documenti Microsoft
description: "La modalità toosend cloud a dispositivo dei messaggi tooa dispositivo da un hub IoT di Azure usando hello Azure IoT SDK per .NET. Per modificare i messaggi di cloud a dispositivo un dispositivo app tooreceive e modificare un messaggio di cloud a dispositivo hello toosend app back-end."
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
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="07646-104">Inviare messaggi da dispositivo di tooyour hello cloud con Hub IoT (.NET)</span><span class="sxs-lookup"><span data-stu-id="07646-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="07646-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="07646-105">Introduction</span></span>
<span data-ttu-id="07646-106">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="07646-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="07646-107">Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app di dispositivo che invia messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="07646-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="07646-108">Questa esercitazione si basa su [iniziare con l'IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="07646-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="07646-109">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="07646-109">It shows you how to:</span></span>

* <span data-ttu-id="07646-110">Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07646-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="07646-111">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="07646-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="07646-112">Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07646-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="07646-113">Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="07646-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="07646-114">Alla fine di hello di questa esercitazione, si esegue due applicazioni di console .NET:</span><span class="sxs-lookup"><span data-stu-id="07646-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="07646-115">**SimulatedDevice**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="07646-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="07646-116">**SendCloudToDevice**, che invia un'app di dispositivo toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.</span><span class="sxs-lookup"><span data-stu-id="07646-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="07646-117">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi, tra cui C, Java e Javascript, tramite gli [SDK del dispositivo IoT Azure].</span><span class="sxs-lookup"><span data-stu-id="07646-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="07646-118">Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="07646-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="07646-119">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="07646-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="07646-120">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="07646-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="07646-121">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="07646-121">An active Azure account.</span></span> <span data-ttu-id="07646-122">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="07646-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="07646-123">Ricezione di messaggi hello dispositivo App</span><span class="sxs-lookup"><span data-stu-id="07646-123">Receive messages in hello device app</span></span>
<span data-ttu-id="07646-124">In questa sezione, che si desidera modificare hello app del dispositivo è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="07646-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="07646-125">In Visual Studio, in hello **SimulatedDevice** del progetto, aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="07646-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
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
   
    <span data-ttu-id="07646-126">Hello `ReceiveAsync` (metodo) restituisce in modo asincrono il messaggio hello ricevuto in fase di hello ricevuto dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="07646-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="07646-127">Restituisce *null* dopo un periodo di timeout specificabile (in questo caso, viene usato predefinito hello è un minuto).</span><span class="sxs-lookup"><span data-stu-id="07646-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="07646-128">Quando applicazione hello riceve un *null*, deve continuare toowait per i nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="07646-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="07646-129">Questo requisito è motivo hello hello `if (receivedMessage == null) continue` riga.</span><span class="sxs-lookup"><span data-stu-id="07646-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="07646-130">Hello chiamata troppo`CompleteAsync()` notifica IoT Hub è stato elaborato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="07646-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="07646-131">messaggio Hello può essere rimossi dalla coda dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="07646-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="07646-132">Se si è verificato tale app dispositivo hello ha impedito di completare l'elaborazione di hello del messaggio hello un IoT Hub recapita nuovamente.</span><span class="sxs-lookup"><span data-stu-id="07646-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="07646-133">È quindi importante è il messaggio hello dispositivo App logica di elaborazione *idempotente*, in modo che la ricezione di hello stesso messaggio più volte produce hello stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="07646-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="07646-134">Un'applicazione può inoltre temporaneamente abbandono di un messaggio, che comporta l'hub IoT mantenendo il messaggio hello nella coda di hello per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="07646-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="07646-135">In alternativa, un'applicazione hello può rifiutare un messaggio, che consente di rimuovere definitivamente il messaggio hello dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="07646-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="07646-136">Per ulteriori informazioni sul ciclo di vita di hello messaggio cloud a dispositivo, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="07646-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="07646-137">Quando si Usa HTTP invece di MQTT o AMQP come trasporto, hello `ReceiveAsync` metodo viene restituito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="07646-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="07646-138">modello di Hello è supportato per i messaggi da cloud a dispositivo con HTTP è occasionali per i dispositivi che consentono di controllare per i messaggi raramente (meno di 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="07646-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="07646-139">Emissione ulteriori HTTP riceve i risultati nelle richieste hello limitazione IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07646-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="07646-140">Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="07646-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="07646-141">Aggiungere al metodo in hello hello **Main** (metodo), immediatamente prima di hello `Console.ReadLine()` riga:</span><span class="sxs-lookup"><span data-stu-id="07646-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="07646-142">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="07646-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="07646-143">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="07646-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="07646-144">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="07646-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="07646-145">In questa sezione, scrivere un'applicazione console .NET che invia messaggi da cloud a dispositivo toohello dispositivo app.</span><span class="sxs-lookup"><span data-stu-id="07646-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="07646-146">Nella soluzione di Visual Studio hello corrente, creare un progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="07646-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="07646-147">Progetto hello nome **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="07646-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Nuovo progetto in Visual Studio][20]
2. <span data-ttu-id="07646-149">In Esplora soluzioni fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione...** .</span><span class="sxs-lookup"><span data-stu-id="07646-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="07646-150">Questa azione apre hello **Gestisci pacchetti NuGet** finestra.</span><span class="sxs-lookup"><span data-stu-id="07646-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="07646-151">Cercare **Microsoft.Azure.Devices**, fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="07646-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="07646-152">Questo download, si installa e si aggiunge un riferimento toohello [pacchetto NuGet SDK del servizio Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="07646-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="07646-153">Aggiungere il seguente hello `using` istruzione nella parte superiore di hello di hello **Program.cs** file:</span><span class="sxs-lookup"><span data-stu-id="07646-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="07646-154">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="07646-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="07646-155">Sostituire il valore di segnaposto hello con stringa di connessione hub IoT hello da [iniziare con l'IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="07646-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="07646-156">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="07646-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="07646-157">Questo metodo invia un nuovo dispositivo toohello cloud a dispositivo messaggio con ID hello, `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="07646-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="07646-158">Modificare questo parametro solo se è stato modificato da hello quello utilizzato nel [iniziare con l'IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="07646-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="07646-159">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="07646-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="07646-160">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**. Selezionare **più progetti di avvio**, quindi selezionare hello **avviare** azione per **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="07646-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="07646-161">Premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="07646-161">Press **F5**.</span></span> <span data-ttu-id="07646-162">Devono avviarsi tutte e tre le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="07646-162">All three applications should start.</span></span> <span data-ttu-id="07646-163">Seleziona hello **SendCloudToDevice** windows e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="07646-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="07646-164">Verrà visualizzato il messaggio hello ricevuto dall'app per dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="07646-164">You should see hello message being received by hello device app.</span></span>
   
   ![Ricezione di un messaggio da parte dell'app][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="07646-166">Ricevere feedback di recapito</span><span class="sxs-lookup"><span data-stu-id="07646-166">Receive delivery feedback</span></span>
<span data-ttu-id="07646-167">È possibile toorequest recapito (scadenza) acknowledgment o dall'IoT Hub per ogni messaggio cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="07646-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="07646-168">Questo tooeasily di opzione Abilita hello soluzione back-end che indicano la logica di compensazione o di tentativi.</span><span class="sxs-lookup"><span data-stu-id="07646-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="07646-169">Per ulteriori informazioni sui commenti cloud a dispositivo, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="07646-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="07646-170">In questa sezione, si modifica hello **SendCloudToDevice** feedback toorequest app e riceve dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07646-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="07646-171">In Visual Studio, in hello **SendCloudToDevice** del progetto, aggiungere hello seguente metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="07646-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="07646-172">Nota di questo modello di ricezione è hello stessi messaggi cloud a dispositivo tooreceive usato uno dall'app per dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="07646-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="07646-173">Aggiungere al metodo in hello hello **Main** metodo subito dopo hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` riga:</span><span class="sxs-lookup"><span data-stu-id="07646-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="07646-174">toorequest commenti e suggerimenti per il recapito del messaggio da cloud a dispositivo hello, aver toospecify una proprietà in hello **SendCloudToDeviceMessageAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="07646-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="07646-175">Aggiungere hello successiva riga, subito dopo hello `var commandMessage = new Message(...);` riga:</span><span class="sxs-lookup"><span data-stu-id="07646-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="07646-176">Eseguire App hello premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="07646-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="07646-177">Si dovrebbero avviare tutte e tre le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="07646-177">You should see all three applications start.</span></span> <span data-ttu-id="07646-178">Seleziona hello **SendCloudToDevice** windows e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="07646-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="07646-179">Dovrebbe essere hello dei messaggi ricevuti dall'app per dispositivi hello e, dopo alcuni secondi, hello messaggio commenti e suggerimenti ricevuto dal **SendCloudToDevice** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07646-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Ricezione di un messaggio da parte dell'app][22]

> [!NOTE]
> <span data-ttu-id="07646-181">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="07646-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="07646-182">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="07646-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="07646-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07646-183">Next steps</span></span>
<span data-ttu-id="07646-184">In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="07646-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="07646-185">esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="07646-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="07646-186">toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="07646-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacchetto NuGet SDK del servizio Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[iniziare con l'IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK del dispositivo IoT Azure]: iot-hub-devguide-sdks.md