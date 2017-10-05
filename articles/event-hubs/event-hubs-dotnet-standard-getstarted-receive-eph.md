---
title: Ricevere eventi a Hub eventi di Azure usando .NET Standard | Microsoft Docs
description: Guida introduttiva alla ricezione di messaggi con EventProcessorHost in .NET Standard
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="b268b-103">Guida introduttiva alla ricezione di messaggi con Event Processor Host in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b268b-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="b268b-104">Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="b268b-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="b268b-105">In questa esercitazione viene illustrata la procedura per scrivere un'applicazione console .NET Core per ricevere messaggi da un hub eventi usando **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="b268b-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="b268b-106">È possibile eseguire la soluzione [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) così com'è, sostituendo le stringhe con i valori dell'hub eventi e dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b268b-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="b268b-107">In alternativa, è possibile seguire la procedura illustrata in questa esercitazione per creare una soluzione propria.</span><span class="sxs-lookup"><span data-stu-id="b268b-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b268b-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b268b-108">Prerequisites</span></span>

* <span data-ttu-id="b268b-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b268b-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="b268b-110">Gli esempi inclusi nell'esercitazione usano Visual Studio 2017, ma è supportato anche Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b268b-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="b268b-111">[Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="b268b-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="b268b-112">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b268b-112">An Azure subscription.</span></span>
* <span data-ttu-id="b268b-113">Uno spazio dei nomi di Hub eventi in Azure.</span><span class="sxs-lookup"><span data-stu-id="b268b-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="b268b-114">Un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b268b-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="b268b-115">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="b268b-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="b268b-116">Il primo passaggio consiste nell'usare il [portale di Azure](https://portal.azure.com) per creare uno spazio dei nomi per il tipo Hub eventi e ottenere le credenziali di gestione richieste dall'applicazione per comunicare con l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="b268b-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="b268b-117">Per creare uno spazio dei nomi e un hub eventi, seguire la procedura descritta in [questo articolo](event-hubs-create.md) e procedere con i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b268b-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b268b-118">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b268b-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="b268b-119">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b268b-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="b268b-120">Nel riquadro di spostamento sinistro del portale fare clic su **Nuovo**, quindi su **Archiviazione** e quindi su **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="b268b-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="b268b-121">Completare i campi nel pannello dell'account di archiviazione e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b268b-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Crea account di archiviazione][1]

4. <span data-ttu-id="b268b-123">Dopo aver visualizzato il messaggio **Le distribuzioni sono riuscite**, fare clic sul nome del nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b268b-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="b268b-124">Nel pannello **Informazioni di base** fare clic su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="b268b-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="b268b-125">Quando si apre il pannello **Servizio BLOB**, fare clic su **+ Contenitore** in alto.</span><span class="sxs-lookup"><span data-stu-id="b268b-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="b268b-126">Assegnare un nome al contenitore, quindi chiudere il pannello **Servizio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="b268b-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="b268b-127">Fare clic su **Chiavi di accesso** nel pannello a sinistra e copiare il nome del contenitore di archiviazione, dell'account di archiviazione e il valore **key1**.</span><span class="sxs-lookup"><span data-stu-id="b268b-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="b268b-128">Salvare questi valori nel Blocco note o in un'altra posizione temporanea.</span><span class="sxs-lookup"><span data-stu-id="b268b-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="b268b-129">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="b268b-129">Create a console application</span></span>

<span data-ttu-id="b268b-130">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b268b-130">Start Visual Studio.</span></span> <span data-ttu-id="b268b-131">Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="b268b-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="b268b-132">Creare un'applicazione console di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b268b-132">Create a .NET Core console application.</span></span>

![Nuovo progetto][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="b268b-134">Aggiungere il pacchetto NuGet di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="b268b-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="b268b-135">Aggiungere i pacchetti NuGet della raccolta .NET standard [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) al progetto eseguendo i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="b268b-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="b268b-136">Fare clic con il pulsante destro del mouse sul progetto appena creato e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b268b-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b268b-137">Fare clic sulla scheda **Sfoglia**, quindi cercare "Microsoft.Azure.EventHubs" e selezionare il pacchetto **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="b268b-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="b268b-138">Fare clic su **Installa** per completare l'installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b268b-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="b268b-139">Ripetere i passaggi 1 e 2 e installare il pacchetto **Microsoft.Azure.EventHubs.Processor**.</span><span class="sxs-lookup"><span data-stu-id="b268b-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="b268b-140">Implementare l'interfaccia IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="b268b-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="b268b-141">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Aggiungi** e fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="b268b-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="b268b-142">Assegnare il nome **SimpleEventProcessor** alla nuova classe.</span><span class="sxs-lookup"><span data-stu-id="b268b-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="b268b-143">Aprire il file SimpleEventProcessor.cs e aggiungere le istruzioni `using` seguenti all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="b268b-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="b268b-144">Implementare l'interfaccia `IEventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="b268b-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="b268b-145">Sostituire l'intero contenuto della classe `SimpleEventProcessor` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b268b-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="b268b-146">Scrivere un metodo console principale che usi la classe SimpleEventProcessor per ricevere i messaggi</span><span class="sxs-lookup"><span data-stu-id="b268b-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="b268b-147">Aggiungere le istruzioni `using` seguenti all'inizio del file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="b268b-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="b268b-148">Aggiungere le costanti alla classe `Program` per la stringa di connessione dell'hub eventi, il nome dell'hub, il nome del contenitore dell'account di archiviazione, il nome dell'account di archiviazione e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b268b-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="b268b-149">Aggiungere il codice seguente, sostituendo i segnaposto con i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="b268b-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="b268b-150">Aggiungere alla classe `Program` un nuovo metodo denominato `MainAsync` come da esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b268b-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="b268b-151">Aggiungere la riga di codice seguente al metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="b268b-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="b268b-152">Ecco l'aspetto che avrà il file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="b268b-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="b268b-153">Eseguire il programma e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="b268b-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="b268b-154">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b268b-154">Congratulations!</span></span> <span data-ttu-id="b268b-155">Sono stati appena ricevuti dei messaggi da un hub eventi usando l'host del processore di eventi.</span><span class="sxs-lookup"><span data-stu-id="b268b-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b268b-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b268b-156">Next steps</span></span>
<span data-ttu-id="b268b-157">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b268b-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="b268b-158">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="b268b-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b268b-159">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="b268b-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="b268b-160">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="b268b-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
