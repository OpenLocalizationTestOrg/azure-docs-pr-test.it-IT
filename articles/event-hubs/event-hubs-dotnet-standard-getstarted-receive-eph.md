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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Introduzione alla ricezione di messaggi con hello Host processore di eventi in .NET Standard

> [!NOTE]
> Questo esempio è disponibile in [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Questa esercitazione viene illustrato come un .NET Core toowrite console applicazione che riceve i messaggi da un hub eventi tramite **EventProcessorHost**. È possibile eseguire hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) soluzione come-la sostituzione, le stringhe di hello con i valori di account hub e di archiviazione di eventi. Oppure è possibile seguire hello i passaggi in questa esercitazione toocreate personalizzati.

## <a name="prerequisites"></a>Prerequisiti

* [Microsoft Visual Studio 2015 o 2017](http://www.visualstudio.com). esempi di Hello in questa esercitazione usare Visual Studio 2017, ma Visual Studio 2015 è anche supportato.
* [Strumenti di Visual Studio 2015 o 2017 per .NET Core](http://www.microsoft.com/net/core).
* Una sottoscrizione di Azure.
* Uno spazio dei nomi di Hub eventi in Azure.
* Un account di archiviazione di Azure.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creare uno spazio dei nomi di Hub eventi e un hub eventi  

primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate uno spazio dei nomi per gli hub di eventi hello digitare e ottenere le credenziali di gestione che l'applicazione deve toocommunicate con hub eventi hello di hello. toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md)e quindi procedere con hello alla procedura seguente.  

## <a name="create-an-azure-storage-account"></a>Creare un account di archiviazione di Azure  

1. Accedi toohello [portale di Azure](https://portal.azure.com).  
2. Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **New**, fare clic su **archiviazione**, quindi fare clic su **Account di archiviazione**.  
3. Completare i campi di hello nel Pannello di account di archiviazione hello e quindi fare clic su **crea**.

    ![Crea account di archiviazione][1]

4. Dopo aver visualizzato hello **ha avuto esito positivo di distribuzioni** del messaggio, fare clic sul nome del nuovo account di archiviazione hello hello. In hello **Essentials** pannello, fare clic su **BLOB**. Quando hello **servizio Blob** fare clic su pannello **+ contenitore** nella parte superiore di hello. Assegnare un nome di contenitore hello e quindi chiudere hello **servizio Blob** blade.  
5. Fare clic su **le chiavi di accesso** hello sinistro blade e copia hello un nome di contenitore di archiviazione hello, account di archiviazione hello e valore hello **key1**. Salvare queste tooNotepad valori o un'altra posizione temporanea.  

## <a name="create-a-console-application"></a>Creare un'applicazione console

Avviare Visual Studio. Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**. Creare un'applicazione console di .NET Core.

![Nuovo progetto][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Aggiungere il pacchetto NuGet di hub eventi hello

Aggiungere hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet pacchetti tooyour progetto di libreria attenendosi alla procedura seguente: 

1. Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.
2. Fare clic su hello **Sfoglia** scheda, quindi cercare "Microsoft.Azure.EventHubs" e seleziona hello **Microsoft.Azure.EventHubs** pacchetto. Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.
3. Ripetere i passaggi 1 e 2 e installare hello **Microsoft.Azure.EventHubs.Processor** pacchetto.

## <a name="implement-hello-ieventprocessor-interface"></a>Implementare l'interfaccia IEventProcessor hello

1. In Esplora soluzioni, progetti hello pulsante destro del mouse, fare clic su **Aggiungi**, quindi fare clic su **classe**. Nome nuova classe hello **SimpleEventProcessor**.

2. Aprire il file SimpleEventProcessor.cs hello e aggiungere il seguente hello `using` top toohello istruzioni del file hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Hello implementare `IEventProcessor` interfaccia. Sostituire l'intero contenuto di hello di hello `SimpleEventProcessor` classe con hello seguente codice:

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Scrivere un metodo di console principale che utilizza i messaggi hello SimpleEventProcessor classe tooreceive

1. Aggiungere il seguente hello `using` top toohello istruzioni del file Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Aggiungere le costanti toohello `Program` classe per la stringa di connessione hub eventi hello, nome hub eventi, il nome di contenitore account di archiviazione, nome account di archiviazione e chiave dell'account di archiviazione. Aggiungere hello nel codice seguente, sostituendo i segnaposto hello con i relativi valori.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Aggiungere un nuovo metodo denominato `MainAsync` toohello `Program` classe, come indicato di seguito:

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

3. Aggiungere hello successiva riga di codice toohello `Main` metodo:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Ecco l'aspetto che avrà il file Program.cs:

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

4. Eseguire il programma hello e assicurarsi che non siano presenti errori.

Congratulazioni. Ora ricevuti messaggi da un hub eventi tramite hello Host processore di eventi.

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
