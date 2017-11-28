---
title: Ricevere eventi da Hub eventi di Azure usando .NET Framework | Documentazione Microsoft
description: Seguire questa esercitazione per ricevere eventi da Hub eventi di Azure usando .NET Framework.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 581af52b3264b1a7c57315c65d5385a372308c27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="fe66b-103">Ricevere eventi da Hub eventi di Azure usando .NET Framework</span><span class="sxs-lookup"><span data-stu-id="fe66b-103">Receive events from Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="fe66b-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="fe66b-104">Introduction</span></span>

<span data-ttu-id="fe66b-105">Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="fe66b-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="fe66b-106">Dopo aver raccolto i dati in Hub eventi, è possibile archiviarli usando un cluster di archiviazione o trasformarli usando un provider di analisi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="fe66b-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="fe66b-107">Questa funzionalità di elaborazione e raccolta di eventi su vasta scala rappresenta un componente chiave delle moderne architetture di applicazioni, tra cui Internet delle cose (IoT).</span><span class="sxs-lookup"><span data-stu-id="fe66b-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="fe66b-108">Questa esercitazione illustra come scrivere un'applicazione console .NET Framework che riceve messaggi da un hub eventi usando l'**[host processore di eventi][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-108">This tutorial shows how to write a .NET Framework console application that receives messages from an event hub using the **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="fe66b-109">Per inviare eventi usando .NET Framework, vedere [Inviare eventi a Hub eventi di Azure usando .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) oppure fare clic sul linguaggio di invio appropriato nel sommario a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fe66b-109">To send events using the .NET Framework, see the [Send events to Azure Event Hubs using the .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click the appropriate sending language in the left-hand table of contents.</span></span>

