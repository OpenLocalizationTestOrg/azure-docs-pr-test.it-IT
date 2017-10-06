---
title: le applicazioni che utilizzano gli argomenti del Bus di servizio di Azure e le sottoscrizioni aaaCreate | Documenti Microsoft
description: "Introduzione toohello funzionalità di pubblicazione-sottoscrizione offerte da sottoscrizioni e gli argomenti del Bus di servizio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Creare applicazioni che usano argomenti e sottoscrizioni del bus di servizio
Il bus di servizio di Azure supporta un set di tecnologie middleware orientate ai messaggi e basate sul cloud, incluso l'accodamento dei messaggi affidabile e la messaggistica di pubblicazione e sottoscrizione permanente. Questo articolo si basa sulle informazioni hello fornite nella [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md) e offre un'introduzione di funzionalità di pubblicazione/sottoscrizione toohello offerte da argomenti del Bus di servizio.

## <a name="evolving-retail-scenario"></a>Scenario di vendita al dettaglio in evoluzione
In questo articolo continua uno scenario di vendita al dettaglio hello utilizzato [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md). Tenere presente che i dati di vendita da singoli terminali di punto di vendita (POS) devono essere indirizzato tooan sistema di gestione inventario che utilizza tale toodetermine dati quando è toobe un nuovo approvvigionamento. Ogni terminale segnala i dati di vendita tramite l'invio di messaggi toohello **DataCollectionQueue** coda, in cui rimangono finché vengono ricevuti dal sistema di gestione inventario hello, come illustrato di seguito:

![Bus di servizio 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve questo scenario, un nuovo requisito è stato aggiunto il sistema toohello: proprietario del Negozio hello vuole toomonitor in grado di toobe come hello del Negozio in tempo reale.

tooaddress questo requisito, il sistema hello deve "toccare" disattivare il flusso di dati di vendita hello. Si vuole comunque che ogni messaggio inviato da hello POS terminali toobe inviati sistema di gestione inventario toohello come prima, ma si desidera che un'altra copia di ogni messaggio che è possibile utilizzare toopresent hello dashboard toohello archivio utente.

In situazioni come questa, in cui è necessario toobe ogni messaggio usato da più parti, è possibile utilizzare il Bus di servizio *argomenti*. Argomenti forniscono un modello di pubblicazione/sottoscrizione in cui ogni messaggio pubblicato viene reso disponibile tooone o più sottoscrizioni registrate con l'argomento hello. Al contrario, con le code ogni messaggio viene ricevuto da un singolo consumer.

Argomento tooa in hello vengono inviati messaggi come inviati tooa coda. Tuttavia, i messaggi non vengono ricevuti dall'argomento hello direttamente. vengono ricevuti dalle sottoscrizioni. È possibile pensare di un argomento tooa sottoscrizione come una coda virtuale che riceve copie dei messaggi hello inviati toothat argomento. I messaggi vengono ricevuti da una sottoscrizione hello stesso modo in cui vengono ricevuti da una coda.

Tornando toohello uno scenario di vendita al dettaglio, coda hello viene sostituita da un argomento e una sottoscrizione viene aggiunto, è possibile utilizzare il componente di sistema hello Gestione inventario. sistema Hello viene visualizzato come segue:

![Bus di servizio 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

configurazione Hello agisce in modo identico toohello precedente basato su coda progettazione. Ovvero, i messaggi inviati argomento toohello sono toohello indirizzato **inventario** sottoscrizione, da cui hello **sistema di gestione inventario** li Usa.

Nel dashboard di gestione hello toosupport ordine, si crea una seconda sottoscrizione in argomento hello, come illustrato di seguito:

![Bus di servizio 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Con questa configurazione, ogni messaggio dai terminali hello POS è reso disponibile tooboth hello **Dashboard** e **inventario** sottoscrizioni.

## <a name="show-me-hello-code"></a>Mostra il codice hello
articolo Hello [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md) viene descritto come toosign fino a un account Azure e creare uno spazio dei nomi del servizio. dipendenze di Hello più semplice modo tooreference Bus di servizio è tooinstall hello Bus di servizio [pacchetto Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). È inoltre possibile trovare hello le librerie del Bus di servizio come parte di hello Azure SDK. Hello è possibile scaricare hello [pagina di download di Azure SDK](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Creazione di sottoscrizioni e argomento hello
Le operazioni di gestione per il Bus di servizio, le entità di messaggistica (code e pubblicazione/sottoscrizione argomenti) vengono eseguite tramite hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe. Sono necessarie le credenziali appropriate in ordine toocreate un **NamespaceManager** istanza per un determinato spazio dei nomi. Il bus di servizio usa un modello di sicurezza basato su [SAS (Shared Access Signature, Firma di accesso condiviso)](service-bus-sas.md). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) classe rappresenta un provider di token di sicurezza con metodi factory incorporati restituzione di alcuni provider di token noti. Si userà un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) le credenziali di firma di accesso condiviso di metodo toohold hello. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) istanza viene quindi costruita con indirizzo di base di spazio dei nomi Service Bus hello e provider di token hello hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe fornisce metodi toocreate, enumerare ed eliminare entità di messaggistica. Hello codice riportata di seguito viene illustrato come hello **NamespaceManager** istanza viene creata e utilizzata toocreate hello **DataCollectionTopic** argomento.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Si noti che esistono overload di hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) metodo che consentono di proprietà tooset di argomento hello. Ad esempio, è possibile impostare hello time-to-live (TTL) predefinita per i messaggi inviati toohello argomento. Successivamente, aggiungere hello **inventario** e **Dashboard** sottoscrizioni.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Inviare l'argomento toohello messaggi
Per le operazioni di runtime su entità del bus di servizio, ad esempio l'invio e la ricezione di messaggi, un'applicazione deve prima creare un oggetto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory). Toohello simile [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe hello **MessagingFactory** dall'indirizzo di base di spazio dei nomi servizio hello e provider di token hello hello viene creata l'istanza.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

I messaggi inviati tooand ricevuto da argomenti del Bus di servizio, sono istanze di hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Questa classe è costituita da un set di proprietà standard (ad esempio [etichetta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dizionario di proprietà dell'applicazione usato toohold e un corpo di dati applicazione arbitrari. Un'applicazione può impostare corpo hello passando qualsiasi oggetto serializzabile (hello seguente esempio di viene passata una **SalesData** oggetto che rappresenta i dati di vendita hello dal terminale POS hello), che verrà utilizzato hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) oggetto hello tooserialize. In alternativa, può essere specificato un oggetto [Flusso](https://msdn.microsoft.com/library/system.io.stream.aspx).

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

argomento con messaggi Hello più semplice modo toosend toohello è toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate un [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) oggetto direttamente da hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) istanza di:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Ricevere messaggi da una sottoscrizione
Le code di toousing simile, tooreceive messaggi da una sottoscrizione è possibile utilizzare un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) oggetto creato direttamente tramite hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) utilizzando [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). È possibile utilizzare uno di hello due diverse modalità di ricezione (**ReceiveAndDelete** e **PeekLock**), come illustrato in [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md).

