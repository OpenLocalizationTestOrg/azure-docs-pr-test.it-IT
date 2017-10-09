---
title: eventi aaaReceive da hub eventi di Azure tramite .NET Framework di hello | Documenti Microsoft
description: Seguire gli eventi di questa esercitazione tooreceive dall'hub di eventi di Azure utilizzando hello .NET Framework.
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
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="a6362-103">Ricevere eventi dall'hub di eventi di Azure utilizzando hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a6362-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="a6362-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a6362-104">Introduction</span></span>

<span data-ttu-id="a6362-105">Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="a6362-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="a6362-106">Dopo aver raccolto i dati in hub eventi, è possibile archiviare i dati di hello utilizzando un cluster di archiviazione o trasformare tramite un provider analitica in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a6362-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="a6362-107">Questa funzionalità di raccolta e l'elaborazione di eventi su larga scala è un componente fondamentale di architetture di applicazioni moderne inclusi hello Internet delle cose (IoT).</span><span class="sxs-lookup"><span data-stu-id="a6362-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="a6362-108">Questa esercitazione viene illustrato come toowrite di .NET Framework console applicazione che riceve i messaggi da un hub di eventi utilizzando hello  **[Host processore di eventi][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="a6362-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="a6362-109">gli eventi di toosend utilizzando hello .NET Framework, vedere hello [inviare eventi di hub di eventi tooAzure utilizzando .NET Framework hello](event-hubs-dotnet-framework-getstarted-send.md) articolo oppure fare clic sulla lingua invio hello appropriata nella tabella a sinistra di hello del contenuto.</span><span class="sxs-lookup"><span data-stu-id="a6362-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="a6362-110">Hello [Host processore di eventi] [ EventProcessorHost] è una classe .NET che semplifica la gestione dei checkpoint permanente ricevere gli eventi dagli hub eventi e parallelo riceve da agli hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="a6362-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="a6362-111">Utilizzo di hello [Host processore di eventi][Event Processor Host], è possibile dividere gli eventi in più ricevitori, anche quando sono ospitati in nodi diversi.</span><span class="sxs-lookup"><span data-stu-id="a6362-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="a6362-112">Questo esempio viene illustrato come hello toouse [Host processore di eventi] [ EventProcessorHost] per un singolo destinatario.</span><span class="sxs-lookup"><span data-stu-id="a6362-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="a6362-113">Hello [scalabilità l'elaborazione di eventi] [ Scale out Event Processing with Event Hubs] esempio viene illustrata la modalità hello toouse [Host processore di eventi] [ EventProcessorHost] con più destinatari.</span><span class="sxs-lookup"><span data-stu-id="a6362-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6362-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a6362-114">Prerequisites</span></span>

<span data-ttu-id="a6362-115">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="a6362-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="a6362-116">[Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a6362-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="a6362-117">le schermate di Hello in questa esercitazione usare Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a6362-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="a6362-118">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="a6362-118">An active Azure account.</span></span> <span data-ttu-id="a6362-119">Se non si ha un account, è possibile crearne uno gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a6362-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="a6362-120">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a6362-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="a6362-121">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a6362-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="a6362-122">primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate spazio dei nomi di tipo hub eventi e ottenere hello le credenziali di gestione, l'applicazione deve toocommunicate con hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a6362-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="a6362-123">toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md), quindi procedere con hello seguendo i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a6362-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a6362-124">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6362-124">Create an Azure Storage account</span></span>

<span data-ttu-id="a6362-125">hello toouse [Host processore di eventi][EventProcessorHost], è necessario disporre di un [account di archiviazione Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="a6362-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="a6362-126">Accesso toohello [portale di Azure][Azure portal], fare clic su **New** in hello in alto a sinistra della schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="a6362-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="a6362-127">Fare clic su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="a6362-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="a6362-128">In hello **creare account di archiviazione** pannello, digitare un nome per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="a6362-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="a6362-129">Scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a6362-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="a6362-130">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a6362-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="a6362-131">Nell'elenco di hello di account di archiviazione, fare clic su hello account di archiviazione appena creato.</span><span class="sxs-lookup"><span data-stu-id="a6362-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="a6362-132">Nel Pannello di account di archiviazione hello, fare clic su **le chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="a6362-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="a6362-133">Copiare il valore di hello di **key1** toouse più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a6362-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="a6362-134">Creare un'applicazione console per il ricevitore</span><span class="sxs-lookup"><span data-stu-id="a6362-134">Create a receiver console application</span></span>

1. <span data-ttu-id="a6362-135">In Visual Studio, creare un nuovo progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="a6362-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="a6362-136">Progetto hello nome **ricevitore**.</span><span class="sxs-lookup"><span data-stu-id="a6362-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="a6362-137">In Esplora soluzioni fare doppio clic su hello **ricevitore** del progetto e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione**.</span><span class="sxs-lookup"><span data-stu-id="a6362-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="a6362-138">Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="a6362-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="a6362-139">Fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="a6362-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="a6362-140">Visual Studio Scarica, installa e aggiunge un riferimento toohello [Hub di eventi di Azure Service Bus - pacchetto EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), con tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a6362-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="a6362-141">Pulsante destro del mouse hello **ricevitore** del progetto, fare clic su **Aggiungi**e quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="a6362-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="a6362-142">Nome nuova classe hello **SimpleEventProcessor**, quindi fare clic su **Aggiungi** classe hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a6362-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="a6362-143">Aggiungere hello seguendo le istruzioni nella parte superiore di hello del file SimpleEventProcessor.cs hello:</span><span class="sxs-lookup"><span data-stu-id="a6362-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="a6362-144">Quindi, sostituire hello seguente codice per il corpo della classe hello hello:</span><span class="sxs-lookup"><span data-stu-id="a6362-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
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
    
  <span data-ttu-id="a6362-145">Questa classe viene chiamata da hello **EventProcessorHost** tooprocess eventi ricevuti dall'hub di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a6362-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="a6362-146">Hello `SimpleEventProcessor` classe Usa un metodo di checkpoint stopwatch tooperiodically chiamata hello in hello **EventProcessorHost** contesto.</span><span class="sxs-lookup"><span data-stu-id="a6362-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="a6362-147">Questa elaborazione garantisce che, se il ricevitore hello viene riavviato, perde non più di cinque minuti di lavoro di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="a6362-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="a6362-148">In hello **programma** classe, aggiungere il seguente hello `using` istruzione all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="a6362-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="a6362-149">Sostituire quindi hello `Main` metodo hello `Program` classe con hello di codice seguente, sostituendo nome hub di eventi hello e connessioni a livello di spazio dei nomi hello stringa che è salvato in precedenza e hello account di archiviazione e la chiave che è stato copiato in hello Nelle sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="a6362-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
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
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="a6362-150">Eseguire il programma hello e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="a6362-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="a6362-151">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a6362-151">Congratulations!</span></span> <span data-ttu-id="a6362-152">Ora hanno ricevuto i messaggi da un hub di eventi utilizzando hello Host processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="a6362-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="a6362-153">Questa esercitazione usa una singola istanza di [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="a6362-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="a6362-154">velocità effettiva tooincrease, si consiglia di eseguire più istanze di [EventProcessorHost][EventProcessorHost], come illustrato nell'hello [scala all'elaborazione di eventi] [scala all'elaborazione di eventi] esempio.</span><span class="sxs-lookup"><span data-stu-id="a6362-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="a6362-155">In questi casi, hello varie istanze automaticamente coordinano tra loro gli eventi di tooload saldo hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="a6362-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="a6362-156">Se si desidera più ricevitori tooeach processo *tutti* hello eventi, è necessario utilizzare hello **gruppo di consumer per** concetto.</span><span class="sxs-lookup"><span data-stu-id="a6362-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="a6362-157">Quando si riceve eventi da computer diversi, potrebbe essere utile toospecify nomi per [EventProcessorHost] [ EventProcessorHost] istanze in base alle macchine hello (o ruoli) in cui vengono distribuiti.</span><span class="sxs-lookup"><span data-stu-id="a6362-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="a6362-158">Per ulteriori informazioni su questi argomenti, vedere hello [Panoramica di hub eventi] [ Event Hubs overview] hello e [Guida alla programmazione di hub eventi] [ Event Hubs Programming Guide] argomenti.</span><span class="sxs-lookup"><span data-stu-id="a6362-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a6362-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6362-159">Next steps</span></span>

<span data-ttu-id="a6362-160">Dopo aver creato un'applicazione funzionante che crea un hub eventi e invia e riceve i dati, per ulteriori informazioni, visitare hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a6362-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="a6362-161">[Host processore di eventi][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="a6362-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="a6362-162">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a6362-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="a6362-163">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a6362-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
