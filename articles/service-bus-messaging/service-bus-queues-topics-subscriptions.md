---
title: aaaOverview di messaggistica code, argomenti e sottoscrizioni di Azure Service Bus | Documenti Microsoft
description: "Panoramica delle entità di messaggistica del bus di servizio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Code, argomenti e sottoscrizioni del bus di servizio

Il bus di servizio di Microsoft Azure supporta un set di tecnologie middleware orientate ai messaggi e basate sul cloud, incluso l'accodamento dei messaggi affidabile e la messaggistica di pubblicazione e sottoscrizione permanente. Queste funzionalità di messaggistica "negoziate" possono essere considerate separato funzionalità che supportano la pubblicazione-sottoscrizione di messaggistica, temporale disaccoppiamento e scenari con l'infrastruttura di messaggistica di hello Bus di servizio di bilanciamento del carico. La comunicazione disaccoppiata presenta molti vantaggi, ad esempio client e server possono connettersi quando necessario ed eseguire le relative operazioni in modo asincrono.

le entità di messaggistica Hello che costituiscono il nucleo di hello del hello funzionalità nel Bus di servizio di messaggistica sono code, argomenti e sottoscrizioni e regole/azioni.

## <a name="queues"></a>Code

Le code consentono *First In, First Out* tooone di recapito messaggi (FIFO) o più consumer concorrenti. Ovvero, i messaggi sono toobe previsto in genere ricevuti ed elaborati dai ricevitori hello in hello ordine in cui sono stati aggiunti toohello coda e ogni messaggio viene ricevuto ed elaborato da un solo consumer di messaggi. Un vantaggio chiave nell'utilizzo delle code è tooachieve "disaccoppiamento temporale" dei componenti dell'applicazione. Hello in altre parole, i producer (mittenti) e i consumer (ricevitori) non dispongono di toobe l'invio e ricezione di messaggi in hello stesso tempo, in quanto i messaggi vengono archiviati nella coda di hello. Inoltre, producer hello non ha toowait per una risposta dal consumer hello in ordine toocontinue tooprocess e inviare messaggi.

Un vantaggio correlato è "livellamento del carico," che consente di toosend producer e consumer e ricezione messaggi con ritmi diversi. In molte applicazioni, il carico del sistema hello varia nel tempo; Tuttavia, il tempo di elaborazione di hello necessario per ogni unità di lavoro è in genere costante. Interposizione messaggio producer e consumer una coda significa che hello utilizzano solo l'applicazione ha toobe toobe provisioning toohandle in grado di carico medio anziché il carico massimo. profondità Hello della coda di hello aumentano e i contratti in base alla variazione carico in ingresso hello. Direttamente, ciò consente di risparmiare denaro con quantità toohello considerare infrastruttura richiesto tooservice hello carico dell'applicazione. Aumento del carico come hello, altri processi di lavoro possono essere aggiunto tooread dalla coda hello. Ogni messaggio viene elaborato da un solo hello di processi di lavoro. Inoltre, il bilanciamento del carico basato su pull consente un uso ottimale dei computer di lavoro hello anche se il computer di lavoro hello differiscono con la potenza di tooprocessing, considerare come verrà estraggono i messaggi alla propria velocità massima. Questo modello viene spesso definito modello "consumer concorrente" hello.

Utilizzo di code toointermediate tra messaggio producer e consumer fornisce un accoppiamento inerente tra i componenti di hello. Poiché producer e consumer non sono consapevoli di altra, è possibile aggiornare un consumer senza causare alcun effetto sul producer hello.

La creazione di una coda è un processo che prevede più passaggi.  Eseguire operazioni di gestione per le entità (code e argomenti) tramite hello di messaggistica del Bus di servizio [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) (classe), che viene creato fornendo l'indirizzo di base hello di hello Bus di servizio spazio dei nomi e hello credenziali utente. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) fornisce i metodi toocreate, enumerare ed eliminare entità di messaggistica. Dopo aver creato un [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) oggetto oggetto dal nome hello e chiave e una gestione dello spazio dei nomi del servizio, è possibile utilizzare hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) coda hello toocreate di metodo. ad esempio:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

