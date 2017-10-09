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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Iniziare l'invio di messaggi tooAzure hub di eventi in .NET Standard

> [!NOTE]
> Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Questa esercitazione viene illustrato come toowrite un'applicazione console .NET Core che invia una serie di messaggi tooan hub di eventi. È possibile eseguire hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) soluzione come-la sostituzione, hello `EhConnectionString` e `EhEntityPath` stringhe con i valori di hub di eventi. Oppure è possibile seguire hello i passaggi in questa esercitazione toocreate personalizzati.

## <a name="prerequisites"></a>Prerequisiti

* [Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com). esempi di Hello in questa esercitazione usare Visual Studio 2017, ma Visual Studio 2015 è anche supportato.
* [Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).
* Una sottoscrizione di Azure.
* Uno spazio dei nomi dell'hub eventi.

hub di eventi tooan messaggi toosend, verrà utilizzato Visual Studio toowrite un'applicazione console c#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creare uno spazio dei nomi di Hub eventi e un hub eventi

primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate uno spazio dei nomi per il tipo di hub eventi hello e ottenere le credenziali di gestione che l'applicazione deve toocommunicate con hub eventi hello di hello. toocreate uno spazio dei nomi e un hub di eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md)e quindi procedere con hello alla procedura seguente.

## <a name="create-a-console-application"></a>Creare un'applicazione console

Avviare Visual Studio. Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**. Creare un'applicazione console di .NET Core.

![Nuovo progetto][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Aggiungere il pacchetto NuGet di hub eventi hello

Aggiungere hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard NuGet pacchetto tooyour progetto di libreria attenendosi alla procedura seguente: 

1. Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.
2. Fare clic su hello **Sfoglia** scheda, quindi cercare "Microsoft.Azure.EventHubs" e seleziona hello **Microsoft.Azure.EventHubs** pacchetto. Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Scrivere alcuni hub di eventi di codice toosend messaggi toohello

1. Aggiungere il seguente hello `using` top toohello istruzioni del file Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Aggiungere le costanti toohello `Program` classe per hello hub eventi connessione entità e stringa di percorso (nome dell'hub eventi singoli). Sostituire i segnaposto hello tra parentesi quadre con i valori appropriati hello ottenute durante la creazione di hub eventi hello.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Aggiungere un nuovo metodo denominato `MainAsync` toohello `Program` classe, come indicato di seguito:

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

4. Aggiungere un nuovo metodo denominato `SendMessagesToEventHub` toohello `Program` classe, come indicato di seguito:

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

5. Aggiungere i seguenti toohello codice hello `Main` metodo hello `Program` classe.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Ecco l'aspetto che avrà il file Program.cs.

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

6. Eseguire il programma hello e assicurarsi che non siano presenti errori.

Congratulazioni. Hub di eventi tooan messaggi inviati a questo punto.

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Receive events from Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md) (Ricezione di eventi dall'Hub eventi)
* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