<span data-ttu-id="fe66b-110">L'[host processore di eventi][EventProcessorHost] è una classe .NET che semplifica la ricezione di eventi dagli hub eventi gestendo checkpoint persistenti e ricezioni parallele da tali hub.</span><span class="sxs-lookup"><span data-stu-id="fe66b-110">The [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="fe66b-111">Usando l'[host processore di eventi][Event Processor Host] è possibile suddividere gli eventi su più ricevitori, anche se ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="fe66b-111">Using the [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="fe66b-112">Questo esempio illustra come usare l'[host processore di eventi][EventProcessorHost] per un ricevitore singolo.</span><span class="sxs-lookup"><span data-stu-id="fe66b-112">This example shows how to use the [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="fe66b-113">L'esempio di [elaborazione di eventi con aumento del numero di istanze][Scale out Event Processing with Event Hubs] illustra come usare l'[host processore di eventi][EventProcessorHost] con più ricevitori.</span><span class="sxs-lookup"><span data-stu-id="fe66b-113">The [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how to use the [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe66b-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fe66b-114">Prerequisites</span></span>

<span data-ttu-id="fe66b-115">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe66b-115">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="fe66b-116">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="fe66b-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="fe66b-117">Gli screenshot in questa esercitazione illustrano Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fe66b-117">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="fe66b-118">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="fe66b-118">An active Azure account.</span></span> <span data-ttu-id="fe66b-119">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="fe66b-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="fe66b-120">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fe66b-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="fe66b-121">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="fe66b-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="fe66b-122">Il primo passaggio consiste nell'usare il [portale di Azure](https://portal.azure.com) per creare uno spazio dei nomi di tipo Hub eventi e ottenere le credenziali di gestione necessarie all'applicazione per comunicare con l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fe66b-122">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="fe66b-123">Per creare uno spazio dei nomi e un hub eventi, seguire la procedura descritta in [questo articolo](event-hubs-create.md) e quindi procedere con i passaggi seguenti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fe66b-123">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="fe66b-124">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fe66b-124">Create an Azure Storage account</span></span>

<span data-ttu-id="fe66b-125">Per usare l'[host processore di eventi][EventProcessorHost] è necessario un [account di archiviazione di Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="fe66b-125">To use the [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="fe66b-126">Accedere al [portale di Azure][Azure portal] e fare clic su **Nuovo** nella parte superiore sinistra della schermata.</span><span class="sxs-lookup"><span data-stu-id="fe66b-126">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
2. <span data-ttu-id="fe66b-127">Fare clic su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="fe66b-128">Nel pannello **Crea account di archiviazione** digitare un nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fe66b-128">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="fe66b-129">Scegliere una sottoscrizione, un gruppo di risorse e una località di Azure in cui creare la risorsa.</span><span class="sxs-lookup"><span data-stu-id="fe66b-129">Choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="fe66b-130">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="fe66b-131">Nell'elenco degli account di archiviazione fare clic su quello appena creato.</span><span class="sxs-lookup"><span data-stu-id="fe66b-131">In the list of storage accounts, click the newly created storage account.</span></span>
5. <span data-ttu-id="fe66b-132">Nel pannello Account di archiviazione fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-132">In the storage account blade, click **Access keys**.</span></span> <span data-ttu-id="fe66b-133">Copiare il valore di **key1** da usare più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fe66b-133">Copy the value of **key1** to use later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="fe66b-134">Creare un'applicazione console per il ricevitore</span><span class="sxs-lookup"><span data-stu-id="fe66b-134">Create a receiver console application</span></span>

1. <span data-ttu-id="fe66b-135">In Visual Studio creare un nuovo progetto di app desktop di Visual C# usando il modello di progetto **Applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-135">In Visual Studio, create a new Visual C# Desktop App project using the **Console  Application** project template.</span></span> <span data-ttu-id="fe66b-136">Assegnare al progetto il nome **Receiver**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-136">Name the project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="fe66b-137">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **Receiver**, quindi scegliere **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-137">In Solution Explorer, right-click the **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="fe66b-138">Fare clic sulla scheda **Sfoglia** e quindi cercare `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="fe66b-138">Click the **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="fe66b-139">Fare clic su **Installa**e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="fe66b-139">Click **Install**, and accept the terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="fe66b-140">Visual Studio scarica e installa il [pacchetto NuGet Azure Service Bus Event Hub - EventProcessorHost](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost)e aggiunge un riferimento al pacchetto con tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="fe66b-140">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="fe66b-141">Fare clic con il pulsante destro del mouse sul progetto **Receiver**, scegliere **Aggiungi** e quindi **Classe**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-141">Right-click the **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="fe66b-142">Assegnare alla nuova classe il nome **SimpleEventProcessor** e quindi fare clic su **Aggiungi** per crearla.</span><span class="sxs-lookup"><span data-stu-id="fe66b-142">Name the new class **SimpleEventProcessor**, and then click **Add** to create the class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="fe66b-143">Aggiungere le istruzioni seguenti all'inizio del file SimpleEventProcessor.cs:</span><span class="sxs-lookup"><span data-stu-id="fe66b-143">Add the following statements at the top of the SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="fe66b-144">Sostituire quindi il corpo della classe con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fe66b-144">Then, substitute the following code for the body of the class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="fe66b-145">Questa classe è chiamata da **EventProcessorHost** per elaborare gli eventi ricevuti dall'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fe66b-145">This class is called by the **EventProcessorHost** to process events received from the event hub.</span></span> <span data-ttu-id="fe66b-146">La classe `SimpleEventProcessor` usa un cronometro per chiamare periodicamente il metodo checkpoint sul contesto di **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="fe66b-146">The `SimpleEventProcessor` class uses a stopwatch to periodically call the checkpoint method on the **EventProcessorHost** context.</span></span> <span data-ttu-id="fe66b-147">Questa elaborazione assicura che, se il ricevitore viene riavviato, non perde più di cinque minuti di lavoro di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="fe66b-147">This processing ensures that, if the receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="fe66b-148">Nella classe **Program** aggiungere l'istruzione `using` seguente all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="fe66b-148">In the **Program** class, add the following `using` statement at the top of the file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="fe66b-149">Sostituire quindi il metodo `Main` nella classe `Program` con il codice seguente, sostituendo il nome dell'hub eventi e la stringa di connessione a livello di spazio dei nomi salvata in precedenza, nonché l'account di archiviazione e la chiave copiata nelle sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="fe66b-149">Then, replace the `Main` method in the `Program` class with the following code, substituting the event hub name and the namespace-level connection string that you saved previously, and the storage account and key that you copied in the previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key to stop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="fe66b-150">Eseguire il programma e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="fe66b-150">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="fe66b-151">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="fe66b-151">Congratulations!</span></span> <span data-ttu-id="fe66b-152">Sono stati ricevuti messaggi da un hub eventi usando l'host processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="fe66b-152">You have now received messages from an event hub using the Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="fe66b-153">Questa esercitazione usa una singola istanza di [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="fe66b-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="fe66b-154">Per aumentare la velocità effettiva, è consigliabile eseguire più istanze di [EventProcessorHost][EventProcessorHost], come illustrato nell'esempio di [elaborazione di eventi con aumento del numero di istanze][elaborazione di eventi con aumento del numero di istanze].</span><span class="sxs-lookup"><span data-stu-id="fe66b-154">To increase throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in the [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="fe66b-155">In questi casi, le varie istanze si coordinano automaticamente tra loro per ottenere il bilanciamento del carico relativo agli eventi ricevuti.</span><span class="sxs-lookup"><span data-stu-id="fe66b-155">In those cases, the various instances automatically coordinate with each other to load balance the received events.</span></span> <span data-ttu-id="fe66b-156">Se si vuole che ognuno dei vari ricevitori elabori *tutti* gli eventi, è necessario usare il concetto **ConsumerGroup** .</span><span class="sxs-lookup"><span data-stu-id="fe66b-156">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="fe66b-157">Quando si ricevono eventi da più macchine, potrebbe risultare utile specificare nomi per le istanze di [EventProcessorHost][EventProcessorHost] in base alle macchine (o ai ruoli) in cui sono distribuite.</span><span class="sxs-lookup"><span data-stu-id="fe66b-157">When receiving events from different machines, it might be useful to specify names for [EventProcessorHost][EventProcessorHost] instances based on the machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="fe66b-158">Per altre informazioni su questi argomenti, vedere [Panoramica di Hub eventi][Event Hubs overview] e gli argomenti della [Guida alla programmazione di Hub eventi][Event Hubs Programming Guide].</span><span class="sxs-lookup"><span data-stu-id="fe66b-158">For more information about these topics, see the [Event Hubs overview][Event Hubs overview] and the [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fe66b-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe66b-159">Next steps</span></span>

<span data-ttu-id="fe66b-160">Ora che è stata creata un'applicazione funzionante che crea un hub eventi e invia e riceve dati, è possibile ottenere altre informazioni visitando i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fe66b-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting the following links:</span></span>

* <span data-ttu-id="fe66b-161">[Host processore di eventi][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="fe66b-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="fe66b-162">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="fe66b-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="fe66b-163">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="fe66b-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
