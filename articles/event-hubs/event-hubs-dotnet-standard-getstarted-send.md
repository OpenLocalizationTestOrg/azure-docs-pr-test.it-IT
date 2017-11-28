---
title: Inviare eventi a Hub eventi di Azure usando .NET Standard | Microsoft Docs
description: Guida introduttiva all'invio di eventi a Hub eventi in .NET Standard
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="239fb-103">Guida introduttiva all'invio di messaggi a Hub eventi di Azure in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="239fb-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="239fb-104">Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="239fb-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="239fb-105">Questa esercitazione illustra come scrivere un'applicazione console .NET Core che invii un set di messaggi a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="239fb-106">È possibile eseguire la soluzione [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) così com'è, sostituendo le stringhe `EhConnectionString` e `EhEntityPath` con i valori dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="239fb-107">In alternativa, è possibile seguire la procedura illustrata in questa esercitazione per creare una soluzione propria.</span><span class="sxs-lookup"><span data-stu-id="239fb-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="239fb-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="239fb-108">Prerequisites</span></span>

* <span data-ttu-id="239fb-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="239fb-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="239fb-110">Gli esempi inclusi nell'esercitazione usano Visual Studio 2017, ma è supportato anche Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="239fb-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="239fb-111">[Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="239fb-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="239fb-112">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="239fb-112">An Azure subscription.</span></span>
* <span data-ttu-id="239fb-113">Uno spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-113">An event hub namespace.</span></span>

<span data-ttu-id="239fb-114">Per inviare messaggi a un hub eventi, viene scritta un'applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="239fb-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="239fb-115">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="239fb-116">Il primo passaggio consiste nell'usare il [portale di Azure](https://portal.azure.com) per creare uno spazio dei nomi per il tipo Hub eventi e ottenere le credenziali di gestione richieste dall'applicazione per comunicare con l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="239fb-117">Per creare uno spazio dei nomi e un hub eventi, seguire la procedura descritta in [questo articolo](event-hubs-create.md) e procedere con i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="239fb-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="239fb-118">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="239fb-118">Create a console application</span></span>

<span data-ttu-id="239fb-119">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="239fb-119">Start Visual Studio.</span></span> <span data-ttu-id="239fb-120">Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="239fb-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="239fb-121">Creare un'applicazione console di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="239fb-121">Create a .NET Core console application.</span></span>

![Nuovo progetto][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="239fb-123">Aggiungere il pacchetto NuGet di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="239fb-124">Aggiungere il pacchetto NuGet della raccolta .NET standard [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) al progetto eseguendo i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="239fb-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="239fb-125">Fare clic con il pulsante destro del mouse sul progetto appena creato e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="239fb-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="239fb-126">Fare clic sulla scheda **Sfoglia**, quindi cercare "Microsoft.Azure.EventHubs" e selezionare il pacchetto **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="239fb-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="239fb-127">Fare clic su **Installa** per completare l'installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="239fb-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="239fb-128">Scrivere il codice per inviare messaggi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="239fb-129">Aggiungere le istruzioni `using` seguenti all'inizio del file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="239fb-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="239fb-130">Aggiungere le costanti per la classe `Program` per la stringa di connessione e il percorso dell'entità di Hub eventi (nome dell'hub eventi singolo).</span><span class="sxs-lookup"><span data-stu-id="239fb-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="239fb-131">Sostituire i segnaposto tra parentesi con i valori specifici ottenuti durante la creazione dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="239fb-132">Aggiungere alla classe `Program` un nuovo metodo denominato `MainAsync` come da esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="239fb-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="239fb-133">Aggiungere alla classe `Program` un nuovo metodo denominato `SendMessagesToEventHub` come da esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="239fb-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="239fb-134">Aggiungere il codice seguente al metodo `Main` nella classe `Program`.</span><span class="sxs-lookup"><span data-stu-id="239fb-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="239fb-135">Ecco l'aspetto che avrà il file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="239fb-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="239fb-136">Eseguire il programma e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="239fb-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="239fb-137">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="239fb-137">Congratulations!</span></span> <span data-ttu-id="239fb-138">Sono stati inviati messaggi a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="239fb-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="239fb-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="239fb-139">Next steps</span></span>
<span data-ttu-id="239fb-140">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="239fb-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="239fb-141">[Receive events from Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md) (Ricezione di eventi dall'Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="239fb-141">[Receive events from Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)</span></span>
* [<span data-ttu-id="239fb-142">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="239fb-143">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="239fb-144">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="239fb-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
