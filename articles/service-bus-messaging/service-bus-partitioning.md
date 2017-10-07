---
title: aaaCreate partizionata argomenti e code del Bus di servizio di Azure | Documenti Microsoft
description: "Descrive la modalità di connessione toopartition code del Bus di servizio e gli argomenti utilizzando più messaggi."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Code e argomenti partizionati
Azure Service Bus sfrutta più messaggi di Service Broker tooprocess messaggi e più messaggistica Archivia messaggi toostore. Una coda o un argomento convenzionale è gestito da un singolo broker messaggi e archiviato in un archivio di messaggistica. Bus di servizio *partizioni* abilitare le code e argomenti, o *entità di messaggistica*, toobe partizionati in più gestori di messaggi e archivi di messaggistica. Ciò significa che hello velocità effettiva complessiva di un'entità partizionata non è più limitata dalle prestazioni hello di un singolo broker messaggi o archivio di messaggistica. Inoltre, un'interruzione temporanea dell'alimentazione di un archivio di messaggistica non determina la mancanza di disponibilità di una coda o di un argomento partizionato. Le code e gli argomenti partizionati possono contenere tutte le funzionalità avanzate del bus di servizio, ad esempio il supporto delle transazioni e delle sessioni.

Per informazioni sui meccanismi interni di Service Bus, vedere hello [architettura del Bus di servizio] [ Service Bus architecture] articolo.

Il partizionamento è abilitato per impostazione predefinita al momento della creazione dell'entità in tutte le code e tutti gli argomenti della messaggistica sia Standard che Premium. È possibile creare entità di livello messaggistica Standard senza il partizionamento, ma le code e gli argomenti in uno spazio dei nomi Premium vengono sempre partizionati. Questa opzione non può essere disabilitata. 

Non è possibile toochange hello partizionamento opzione in una coda esistente o un argomento nei livelli Standard o Premium, è possibile impostare solo opzione hello quando si crea entità hello.

## <a name="how-it-works"></a>Funzionamento

Ogni coda o argomento partizionato è costituito da più frammenti. Ogni frammento viene memorizzato in un archivio di messaggistica differente e gestito da un broker messaggi diverso. Quando viene inviato un messaggio tooa coda o argomento partizionato, Bus di servizio assegna tooone messaggio hello di frammenti di hello. selezione di Hello viene eseguita in modo casuale dal Bus di servizio o tramite una chiave di partizione che hello mittente è possibile specificare.

Quando un client richiede che un messaggio da una coda partizionata tooreceive o da un argomento partizionato tooa di sottoscrizione, Bus di servizio esegue una query di tutti i frammenti dei messaggi, quindi restituisce hello primo messaggio viene ottenuto da una qualsiasi delle hello ricevitore toohello archivi di messaggistica. Bus di servizio cache di hello altri messaggi e restituisce quando riceve altre richieste di ricezione. Un client destinatario non è a conoscenza di partizionamento hello. Hello comportamento destinata al client di una coda o argomento partizionato (ad esempio, lettura, completamento, rinvio, non recapitabilità, prelettura) è identico toohello comportamento di un'entità normale.

I messaggi a una coda o a un argomento partizionato non presentano costi aggiuntivi, né in invio né in ricezione.

## <a name="enable-partitioning"></a>Abilitare il partizionamento

toouse partizionare code e argomenti con il Bus di servizio di Azure, utilizzare hello Azure SDK 2.2 o versione successiva oppure specificare `api-version=2013-10` nelle richieste HTTP.

### <a name="standard"></a>Standard

Nel livello di messaggistica hello Standard, è possibile creare le code del Bus di servizio e gli argomenti in dimensioni di 1, 2, 3, 4 o 5 GB (valore predefinito di hello è 1 GB). Con il partizionamento abilitato, Bus di servizio crea 16 copie (16 partizioni) dell'entità hello per ogni GB specificato. Di conseguenza, se si crea una coda è di 5 GB di dimensioni, con 16 partizioni le dimensioni massime della coda di hello diventa (5 \* 16) = 80 GB. È possibile visualizzare dimensioni massime di hello della coda o argomento partizionato esaminando relativa voce nel hello [portale di Azure][Azure portal], in hello **Panoramica** pannello per l'entità.

### <a name="premium"></a>Premium

