---
title: eventi aaaReceive dall'hub di eventi di Azure usando .NET Standard | Documenti Microsoft
description: Introduzione alla ricezione di messaggi con hello EventProcessorHost in .NET Standard
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="01686-103">Introduzione alla ricezione di messaggi con hello Host processore di eventi in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="01686-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="01686-104">Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="01686-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="01686-105">Questa esercitazione viene illustrato come un .NET Core toowrite console applicazione che riceve i messaggi da un hub eventi tramite **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="01686-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="01686-106">È possibile eseguire hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) soluzione come-la sostituzione, le stringhe di hello con i valori di account hub e di archiviazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="01686-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="01686-107">Oppure è possibile seguire hello i passaggi in questa esercitazione toocreate personalizzati.</span><span class="sxs-lookup"><span data-stu-id="01686-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01686-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="01686-108">Prerequisites</span></span>

* <span data-ttu-id="01686-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="01686-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="01686-110">esempi di Hello in questa esercitazione usare Visual Studio 2017, ma Visual Studio 2015 è anche supportato.</span><span class="sxs-lookup"><span data-stu-id="01686-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="01686-111">[Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="01686-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="01686-112">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="01686-112">An Azure subscription.</span></span>
* <span data-ttu-id="01686-113">Uno spazio dei nomi di Hub eventi in Azure.</span><span class="sxs-lookup"><span data-stu-id="01686-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="01686-114">Un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="01686-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="01686-115">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="01686-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="01686-116">primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate uno spazio dei nomi per gli hub di eventi hello digitare e ottenere le credenziali di gestione che l'applicazione deve toocommunicate con hub eventi hello di hello.</span><span class="sxs-lookup"><span data-stu-id="01686-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="01686-117">toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md)e quindi procedere con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="01686-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="01686-118">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="01686-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="01686-119">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01686-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="01686-120">Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, fare clic su **archiviazione**, quindi fare clic su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="01686-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="01686-121">Completare i campi di hello nel Pannello di account di archiviazione hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="01686-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Crea account di archiviazione][1]

4. <span data-ttu-id="01686-123">Dopo aver visualizzato hello **ha avuto esito positivo di distribuzioni** del messaggio, fare clic sul nome del nuovo account di archiviazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="01686-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="01686-124">In hello **Essentials** pannello, fare clic su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="01686-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="01686-125">Quando hello **servizio Blob** fare clic su pannello **+ contenitore** nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="01686-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="01686-126">Assegnare un nome di contenitore hello e quindi chiudere hello **servizio Blob** blade.</span><span class="sxs-lookup"><span data-stu-id="01686-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="01686-127">Fare clic su **le chiavi di accesso** hello sinistro blade e copia hello un nome di contenitore di archiviazione hello, account di archiviazione hello e valore hello **key1**.</span><span class="sxs-lookup"><span data-stu-id="01686-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="01686-128">Salvare queste tooNotepad valori o un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="01686-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="01686-129">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="01686-129">Create a console application</span></span>

<span data-ttu-id="01686-130">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01686-130">Start Visual Studio.</span></span> <span data-ttu-id="01686-131">Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="01686-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="01686-132">Creare un'applicazione console di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="01686-132">Create a .NET Core console application.</span></span>

![Nuovo progetto][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="01686-134">Aggiungere il pacchetto NuGet di hub eventi hello</span><span class="sxs-lookup"><span data-stu-id="01686-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="01686-135">Aggiungere hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet pacchetti tooyour progetto di libreria attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="01686-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="01686-136">Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="01686-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="01686-137">Fare clic su hello **Sfoglia** scheda, quindi cercare "Microsoft.Azure.EventHubs" e seleziona hello **Microsoft.Azure.EventHubs** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="01686-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="01686-138">Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="01686-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="01686-139">Ripetere i passaggi 1 e 2 e installare hello **Microsoft.Azure.EventHubs.Processor** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="01686-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="01686-140">Implementare l'interfaccia IEventProcessor hello</span><span class="sxs-lookup"><span data-stu-id="01686-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="01686-141">In Esplora soluzioni, progetti hello pulsante destro del mouse, fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="01686-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="01686-142">Nome nuova classe hello **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="01686-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="01686-143">Aprire il file SimpleEventProcessor.cs hello e aggiungere il seguente hello `using` top toohello istruzioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="01686-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="01686-144">Hello implementare `IEventProcessor` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="01686-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="01686-145">Sostituire l'intero contenuto di hello di hello `SimpleEventProcessor` classe con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="01686-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="01686-146">Scrivere un metodo di console principale che utilizza i messaggi hello SimpleEventProcessor classe tooreceive</span><span class="sxs-lookup"><span data-stu-id="01686-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="01686-147">Aggiungere il seguente hello `using` top toohello istruzioni del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="01686-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="01686-148">Aggiungere le costanti toohello `Program` classe per la stringa di connessione hub eventi hello, nome hub eventi, il nome di contenitore account di archiviazione, nome account di archiviazione e chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="01686-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="01686-149">Aggiungere hello nel codice seguente, sostituendo i segnaposto hello con i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="01686-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="01686-150">Aggiungere un nuovo metodo denominato `MainAsync` toohello `Program` classe, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="01686-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="01686-151">Aggiungere hello successiva riga di codice toohello `Main` metodo:</span><span class="sxs-lookup"><span data-stu-id="01686-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="01686-152">Ecco l'aspetto che avrà il file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="01686-152">Here is what your Program.cs file should look like:</span></span>

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="01686-153">Eseguire il programma hello e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="01686-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="01686-154">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="01686-154">Congratulations!</span></span> <span data-ttu-id="01686-155">Ora ricevuti messaggi da un hub eventi tramite hello Host processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="01686-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01686-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01686-156">Next steps</span></span>
<span data-ttu-id="01686-157">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="01686-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="01686-158">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="01686-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="01686-159">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="01686-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="01686-160">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="01686-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
