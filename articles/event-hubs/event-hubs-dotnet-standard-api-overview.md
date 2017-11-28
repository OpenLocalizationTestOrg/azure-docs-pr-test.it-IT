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
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="90d3e-103">Panoramica dell'API .NET Standard di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="90d3e-104">In questo articolo riepiloga alcune delle chiave hello API client .NET hub eventi Standard.</span><span class="sxs-lookup"><span data-stu-id="90d3e-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="90d3e-105">Esistono attualmente due librerie client .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="90d3e-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="90d3e-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="90d3e-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="90d3e-107">Questa libreria offre tutte le operazioni di runtime di base.</span><span class="sxs-lookup"><span data-stu-id="90d3e-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="90d3e-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="90d3e-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="90d3e-109">Questa libreria aggiunge nuove funzionalità che consente di tenere traccia di eventi elaborati, hello tooread di modo più semplice da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="90d3e-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="90d3e-110">Client di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-110">Event Hubs client</span></span>
<span data-ttu-id="90d3e-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) è hello oggetto primario, utilizzare eventi toosend, creare ricevitori e informazioni di run-time tooget.</span><span class="sxs-lookup"><span data-stu-id="90d3e-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="90d3e-112">Questo client è collegato tooa particolare evento hub e crea un nuovo endpoint di hub eventi toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="90d3e-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="90d3e-113">Creare un client di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-113">Create an Event Hubs client</span></span>
<span data-ttu-id="90d3e-114">Un oggetto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) viene creato da una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="90d3e-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="90d3e-115">tooinstantiate modo più semplice di Hello un nuovo client è illustrata nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="90d3e-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="90d3e-116">tooprogrammatically modificare la stringa di connessione hello, è possibile usare hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) classe e passare la stringa di connessione hello come parametro troppo[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="90d3e-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="90d3e-117">Inviare eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-117">Send events</span></span>
<span data-ttu-id="90d3e-118">hub di eventi di toosend eventi tooan, utilizzare hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) classe.</span><span class="sxs-lookup"><span data-stu-id="90d3e-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="90d3e-119">corpo Hello deve essere un `byte` , matrice o un `byte` segmento di matrice.</span><span class="sxs-lookup"><span data-stu-id="90d3e-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="90d3e-120">Ricevere eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-120">Receive events</span></span>
<span data-ttu-id="90d3e-121">Hello consigliato eventi tooreceive modo dagli hub eventi Usa hello [Host processore di eventi](#event-processor-host-apis), che fornisce funzionalità tooautomatically tenere traccia dell'offset e informazioni sulla partizione.</span><span class="sxs-lookup"><span data-stu-id="90d3e-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="90d3e-122">Tuttavia, esistono determinate situazioni in cui è possibile scegliere flessibilità hello toouse eventi hello core hub eventi libreria tooreceive.</span><span class="sxs-lookup"><span data-stu-id="90d3e-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="90d3e-123">Creare un ricevitore</span><span class="sxs-lookup"><span data-stu-id="90d3e-123">Create a receiver</span></span>
<span data-ttu-id="90d3e-124">Ricevitori sono legati toospecific partizioni, pertanto, in ordine tooreceive tutti gli eventi in un hub eventi, è necessario toocreate più istanze.</span><span class="sxs-lookup"><span data-stu-id="90d3e-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="90d3e-125">In genere, si tratta una buona norma tooget hello partizione informazioni a livello di codice, anziché a livello di codice gli ID di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="90d3e-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="90d3e-126">In ordine toodo questa operazione, è possibile usare hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) metodo.</span><span class="sxs-lookup"><span data-stu-id="90d3e-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

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

<span data-ttu-id="90d3e-127">Poiché gli eventi non vengono mai rimosse da un hub di eventi (e solo scadono), è necessario punto iniziale di toospecify hello appropriato.</span><span class="sxs-lookup"><span data-stu-id="90d3e-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="90d3e-128">Hello seguito sono riportate le possibili combinazioni.</span><span class="sxs-lookup"><span data-stu-id="90d3e-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="90d3e-129">Usare un evento</span><span class="sxs-lookup"><span data-stu-id="90d3e-129">Consume an event</span></span>
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

## <a name="event-processor-host-apis"></a><span data-ttu-id="90d3e-130">API host processore di eventi</span><span class="sxs-lookup"><span data-stu-id="90d3e-130">Event Processor Host APIs</span></span>
<span data-ttu-id="90d3e-131">Le API forniscono processi tooworker resilienza che potrebbero diventare non disponibili, distribuendo le partizioni tra thread di lavoro disponibili.</span><span class="sxs-lookup"><span data-stu-id="90d3e-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

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

<span data-ttu-id="90d3e-132">Hello seguito è riportato un esempio di implementazione di hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="90d3e-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="90d3e-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90d3e-133">Next steps</span></span>
<span data-ttu-id="90d3e-134">toolearn più sugli scenari di hub eventi, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="90d3e-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="90d3e-135">Che cos'è l'hub di eventi di Azure?</span><span class="sxs-lookup"><span data-stu-id="90d3e-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="90d3e-136">[Available Event Hubs apis](event-hubs-api-overview.md) (API di Hub eventi disponibili)</span><span class="sxs-lookup"><span data-stu-id="90d3e-136">[Available Event Hubs apis](event-hubs-api-overview.md)</span></span>

<span data-ttu-id="90d3e-137">in questa sezione sono riportati i riferimenti alle API di .NET di Hello:</span><span class="sxs-lookup"><span data-stu-id="90d3e-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="90d3e-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="90d3e-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="90d3e-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="90d3e-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)