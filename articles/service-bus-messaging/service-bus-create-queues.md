---
title: le applicazioni che usano code di Azure Service Bus aaaWrite | Documenti Microsoft
description: Come toowrite una semplice applicazione basata su coda che utilizza Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Creare applicazioni che utilizzano le code del Bus di servizio
In questo argomento vengono descritte le code di Service Bus e Mostra come toowrite una semplice applicazione basata su coda che utilizza Service Bus.

Si consideri uno scenario da HelloWorld vendita al dettaglio, in cui i dati di vendita da singoli punto vendita (POS) terminali devono essere indirizzati tooan sistema di gestione che usa hello dati toodetermine quando è toobe un nuovo approvvigionamento. Questa soluzione Usa messaggistica del Bus di servizio per la comunicazione hello tra i terminali hello e sistema di gestione inventario hello, come illustrato nella seguente illustrazione hello:

![Figura 1 Code del bus di servizio](./media/service-bus-create-queues/IC657161.gif)

Ogni terminale segnala i dati di vendita tramite l'invio di messaggi toohello **DataCollectionQueue**. I messaggi rimangono nella coda finché vengono recuperati dal sistema di gestione inventario hello. Questo modello viene spesso definito *messaggistica asincrona*, perché non dispone di toowait per una risposta dall'elaborazione di hello inventario Gestione sistema toocontinue terminal hello POS.

## <a name="why-queuing"></a>Quali sono i vantaggi offerti dalle code?
Prima di esaminare il codice hello in tooset necessario configurare l'applicazione, prendere in considerazione i vantaggi di hello dell'utilizzo di una coda in questo scenario invece di dover terminali hello POS comunicare direttamente (sincrona) toohello inventario di sistema di gestione.

### <a name="temporal-decoupling"></a>Disaccoppiamento temporaneo.
Con modello di messaggistica asincrona di hello, producer e consumer non è in linea toobe in hello contemporaneamente. infrastruttura di messaggistica Hello archivia in modo affidabile i messaggi hello finché consumer non è pronto tooreceive li. Ciò significa che i componenti di hello di un'applicazione hello distribuita possono essere disconnesso, sia volontariamente; ad esempio, per la manutenzione o a causa di arresto anomalo del componente tooa, senza influire sull'intero sistema hello. Inoltre, utilizzano l'applicazione hello può avere solo toobe online durante determinate ore del giorno hello. Ad esempio, in questo scenario di vendita al dettaglio, il sistema di gestione inventario hello può avere toocome online dopo la fine di hello della giornata lavorativa hello.

### <a name="load-leveling"></a>Livellamento del carico
In molte applicazioni carico del sistema varia nel tempo, mentre il tempo di elaborazione di hello necessario per ogni unità di lavoro è in genere costante. Messaggio interposizione producer e consumer indica una coda che hello applicazione consumer (lavoratore hello) ha solo toobe il provisioning tooservice anziché un carico di picco di carico una Media. profondità Hello della coda di hello aumenteranno e contratto come hello in arrivo carico varia. Direttamente, ciò consente di risparmiare denaro con quantità toohello considerare infrastruttura richiesto tooservice hello carico dell'applicazione.

![Figura 2 Code del bus di servizio](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Bilanciamento del carico.
Aumento del carico come hello, altri processi di lavoro possono essere aggiunto tooread dalla coda di lavoro hello. Ogni messaggio viene elaborato da un solo hello di processi di lavoro. Inoltre, il bilanciamento del carico basato su pull consente un uso ottimale dei computer di lavoro hello anche se il computer di lavoro hello differiscono con power tooprocessing conto, come verrà estraggono i messaggi alla propria velocità massima. Questo modello viene spesso definito modello consumer concorrenti hello.

![Figura 3 Code del bus di servizio](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Accoppiamento di tipo loose
Utilizzo di toointermediate accodamento del messaggio tra messaggio producer e consumer fornisce un accoppiamento intrinseco tra i componenti di hello. Poiché producer e consumer non sono consapevoli di altra, è possibile aggiornare un consumer senza causare alcun effetto sul producer hello. Inoltre, hello topologia di messaggistica può evolvere senza influire sull'endpoint esistenti hello. Tratteremo questo in modo più approfondito quando si parlerà di pubblicazione/sottoscrizione.

## <a name="show-me-hello-code"></a>Mostra il codice hello
Hello seguente sezione mostra come toouse Bus di servizio toobuild questa applicazione.

### <a name="sign-up-for-an-azure-account"></a>Iscriversi a un account Azure
È necessario un account Azure in ordine toostart funziona con il Bus di servizio. Se non si ha già una sottoscrizione, è possibile registrarsi per un account gratuito [qui](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Creare uno spazio dei nomi
Dopo avere creato una sottoscrizione è possibile [creare uno spazio dei nomi del servizio](service-bus-create-namespace-portal.md). Ogni spazio dei nomi funge da contenitore di ambito per un set di entità del Bus di servizio. Assegnare al nuovo spazio dei nomi un nome univoco tra tutti gli account del Bus di servizio. 

### <a name="install-hello-nuget-package"></a>Installare il pacchetto NuGet hello
spazio dei nomi Service Bus toouse hello, un'applicazione deve fare riferimento hello assembly Bus di servizio, in particolare Microsoft.ServiceBus.dll. È possibile trovare questo assembly come parte di Microsoft Azure SDK hello e download di hello è disponibile all'indirizzo hello [pagina di download di Azure SDK](https://azure.microsoft.com/downloads/). Tuttavia, hello [pacchetto NuGet di Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) è hello più semplice modo tooget hello API del Bus di servizio e tooconfigure l'applicazione con tutte le dipendenze di hello Bus di servizio.

### <a name="create-hello-queue"></a>Creare la coda hello
Le operazioni di gestione per il Bus di servizio, le entità di messaggistica (code e pubblicazione/sottoscrizione argomenti) vengono eseguite tramite hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe. Il bus di servizio usa un modello di sicurezza basato su [SAS (Shared Access Signature, Firma di accesso condiviso)](service-bus-sas.md). Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe rappresenta un provider di token di sicurezza con metodi factory incorporati restituzione di alcuni provider di token noti. Si userà un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) le credenziali di firma di accesso condiviso di metodo toohold hello. Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) istanza viene quindi costruita con indirizzo di base di spazio dei nomi Service Bus hello e provider di token hello hello.

Hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe fornisce metodi toocreate, enumerare ed eliminare entità di messaggistica. Hello codice riportata di seguito viene illustrato come hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) istanza viene creata e utilizzata toocreate hello **DataCollectionQueue** coda.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Si noti che esistono overload di hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) metodo che abilita le proprietà di hello coda toobe ottimizzati. Ad esempio, è possibile impostare hello time-to-live (TTL) predefinita per i messaggi inviati toohello coda.

