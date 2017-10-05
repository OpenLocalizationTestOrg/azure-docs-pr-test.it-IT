---
title: "Inoltro automatico di entità di messaggistica del bus di servizio di Azure | Documentazione Microsoft"
description: Come concatenare una coda del bus di servizio o una sottoscrizione a un'altra coda o argomento.
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
ms.openlocfilehash: 2656b3a276c542ca836b3949e4e493d7c7f48f16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="bc57d-103">Concatenamento di entità del bus di servizio con l'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="bc57d-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="bc57d-104">La funzionalità di *inoltro automatico* del bus di servizio consente di concatenare una coda o una sottoscrizione a un'altra coda o a un altro argomento che fa parte dello stesso spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="bc57d-104">The Service Bus *auto-forwarding* feature enables you to chain a queue or subscription to another queue or topic that is part of the same namespace.</span></span> <span data-ttu-id="bc57d-105">Quando l'inoltro automatico è abilitato, il bus di servizio rimuove automaticamente i messaggi presenti nella prima coda o sottoscrizione (origine) e li inserisce nella seconda coda o argomento (destinazione).</span><span class="sxs-lookup"><span data-stu-id="bc57d-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in the first queue or subscription (source) and puts them in the second queue or topic (destination).</span></span> <span data-ttu-id="bc57d-106">Si noti che è comunque possibile inviare un messaggio direttamente all'entità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bc57d-106">Note that it is still possible to send a message to the destination entity directly.</span></span> <span data-ttu-id="bc57d-107">Tenere presente che non è possibile concatenare una coda secondaria, ad esempio una coda di messaggi non recapitabili, a una coda o a un argomento differente.</span><span class="sxs-lookup"><span data-stu-id="bc57d-107">Also, it is not possible to chain a subqueue, such as a deadletter queue, to another queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="bc57d-108">Utilizzo dell'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="bc57d-108">Using auto-forwarding</span></span>
<span data-ttu-id="bc57d-109">Per abilitare l'inoltro automatico, è possibile impostare la proprietà [QueueDescription.ForwardTo][QueueDescription.ForwardTo] o [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] nell'oggetto [QueueDescription][QueueDescription] o [SubscriptionDescription][SubscriptionDescription] per l'origine, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="bc57d-109">You can enable auto-forwarding by setting the [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on the [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for the source, as in the following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="bc57d-110">L'entità di destinazione deve essere presente al momento della creazione dell'entità di origine.</span><span class="sxs-lookup"><span data-stu-id="bc57d-110">The destination entity must exist at the time the source entity is created.</span></span> <span data-ttu-id="bc57d-111">In caso contrario, il bus di servizio restituisce un'eccezione quando gli viene chiesto di creare l'entità di origine. </span><span class="sxs-lookup"><span data-stu-id="bc57d-111">If the destination entity does not exist, Service Bus returns an exception when asked to create the source entity.</span></span>

<span data-ttu-id="bc57d-112">È possibile usare l'inoltro automatico per aumentare il numero di istanze di un singolo argomento.</span><span class="sxs-lookup"><span data-stu-id="bc57d-112">You can use auto-forwarding to scale out an individual topic.</span></span> <span data-ttu-id="bc57d-113">Il bus di servizio limita il [numero delle sottoscrizioni per un determinato argomento](service-bus-quotas.md) a 2000.</span><span class="sxs-lookup"><span data-stu-id="bc57d-113">Service Bus limits the [number of subscriptions on a given topic](service-bus-quotas.md) to 2,000.</span></span> <span data-ttu-id="bc57d-114">Creando argomenti di secondo livello, è possibile aggiungere altre sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="bc57d-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="bc57d-115">Si noti che, pur non essendo vincolati dalla limitazione del bus di servizio relativa al numero delle sottoscrizioni, l'aggiunta di un secondo livello di argomenti consente complessivamente di migliorare la velocità effettiva dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="bc57d-115">Note that even if you are not bound by the Service Bus limitation on the number of subscriptions, adding a second level of topics can improve the overall throughput of your topic.</span></span>

![Scenario di inoltro automatico][0]

<span data-ttu-id="bc57d-117">È possibile usare l'inoltro automatico anche per disaccoppiare i mittenti dei messaggi dai destinatari.</span><span class="sxs-lookup"><span data-stu-id="bc57d-117">You can also use auto-forwarding to decouple message senders from receivers.</span></span> <span data-ttu-id="bc57d-118">Si consideri ad esempio un sistema ERP costituito da tre moduli: elaborazione degli ordini, gestione del magazzino e gestione dei rapporti con i clienti.</span><span class="sxs-lookup"><span data-stu-id="bc57d-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="bc57d-119">Ognuno di questi moduli genera messaggi che vengono accodati in un argomento corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bc57d-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="bc57d-120">Due dei rappresentanti di vendita sono interessati a tutti i messaggi correlati ai propri clienti.</span><span class="sxs-lookup"><span data-stu-id="bc57d-120">Alice and Bob are sales representatives that are interested in all messages that relate to their customers.</span></span> <span data-ttu-id="bc57d-121">Per ricevere questi messaggi, i due rappresentanti creano una coda personale e una sottoscrizione per ognuno degli argomenti ERP che inoltrano automaticamente tutti i messaggi alla rispettiva coda.</span><span class="sxs-lookup"><span data-stu-id="bc57d-121">To receive those messages, Alice and Bob each create a personal queue and a subscription on each of the ERP topics that automatically forward all messages to their queue.</span></span>

