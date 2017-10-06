---
title: aaaProgramming Guida per gli hub di eventi di Azure | Documenti Microsoft
description: Scrivere codice per gli hub di eventi di Azure utilizzando hello Azure .NET SDK.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Guida alla programmazione di Hub eventi

In questo articolo vengono illustrati alcuni scenari comuni nella scrittura del codice tramite hub di eventi di Azure e hello Azure .NET SDK. Si presuppone una conoscenza preliminare di Hub eventi. Per una panoramica concettuale di hub eventi, vedere hello [Panoramica di hub eventi](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Publisher di eventi

Si invia l'hub di eventi eventi tooan usando HTTP POST o tramite una connessione AMQP 1.0. scelta di quali toouse Hello e quando dipende hello scenario specifico. Le connessioni AMQP 1.0 sono misurate come connessioni negoziate nel bus di servizio e sono più appropriate in scenari in cui sono frequenti volumi di messaggi più elevati e con requisiti di latenza inferiori, perché offrono un canale di messaggistica persistente.

Per creare e gestire hub eventi utilizzando hello [NamespaceManager][] classe. Quando si utilizza .NET hello gestito API, hello primario costrutti per la pubblicazione di dati tooEvent gli hub sono hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) e [EventData][] classi. [EventHubClient][] fornisce canale di comunicazione AMQP hello in cui gli eventi vengono inviati toohello hub di eventi. Hello [EventData][] classe rappresenta un evento ed è l'hub di eventi utilizzati toopublish messaggi tooan. Questa classe include informazioni di intestazione sull'evento hello corpo hello e alcuni metadati. Altre proprietà vengono aggiunte toohello [EventData][] oggetto durante il passaggio attraverso un hub eventi.

## <a name="get-started"></a>Attività iniziali

classi di .NET Hello che supportano hub eventi sono incluse nei hello assembly Microsoft.ServiceBus.dll. Hello più semplice hello tooreference modo API del Bus di servizio e tooconfigure l'applicazione con tutte le dipendenze di Service Bus hello è hello toodownload [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus). In alternativa, è possibile utilizzare hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) in Visual Studio. toodo in tal caso, eseguire comando in hello seguente hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) finestra:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Creare un hub eventi
È possibile utilizzare hello [NamespaceManager][] classe toocreate hub di eventi. ad esempio:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

Nella maggior parte dei casi, è consigliabile utilizzare hello [CreateEventHubIfNotExists][] tooavoid metodi generare eccezioni se si riavvia il servizio di hello. ad esempio:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Tutte le operazioni di creazione di hub eventi, inclusi [CreateEventHubIfNotExists][], richiedono **Gestisci** autorizzazioni nello spazio dei nomi hello in questione. Se si desidera che le autorizzazioni hello toolimit delle applicazioni publisher o consumer, è possibile evitare queste creare chiamate dell'operazione nel codice di produzione quando si usano credenziali con autorizzazioni limitate.

Hello [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) classe contiene informazioni dettagliate su un hub eventi, inclusi le regole di autorizzazione hello, intervallo di conservazione dei messaggi hello, ID di partizione, lo stato e percorso. È possibile utilizzare questi metadati hello tooupdate di classe in un hub eventi.

## <a name="create-an-event-hubs-client"></a>Creare un client di Hub eventi
Hello classe primaria per l'interazione con hub eventi è [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Questa classe fornisce funzionalità di mittente e destinatario. È possibile creare un'istanza di questa classe utilizzando hello [crea](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) (metodo), come illustrato nell'esempio seguente hello.

```csharp
var client = EventHubClient.Create(description.Path);
```

Questo metodo utilizza informazioni di connessione del Bus di servizio hello nel file app. config hello nella hello `appSettings` sezione. Per un esempio di hello `appSettings` XML informazioni di connessione del Bus di servizio toostore hello, vedere la documentazione di hello per hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) metodo.

Un'altra opzione consiste client hello toocreate da una stringa di connessione. Questa opzione funziona bene quando si usano i ruoli di lavoro di Azure, poiché è possibile archiviare la stringa hello nelle proprietà di configurazione hello di thread di lavoro hello. ad esempio:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