### <a name="send-messages-toohello-queue"></a>Messaggi toohello coda di invio
Per le operazioni di runtime su entità del bus di servizio, ad esempio l'invio e la ricezione di messaggi, un'applicazione deve prima creare un oggetto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory). Toohello simile [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) dall'indirizzo di base di spazio dei nomi servizio hello e provider di token hello hello viene creata l'istanza.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

I messaggi inviati a e ricevuti dal Bus di servizio code sono istanze di hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Questa classe è costituita da un set di proprietà standard (ad esempio [etichetta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dizionario di proprietà dell'applicazione usato toohold e un corpo di dati applicazione arbitrari. Un'applicazione può impostare corpo hello passando qualsiasi oggetto serializzabile (hello seguente esempio di viene passata una **SalesData** oggetto che rappresenta i dati di vendita hello dal terminale POS hello), che verrà utilizzato hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) oggetto hello tooserialize. In alternativa, può essere specificato un oggetto [Flusso](https://msdn.microsoft.com/library/system.io.stream.aspx).

Hello tooa messaggi toosend di modo più semplice al coda, il case hello **DataCollectionQueue**, è toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate un [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) oggetto direttamente dal hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) istanza.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Ricezione di messaggi dalla coda hello
tooreceive messaggi dalla coda di hello, è possibile utilizzare un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) oggetto creato direttamente tramite hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) utilizzando [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). I ricevitori dei messaggi possono lavorare in due modalità diverse: **ReceiveAndDelete** e **PeekLock**. Hello [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) è impostato quando viene creato dal destinatario del messaggio hello, come un parametro toohello [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) chiamare.

Quando si utilizza hello **ReceiveAndDelete** hello di modalità di ricezione è un'operazione singola cattura; vale a dire quando Bus di servizio riceve una richiesta di hello, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione. **ReceiveAndDelete** modalità modello più semplice di hello ed è adatta per scenari in cui hello un'applicazione può tollerare non elabora un messaggio se un errore toooccur. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché il Bus di servizio è contrassegnato come messaggio come usato, quando riavvio dell'applicazione hello e inizia a usare nuovamente, i messaggi risulterà perso messaggio hello utilizzato prima dell'arresto anomalo di hello.

In **PeekLock** hello di modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta di hello, trova hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) nel messaggio ricevuto. Quando il Bus di servizio rileva hello [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) chiamata, contrassegna il messaggio hello come usato.

Sono possibili altri due risultati. Innanzitutto, se è in grado di un'applicazione hello tooprocess hello messaggio per qualche motivo, è possibile chiamare [abbandonare](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) nel messaggio ricevuto (invece di [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). In questo modo messaggio hello toounlock del Bus di servizio e renderlo disponibile toobe nuovamente ricevuto, tramite hello stesso consumer o da un altro consumer concorrente. In secondo luogo, vi è un timeout associato hello blocco e, se l'applicazione hello Impossibile elaborare il messaggio hello prima che il timeout di blocco hello scade (ad esempio, se si blocca l'applicazione hello), quindi verrà sbloccato Bus di servizio hello messaggio e renderlo disponibile toobe ricevuto nuovo (esecuzione essenzialmente un [abbandonare](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operazione per impostazione predefinita).

Si noti che se hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello [completa](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) richiesta inoltrata, il messaggio hello sarà applicazione toohello consegnati nuovamente dopo il riavvio. Questo è spesso definito * almeno una volta * l'elaborazione. Ciò significa che ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, sarà necessaria logica aggiuntiva dei duplicati di toodetect applicazione hello. Ciò può essere ottenuto in base a hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) proprietà del messaggio hello. il valore di Hello di questa proprietà rimane costante tra i tentativi di recapito. In questo caso si parla di elaborazione *Una sola volta*.

riceve Hello codice riportata di seguito ed elabora un messaggio hello utilizzando **PeekLock** modalità, che è hello predefinito se non [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) valore viene fornito in modo esplicito.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Utilizzare il client di coda hello
Negli esempi precedenti in questa sezione creato Hello [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) e [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) oggetti direttamente da hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend e ricevere messaggi dalla coda di hello, rispettivamente. Un approccio alternativo consiste toouse un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) oggetto, che supporta sia Invia e ricezione le operazioni in aggiunta toomore funzionalità avanzate, ad esempio le sessioni.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni fondamentali di hello di code, vedere [creare applicazioni che utilizzano gli argomenti del Bus di servizio e le sottoscrizioni](service-bus-create-topics-subscriptions.md) toocontinue questa discussione con funzionalità di pubblicazione/sottoscrizione hello di argomenti del Bus di servizio e sottoscrizioni.

