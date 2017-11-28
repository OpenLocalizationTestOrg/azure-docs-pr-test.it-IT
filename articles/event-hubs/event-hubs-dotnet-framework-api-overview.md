---
title: aaaOverview di hello Azure evento hub API di .NET Framework | Documenti Microsoft
description: Un riepilogo di alcuni dei client di .NET Framework gli hub di eventi chiave hello API.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b0e12e43f91b025d7aa4ca03e664b9ff31b04097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="14d17-103">Panoramica dell'API .NET Framework di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="14d17-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="14d17-104">In questo articolo riepiloga alcune delle chiave hello API client di hub di eventi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="14d17-104">This article summarizes some of hello key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="14d17-105">Esistono due categorie: API di runtime e gestione.</span><span class="sxs-lookup"><span data-stu-id="14d17-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="14d17-106">API di runtime sono costituiti da tutte le operazioni necessarie toosend e ricevano un messaggio.</span><span class="sxs-lookup"><span data-stu-id="14d17-106">Run-time APIs consist of all operations needed toosend and receive a message.</span></span> <span data-ttu-id="14d17-107">Operazioni di gestione attiva è toomanage uno stato di entità di hub eventi per la creazione, aggiornamento e l'eliminazione delle entità.</span><span class="sxs-lookup"><span data-stu-id="14d17-107">Management operations enable you toomanage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="14d17-108">Gli scenari di monitoraggio comprendono sia la gestione che il runtime.</span><span class="sxs-lookup"><span data-stu-id="14d17-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="14d17-109">Per la documentazione di riferimento dettagliate sulle hello API .NET, vedere hello [.NET del Bus di servizio](/dotnet/api/microsoft.servicebus.messaging) e [API EventProcessorHost](/dotnet/api/microsoft.azure.eventhubs.processor) riferimenti.</span><span class="sxs-lookup"><span data-stu-id="14d17-109">For detailed reference documentation on hello .NET APIs, see hello [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="14d17-110">API di gestione</span><span class="sxs-lookup"><span data-stu-id="14d17-110">Management APIs</span></span>
<span data-ttu-id="14d17-111">tooperform hello dopo operazioni di gestione, è necessario **Gestisci** le autorizzazioni per lo spazio dei nomi di hello hub eventi:</span><span class="sxs-lookup"><span data-stu-id="14d17-111">tooperform hello following management operations, you must have **Manage** permissions on hello Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="14d17-112">Create</span><span class="sxs-lookup"><span data-stu-id="14d17-112">Create</span></span>
```csharp
// Create hello event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="14d17-113">Aggiornamento</span><span class="sxs-lookup"><span data-stu-id="14d17-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="14d17-114">Elimina</span><span class="sxs-lookup"><span data-stu-id="14d17-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="14d17-115">API di runtime</span><span class="sxs-lookup"><span data-stu-id="14d17-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="14d17-116">Crea editore</span><span class="sxs-lookup"><span data-stu-id="14d17-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="14d17-117">Pubblica messaggio</span><span class="sxs-lookup"><span data-stu-id="14d17-117">Publish message</span></span>
```csharp
// Create hello device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="14d17-118">Crea consumer</span><span class="sxs-lookup"><span data-stu-id="14d17-118">Create consumer</span></span>
```csharp
// Create hello Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get hello default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="14d17-119">Utilizzare messaggio</span><span class="sxs-lookup"><span data-stu-id="14d17-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="14d17-120">API host processore di eventi</span><span class="sxs-lookup"><span data-stu-id="14d17-120">Event Processor Host APIs</span></span>
<span data-ttu-id="14d17-121">Le API forniscono processi tooworker resilienza che potrebbero diventare non disponibili, distribuendo le partizioni tra thread di lavoro disponibili.</span><span class="sxs-lookup"><span data-stu-id="14d17-121">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use hello EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// tooclose
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="14d17-122">Hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interfaccia sia definita come segue:</span><span class="sxs-lookup"><span data-stu-id="14d17-122">hello [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="14d17-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14d17-123">Next steps</span></span>
<span data-ttu-id="14d17-124">toolearn più sugli scenari di hub eventi, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="14d17-124">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="14d17-125">Che cos'è l'hub di eventi di Azure?</span><span class="sxs-lookup"><span data-stu-id="14d17-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="14d17-126">Guida alla programmazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="14d17-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="14d17-127">in questa sezione sono riportati i riferimenti alle API di .NET di Hello:</span><span class="sxs-lookup"><span data-stu-id="14d17-127">hello .NET API references are here:</span></span>

* [<span data-ttu-id="14d17-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="14d17-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="14d17-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="14d17-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
