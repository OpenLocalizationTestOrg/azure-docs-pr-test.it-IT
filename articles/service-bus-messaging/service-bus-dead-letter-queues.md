---
title: le code di messaggi non recapitabili Bus aaaService | Documenti Microsoft
description: Panoramica delle code dei messaggi non recapitabili del bus di servizio Azure
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Panoramica delle code dei messaggi non recapitabili del bus di servizio

Le code del bus di servizio e le sottoscrizioni dell'argomento includono una coda secondaria chiamata *coda di messaggi non recapitabili* (DLQ, Dead-Letter Queue). coda di messaggi non recapitabili Hello non è necessario toobe creati in modo esplicito e non può essere eliminato o in caso contrario gestito indipendentemente dall'entità principale hello.

Questo articolo descrive le code dei messaggi non recapitabili nel bus di servizio di Azure. Gran parte della discussione hello è illustrata hello [esempio recapitabili](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) su GitHub.
 
## <a name="hello-dead-letter-queue"></a>coda di messaggi non recapitabili Hello

scopo di Hello della coda di messaggi non recapitabili hello è toohold messaggi che non possono essere recapitati tooany ricevitore o i messaggi che non è stato possibile elaborare. I messaggi possono essere rimosse da DLQ hello e controllati. Un'applicazione potrebbe, con l'aiuto di un operatore, correggere i problemi e inviare nuovamente il messaggio hello, registrare hello fatto che si è verificato un errore e intraprendere l'azione correttiva. 

Da una prospettiva di API e il protocollo, hello DLQ è principalmente simile tooany altra coda, ad eccezione del fatto che i messaggi possono essere inviati solo mediante i movimenti di messaggi non recapitabili hello dell'entità padre hello. Inoltre, il parametro time-to-live non viene rispettato e non è possibile impostare come non recapitabile un messaggio di una coda DLQ. coda di messaggi non recapitabili Hello supporta operazioni transazionali e il recapito di blocco di visualizzazione.

Si noti che non vi sia alcuna pulizia automatica di hello DLQ. I messaggi rimangono nella hello DLQ fino a quando non è in modo esplicito recuperarli da DLQ hello e chiamare [complete ()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) nel messaggio non recapitabile hello.

## <a name="moving-messages-toohello-dlq"></a>Lo spostamento di messaggi toohello DLQ

Esistono diverse attività di Service Bus che causano tooget messaggi inserito toohello DLQ all'interno di hello motore di messaggistica. Un'applicazione in modo esplicito anche possibile spostare messaggi toohello DLQ. 

Come messaggio hello viene spostato dal broker hello, due proprietà vengono aggiunti toohello messaggio come broker hello chiama la versione di hello interna [dei messaggi non recapitabili](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) metodo sul messaggio hello: `DeadLetterReason` e `DeadLetterErrorDescription`.

Le applicazioni possono definire i propri codici per hello `DeadLetterReason` proprietà, ma hello sistema set hello seguenti valori.

| Condizione | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Sempre |HeaderSizeExceeded |Hello dimensioni per il flusso è stato superato. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing e SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |messaggio Hello scaduta e è stato recapitabile. |
| SubscriptionDescription.RequiresSession |L'ID sessione ha valore null. |L'entità attivata dalla sessione non consente il recapito di un messaggio il cui identificatore di sessione è null. |
| !dead letter queue |MaxTransferHopCountExceeded |Null |
| Configurazione esplicita di messaggio non recapitabile da parte dell'applicazione  |Specificato dall'applicazione |Specificato dall'applicazione |

## <a name="exceeding-maxdeliverycount"></a>Superamento di MaxDeliveryCount
Code e sottoscrizioni hanno una [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) e [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) proprietà hello; rispettivamente il valore predefinito è 10. Ogni volta che un messaggio è stato recapitato in un blocco ([Receivemode](/dotnet/api/microsoft.servicebus.messaging.receivemode)), ma è stato uno in modo esplicito il blocco di hello scaduto, del messaggio hello o abbandonata [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) è incrementato. Quando [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) supera [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), il messaggio hello viene spostata toohello DLQ, specificando hello `MaxDeliveryCountExceeded` codice motivo.

Non è possibile disabilitare questo comportamento, ma è possibile impostare [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa numero di dimensioni molto grandi.

## <a name="exceeding-timetolive"></a>Superamento di TimeToLive
Quando hello [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) o [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) impostata troppo**true** (valore predefinito di hello è **false**), tutti i messaggi scaduti vengono spostato toohello DLQ, specificando hello `TTLExpiredException` codice motivo.

Si noti che i messaggi scaduti vengono eliminati solo e pertanto spostato toohello DLQ quando è presente almeno un destinatario active pull nella coda principale hello o nella sottoscrizione; Questo comportamento è da progettazione.

## <a name="errors-while-processing-subscription-rules"></a>Errori durante l'elaborazione di regole di sottoscrizione
Quando hello [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) proprietà è abilitata per una sottoscrizione, eventuali errori che si verificano durante l'esecuzione di regola di filtro di una sottoscrizione SQL vengono acquisite in hello DLQ insieme a hello danneggiata di messaggio.

## <a name="application-level-dead-lettering"></a>Definizione di messaggi non recapitabili a livello di applicazione
In toohello fornita dal sistema mancato recapito dei messaggi non recapitabili funzionalità aggiuntive, le applicazioni possono utilizzare messaggi inaccettabili hello DLQ tooexplicitly rifiuto. Ciò può includere i messaggi che non possono essere elaborati correttamente a causa di ordinamento tooany di errore di sistema, i messaggi contenenti payload in formato non valido o che l'autenticazione non riesce quando viene utilizzato un schema di sicurezza a livello di messaggio.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Messaggi non recapitabili negli scenari ForwardTo o SendVia

I messaggi verranno inviati toohello trasferimento non recapitabili in hello seguenti condizioni:

- Un messaggio passa attraverso più di 3 code o argomenti che sono [concatenati](service-bus-auto-forwarding.md).
- argomento o coda di destinazione di Hello è disabilitato o eliminato.
- coda di destinazione Hello o un argomento supera le dimensioni massime entità hello.

tooretrieve questi messaggi recapitabile dei messaggi non recapitabili, è possibile creare un ricevitore di hello [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) metodo di utilità.

## <a name="example"></a>Esempio
Hello frammento di codice seguente crea un ricevitore del messaggio. In hello ricezione ciclo per la coda principale hello, codice hello recupera il messaggio hello con [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), che richiede hello broker tooinstantly restituito qualsiasi messaggio disponibile o tooreturn con nessun risultato. Se il codice hello riceve un messaggio, immediatamente Ignora, che viene incrementato hello `DeliveryCount`. Una volta sistema hello Sposta toohello messaggio hello DLQ, coda principale hello è vuota e hello viene chiusa ciclo, come [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) restituisce **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Vedere i seguenti articoli per ulteriori informazioni sulle code Service Bus hello:

* [Introduzione alle code del bus di servizio](service-bus-dotnet-get-started-with-queues.md)
* [Analogie e differenze tra le code di Azure e le code del bus di servizio](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