stringa di connessione Hello sarà in hello stesso formato così come appare nel file app. config hello metodi precedenti hello:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Infine, è anche possibile toocreate un [EventHubClient][] dell'oggetto da un [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) istanza, come illustrato nell'esempio seguente hello.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

È importante toonote che ulteriori [EventHubClient][] gli oggetti creati da un'istanza di factory di messaggistica riutilizzerà hello stessa connessione TCP sottostante. Di conseguenza, questi oggetti prevedono un limite sul lato client per la velocità effettiva. Hello [crea](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) metodo riutilizza una singola factory di messaggistica. Se è necessario molto elevata velocità effettiva di un singolo mittente, è possibile creare più factory di messaggistica e un oggetto [EventHubClient][] factory di messaggistica.

## <a name="send-events-tooan-event-hub"></a>Hub di eventi tooan gli eventi di trasmissione
Hub di eventi eventi tooan si invia tramite la creazione di un [EventData][] istanza e inviarlo tramite hello [inviare](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) metodo. Questo metodo accetta un singolo [EventData][] parametro dell'istanza e lo invia in modo sincrono tooan hub di eventi.

## <a name="event-serialization"></a>Serializzazione degli eventi
Hello [EventData][] classe ha [quattro costruttori di overload](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) che accettano una serie di parametri, ad esempio un oggetto e serializzatore, una matrice di byte o un flusso. È inoltre possibile tooinstantiate hello [EventData][] e impostare flusso del corpo hello in seguito. Quando si usa JSON con [EventData][], è possibile utilizzare **Encoding.UTF8.GetBytes()** tooretrieve hello matrice di byte una stringa con codifica JSON.

## <a name="partition-key"></a>Chiave di partizione
Hello [EventData][] classe dispone di un [PartitionKey][] proprietà che consente di hello mittente toospecify un valore che è stato eseguito l'hashing tooproduce un'assegnazione della partizione. L'utilizzo di una chiave di partizione assicura che hello tutti gli eventi con hello stessa chiave vengono inviati toohello stessa partizione nell'hub eventi hello. Le chiavi di partizione comuni includono ID sessione utente e ID mittente univoci. Hello [PartitionKey][] proprietà è facoltativa e può essere fornito quando si utilizza hello [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) o [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) metodi. Se non si specifica un valore per [PartitionKey][], inviati gli eventi sono toopartitions distribuita tramite un modello round robin.

### <a name="availability-considerations"></a>Considerazioni sulla disponibilità

L'utilizzo di una chiave di partizione è facoltativo e valutare con attenzione se toouse uno. La chiave di partizione è un'ottima scelta se l'ordine degli eventi è importante. Quando si usa una chiave di partizione, queste partizioni richiedono la disponibilità in un singolo nodo. Nel tempo possono verificarsi interruzioni, ad esempio al riavvio dei nodi di calcolo e all'applicazione di patch. Di conseguenza, se si imposta un ID di partizione e tale partizione diventa non disponibile per qualche motivo, un tentativo tooaccess di dati hello in quella partizione avrà esito negativo. Se la disponibilità elevata è la più importante, non specificare una chiave di partizione. In questo caso gli eventi verranno inviati toopartitions utilizzando hello round-robin modello descritto in precedenza. In questo scenario, si stanno apportando una scelta esplicita tra disponibilità (Nessun ID di partizione) e la coerenza (ID di partizione tooa degli eventi di blocco).

Va anche considerata la gestione dei ritardi nell'elaborazione degli eventi. In alcuni casi potrebbe essere migliore toodrop dati e ripetere più tootry e sincronizzato con l'elaborazione, che può causare ritardi un'ulteriore elaborazione a valle. Ad esempio, con le quotazioni di borsa è toowait migliori per i dati aggiornati completati, ma in una chat in tempo reale o scenario VOIP invece si desidera utilizzare dati hello rapidamente, anche se non è completo.

Specificato queste considerazioni sulla disponibilità, in questi scenari è possibile scegliere una delle seguenti strategie di gestione degli errori di hello:

