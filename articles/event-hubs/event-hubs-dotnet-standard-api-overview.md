---
title: Panoramica delle API .NET Standard di Azure Hub eventi | Microsoft Docs
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
ms.openlocfilehash: eea682c40cd415b383a8b2f0004a5f3648e2f01f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="1ca68-103">Panoramica dell'API .NET Standard di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="1ca68-104">In questo articolo vengono riepilogate alcune delle principali API client .NET Standard di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1ca68-104">This article summarizes some of the key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="1ca68-105">Esistono attualmente due librerie client .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="1ca68-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="1ca68-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="1ca68-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="1ca68-107">Questa libreria offre tutte le operazioni di runtime di base.</span><span class="sxs-lookup"><span data-stu-id="1ca68-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="1ca68-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="1ca68-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="1ca68-109">Questa libreria consente di aggiungere altre funzionalità che permettono di tenere traccia degli eventi elaborati e rappresenta la modalità più semplice di lettura da un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1ca68-109">This library adds additional functionality that allows for keeping track of processed events, and is the easiest way to read from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="1ca68-110">Client di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-110">Event Hubs client</span></span>
<span data-ttu-id="1ca68-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) è l'oggetto principale da usare per inviare eventi, creare ricevitori e ottenere informazioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="1ca68-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is the primary object you use to send events, create receivers, and to get run-time information.</span></span> <span data-ttu-id="1ca68-112">Questo client è collegato a un determinato hub eventi e crea una nuova connessione all'endpoint di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="1ca68-112">This client is linked to a particular event hub, and creates a new connection to the Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="1ca68-113">Creare un client di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-113">Create an Event Hubs client</span></span>
<span data-ttu-id="1ca68-114">Un oggetto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) viene creato da una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="1ca68-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="1ca68-115">Nell'esempio seguente viene illustrato il modo più semplice per creare un'istanza di un nuovo client:</span><span class="sxs-lookup"><span data-stu-id="1ca68-115">The simplest way to instantiate a new client is shown in the following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="1ca68-116">Per modificare la stringa di connessione a livello di codice, è possibile usare la classe [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) e passare la stringa di connessione come parametro a [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="1ca68-116">To programmatically edit the connection string, you can use the [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass the connection string as a parameter to [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="1ca68-117">Inviare eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-117">Send events</span></span>
<span data-ttu-id="1ca68-118">Per inviare eventi a un hub eventi, usare la classe [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata).</span><span class="sxs-lookup"><span data-stu-id="1ca68-118">To send events to an event hub, use the [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="1ca68-119">Il corpo deve essere un array `byte` o un segmento di array `byte`.</span><span class="sxs-lookup"><span data-stu-id="1ca68-119">The body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="1ca68-120">Ricevere eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-120">Receive events</span></span>
<span data-ttu-id="1ca68-121">Il metodo consigliato per ricevere eventi da Hub eventi è tramite [EventProcessorHost](#event-processor-host-apis), che offre funzionalità che permettono di tenere automaticamente traccia dell'offset e delle informazioni di partizione.</span><span class="sxs-lookup"><span data-stu-id="1ca68-121">The recommended way to receive events from Event Hubs is using the [Event Processor Host](#event-processor-host-apis), which provides functionality to automatically keep track of offset, and partition information.</span></span> <span data-ttu-id="1ca68-122">Tuttavia, in alcune situazioni per ricevere eventi è preferibile usare la flessibilità della libreria di Hub eventi di base.</span><span class="sxs-lookup"><span data-stu-id="1ca68-122">However, there are certain situations in which you may want to use the flexibility of the core Event Hubs library to receive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="1ca68-123">Creare un ricevitore</span><span class="sxs-lookup"><span data-stu-id="1ca68-123">Create a receiver</span></span>
<span data-ttu-id="1ca68-124">I ricevitori sono legati a partizioni specifiche, pertanto, per ricevere tutti gli eventi in un hub eventi, è necessario creare più istanze.</span><span class="sxs-lookup"><span data-stu-id="1ca68-124">Receivers are tied to specific partitions, so in order to receive all events in an event hub, you will need to create multiple instances.</span></span> <span data-ttu-id="1ca68-125">In generale, è buona norma ottenere le informazioni di partizione a livello di programmazione, anziché impostare come hardcoded gli ID di partizione.</span><span class="sxs-lookup"><span data-stu-id="1ca68-125">Generally speaking, it is a good practice to get the partition information programatically, rather than hard-coding the partition ids.</span></span> <span data-ttu-id="1ca68-126">A tale scopo, è possibile usare il metodo [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync).</span><span class="sxs-lookup"><span data-stu-id="1ca68-126">In order to do so, you can use the [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

<span data-ttu-id="1ca68-127">Dato che gli eventi non vengono mai rimossi da un hub eventi e possono solo scadere, è necessario specificare il punto di partenza appropriato.</span><span class="sxs-lookup"><span data-stu-id="1ca68-127">Since events are never removed from an event hub (and only expire), you need to specify the proper starting point.</span></span> <span data-ttu-id="1ca68-128">L'esempio seguente mostra le combinazioni possibili.</span><span class="sxs-lookup"><span data-stu-id="1ca68-128">The following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="1ca68-129">Usare un evento</span><span class="sxs-lookup"><span data-stu-id="1ca68-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="1ca68-130">API host processore di eventi</span><span class="sxs-lookup"><span data-stu-id="1ca68-130">Event Processor Host APIs</span></span>
<span data-ttu-id="1ca68-131">Queste API garantiscono resilienza ai processi di lavoro che possono diventare non disponibili, distribuendo tuttavia partizioni tra i ruoli di lavoro disponibili.</span><span class="sxs-lookup"><span data-stu-id="1ca68-131">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes of the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="1ca68-132">Di seguito è riportato un esempio di implementazione di [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="1ca68-132">The following is a sample implementation of the [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1ca68-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1ca68-133">Next steps</span></span>
<span data-ttu-id="1ca68-134">Per altre informazioni sugli scenari di Hub eventi, visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1ca68-134">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="1ca68-135">Che cos'è l'hub di eventi di Azure?</span><span class="sxs-lookup"><span data-stu-id="1ca68-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="1ca68-136">[Available Event Hubs apis](event-hubs-api-overview.md) (API di Hub eventi disponibili)</span><span class="sxs-lookup"><span data-stu-id="1ca68-136">[Available Event Hubs apis](event-hubs-api-overview.md)</span></span>

<span data-ttu-id="1ca68-137">I riferimenti API .NET sono qui:</span><span class="sxs-lookup"><span data-stu-id="1ca68-137">The .NET API references are here:</span></span>

* [<span data-ttu-id="1ca68-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="1ca68-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="1ca68-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="1ca68-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)