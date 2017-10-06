---
title: aaaOverview di hello API .NET di hub eventi Azure Standard | Documenti Microsoft
description: Panoramica dell'API .NET Standard
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a>Panoramica dell'API .NET Standard di Hub eventi
In questo articolo riepiloga alcune delle chiave hello API client .NET hub eventi Standard. Esistono attualmente due librerie client .NET Standard:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Questa libreria offre tutte le operazioni di runtime di base.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Questa libreria aggiunge nuove funzionalità che consente di tenere traccia di eventi elaborati, hello tooread di modo più semplice da un hub eventi.

## <a name="event-hubs-client"></a>Client di Hub eventi
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) è hello oggetto primario, utilizzare eventi toosend, creare ricevitori e informazioni di run-time tooget. Questo client è collegato tooa particolare evento hub e crea un nuovo endpoint di hub eventi toohello di connessione.

### <a name="create-an-event-hubs-client"></a>Creare un client di Hub eventi
Un oggetto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) viene creato da una stringa di connessione. tooinstantiate modo più semplice di Hello un nuovo client è illustrata nell'esempio seguente hello:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically modificare la stringa di connessione hello, è possibile usare hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passare la stringa di connessione hello come parametro troppo[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Inviare eventi
hub di eventi di toosend eventi tooan, utilizzare hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe. corpo Hello deve essere un `byte` , matrice o un `byte` segmento di matrice.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Ricevere eventi
Hello consigliato eventi tooreceive modo dagli hub eventi Usa hello [Host processore di eventi](#event-processor-host-apis), che fornisce funzionalità tooautomatically tenere traccia dell'offset e informazioni sulla partizione. Tuttavia, esistono determinate situazioni in cui è possibile scegliere flessibilità hello toouse eventi hello core hub eventi libreria tooreceive.

#### <a name="create-a-receiver"></a>Creare un ricevitore
Ricevitori sono legati toospecific partizioni, pertanto, in ordine tooreceive tutti gli eventi in un hub eventi, è necessario toocreate più istanze. In genere, si tratta una buona norma tooget hello partizione informazioni a livello di codice, anziché a livello di codice gli ID di partizione hello. In ordine toodo questa operazione, è possibile usare hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) metodo.

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

Poiché gli eventi non vengono mai rimosse da un hub di eventi (e solo scadono), è necessario punto iniziale di toospecify hello appropriato. Hello seguito sono riportate le possibili combinazioni.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Usare un evento
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a>API host processore di eventi
Le API forniscono processi tooworker resilienza che potrebbero diventare non disponibili, distribuendo le partizioni tra thread di lavoro disponibili.

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

Hello seguito è riportato un esempio di implementazione di hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Passaggi successivi
toolearn più sugli scenari di hub eventi, visitare i collegamenti:

* [Che cos'è l'hub di eventi di Azure?](event-hubs-what-is-event-hubs.md)
* [Available Event Hubs apis](event-hubs-api-overview.md) (API di Hub eventi disponibili)

in questa sezione sono riportati i riferimenti alle API di .NET di Hello:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)