- Arresto (arresto della lettura da Hub eventi fino alla risoluzione del problema)
- Eliminazione (i messaggi non sono importanti, eliminarli)
- Ripetere (Buongiorno tentativi messaggi come base)
- [Recapitabili](../service-bus-messaging/service-bus-dead-letter-queues.md) (usare una coda o un altro evento hub toodead lettera solo messaggi hello elaborazione)

Per ulteriori informazioni e una discussione su hello compromesso tra disponibilità e la coerenza, vedere [disponibilità e la coerenza in hub eventi](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Operazioni di invio di eventi in batch
L'invio di eventi in batch può aumentare la velocità effettiva. Hello [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) metodo accetta un **IEnumerable** parametro di tipo [EventData][] e invia hello dell'intero batch come hub di eventi toohello un'operazione atomica.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Si noti che un singolo batch non deve superare il limite di 256 KB hello di un evento. Inoltre, ogni messaggio in batch hello utilizza hello stessa identità del server di pubblicazione. È responsabilità di hello di hello mittente tooensure che hello batch non superi le dimensioni eventi massime hello. In questo caso, viene generato un errore di **invio** del client.

## <a name="send-asynchronously-and-send-at-scale"></a>Inviare in modo asincrono e inviare a livello di scalabilità
È anche possibile inviare in modo asincrono l'hub di eventi tooan di eventi. Invio in modo asincrono, è possibile aumentare il tasso di hello in corrispondenza del quale un client è in grado di toosend eventi. Entrambi hello [inviare](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) e [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) metodi sono disponibili nelle versioni asincrone, che restituiscono un [attività](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) oggetto. Sebbene questa tecnica può aumentare la velocità effettiva, inoltre causare hello client toocontinue toosend eventi anche durante la è limitata da hello servizio hub eventi e può comportare errori hello client o perdita di messaggi in caso contrario implementata correttamente. Inoltre, è possibile utilizzare hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) proprietà opzioni di ripetizione di hello client toocontrol client.

## <a name="create-a-partition-sender"></a>Creare un mittente di partizione
Sebbene sia più comune toosend eventi tooan hub eventi senza una chiave di partizione, in alcuni casi potrebbe essere toosend eventi direttamente tooa la partizione specificata. ad esempio:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) restituisce un [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) che è possibile utilizzare toopublish partizione dell'hub eventi specifico tooa eventi.

## <a name="event-consumers"></a>Consumer di eventi
Hub eventi dispone di due modelli principali per l'utilizzo di eventi: ricevitori diretti e astrazioni di livello superiore, ad esempio [EventProcessorHost][]. Ricevitori diretti sono responsabili per i propri coordinamento di accesso toopartitions all'interno di un gruppo di consumer.

### <a name="direct-consumer"></a>Consumer diretto
Hello tooread di modo più diretto da una partizione all'interno di un gruppo di consumer è hello toouse [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) classe. toocreate un'istanza di questa classe, è necessario utilizzare un'istanza di hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) classe. Nell'esempio seguente di hello, è necessario specificare ID di partizione hello durante la creazione di ricevitore hello per il gruppo di consumer hello.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Hello [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) dispone di diversi overload che facilitano il controllo sul reader hello creato. Questi metodi includono la specifica di un offset sotto forma di stringa o timestamp e hello possibilità toospecify se tooinclude questo offset specificato in hello restituito stream o iniziare dopo di esso. Dopo aver creato il ricevitore hello, è possibile avviare la ricezione di eventi in hello restituito l'oggetto. Hello [ricezione](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) metodo dispone di quattro overload che hello controllo parametri dell'operazione, ad esempio le dimensioni di batch di ricezione e tempo di attesa. È possibile utilizzare versioni asincrone di hello della velocità effettiva di hello tooincrease metodi di un consumer. ad esempio:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Con una partizione specifica tooa riguardo, vengono ricevuti messaggi hello in ordine di hello in cui sono stati inviati toohello hub di eventi. offset di Hello è un token di stringa di utilizzati tooidentify un messaggio in una partizione.