![Scenario di inoltro automatico][1]

<span data-ttu-id="bc57d-123">Se uno dei rappresentanti si assenta, viene riempita la coda personale, ma non l'argomento ERP.</span><span class="sxs-lookup"><span data-stu-id="bc57d-123">If Alice goes on vacation, her personal queue, rather than the ERP topic, fills up.</span></span> <span data-ttu-id="bc57d-124">In questo scenario, poiché un rappresentante di vendita non ha ricevuto alcun messaggio, nessuno degli argomenti ERP raggiunge la quota.</span><span class="sxs-lookup"><span data-stu-id="bc57d-124">In this scenario, because a sales representative has not received any messages, none of the ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="bc57d-125">Considerazioni sulla funzionalità di inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="bc57d-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="bc57d-126">Se l'entità di destinazione accumula troppi messaggi e supera la quota oppure è disabilitata, l'entità di origine aggiunge i messaggi alla relativa [coda dei messaggi non recapitabili](service-bus-dead-letter-queues.md) finché non si libera spazio nella destinazione o l'entità non viene riabilitata.</span><span class="sxs-lookup"><span data-stu-id="bc57d-126">If the destination entity accumulates too many messages and exceeds the quota, or the destination entity is disabled, the source entity adds the messages to its [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in the destination (or the entity is re-enabled).</span></span> <span data-ttu-id="bc57d-127">I messaggi resteranno nella coda dei messaggi non recapitabili, pertanto sarà necessario riceverli ed elaborarli in modo esplicito da tale coda.</span><span class="sxs-lookup"><span data-stu-id="bc57d-127">Those messages will continue to live in the dead-letter queue, so you must explicitly receive and process them from the dead-letter queue.</span></span>

<span data-ttu-id="bc57d-128">Se si concatenano singoli argomenti per ottenere un argomento composito con diverse sottoscrizioni, è consigliabile avere un certo numero di sottoscrizioni nell'argomento di primo livello e un numero più elevato di sottoscrizioni negli argomenti di secondo livello.</span><span class="sxs-lookup"><span data-stu-id="bc57d-128">When chaining together individual topics to obtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on the first-level topic and many subscriptions on the second-level topics.</span></span> <span data-ttu-id="bc57d-129">Ad esempio, un argomento di primo livello con 20 sottoscrizioni, ognuna delle quali concatenata a un argomento di secondo livello con 200 sottoscrizioni, consente una velocità effettiva più alta rispetto a un argomento di primo livello con 200 sottoscrizioni, ognuna delle quali concatenata a un argomento di secondo livello con 20 sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="bc57d-129">For example, a first-level topic with 20 subscriptions, each of them chained to a second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained to a second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="bc57d-130">Il bus di servizio addebita un'operazione per ogni messaggio inoltrato.</span><span class="sxs-lookup"><span data-stu-id="bc57d-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="bc57d-131">Ad esempio, se viene inviato un messaggio a un argomento con 20 sottoscrizioni, ognuna delle quali configurata per l'inoltro automatico dei messaggi a una coda o un argomento differente, vengono addebitate 21 operazioni se tutte le sottoscrizioni di primo livello ricevono una copia del messaggio.</span><span class="sxs-lookup"><span data-stu-id="bc57d-131">For example, sending a message to a topic with 20 subscriptions, each of them configured to auto-forward messages to another queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of the message.</span></span>

<span data-ttu-id="bc57d-132">Per creare una sottoscrizione concatenata a una coda o a un argomento diverso, l'autore deve avere le autorizzazioni di **gestione** per l'entità di origine e per quella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bc57d-132">To create a subscription that is chained to another queue or topic, the creator of the subscription must have **Manage** permissions on both the source and the destination entity.</span></span> <span data-ttu-id="bc57d-133">Per l'invio di messaggi solo all'argomento di origine sono necessarie le autorizzazioni di **invio** per l'argomento di origine.</span><span class="sxs-lookup"><span data-stu-id="bc57d-133">Sending messages to the source topic only requires **Send** permissions on the source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc57d-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc57d-134">Next steps</span></span>

<span data-ttu-id="bc57d-135">Per informazioni dettagliate sull'inoltro automatico, vedere gli argomenti di riferimento seguenti:</span><span class="sxs-lookup"><span data-stu-id="bc57d-135">For detailed information about auto-forwarding, see the following reference topics:</span></span>

* <span data-ttu-id="bc57d-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="bc57d-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="bc57d-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="bc57d-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="bc57d-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="bc57d-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="bc57d-139">Per altre informazioni sui miglioramenti delle prestazioni del bus di servizio, vedere</span><span class="sxs-lookup"><span data-stu-id="bc57d-139">To learn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="bc57d-140">Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="bc57d-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="bc57d-141">[Entità di messaggistica partizionate][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="bc57d-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