In uno spazio dei nomi livello Premium, è possibile creare le code del Bus di servizio e gli argomenti in dimensioni di 1, 2, 3, 4, 5, 10, 20, 40 o 80 GB (valore predefinito di hello è 1 GB). Con il partizionamento abilitato per impostazione predefinita, il bus di servizio crea due partizioni per ogni entità. È possibile visualizzare dimensioni massime di hello della coda o argomento partizionato esaminando relativa voce nel hello [portale di Azure][Azure portal], in hello **Panoramica** pannello per l'entità.

Per ulteriori informazioni sul partizionamento nel livello di messaggistica di hello Premium, vedere [livelli di messaggistica Standard e Premium Bus di servizio](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Creare una tabella partizionata

Esistono diversi modi toocreate una coda partizionata o argomento. Quando si crea la coda hello o un argomento dall'applicazione, è possibile abilitare il partizionamento per hello coda o argomento da rispettivamente hello di impostazione [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] o [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] proprietà troppo**true**. Queste proprietà devono essere impostate su hello tempo hello coda o argomento viene creato. Come indicato in precedenza, è Impossibile toochange queste proprietà in una coda esistente o un argomento. ad esempio:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

In alternativa, è possibile creare una coda o argomento partizionato in hello [portale di Azure] [ Azure portal] o in Visual Studio. Quando si crea una coda o argomento nel portale di hello, hello **abilitare il partizionamento** opzione hello coda o argomento **crea** pannello è selezionato per impostazione predefinita. È solo possibile disabilitare questa opzione in un'entità di livello Standard. in hello partizionamento livello Premium è sempre abilitato. In Visual Studio, fare clic su hello **Abilita partizionamento** casella di controllo in hello **nuova coda** o **nuovo argomento** la finestra di dialogo.

## <a name="use-of-partition-keys"></a>Uso delle chiavi di partizione
Quando un messaggio è accodato in una coda o argomento partizionato, Service Bus verifica hello presenza di una chiave di partizione. Se ne trova uno, viene selezionato il frammento di hello in base a tale chiave. Se non trova una chiave di partizione, seleziona il frammento di hello in base a un algoritmo interno.

### <a name="using-a-partition-key"></a>Uso di una chiave di partizione
Alcuni scenari, ad esempio le sessioni o le transazioni richiedono toobe messaggi archiviati in un frammento specifico. Tutti questi scenari richiedono l'uso di hello di una chiave di partizione. Tutti i messaggi hello tale uso stessa chiave di partizione vengono assegnati toohello stesso frammento. Se il frammento di hello è temporaneamente non disponibile, Bus di servizio restituisce un errore.

A seconda dello scenario di hello, diverse proprietà dei messaggi vengono utilizzate come chiave di partizione:

**SessionId**: se dispone di un messaggio hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] imposta proprietà, quindi il Bus di servizio utilizza questa proprietà come chiave di partizione hello. In questo modo, tutti i messaggi che appartengono toohello stessa sessione vengono gestiti da hello stesso broker messaggi. In questo modo, messaggio di Service Bus tooguarantee ordinamento e la coerenza di hello degli stati sessione.

**PartitionKey**: se dispone di un messaggio hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] proprietà ma non hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] imposta proprietà, quindi Service Bus Usa hello [PartitionKey] [ PartitionKey] proprietà come chiave di partizione hello. Se il messaggio hello ha entrambi hello [SessionId] [ SessionId] hello e [PartitionKey] [ PartitionKey] set di proprietà, entrambe le proprietà devono essere identiche. Se hello [PartitionKey] [ PartitionKey] proprietà è impostata tooa valore diverso hello [SessionId] [ SessionId] , Bus di servizio restituisce un oggetto non valido un'operazione. Hello [PartitionKey] [ PartitionKey] proprietà deve essere utilizzata se un mittente invia messaggi transazionali grado di riconoscere non di sessione. Hello chiave di partizione assicura che tutti i messaggi inviati all'interno di una transazione vengono gestiti da hello stesso broker di messaggistica.

**MessageId**: se la coda hello o un argomento ha hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] impostata troppo**true** e hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] o [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] proprietà non sono impostate, quindi hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] proprietà viene utilizzata come chiave di partizione hello. Si noti che le librerie di Microsoft .NET e AMQP hello assegnare automaticamente un ID messaggio se non dispone di un'applicazione hello invio. In questo caso, tutte le copie di hello stesso messaggio vengono gestiti da hello stesso broker messaggi. Questo consente toodetect Bus di servizio, eliminare i messaggi duplicati. Se hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] non è impostata troppo**true**, Bus di servizio non considera hello [MessageId] [ MessageId] proprietà come chiave di partizione.

