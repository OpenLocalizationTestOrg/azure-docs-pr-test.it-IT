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
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Concatenamento di entità del bus di servizio con l'inoltro automatico

Bus di servizio Hello *inoltro automatico* funzionalità permette di toochain una coda o sottoscrizione tooanother coda o un argomento che fa parte di hello stesso spazio dei nomi. Quando l'inoltro automatico è abilitato, Bus di servizio automaticamente rimuove i messaggi che vengono inseriti nella coda prima di hello o una sottoscrizione (origine) e li inserisce in coda secondo hello o un argomento (destinazione). Si noti che è comunque possibile toosend un'entità di destinazione toohello messaggio direttamente. Inoltre, non è possibile toochain una coda secondaria, ad esempio una coda di messaggi non recapitabili, tooanother coda o argomento.

## <a name="using-auto-forwarding"></a>Utilizzo dell'inoltro automatico
È possibile abilitare l'inoltro automatico impostando hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] o [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] proprietà hello [QueueDescription] [ QueueDescription] o [SubscriptionDescription] [ SubscriptionDescription] oggetti per l'origine di hello, come in hello esempio seguente.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

entità di destinazione Hello deve esistere in fase di hello viene creata l'entità di origine hello. Se non esiste l'entità di destinazione hello, Bus di servizio restituisce un'eccezione quando toocreate frequenti hello entità di origine.

È possibile usare l'inoltro automatico tooscale out un singolo argomento. Bus di servizio limiti hello [numero di sottoscrizioni per un determinato argomento](service-bus-quotas.md) too2, 000. Creando argomenti di secondo livello, è possibile aggiungere altre sottoscrizioni. Si noti che anche se non si è vincolati dal hello Bus di servizio limitazione hello numero di sottoscrizioni, aggiungere un secondo livello può migliorare hello velocità effettiva globale dell'argomento.

![Scenario di inoltro automatico][0]

È possibile utilizzare anche l'inoltro automatico toodecouple mittenti dai destinatari. Si consideri ad esempio un sistema ERP costituito da tre moduli: elaborazione degli ordini, gestione del magazzino e gestione dei rapporti con i clienti. Ognuno di questi moduli genera messaggi che vengono accodati in un argomento corrispondente. Alice e Bob sono rappresentanti di vendita sono interessati a tutti i messaggi correlati tootheir clienti. tooreceive tali messaggi, Alice e Bob creare una coda personale e una sottoscrizione in ognuno degli argomenti ERP hello che inoltrano automaticamente tutti i messaggi tootheir coda.

![Scenario di inoltro automatico][1]

Se uno dei rappresentanti si vacanza, la coda personale, anziché argomento ERP hello, esaurirsi. In questo scenario, poiché un rappresentante di vendita non ha ricevuto alcun messaggio, nessuno degli argomenti ERP hello raggiunge la quota.

## <a name="auto-forwarding-considerations"></a>Considerazioni sulla funzionalità di inoltro automatico

Se l'entità di destinazione hello accumula troppi messaggi e supera la quota di hello o entità di destinazione hello è disabilitato, entità di origine hello aggiunge hello messaggi tooits [recapitabili](service-bus-dead-letter-queues.md) fino a quando non è presente spazio nella destinazione hello (o entità hello viene riabilitata.) Tali messaggi verranno comunque toolive nella coda di messaggi non recapitabili hello, è necessario in modo esplicito di ricezione, elaborati dalla coda di messaggi non recapitabili hello.

Quando il concatenamento di singoli argomenti tooobtain un argomento composito con più sottoscrizioni, è consigliabile disporre di un numero limitato di sottoscrizioni per argomento di primo livello hello e numero di sottoscrizioni sugli argomenti di secondo livello hello. Ad esempio, un argomento di primo livello con 20 sottoscrizioni, ognuno di essi concatenate tooa argomento di secondo livello con 200 sottoscrizioni, consente una velocità effettiva rispetto a un argomento di primo livello con 200 sottoscrizioni, ciascuna concatenate tooa argomento di secondo livello con 20 sottoscrizioni .

Il bus di servizio addebita un'operazione per ogni messaggio inoltrato. Ad esempio, l'invio di un argomento di messaggio tooa con 20 sottoscrizioni, ciascuna di esse configurato messaggi tooauto forward tooanother coda o argomento, è addebitate 21 operazioni se tutte le sottoscrizioni di primo livello ricevono una copia del messaggio hello.

toocreate una sottoscrizione concatenata tooanother coda o argomento, è necessario disporre autore hello della sottoscrizione hello **Gestisci** autorizzazioni sul origine hello ed entità di destinazione hello. Invio richiede solo l'argomento di origine di messaggi toohello **inviare** le autorizzazioni per l'argomento di origine hello.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni dettagliate sulle funzionalità di inoltro automatico, vedere hello seguenti argomenti di riferimento:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn ulteriori informazioni sui miglioramenti delle prestazioni di Service Bus, vedere 

* [Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica del bus di servizio](service-bus-performance-improvements.md)
* [Entità di messaggistica partizionate][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
