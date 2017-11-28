---
title: "Disponibilità e coerenza nell'Hub eventi di Azure | Microsoft Docs"
description: "Come fornire la quantità massima di disponibilità e coerenza con l'Hub eventi di Azure usando le partizioni."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="d13b3-103">Disponibilità e coerenza nell'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="d13b3-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="d13b3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d13b3-104">Overview</span></span>
<span data-ttu-id="d13b3-105">Hub eventi di Azure usa un [modello di partizionamento](event-hubs-features.md#partitions) per migliorare la disponibilità e la parallelizzazione all'interno di un singolo hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d13b3-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="d13b3-106">Se ad esempio un hub eventi include quattro partizioni e una di queste partizioni viene spostata da un server a un altro in un'operazione di bilanciamento del carico, è comunque possibile inviare e ricevere dalle altre tre partizioni.</span><span class="sxs-lookup"><span data-stu-id="d13b3-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="d13b3-107">Più partizioni consentono anche di avere più lettori simultaneamente che elaborano i dati, migliorando la velocità effettiva di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="d13b3-108">Comprendere le implicazioni del partizionamento e dell'ordinamento in un sistema distribuito è un aspetto critico della progettazione di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="d13b3-109">Per spiegare il compromesso tra ordinamento e disponibilità, vedere il [teorema CAP](https://en.wikipedia.org/wiki/CAP_theorem), noto anche come teorema di Brewer.</span><span class="sxs-lookup"><span data-stu-id="d13b3-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="d13b3-110">Il teorema discute la scelta tra coerenza, disponibilità e tolleranza di partizione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="d13b3-111">Il teorema di Brewer definisce coerenza e disponibilità come segue:</span><span class="sxs-lookup"><span data-stu-id="d13b3-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="d13b3-112">Tolleranza di partizione: la capacità di un sistema di elaborazione dei dati di continuare l'elaborazione dei dati anche se si verifica un errore della partizione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="d13b3-113">Disponibilità: un nodo non di errore restituisce una risposta accettabile in un periodo ragionevole di tempo, senza errori o timeout.</span><span class="sxs-lookup"><span data-stu-id="d13b3-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="d13b3-114">Coerenza: una lettura garantisce la restituzione della scrittura più recente per un determinato client.</span><span class="sxs-lookup"><span data-stu-id="d13b3-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="d13b3-115">Tolleranza di partizione</span><span class="sxs-lookup"><span data-stu-id="d13b3-115">Partition tolerance</span></span>
<span data-ttu-id="d13b3-116">L'Hub eventi si basa su un modello di dati partizionato.</span><span class="sxs-lookup"><span data-stu-id="d13b3-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="d13b3-117">È possibile configurare il numero di partizioni nell'hub eventi durante l'installazione, ma non è possibile modificare questo valore in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d13b3-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="d13b3-118">Poiché è obbligatorio usare le partizioni con l'Hub eventi, è necessario prendere una decisione relativa a disponibilità e coerenza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="d13b3-119">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="d13b3-119">Availability</span></span>
<span data-ttu-id="d13b3-120">Il modo più semplice per iniziare a usare l'Hub eventi è il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="d13b3-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="d13b3-121">Se si crea un nuovo oggetto `EventHubClient` e si usa il metodo `Send`, gli eventi vengono distribuiti automaticamente tra le partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d13b3-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="d13b3-122">Questo comportamento consente la maggiore quantità di tempo di attività.</span><span class="sxs-lookup"><span data-stu-id="d13b3-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="d13b3-123">Per i casi di uso che richiedono il massimo del tempo di attività, è preferibile usare questo modello.</span><span class="sxs-lookup"><span data-stu-id="d13b3-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="d13b3-124">Coerenza</span><span class="sxs-lookup"><span data-stu-id="d13b3-124">Consistency</span></span>
<span data-ttu-id="d13b3-125">In alcuni scenari, l'ordinamento degli eventi può essere importante.</span><span class="sxs-lookup"><span data-stu-id="d13b3-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="d13b3-126">È ad esempio, potrebbe essere necessario che il sistema back-end elabori un comando di aggiornamento prima di un comando di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="d13b3-127">In questo caso, è possibile impostare la chiave di partizione su un evento oppure usare un oggetto `PartitionSender` solo per inviare eventi a una determinata partizione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="d13b3-128">In tal modo, quando questi eventi vengono letti dalla partizione, vengono letti nell'ordine.</span><span class="sxs-lookup"><span data-stu-id="d13b3-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="d13b3-129">Con questa configurazione, tenere presente che se la partizione specifica alla quale si esegue l'invio non è disponibile, si riceverà una risposta di errore.</span><span class="sxs-lookup"><span data-stu-id="d13b3-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="d13b3-130">Per fare un confronto, se non è presente un'affinità a una singola partizione, il servizio dell'Hub eventi invia l'evento alla partizione successiva disponibile.</span><span class="sxs-lookup"><span data-stu-id="d13b3-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="d13b3-131">Una possibile soluzione per garantire l'ordinamento ottimizzando allo stesso tempo i tempi di attività sarebbe l'aggregazione di eventi come parte dell'applicazione di elaborazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="d13b3-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="d13b3-132">Il modo più semplice per eseguire questa operazione è contrassegnare l'evento con una proprietà con numero di sequenza personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d13b3-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="d13b3-133">Il codice seguente mostra un esempio:</span><span class="sxs-lookup"><span data-stu-id="d13b3-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="d13b3-134">In questo esempio l'evento viene inviato a una delle partizioni disponibili nell'hub eventi e il numero di sequenza corrispondente viene impostato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d13b3-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="d13b3-135">Questa soluzione richiede che l'applicazione di elaborazione mantenga lo stato, ma propone ai mittenti un endpoint che ha maggiori probabilità di essere disponibile.</span><span class="sxs-lookup"><span data-stu-id="d13b3-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d13b3-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d13b3-136">Next steps</span></span>
<span data-ttu-id="d13b3-137">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d13b3-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="d13b3-138">Panoramica del servizio Hub eventi</span><span class="sxs-lookup"><span data-stu-id="d13b3-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d13b3-139">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="d13b3-139">Create an event hub</span></span>](event-hubs-create.md)