### <a name="not-using-a-partition-key"></a>Senza l'uso di una chiave di partizione
In assenza di hello di una chiave di partizione, Bus di servizio consente di distribuire i messaggi in un frammenti di hello schema round-robin tooall di hello coda o argomento partizionato. Se il frammento di hello scelto non è disponibile, Bus di servizio assegna differenti frammenti tooa messaggio hello. In questo modo, hello trasmissione operazione ha esito positivo nonostante la temporanea indisponibilità hello di un archivio di messaggistica. Tuttavia, si otterranno non hello garantito l'ordinamento che fornisce una chiave di partizione.

Per una discussione più dettagliata di compromesso hello tra disponibilità (nessuna chiave di partizione) e la coerenza (tramite una chiave di partizione), vedere [questo articolo](../event-hubs/event-hubs-availability-and-consistency.md). Queste informazioni si applicano ugualmente toopartitioned entità del Bus di servizio e le partizioni degli hub di eventi.

toogive Service Bus sufficiente messaggio hello tooenqueue di tempo in un frammento differente, hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] valore specificato dal client hello che invia il messaggio hello deve essere maggiore di 15 secondi. È consigliabile impostare hello [OperationTimeout] [ OperationTimeout] valore predefinito della proprietà toohello di 60 secondi.

Si noti che una chiave di partizione "associa" un frammento di messaggio tooa specifico. Se l'archivio di messaggistica hello contenente questo frammento non è disponibile, Bus di servizio restituisce un errore. In assenza di hello di una chiave di partizione, Bus di servizio è possibile scegliere un frammento differente e hello operazione ha esito positivo. È quindi consigliabile non specificare una chiave di partizione, a meno che non sia necessario.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Argomenti avanzati: usare le transazioni con entità partizionate
I messaggi inviati come parte di una transazione devono specificare una chiave di partizione. Può trattarsi di una delle seguenti proprietà hello: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], o [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Tutti i messaggi vengono inviati come parte della stessa transazione debba specificare hello hello stessa chiave di partizione. Se si tenta di toosend un messaggio senza una chiave di partizione in una transazione, Bus di servizio restituisce un'eccezione di operazione non valida. Se si tenta di toosend più messaggi all'interno di hello stessa transazione che presentano le chiavi di partizione, Bus di servizio restituisce un'eccezione di operazione non valida. ad esempio:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Se sono impostate le proprietà di hello che fungono da una chiave di partizione, pin di Service Bus hello frammenti di messaggi tooa specifico. Questo comportamento si verifica indipendentemente dall'uso di una transazione. È consigliabile non specificare una chiave di partizione, a meno che non sia necessario.

## <a name="using-sessions-with-partitioned-entities"></a>Uso delle sessioni con entità partizionate
toosend un argomento di un messaggio transazionale tooa con supporto della sessione o una coda, il messaggio hello deve avere hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] set di proprietà. Se hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] proprietà viene anche specificato deve essere identico toohello [SessionId] [ SessionId] proprietà. In caso contrario, il bus di servizio restituisce un'eccezione di operazione non valida.

A differenza delle code di regolare (non partizionata) o argomenti, non è possibile toouse toosend una singola transazione più sessioni toodifferent di messaggi. Se è stato effettuato un tentativo, il bus di servizio restituirà un'eccezione di operazione non valida, ad esempio:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Inoltro automatico dei messaggi con entità partizionate
Il bus di servizio supporta l'inoltro automatico dei messaggi da, a o tra entità partizionate. tooenable inoltro automatico dei messaggi, impostare hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] proprietà hello origine coda o sottoscrizione. Se il messaggio hello viene specificata una chiave di partizione ([SessionId][SessionId], [PartitionKey][PartitionKey], o [MessageId] [ MessageId]), la chiave di partizione viene utilizzata per entità di destinazione hello.

