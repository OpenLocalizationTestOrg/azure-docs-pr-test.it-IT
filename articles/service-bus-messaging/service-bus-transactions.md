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
# <a name="overview-of-service-bus-transaction-processing"></a>Panoramica dell'elaborazione delle transazioni del bus di servizio
Questo articolo illustra la funzionalità di transazione hello del Bus di servizio di Azure. Gran parte della discussione hello è illustrata hello [transazioni atomiche con esempio di Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Questo articolo è limitato tooan Panoramica l'elaborazione delle transazioni e hello *invio tramite* funzionalità di Service Bus, mentre: esempio hello transazioni atomiche è più ampia e più complessi nell'ambito.

## <a name="transactions-in-service-bus"></a>Transazioni nel bus di servizio
Una [transazione](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) raggruppa due o più operazioni in un *ambito di esecuzione*. Per natura, tale transazione è necessario assicurarsi che tutte le operazioni appartenenti tooa dato gruppo di operazioni di esito positivo o esito negativo congiuntamente. In questo senso le transazioni agiscono come una singola unità, è spesso a cui viene fatto riferimento tooas *atomicità*. 

Il bus di servizio è un gestore di messaggi transazionali e assicura l'integrità transazionale per tutte le operazioni interne eseguite in relazione agli archivi del messaggio. Tutti i trasferimenti di messaggi all'interno di Service Bus, ad esempio lo spostamento messaggi tooa [recapitabili](service-bus-dead-letter-queues.md) o [l'inoltro automatico](service-bus-auto-forwarding.md) dei messaggi tra le entità, sono transazionali. Di conseguenza, se il bus di servizio accetta un messaggio, questo è già stato archiviato e contrassegnato con un numero di sequenza. In poi, i trasferimenti di messaggi all'interno di Service Bus sono operazioni coordinate tra entità e non causare tooloss (origine ha esito positivo e di destinazione ha esito negativo) o tooduplication (origine e destinazione negativi conseguiti) del messaggio hello.

Bus di servizio supporta le operazioni di raggruppamento in una singola entità di messaggistica (coda, argomento o sottoscrizione) nell'ambito di hello di una transazione. Ad esempio, è possibile inviare più messaggi tooone coda da un ambito di transazione e messaggi hello sarà log toohello eseguito il commit della coda solo quando la transazione hello è stata completata correttamente.

## <a name="operations-within-a-transaction-scope"></a>Operazioni nell'ambito di una transazione
di seguito sono riportate le operazioni di Hello che possono essere eseguite all'interno di un ambito di transazione:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Ricezione operazioni non sono incluse, in quanto si presuppone che un'applicazione hello acquisisce i messaggi utilizzando hello [Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità, in alcune ciclo di ricezione o con un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, Apre quindi solo una transazione di ambito per l'elaborazione del messaggio hello e.

Hello disposizione di messaggio hello (completa, abandon, messaggi non recapitabili, deve rinviare) viene quindi eseguito all'interno di portata hello e dipendenti, hello risultato complessivo di transazione hello.

## <a name="transfers-and-send-via"></a>Trasferimenti e "invia tramite"
tooenable passaggio transazionale dei dati da un processore tooa coda e coda tooanother, Bus di servizio supporta *trasferimenti*. In un'operazione di trasferimento di un mittente invia un messaggio tooa "coda di trasferimento" e coda di trasferimento hello passa immediatamente toohello messaggio hello destinato coda di destinazione mediante hello stesso affidabile trasferimento implementazione che si basano le funzionalità di inoltro automatico hello in. non è mai messaggio Hello del log della coda di trasferimento toohello eseguito il commit in modo che diventi visibile per i consumer della coda di trasferimento hello.

potenza Hello di questa funzionalità transazionale diventa evidente quando coda di trasferimento hello stessa origine hello dei messaggi di input del mittente hello. In altre parole, il Bus di servizio possono trasferire coda di destinazione toohello messaggi hello "via" coda di trasferimento hello, durante l'esecuzione completa (o rinviare, o messaggi non recapitabili) operazione sul messaggio di input hello, in una singola operazione atomica. 

### <a name="see-it-in-code"></a>Codice di esempio
tooset di tali trasferimenti, si crea il mittente del messaggio che ha come destinazione la coda di destinazione hello tramite una coda di trasferimento hello. Sarà inoltre disponibile un destinatario che estrae i messaggi dalla stessa coda. ad esempio:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Una transazione semplice quindi utilizza questi elementi, come in hello di esempio seguente:

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

## <a name="next-steps"></a>Passaggi successivi

Vedere i seguenti articoli per ulteriori informazioni sulle code Service Bus hello:

* [Concatenamento del bus di servizio con l'inoltro automatico](service-bus-auto-forwarding.md)
* [Esempio di inoltro automatico](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Esempio di transazioni atomiche con il bus di servizio](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Analogie e differenze tra le code di Azure e le code del bus di servizio](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Come le code del Bus di servizio toouse](service-bus-dotnet-get-started-with-queues.md)

