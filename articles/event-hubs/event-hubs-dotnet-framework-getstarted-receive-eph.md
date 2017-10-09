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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Ricevere eventi dall'hub di eventi di Azure utilizzando hello .NET Framework

## <a name="introduction"></a>Introduzione

Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi. Dopo aver raccolto i dati in hub eventi, è possibile archiviare i dati di hello utilizzando un cluster di archiviazione o trasformare tramite un provider analitica in tempo reale. Questa funzionalità di raccolta e l'elaborazione di eventi su larga scala è un componente fondamentale di architetture di applicazioni moderne inclusi hello Internet delle cose (IoT).

Questa esercitazione viene illustrato come toowrite di .NET Framework console applicazione che riceve i messaggi da un hub di eventi utilizzando hello  **[Host processore di eventi][EventProcessorHost]**. gli eventi di toosend utilizzando hello .NET Framework, vedere hello [inviare eventi di hub di eventi tooAzure utilizzando .NET Framework hello](event-hubs-dotnet-framework-getstarted-send.md) articolo oppure fare clic sulla lingua invio hello appropriata nella tabella a sinistra di hello del contenuto.

Hello [Host processore di eventi] [ EventProcessorHost] è una classe .NET che semplifica la gestione dei checkpoint permanente ricevere gli eventi dagli hub eventi e parallelo riceve da agli hub di eventi. Utilizzo di hello [Host processore di eventi][Event Processor Host], è possibile dividere gli eventi in più ricevitori, anche quando sono ospitati in nodi diversi. Questo esempio viene illustrato come hello toouse [Host processore di eventi] [ EventProcessorHost] per un singolo destinatario. Hello [scalabilità l'elaborazione di eventi] [ Scale out Event Processing with Event Hubs] esempio viene illustrata la modalità hello toouse [Host processore di eventi] [ EventProcessorHost] con più destinatari.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* [Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com). le schermate di Hello in questa esercitazione usare Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creare uno spazio dei nomi di Hub eventi e un hub eventi

primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate spazio dei nomi di tipo hub eventi e ottenere hello le credenziali di gestione, l'applicazione deve toocommunicate con hub eventi hello. toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md), quindi procedere con hello seguendo i passaggi in questa esercitazione.

## <a name="create-an-azure-storage-account"></a>Creare un account di Archiviazione di Azure

hello toouse [Host processore di eventi][EventProcessorHost], è necessario disporre di un [account di archiviazione Azure][Azure Storage account]:

1. Accesso toohello [portale di Azure][Azure portal], fare clic su **New** in hello in alto a sinistra della schermata di hello.
2. Fare clic su **Archiviazione** e quindi su **Account di archiviazione**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. In hello **creare account di archiviazione** pannello, digitare un nome per l'account di archiviazione hello. Scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate. Fare quindi clic su **Crea**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Nell'elenco di hello di account di archiviazione, fare clic su hello account di archiviazione appena creato.
5. Nel Pannello di account di archiviazione hello, fare clic su **le chiavi di accesso**. Copiare il valore di hello di **key1** toouse più avanti in questa esercitazione.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Creare un'applicazione console per il ricevitore

1. In Visual Studio, creare un nuovo progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **ricevitore**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. In Esplora soluzioni fare doppio clic su hello **ricevitore** del progetto e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione**.
3. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Fare clic su **installare**e accettare le condizioni di hello d'uso.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio Scarica, installa e aggiunge un riferimento toohello [Hub di eventi di Azure Service Bus - pacchetto EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), con tutte le relative dipendenze.
4. Pulsante destro del mouse hello **ricevitore** del progetto, fare clic su **Aggiungi**e quindi fare clic su **classe**. Nome nuova classe hello **SimpleEventProcessor**, quindi fare clic su **Aggiungi** classe hello toocreate.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Aggiungere hello seguendo le istruzioni nella parte superiore di hello del file SimpleEventProcessor.cs hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Quindi, sostituire hello seguente codice per il corpo della classe hello hello:
    
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
    
  Questa classe viene chiamata da hello **EventProcessorHost** tooprocess eventi ricevuti dall'hub di eventi hello. Hello `SimpleEventProcessor` classe Usa un metodo di checkpoint stopwatch tooperiodically chiamata hello in hello **EventProcessorHost** contesto. Questa elaborazione garantisce che, se il ricevitore hello viene riavviato, perde non più di cinque minuti di lavoro di elaborazione.
6. In hello **programma** classe, aggiungere il seguente hello `using` istruzione all'inizio di hello del file hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Sostituire quindi hello `Main` metodo hello `Program` classe con hello di codice seguente, sostituendo nome hub di eventi hello e connessioni a livello di spazio dei nomi hello stringa che è salvato in precedenza e hello account di archiviazione e la chiave che è stato copiato in hello Nelle sezioni precedenti. 
    
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

7. Eseguire il programma hello e assicurarsi che non siano presenti errori.
  
Congratulazioni. Ora hanno ricevuto i messaggi da un hub di eventi utilizzando hello Host processore di eventi.


> [!NOTE]
> Questa esercitazione usa una singola istanza di [EventProcessorHost][EventProcessorHost]. velocità effettiva tooincrease, si consiglia di eseguire più istanze di [EventProcessorHost][EventProcessorHost], come illustrato nell'hello [scala all'elaborazione di eventi] [scala all'elaborazione di eventi] esempio. In questi casi, hello varie istanze automaticamente coordinano tra loro gli eventi di tooload saldo hello ricevuto. Se si desidera più ricevitori tooeach processo *tutti* hello eventi, è necessario utilizzare hello **gruppo di consumer per** concetto. Quando si riceve eventi da computer diversi, potrebbe essere utile toospecify nomi per [EventProcessorHost] [ EventProcessorHost] istanze in base alle macchine hello (o ruoli) in cui vengono distribuiti. Per ulteriori informazioni su questi argomenti, vedere hello [Panoramica di hub eventi] [ Event Hubs overview] hello e [Guida alla programmazione di hub eventi] [ Event Hubs Programming Guide] argomenti.
> 
> 

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un'applicazione funzionante che crea un hub eventi e invia e riceve i dati, per ulteriori informazioni, visitare hello seguenti collegamenti:

* [Host processore di eventi][Event Processor Host]
* [Panoramica di Hub eventi][Event Hubs overview]
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

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