## <a name="considerations-and-guidelines"></a>Considerazioni e indicazioni
* **Funzionalità alti livelli di coerenza**: se un'entità vengono utilizzate caratteristiche quali sessioni, il rilevamento dei duplicati o il controllo esplicito di chiave di partizionamento, quindi le operazioni di messaggistica hello sono sempre toospecific indirizzato frammenti. Se uno qualsiasi dei frammenti di hello riscontrare traffico elevato o archivio sottostante hello è integro, tali operazioni esito negativo e viene ridotto di disponibilità. In generale, la coerenza di hello è ancora molto più elevata rispetto alle entità non partizionate; solo un subset di traffico di problemi, come il traffico hello tooall anziché. Per altre informazioni, vedere la [discussione relativa a disponibilità e coerenza](../event-hubs/event-hubs-availability-and-consistency.md).
* **Gestione**: operazioni, ad esempio Create, Update e Delete devono essere eseguite su tutti i frammenti di hello di entità hello. Se un frammento non è integro, potrebbero verificarsi errori per queste operazioni. Per l'operazione Get hello, informazioni come numero messaggi devono essere aggregate da tutti i frammenti. Se qualsiasi frammento non è integro, lo stato di disponibilità di hello entità risulta limitato.
* **Memoria insufficiente. gli scenari con messaggi**: tali scenari, soprattutto quando si utilizza il protocollo HTTP hello, potrebbe essere tooperform più operazioni di ricezione in ordine tooobtain tutti i messaggi hello. Per le richieste di ricezione, hello front-end esegue un'operazione di ricezione su tutti i frammenti di hello e memorizza nella cache tutte le risposte hello ricevute. Una richiesta di ricezione successive nella stessa connessione sarebbe vantaggioso la memorizzazione nella cache e ricevere le latenze di hello saranno inferiore. Se tuttavia sono presenti più connessioni o si usa HTTP, ciò crea una nuova connessione per ogni richiesta. Di conseguenza, non c'è garanzia che viene reindirizzato hello stesso nodo. Se tutti i messaggi esistenti sono bloccati e memorizzati nella cache in un altro front-end, hello visualizzato operazione restituisce **null**. I messaggi raggiungeranno infine la scadenza e verranno ricevuti di nuovo. È consigliabile usare la connessione keep-alive HTTP.
* **Sfoglia/Peek messaggi**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) non restituiscono sempre il numero di hello di messaggi specificati nel hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) proprietà. a causa di due motivi comuni. Uno dei motivi è che hello aggregate dimensioni della raccolta hello di messaggi raggiungono hello massimo di 256KB. Un altro motivo è che, se l'argomento o coda hello è hello [proprietà proprietà EnablePartitioning](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) impostare troppo**true**, una partizione potrebbe non essere sufficiente messaggi hello toocomplete richiesto numero di messaggi. In generale, se un'applicazione richiede un numero specifico di messaggi tooreceive, questo deve chiamare [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) ripetutamente finché non raggiunge il numero di messaggi o se è presente alcun toopeek messaggi più. Per altre informazioni, inclusi esempi di codice, vedere [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) o [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Funzionalità aggiunte di recente
* L'aggiunta o la rimozione di una regola è ora supportata con le entità partizionate. A differenza delle entità non partizionate, queste operazioni non sono supportate nelle transazioni. 
* AMQP è ora supportato per l'invio e ricezione di messaggi tooand da un'entità partizionata.
* AMQP è ora supportata per hello seguenti operazioni: [inviare Batch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [Batch di ricezione](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [ricezione dal numero di sequenza](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [Visualizza](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Rinnovare il blocco](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [pianificare messaggio](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [pianificato messaggio di annullamento](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Aggiungi regola](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [rimuovere regola](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Rinnovo della sessione di blocco](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [lo stato della sessione Set](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [lo stato della sessione Get](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), e [enumerare sessioni](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Limiti delle entità partizionate
Attualmente il Bus di servizio impone limitazioni seguenti su code e argomenti partizionati hello:

* Partizionata code e argomenti non supportano l'invio di messaggi che appartengono toodifferent sessioni in una singola transazione.
* Bus di servizio consente attualmente too100 partizionata code o argomenti per ogni spazio dei nomi. Ogni coda o argomento partizionato viene conteggiato quota hello di 10.000 entità per spazio dei nomi (si applica tooPremium livello).

## <a name="next-steps"></a>Passaggi successivi
Vedere la discussione hello di [AMQP 1.0 di supporto per il Bus di servizio partizionati code e argomenti] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn ulteriori informazioni sul partizionamento delle entità di messaggistica. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
