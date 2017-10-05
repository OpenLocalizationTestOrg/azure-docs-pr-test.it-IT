---
title: Panoramica dell'elaborazione delle transazioni nel bus di servizio di Azure | Documentazione Microsoft
description: Panoramica delle transazioni atomiche del bus di servizio di Azure e invia tramite
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="ff17b-103">Panoramica dell'elaborazione delle transazioni del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ff17b-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="ff17b-104">Questo articolo descrive le funzionalità delle transazioni del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="ff17b-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="ff17b-105">Gran parte della discussione si basa sull'[esempio delle transazioni atomiche con il bus di servizio](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="ff17b-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="ff17b-106">Questo articolo si limita a una panoramica dell'elaborazione delle transazioni e della funzionalità *invia tramite* nel bus di servizio, invece l'esempio delle transazioni atomiche ha un ambito di riferimento più ampio e complesso.</span><span class="sxs-lookup"><span data-stu-id="ff17b-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="ff17b-107">Transazioni nel bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ff17b-107">Transactions in Service Bus</span></span>
<span data-ttu-id="ff17b-108">Una [transazione](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) raggruppa due o più operazioni in un *ambito di esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="ff17b-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="ff17b-109">Per natura, questo tipo di transazione deve garantire che tutte le operazioni appartenenti a un determinato gruppo di operazioni abbiano esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="ff17b-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="ff17b-110">In questo contesto, le transazioni agiscono come unità, spesso definita *atomicità*.</span><span class="sxs-lookup"><span data-stu-id="ff17b-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="ff17b-111">Il bus di servizio è un gestore di messaggi transazionali e assicura l'integrità transazionale per tutte le operazioni interne eseguite in relazione agli archivi del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ff17b-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="ff17b-112">Tutti i trasferimenti di messaggi all'interno del bus di servizio, ad esempio lo spostamento di messaggi a una [coda dei messaggi non recapitabili](service-bus-dead-letter-queues.md) o all'[inoltro automatico](service-bus-auto-forwarding.md) dei messaggi tra entità, sono transazionali.</span><span class="sxs-lookup"><span data-stu-id="ff17b-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="ff17b-113">Di conseguenza, se il bus di servizio accetta un messaggio, questo è già stato archiviato e contrassegnato con un numero di sequenza.</span><span class="sxs-lookup"><span data-stu-id="ff17b-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="ff17b-114">Da questo momento, i trasferimenti di messaggi all'interno del bus di servizio sono operazioni coordinate tra le entità e non causeranno una perdita (l'origine ha esito positivo, mentre la destinazione ha esito negativo) o una duplicazione (l'origine ha esito negativo, mentre la destinazione ha esito positivo) del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ff17b-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="ff17b-115">Il bus di servizio supporta le operazioni di raggruppamento in una singola entità di messaggistica (coda, argomento, sottoscrizione) nell'ambito di una transazione.</span><span class="sxs-lookup"><span data-stu-id="ff17b-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="ff17b-116">Ad esempio, è possibile inviare più messaggi a una coda da un ambito di transazione e verrà eseguito il commit dei messaggi al log della coda solo quando la transazione viene completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="ff17b-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="ff17b-117">Operazioni nell'ambito di una transazione</span><span class="sxs-lookup"><span data-stu-id="ff17b-117">Operations within a transaction scope</span></span>
<span data-ttu-id="ff17b-118">È possibile eseguire le operazioni nell'ambito di una transazione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ff17b-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="ff17b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="ff17b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="ff17b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="ff17b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="ff17b-121">Le operazioni di ricezione non vengono incluse perché si presuppone che l'applicazione acquisisca i messaggi usando la modalità [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode), all'interno di alcuni cicli di ricezione o di un callback [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_), e solo successivamente apra un ambito di transazione per l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ff17b-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="ff17b-122">La ricezione del messaggio (completamento, abbandono, non recapitabilità, rinvio) si verifica all'interno dell'ambito e dipende dal risultato complessivo della transazione.</span><span class="sxs-lookup"><span data-stu-id="ff17b-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="ff17b-123">Trasferimenti e "invia tramite"</span><span class="sxs-lookup"><span data-stu-id="ff17b-123">Transfers and "send via"</span></span>
<span data-ttu-id="ff17b-124">Per abilitare il passaggio transazionale dei dati da una coda a un processore e successivamente a un'altra coda, il bus di servizio supporta i *trasferimenti*.</span><span class="sxs-lookup"><span data-stu-id="ff17b-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="ff17b-125">In un'operazione di trasferimento, un mittente invia un messaggio a una "coda di trasferimento" e quest'ultima sposta immediatamente il messaggio alla coda di destinazione prestabilita usando la stessa implementazione di trasferimento affidabile su cui si basa la funzionalità di inoltro automatico.</span><span class="sxs-lookup"><span data-stu-id="ff17b-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="ff17b-126">Non viene mai eseguito il commit del messaggio al log della coda di trasferimento in modo che diventi visibile agli utenti della coda di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="ff17b-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="ff17b-127">L'efficacia di questa funzionalità transazionale diventa evidente quando la coda di trasferimento stessa è l'origine dei messaggi di input del mittente.</span><span class="sxs-lookup"><span data-stu-id="ff17b-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="ff17b-128">In altri termini, il bus di servizio può trasferire il messaggio alla coda di destinazione "tramite" la coda di trasferimento, durante l'esecuzione di un'operazione di completamento (o rinvio o non recapitabilità) nel messaggio di input, il tutto in una singola operazione atomica.</span><span class="sxs-lookup"><span data-stu-id="ff17b-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="ff17b-129">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="ff17b-129">See it in code</span></span>
<span data-ttu-id="ff17b-130">Per impostare tali trasferimenti, si crea un mittente del messaggio che fa riferimento alla coda di destinazione tramite la coda di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="ff17b-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="ff17b-131">Sarà inoltre disponibile un destinatario che estrae i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="ff17b-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="ff17b-132">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ff17b-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="ff17b-133">Una transazione semplice usa questi elementi, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="ff17b-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="ff17b-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff17b-134">Next steps</span></span>

<span data-ttu-id="ff17b-135">Per altre informazioni sulle code del bus di servizio, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff17b-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="ff17b-136">Concatenamento del bus di servizio con l'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="ff17b-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="ff17b-137">Esempio di inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="ff17b-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="ff17b-138">Esempio di transazioni atomiche con il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ff17b-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="ff17b-139">Analogie e differenze tra le code di Azure e le code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ff17b-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="ff17b-140">Come usare le code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ff17b-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