Si noti che quando si crea un **MessageReceiver** per le sottoscrizioni, hello *entityPath* parametro è formato hello `topicPath/subscriptions/subscriptionName`. Pertanto, toocreate un **MessageReceiver** per hello **inventario** sottoscrizione di hello **DataCollectionTopic** argomento *entityPath*deve essere impostato troppo`DataCollectionTopic/subscriptions/Inventory`. codice Hello visualizzato come segue:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Filtri di sottoscrizione
Finora, in questo scenario tutti i messaggi inviati argomento toohello vengono effettuati le sottoscrizioni disponibili tooall registrato. di seguito frase chiave Hello "diventa disponibile." Mentre le sottoscrizioni del Bus di servizio vedere tutti i messaggi inviati toohello argomento, è possibile copiare solo un subset della coda di sottoscrizione virtuale toohello tali messaggi. Questa operazione viene eseguita usando i *filtri* della sottoscrizione. Quando si crea una sottoscrizione, è possibile fornire un'espressione di filtro sotto forma di hello di un predicato di tipo SQL92 opera sulle proprietà del messaggio hello di hello, entrambi hello le proprietà di sistema (ad esempio, [etichetta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) e un'applicazione hello proprietà, ad esempio **StoreName** nell'esempio precedente hello.

Evoluzione hello scenario tooillustrate questo, un secondo negozio è uno scenario di vendita al dettaglio tooour aggiunto toobe. Sistema di gestione inventario toohello centralizzata toobe indirizzato ancora su dati di vendita da tutti i terminali hello POS da entrambi gli archivi, ma un gestore dell'archivio utilizzando lo strumento dashboard hello è solo interessato prestazioni hello dell'archivio. È possibile utilizzare filtri tooachieve questa sottoscrizione. Si noti che quando i terminali hello POS pubblicano i messaggi, impostano hello **StoreName** proprietà applicazione messaggio hello. Ha due archivi, ad esempio **Redmond** e **Seattle**, i terminali hello POS hello Redmond archiviano i dati di vendita messaggi con timestamp un **StoreName** uguale troppo **Redmond**, mentre hello Seattle archivio utilizzare terminali POS un **StoreName** uguale troppo**Seattle**. gestore del negozio di Redmond archiviare solo hello Hello vuole toosee dati dal relativo terminali di punti vendita. sistema Hello visualizzato come segue:

![Servizio Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset di questo ciclo, si crea hello **Dashboard** sottoscrizione come indicato di seguito:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Con questo [filtro di sottoscrizione](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), solo i messaggi hello **StoreName** impostata troppo**Redmond** saranno copiati toohello coda virtuale hello **Dashboard** sottoscrizione. È molto più toosubscription tuttavia il filtro. Le applicazioni possono avere più regole di filtro per ogni sottoscrizione nelle proprietà hello toomodify delle possibilità di toohello di aggiunta di un messaggio quando viene posizionato coda virtuale tooa della sottoscrizione.

## <a name="summary"></a>Riepilogo
Tutti di hello motivi toouse Accodamento descritti nel [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md) si applicano anche tootopics, in particolare:

* Disaccoppiamento temporale: messaggio producer e consumer non è in linea toobe in hello contemporaneamente.
* Livellamento del carico: i picchi di carico vengono smussati dall'argomento di hello abilitando il provisioning per un carico medio anziché il carico massimo dispendiosa in termini di toobe di applicazioni.
* Bilanciamento del carico: coda tooa simili, è possibile disporre di più consumer concorrenti in attesa su una singola sottoscrizione, con ogni messaggio passato tooonly consumer hello, in tal modo il bilanciamento del carico.
* Regime di controllo: è possibile sviluppare hello messaggistica rete senza influire sull'endpoint esistente. ad esempio, l'aggiunta di sottoscrizioni o modificando i filtri tooa argomento tooallow di nuovi consumer.

## <a name="next-steps"></a>Passaggi successivi

Vedere [creare applicazioni che utilizzano le code del Bus di servizio](service-bus-create-queues.md) per informazioni su come toouse code in uno scenario di vendita al dettaglio hello POS.

