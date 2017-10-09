---
title: aaaAvailability e la coerenza in hub eventi di Azure | Documenti Microsoft
description: "La quantità massima di hello tooprovide di disponibilità e la coerenza con gli hub di eventi di Azure partizioni."
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="7184a-103">Disponibilità e coerenza nell'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="7184a-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="7184a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7184a-104">Overview</span></span>
<span data-ttu-id="7184a-105">Azure hub eventi Usa un [partizionamento modello](event-hubs-features.md#partitions) tooimprove disponibilità e la parallelizzazione all'interno di un hub singolo evento.</span><span class="sxs-lookup"><span data-stu-id="7184a-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="7184a-106">Ad esempio, un hub eventi include quattro partizioni, se uno di tali partizioni viene spostato da un server tooanother in un'operazione di bilanciamento del carico, possono comunque inviare e ricevere tre altre partizioni.</span><span class="sxs-lookup"><span data-stu-id="7184a-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="7184a-107">Consente, inoltre, con più partizioni toohave simultanea di più lettori l'elaborazione dei dati, migliorare la velocità effettiva aggregata.</span><span class="sxs-lookup"><span data-stu-id="7184a-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="7184a-108">Informazioni sulle implicazioni hello di partizionamento e l'ordinamento in un sistema distribuito è un aspetto di fondamentale importanza della progettazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="7184a-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="7184a-109">toohelp spiegare compromesso hello tra l'ordinamento e la disponibilità, vedere hello [teorema di CAP](https://en.wikipedia.org/wiki/CAP_theorem), noto anche come Teorema di Brewer.</span><span class="sxs-lookup"><span data-stu-id="7184a-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="7184a-110">Questo teorema viene scelta hello tra la coerenza, disponibilità e tolleranza di partizione.</span><span class="sxs-lookup"><span data-stu-id="7184a-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="7184a-111">Il teorema di Brewer definisce coerenza e disponibilità come segue:</span><span class="sxs-lookup"><span data-stu-id="7184a-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="7184a-112">Tolleranza di partizione: hello capacità di un toocontinue di sistema di elaborazione dei dati l'elaborazione dei dati, anche se si verifica un errore della partizione.</span><span class="sxs-lookup"><span data-stu-id="7184a-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="7184a-113">Disponibilità: un nodo non di errore restituisce una risposta accettabile in un periodo ragionevole di tempo, senza errori o timeout.</span><span class="sxs-lookup"><span data-stu-id="7184a-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="7184a-114">Coerenza: un'operazione di lettura è garantita la scrittura di più recente hello tooreturn per un determinato client.</span><span class="sxs-lookup"><span data-stu-id="7184a-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="7184a-115">Tolleranza di partizione</span><span class="sxs-lookup"><span data-stu-id="7184a-115">Partition tolerance</span></span>
<span data-ttu-id="7184a-116">L'Hub eventi si basa su un modello di dati partizionato.</span><span class="sxs-lookup"><span data-stu-id="7184a-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="7184a-117">È possibile configurare il numero di hello di partizioni nell'hub eventi durante l'installazione, ma non è possibile modificare questo valore in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="7184a-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="7184a-118">Poiché è necessario utilizzare le partizioni con hub eventi, è necessario toomake una decisione sulla disponibilità e la coerenza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7184a-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="7184a-119">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="7184a-119">Availability</span></span>
<span data-ttu-id="7184a-120">Hello tooget modo più semplice avviato con hub eventi è il comportamento predefinito di toouse hello.</span><span class="sxs-lookup"><span data-stu-id="7184a-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="7184a-121">Se si crea un nuovo `EventHubClient` e utilizzare hello `Send` (metodo), gli eventi vengono automaticamente distribuiti tra partizioni nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="7184a-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="7184a-122">Questo comportamento, per la maggior quantità hello di tempo.</span><span class="sxs-lookup"><span data-stu-id="7184a-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="7184a-123">Per i casi di utilizzo che richiedono massime hello tempo di attività, questo modello è preferito.</span><span class="sxs-lookup"><span data-stu-id="7184a-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="7184a-124">Coerenza</span><span class="sxs-lookup"><span data-stu-id="7184a-124">Consistency</span></span>
<span data-ttu-id="7184a-125">In alcuni scenari, può essere importante hello ordinamento degli eventi.</span><span class="sxs-lookup"><span data-stu-id="7184a-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="7184a-126">Ad esempio, si consiglia il tooprocess sistema back-end, un comando di aggiornamento prima di un comando di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="7184a-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="7184a-127">In questo caso, è possibile impostare la chiave di partizione hello un evento o utilizzare un `PartitionSender` tooonly oggetto inviare eventi tooa determinata partizione.</span><span class="sxs-lookup"><span data-stu-id="7184a-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="7184a-128">In modo da garantire che, quando questi eventi vengono letti dalla partizione hello, in cui vengono letti nell'ordine.</span><span class="sxs-lookup"><span data-stu-id="7184a-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="7184a-129">Con questa configurazione, tenere presente che se hello partizione specifica toowhich che mittente non è disponibile, si riceverà una risposta di errore.</span><span class="sxs-lookup"><span data-stu-id="7184a-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="7184a-130">Come un punto di confronto, se non si dispone di una partizione singola tooa di affinità, hello servizio hub eventi invia l'evento toohello partizione successiva formattata disponibile.</span><span class="sxs-lookup"><span data-stu-id="7184a-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="7184a-131">Una possibile soluzione tooensure, ordinamento, ottimizzando inoltre ora, sarebbe tooaggregate eventi durante l'applicazione di elaborazione di eventi.</span><span class="sxs-lookup"><span data-stu-id="7184a-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="7184a-132">Hello questo tooaccomplish modo più semplice è toostamp l'evento con una proprietà con numero sequenza personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7184a-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="7184a-133">Hello di codice seguente viene illustrato un esempio:</span><span class="sxs-lookup"><span data-stu-id="7184a-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="7184a-134">In questo esempio invia l'evento tooone delle partizioni disponibili hello nell'hub eventi e imposta il numero di sequenza corrispondente hello dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7184a-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="7184a-135">Questa soluzione richiede toobe stato mantenuto dall'applicazione di elaborazione, ma consente i mittenti un endpoint che è più probabile toobe disponibili.</span><span class="sxs-lookup"><span data-stu-id="7184a-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7184a-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7184a-136">Next steps</span></span>
<span data-ttu-id="7184a-137">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="7184a-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="7184a-138">Panoramica del servizio Hub eventi</span><span class="sxs-lookup"><span data-stu-id="7184a-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7184a-139">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="7184a-139">Create an event hub</span></span>](event-hubs-create.md)
