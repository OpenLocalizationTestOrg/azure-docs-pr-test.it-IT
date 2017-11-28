---
title: "le entità di messaggistica di inoltro aaaAuto Service Bus di Azure | Documenti Microsoft"
description: Come toochain un Bus di servizio coda o sottoscrizione tooanother coda o un argomento.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="f5fb5-103">Concatenamento di entità del bus di servizio con l'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="f5fb5-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="f5fb5-104">Bus di servizio Hello *inoltro automatico* funzionalità permette di toochain una coda o sottoscrizione tooanother coda o un argomento che fa parte di hello stesso spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="f5fb5-105">Quando l'inoltro automatico è abilitato, Bus di servizio automaticamente rimuove i messaggi che vengono inseriti nella coda prima di hello o una sottoscrizione (origine) e li inserisce in coda secondo hello o un argomento (destinazione).</span><span class="sxs-lookup"><span data-stu-id="f5fb5-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="f5fb5-106">Si noti che è comunque possibile toosend un'entità di destinazione toohello messaggio direttamente.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="f5fb5-107">Inoltre, non è possibile toochain una coda secondaria, ad esempio una coda di messaggi non recapitabili, tooanother coda o argomento.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="f5fb5-108">Utilizzo dell'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="f5fb5-108">Using auto-forwarding</span></span>
<span data-ttu-id="f5fb5-109">È possibile abilitare l'inoltro automatico impostando hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] o [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] proprietà hello [QueueDescription] [ QueueDescription] o [SubscriptionDescription] [ SubscriptionDescription] oggetti per l'origine di hello, come in hello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="f5fb5-110">entità di destinazione Hello deve esistere in fase di hello viene creata l'entità di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="f5fb5-111">Se non esiste l'entità di destinazione hello, Bus di servizio restituisce un'eccezione quando toocreate frequenti hello entità di origine.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="f5fb5-112">È possibile usare l'inoltro automatico tooscale out un singolo argomento.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="f5fb5-113">Bus di servizio limiti hello [numero di sottoscrizioni per un determinato argomento](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="f5fb5-114">Creando argomenti di secondo livello, è possibile aggiungere altre sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="f5fb5-115">Si noti che anche se non si è vincolati dal hello Bus di servizio limitazione hello numero di sottoscrizioni, aggiungere un secondo livello può migliorare hello velocità effettiva globale dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Scenario di inoltro automatico][0]

<span data-ttu-id="f5fb5-117">È possibile utilizzare anche l'inoltro automatico toodecouple mittenti dai destinatari.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="f5fb5-118">Si consideri ad esempio un sistema ERP costituito da tre moduli: elaborazione degli ordini, gestione del magazzino e gestione dei rapporti con i clienti.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="f5fb5-119">Ognuno di questi moduli genera messaggi che vengono accodati in un argomento corrispondente.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="f5fb5-120">Alice e Bob sono rappresentanti di vendita sono interessati a tutti i messaggi correlati tootheir clienti.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="f5fb5-121">tooreceive tali messaggi, Alice e Bob creare una coda personale e una sottoscrizione in ognuno degli argomenti ERP hello che inoltrano automaticamente tutti i messaggi tootheir coda.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Scenario di inoltro automatico][1]

<span data-ttu-id="f5fb5-123">Se uno dei rappresentanti si vacanza, la coda personale, anziché argomento ERP hello, esaurirsi.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="f5fb5-124">In questo scenario, poiché un rappresentante di vendita non ha ricevuto alcun messaggio, nessuno degli argomenti ERP hello raggiunge la quota.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="f5fb5-125">Considerazioni sulla funzionalità di inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="f5fb5-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="f5fb5-126">Se l'entità di destinazione hello accumula troppi messaggi e supera la quota di hello o entità di destinazione hello è disabilitato, entità di origine hello aggiunge hello messaggi tooits [recapitabili](service-bus-dead-letter-queues.md) fino a quando non è presente spazio nella destinazione hello (o entità hello viene riabilitata.)</span><span class="sxs-lookup"><span data-stu-id="f5fb5-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="f5fb5-127">Tali messaggi verranno comunque toolive nella coda di messaggi non recapitabili hello, è necessario in modo esplicito di ricezione, elaborati dalla coda di messaggi non recapitabili hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="f5fb5-128">Quando il concatenamento di singoli argomenti tooobtain un argomento composito con più sottoscrizioni, è consigliabile disporre di un numero limitato di sottoscrizioni per argomento di primo livello hello e numero di sottoscrizioni sugli argomenti di secondo livello hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="f5fb5-129">Ad esempio, un argomento di primo livello con 20 sottoscrizioni, ognuno di essi concatenate tooa argomento di secondo livello con 200 sottoscrizioni, consente una velocità effettiva rispetto a un argomento di primo livello con 200 sottoscrizioni, ciascuna concatenate tooa argomento di secondo livello con 20 sottoscrizioni .</span><span class="sxs-lookup"><span data-stu-id="f5fb5-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="f5fb5-130">Il bus di servizio addebita un'operazione per ogni messaggio inoltrato.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="f5fb5-131">Ad esempio, l'invio di un argomento di messaggio tooa con 20 sottoscrizioni, ciascuna di esse configurato messaggi tooauto forward tooanother coda o argomento, è addebitate 21 operazioni se tutte le sottoscrizioni di primo livello ricevono una copia del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="f5fb5-132">toocreate una sottoscrizione concatenata tooanother coda o argomento, è necessario disporre autore hello della sottoscrizione hello **Gestisci** autorizzazioni sul origine hello ed entità di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="f5fb5-133">Invio richiede solo l'argomento di origine di messaggi toohello **inviare** le autorizzazioni per l'argomento di origine hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb5-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5fb5-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5fb5-134">Next steps</span></span>

<span data-ttu-id="f5fb5-135">Per informazioni dettagliate sulle funzionalità di inoltro automatico, vedere hello seguenti argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="f5fb5-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="f5fb5-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="f5fb5-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="f5fb5-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="f5fb5-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="f5fb5-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="f5fb5-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="f5fb5-139">toolearn ulteriori informazioni sui miglioramenti delle prestazioni di Service Bus, vedere</span><span class="sxs-lookup"><span data-stu-id="f5fb5-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="f5fb5-140">Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f5fb5-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="f5fb5-141">[Entità di messaggistica partizionate][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="f5fb5-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