Si noti che una singola partizione all'interno di un gruppo di consumer non può avere più di cinque lettori concorrenti connessi in un determinato momento. Come i lettori connettono o si disconnettono, le relative sessioni potrebbero rimanere attive per alcuni minuti prima che il servizio hello riconosca che si sono disconnessi. Durante questo periodo, la riconnessione tooa partizione potrebbe non riuscire. Per un esempio completo di scrittura di un ricevitore diretto per hub eventi, vedere hello [ricevitori diretti di hub eventi](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) esempio.

### <a name="event-processor-host"></a>Host processore di eventi
Hello [EventProcessorHost][] classe elabora i dati dall'hub eventi. È consigliabile utilizzare questa implementazione durante la generazione reader di eventi sulla piattaforma .NET hello. [EventProcessorHost][] fornisce un ambiente di runtime thread-safe, multiprocesso e sicuro per le implementazioni del processore di eventi che fornisce inoltre la gestione di lease di Checkpoint e la partizione.

hello toouse [EventProcessorHost][] (classe), è possibile implementare [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Questa interfaccia contiene tre metodi:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

creare un'istanza di elaborazione, l'evento toostart [EventProcessorHost][], fornendo i parametri appropriati hello per l'hub eventi. Chiamare quindi [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister il [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementazione con runtime hello. A questo punto, l'host di hello tenterà tooacquire un lease per ogni partizione nell'hub di eventi hello usando un algoritmo "greedy". Tali lease dureranno per un determinato intervallo di tempo e quindi devono essere rinnovati. Appena nuovi nodi, istanze di lavoro in questo caso, portare in linea, questi effettuano le prenotazioni di lease e nel tempo carico hello sposta tra i nodi come ognuno tenta tooacquire più lease.

![Host processore di eventi](./media/event-hubs-programming-guide/IC759863.png)

Con il passare del tempo, viene stabilito un equilibrio. Questa funzionalità dinamica consente la scalabilità automatica basata sulla CPU toobe applicato tooconsumers per la scalabilità verticale e scalabilità verticale. Poiché gli hub di eventi non hanno una conoscenza diretta del numero di messaggi, utilizzo medio della CPU è spesso hello migliore meccanismo toomeasure back-end o consumer scala. Se i Publisher iniziano toopublish in grado di elaborare ulteriori eventi di consumer, aumento della CPU hello sui consumer può essere utilizzato toocause scalabilità automatica sul numero di istanze di lavoro.

Hello [EventProcessorHost][] implementa anche un meccanismo di checkpoint basato su archiviazione di Azure. È stata hello di archivi questo meccanismo offset nei singoli per ogni partizione, in modo che ogni consumer possa determinare quali ultimo checkpoint hello consumer precedente hello. Come per le partizioni passano tra i nodi tramite lease, si tratta di meccanismo di sincronizzazione hello che facilita lo spostamento del carico.

## <a name="publisher-revocation"></a>Revoca di publisher
Inoltre toohello funzionalità avanzate per la fase di esecuzione di [EventProcessorHost][], hub eventi consente la revoca di publisher in ordine tooblock Publisher specifici di hub di eventi tooan evento di invio. Queste funzionalità sono particolarmente utili se un token del server di pubblicazione è stata compromessa, o un aggiornamento software sta provocando toobehave non corretta. In questi casi, l'identità del server di pubblicazione di hello, che fa parte del token di firma di accesso condiviso, può essere bloccato dalla pubblicazione di eventi.

Per ulteriori informazioni sulla revoca di publisher e come toosend tooEvent hub come server di pubblicazione, vedere hello [evento hub grande scala pubblicazione sicura](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) esempio.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sugli scenari di hub eventi, visitare i collegamenti:

* [Panoramica dell'API di Hub eventi](event-hubs-api-overview.md)
* [Che cos'è Hub eventi?](event-hubs-what-is-event-hubs.md)
* [Disponibilità e coerenza nell'Hub eventi](event-hubs-availability-and-consistency.md)
* [Riferimento all'API dell'host processore di eventi](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