È quindi possibile creare un oggetto coda e una factory di messaggistica con hello URI del Bus di servizio come argomento. ad esempio:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

È quindi possibile inviare messaggi toohello coda. Ad esempio, se si dispone di un elenco di messaggi negoziati denominato `MessageList`, codice di hello sembra simile toohello seguenti:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Quindi ricevere messaggi dalla coda hello come indicato di seguito:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

In hello [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) ricezione hello modalità, l'operazione è l'unica; vale a dire quando Bus di servizio riceve una richiesta di hello, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione. **ReceiveAndDelete** modalità modello più semplice di hello ed è adatta per scenari in cui hello un'applicazione può tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché il Bus di servizio contrassegna il messaggio hello come usato, quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello di modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando Service Bus riceve una richiesta di hello, trova hello successivo messaggio toobe utilizzata, blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) nel messaggio ricevuto. Quando il Bus di servizio rileva hello **completa** chiamata, contrassegna il messaggio hello come usato.

Se è in grado di un'applicazione hello tooprocess hello messaggio per qualche motivo, è possibile chiamare hello [abbandonare](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) metodo sul messaggio ricevuto (invece di [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). In questo modo messaggio hello toounlock del Bus di servizio e renderlo disponibile toobe nuovamente ricevuto, tramite hello stesso consumer o da un altro consumer concorrente. In secondo luogo, vi è un timeout associato blocco hello e se un'applicazione hello avrà esito negativo tooprocess hello messaggio prima che il timeout di blocco hello scade (ad esempio, se si blocca l'applicazione hello), quindi Sblocca messaggio hello e rende disponibili toobe Service Bus ricevuto nuovo (esecuzione essenzialmente un [abbandonare](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operazione per impostazione predefinita).

Si noti che in hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello, ma prima di hello **completa** richiesta viene eseguita, il messaggio hello è applicazione toohello consegnati nuovamente dopo il riavvio. Questo processo di elaborazione viene spesso definito di tipo *At-Least-Once*, per indicare che ogni messaggio viene elaborato almeno una volta. Tuttavia, in determinati hello situazioni stesso potrà essere recapitato. Se hello scenario non tollera la doppia elaborazione, sarà necessaria logica aggiuntiva dei duplicati di toodetect applicazione hello che può essere raggiunto in base al hello **MessageId** proprietà del messaggio hello, che rimane costante tra i tentativi di recapito. Questo tipo di elaborazione viene definito di tipo *Exactly Once*.

## <a name="topics-and-subscriptions"></a>Argomenti e sottoscrizioni
In contrasto tooqueues, in cui ogni messaggio viene elaborato da un singolo consumer *argomenti* e *sottoscrizioni* forniscono una comunicazione, forma uno-a-molti un *dipubblicazione/sottoscrizione* modello. Utile per la scalabilità toovery un numero elevato di destinatari, ogni messaggio pubblicato viene reso disponibile tooeach sottoscrizione registrata con argomento hello. I messaggi vengono inviati tooa argomento e recapitati tooone o più sottoscrizioni associate, a seconda delle regole di filtro che possono essere impostate su una base per ogni sottoscrizione. le sottoscrizioni di Hello è possono utilizzare messaggi hello toorestrict di filtri aggiuntivi che desiderano tooreceive. I messaggi vengono inviati tooa argomento nella hello stesso modo vengono inviati tooa coda, ma i messaggi non vengono ricevuti direttamente dall'argomento hello. Vengono ricevuti dalle sottoscrizioni. Una sottoscrizione dell'argomento è simile a una coda virtuale che riceve copie dei messaggi hello inviati toohello argomento. I messaggi vengono ricevuti da una sottoscrizione in modo identico modo toohello vengono ricevuti da una coda.

A scopo di confronto, hello funzionalità di invio di una coda viene eseguito il mapping direttamente tooa argomento e la relativa funzionalità di ricezione del messaggio mappe tooa sottoscrizione. Tra le altre cose, ciò significa che le sottoscrizioni supportano hello stessi modelli descritti in precedenza in questa sezione con considerare tooqueues: consumer concorrente, disaccoppiamento temporale, livellamento del carico e bilanciamento del carico.

Creazione di un argomento è simile toocreating una coda, come illustrato nell'esempio hello nella sezione precedente hello. Creare l'URI del servizio hello e quindi utilizzare hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) client dello spazio dei nomi di classe toocreate hello. È quindi possibile creare un argomento utilizzando hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) metodo. ad esempio:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Aggiungere quindi le sottoscrizioni desiderate:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Sarà quindi possibile creare un client dell'argomento. ad esempio:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Utilizza mittente del messaggio hello, è possibile inviare e ricevere messaggi tooand dall'argomento hello, come illustrato nella sezione precedente hello. ad esempio:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Tooqueues simile, i messaggi vengono ricevuti da una sottoscrizione tramite un [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) oggetto anziché un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) oggetto. Creare hello sottoscrizione client, passando il nome di hello di argomento hello, nome hello di sottoscrizione hello e (facoltativamente) hello modalità di ricezione come parametri. Ad esempio, con hello **inventario** sottoscrizione:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Regole e azioni
In molti scenari, i messaggi con caratteristiche specifiche devono essere elaborati in modi specifici. tooenable, si possono configurare sottoscrizioni toofind messaggi che presentano le proprietà desiderate e quindi eseguono determinate proprietà toothose modifiche. Mentre le sottoscrizioni del Bus di servizio vedere tutti i messaggi inviati toohello argomento, è possibile copiare solo un subset della coda di sottoscrizione virtuale toohello tali messaggi. Questa operazione viene eseguita usando i filtri della sottoscrizione. Queste modifiche sono chiamate *azioni di filtro*. Quando viene creata una sottoscrizione, è possibile fornire un'espressione di filtro che opera sulle proprietà hello del messaggio hello, entrambi hello le proprietà di sistema (ad esempio, **etichetta**) e le proprietà personalizzate dell'applicazione (ad esempio, **StoreName**.) hello espressione di filtro SQL è facoltativa. senza un'espressione di filtro SQL, verrà eseguita alcuna azione di filtro definita in una sottoscrizione in tutti i messaggi hello per la sottoscrizione.

