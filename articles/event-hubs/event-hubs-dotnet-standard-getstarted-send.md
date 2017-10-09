---
title: aaaSend eventi tooAzure hub di eventi tramite .NET Standard | Documenti Microsoft
description: Iniziare l'invio di tooEvent hub eventi in .NET Standard
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="a5159-103">Iniziare l'invio di messaggi tooAzure hub di eventi in .NET Standard</span><span class="sxs-lookup"><span data-stu-id="a5159-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="a5159-104">Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="a5159-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="a5159-105">Questa esercitazione viene illustrato come toowrite un'applicazione console .NET Core che invia una serie di messaggi tooan hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="a5159-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="a5159-106">È possibile eseguire hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) soluzione come-la sostituzione, hello `EhConnectionString` e `EhEntityPath` stringhe con i valori di hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="a5159-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="a5159-107">Oppure è possibile seguire hello i passaggi in questa esercitazione toocreate personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a5159-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5159-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5159-108">Prerequisites</span></span>

* <span data-ttu-id="a5159-109">[Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a5159-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="a5159-110">esempi di Hello in questa esercitazione usare Visual Studio 2017, ma Visual Studio 2015 è anche supportato.</span><span class="sxs-lookup"><span data-stu-id="a5159-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="a5159-111">[Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="a5159-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="a5159-112">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5159-112">An Azure subscription.</span></span>
* <span data-ttu-id="a5159-113">Uno spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a5159-113">An event hub namespace.</span></span>

<span data-ttu-id="a5159-114">hub di eventi tooan messaggi toosend, verrà utilizzato Visual Studio toowrite un'applicazione console c#.</span><span class="sxs-lookup"><span data-stu-id="a5159-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="a5159-115">Creare uno spazio dei nomi di Hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a5159-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="a5159-116">primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate uno spazio dei nomi per il tipo di hub eventi hello e ottenere le credenziali di gestione che l'applicazione deve toocommunicate con hub eventi hello di hello.</span><span class="sxs-lookup"><span data-stu-id="a5159-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="a5159-117">toocreate uno spazio dei nomi e un hub di eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md)e quindi procedere con hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="a5159-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="a5159-118">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="a5159-118">Create a console application</span></span>

<span data-ttu-id="a5159-119">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5159-119">Start Visual Studio.</span></span> <span data-ttu-id="a5159-120">Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="a5159-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="a5159-121">Creare un'applicazione console di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a5159-121">Create a .NET Core console application.</span></span>

![Nuovo progetto][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="a5159-123">Aggiungere il pacchetto NuGet di hub eventi hello</span><span class="sxs-lookup"><span data-stu-id="a5159-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="a5159-124">Aggiungere hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard NuGet pacchetto tooyour progetto di libreria attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a5159-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="a5159-125">Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a5159-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a5159-126">Fare clic su hello **Sfoglia** scheda, quindi cercare "Microsoft.Azure.EventHubs" e seleziona hello **Microsoft.Azure.EventHubs** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a5159-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="a5159-127">Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a5159-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="a5159-128">Scrivere alcuni hub di eventi di codice toosend messaggi toohello</span><span class="sxs-lookup"><span data-stu-id="a5159-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="a5159-129">Aggiungere il seguente hello `using` top toohello istruzioni del file Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="a5159-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="a5159-130">Aggiungere le costanti toohello `Program` classe per hello hub eventi connessione entità e stringa di percorso (nome dell'hub eventi singoli).</span><span class="sxs-lookup"><span data-stu-id="a5159-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="a5159-131">Sostituire i segnaposto hello tra parentesi quadre con i valori appropriati hello ottenute durante la creazione di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="a5159-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="a5159-132">Aggiungere un nuovo metodo denominato `MainAsync` toohello `Program` classe, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5159-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="a5159-133">Aggiungere un nuovo metodo denominato `SendMessagesToEventHub` toohello `Program` classe, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5159-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="a5159-134">Aggiungere i seguenti toohello codice hello `Main` metodo hello `Program` classe.</span><span class="sxs-lookup"><span data-stu-id="a5159-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="a5159-135">Ecco l'aspetto che avrà il file Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a5159-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="a5159-136">Eseguire il programma hello e assicurarsi che non siano presenti errori.</span><span class="sxs-lookup"><span data-stu-id="a5159-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="a5159-137">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="a5159-137">Congratulations!</span></span> <span data-ttu-id="a5159-138">Hub di eventi tooan messaggi inviati a questo punto.</span><span class="sxs-lookup"><span data-stu-id="a5159-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5159-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5159-139">Next steps</span></span>
<span data-ttu-id="a5159-140">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="a5159-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="a5159-141">[Receive events from Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md) (Ricezione di eventi dall'Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="a5159-141">[Receive events from Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)</span></span>
* [<span data-ttu-id="a5159-142">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a5159-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a5159-143">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="a5159-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a5159-144">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a5159-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
