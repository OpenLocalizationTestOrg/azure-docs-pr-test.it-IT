---
title: aaaOverview del Bus di servizio di Azure di elaborazione delle transazioni | Documenti Microsoft
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
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="d8c93-103">Panoramica dell'elaborazione delle transazioni del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d8c93-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="d8c93-104">Questo articolo illustra la funzionalità di transazione hello del Bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8c93-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="d8c93-105">Gran parte della discussione hello è illustrata hello [transazioni atomiche con esempio di Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="d8c93-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="d8c93-106">Questo articolo è limitato tooan Panoramica l'elaborazione delle transazioni e hello *invio tramite* funzionalità di Service Bus, mentre: esempio hello transazioni atomiche è più ampia e più complessi nell'ambito.</span><span class="sxs-lookup"><span data-stu-id="d8c93-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="d8c93-107">Transazioni nel bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d8c93-107">Transactions in Service Bus</span></span>
<span data-ttu-id="d8c93-108">Una [transazione](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) raggruppa due o più operazioni in un *ambito di esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="d8c93-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="d8c93-109">Per natura, tale transazione è necessario assicurarsi che tutte le operazioni appartenenti tooa dato gruppo di operazioni di esito positivo o esito negativo congiuntamente.</span><span class="sxs-lookup"><span data-stu-id="d8c93-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="d8c93-110">In questo senso le transazioni agiscono come una singola unità, è spesso a cui viene fatto riferimento tooas *atomicità*.</span><span class="sxs-lookup"><span data-stu-id="d8c93-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="d8c93-111">Il bus di servizio è un gestore di messaggi transazionali e assicura l'integrità transazionale per tutte le operazioni interne eseguite in relazione agli archivi del messaggio.</span><span class="sxs-lookup"><span data-stu-id="d8c93-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="d8c93-112">Tutti i trasferimenti di messaggi all'interno di Service Bus, ad esempio lo spostamento messaggi tooa [recapitabili](service-bus-dead-letter-queues.md) o [l'inoltro automatico](service-bus-auto-forwarding.md) dei messaggi tra le entità, sono transazionali.</span><span class="sxs-lookup"><span data-stu-id="d8c93-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="d8c93-113">Di conseguenza, se il bus di servizio accetta un messaggio, questo è già stato archiviato e contrassegnato con un numero di sequenza.</span><span class="sxs-lookup"><span data-stu-id="d8c93-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="d8c93-114">In poi, i trasferimenti di messaggi all'interno di Service Bus sono operazioni coordinate tra entità e non causare tooloss (origine ha esito positivo e di destinazione ha esito negativo) o tooduplication (origine e destinazione negativi conseguiti) del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="d8c93-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="d8c93-115">Bus di servizio supporta le operazioni di raggruppamento in una singola entità di messaggistica (coda, argomento o sottoscrizione) nell'ambito di hello di una transazione.</span><span class="sxs-lookup"><span data-stu-id="d8c93-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="d8c93-116">Ad esempio, è possibile inviare più messaggi tooone coda da un ambito di transazione e messaggi hello sarà log toohello eseguito il commit della coda solo quando la transazione hello è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="d8c93-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="d8c93-117">Operazioni nell'ambito di una transazione</span><span class="sxs-lookup"><span data-stu-id="d8c93-117">Operations within a transaction scope</span></span>
<span data-ttu-id="d8c93-118">di seguito sono riportate le operazioni di Hello che possono essere eseguite all'interno di un ambito di transazione:</span><span class="sxs-lookup"><span data-stu-id="d8c93-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="d8c93-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="d8c93-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="d8c93-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="d8c93-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="d8c93-121">Ricezione operazioni non sono incluse, in quanto si presuppone che un'applicazione hello acquisisce i messaggi utilizzando hello [Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità, in alcune ciclo di ricezione o con un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, Apre quindi solo una transazione di ambito per l'elaborazione del messaggio hello e.</span><span class="sxs-lookup"><span data-stu-id="d8c93-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="d8c93-122">Hello disposizione di messaggio hello (completa, abandon, messaggi non recapitabili, deve rinviare) viene quindi eseguito all'interno di portata hello e dipendenti, hello risultato complessivo di transazione hello.</span><span class="sxs-lookup"><span data-stu-id="d8c93-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="d8c93-123">Trasferimenti e "invia tramite"</span><span class="sxs-lookup"><span data-stu-id="d8c93-123">Transfers and "send via"</span></span>
<span data-ttu-id="d8c93-124">tooenable passaggio transazionale dei dati da un processore tooa coda e coda tooanother, Bus di servizio supporta *trasferimenti*.</span><span class="sxs-lookup"><span data-stu-id="d8c93-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="d8c93-125">In un'operazione di trasferimento di un mittente invia un messaggio tooa "coda di trasferimento" e coda di trasferimento hello passa immediatamente toohello messaggio hello destinato coda di destinazione mediante hello stesso affidabile trasferimento implementazione che si basano le funzionalità di inoltro automatico hello in.</span><span class="sxs-lookup"><span data-stu-id="d8c93-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="d8c93-126">non è mai messaggio Hello del log della coda di trasferimento toohello eseguito il commit in modo che diventi visibile per i consumer della coda di trasferimento hello.</span><span class="sxs-lookup"><span data-stu-id="d8c93-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="d8c93-127">potenza Hello di questa funzionalità transazionale diventa evidente quando coda di trasferimento hello stessa origine hello dei messaggi di input del mittente hello.</span><span class="sxs-lookup"><span data-stu-id="d8c93-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="d8c93-128">In altre parole, il Bus di servizio possono trasferire coda di destinazione toohello messaggi hello "via" coda di trasferimento hello, durante l'esecuzione completa (o rinviare, o messaggi non recapitabili) operazione sul messaggio di input hello, in una singola operazione atomica.</span><span class="sxs-lookup"><span data-stu-id="d8c93-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="d8c93-129">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="d8c93-129">See it in code</span></span>
<span data-ttu-id="d8c93-130">tooset di tali trasferimenti, si crea il mittente del messaggio che ha come destinazione la coda di destinazione hello tramite una coda di trasferimento hello.</span><span class="sxs-lookup"><span data-stu-id="d8c93-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="d8c93-131">Sarà inoltre disponibile un destinatario che estrae i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="d8c93-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="d8c93-132">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d8c93-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="d8c93-133">Una transazione semplice quindi utilizza questi elementi, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d8c93-133">A simple transaction then uses these elements, as in hello following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="d8c93-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8c93-134">Next steps</span></span>

<span data-ttu-id="d8c93-135">Vedere i seguenti articoli per ulteriori informazioni sulle code Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="d8c93-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="d8c93-136">Concatenamento del bus di servizio con l'inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="d8c93-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="d8c93-137">Esempio di inoltro automatico</span><span class="sxs-lookup"><span data-stu-id="d8c93-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="d8c93-138">Esempio di transazioni atomiche con il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d8c93-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="d8c93-139">Analogie e differenze tra le code di Azure e le code del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d8c93-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="d8c93-140">Come le code del Bus di servizio toouse</span><span class="sxs-lookup"><span data-stu-id="d8c93-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