Utilizzando hello esempio precedente, i messaggi toofilter provenienti solo da **Store1**, è necessario creare una sottoscrizione di hello Dashboard come indicato di seguito:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Con questo filtro di sottoscrizione sul posto, solo i messaggi hello `StoreName` impostata troppo`Store1` vengono copiati toohello coda virtuale hello `Dashboard` sottoscrizione.

Per ulteriori informazioni sui valori di filtro possibili, vedere la documentazione di hello per hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) e [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classi. Vedere anche hello [messaggistica negoziata: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) e [argomento filtri](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) esempi.

## <a name="next-steps"></a>Passaggi successivi
Vedere di seguito hello avanzata per ulteriori informazioni ed esempi di utilizzo di messaggistica del Bus di servizio.

* [Panoramica della messaggistica del bus di servizio](service-bus-messaging-overview.md)
* [Esercitazione sulla messaggistica negoziata del bus di servizio - .NET](service-bus-brokered-tutorial-dotnet.md)
* [Esercitazione sulla messaggistica negoziata del bus di servizio - REST](service-bus-brokered-tutorial-rest.md)
* [Topic filters sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters) (Esempio Filtri di argomento)
* [Brokered Messaging: Advanced Filters sample](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) (Esempio Messaggistica negoziata: filtri avanzati)

