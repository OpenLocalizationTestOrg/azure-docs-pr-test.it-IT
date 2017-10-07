---
title: gli argomenti del Bus di servizio di Azure toouse aaaHow con Java | Documenti Microsoft
description: Usare gli argomenti e le sottoscrizioni del bus di servizio in Azure.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Il Bus di servizio toouse argomenti e sottoscrizioni con Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Questa guida viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni. esempi di Hello sono scritti in Java e usano hello [Azure SDK per Java][Azure SDK for Java]. Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?
Gli argomenti e le sottoscrizioni del bus di servizio supportano un modello di comunicazione con messaggistica di *pubblicazione-sottoscrizione* . Quando si usano gli argomenti e le sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente l'uno con l'altro, ma scambiano messaggi tramite un argomento, che agisce da intermediario.

![Concetti relativi agli argomenti](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

Diversamente dalle code del bus di servizio, in cui ogni messaggio viene elaborato da un unico consumer, gli argomenti e le sottoscrizioni offrono una forma di comunicazione "uno a molti" tramite un modello di pubblicazione-sottoscrizione. È possibile registrare l'argomento di tooa più sottoscrizioni. Quando l'argomento tooa viene inviato un messaggio, viene quindi reso disponibile tooeach sottoscrizione toohandle o il processo in modo indipendente.

Un argomento tooa sottoscrizione simile a una coda virtuale che riceve copie dei messaggi hello inviati toohello argomento. Facoltativamente, è possibile registrare le regole di filtro per un argomento in una base per ogni sottoscrizione, che consente di toofilter o limitare l'argomento tooa i messaggi vengono ricevuti dal quale le sottoscrizioni dell'argomento.

Le sottoscrizioni e gli argomenti del Bus di servizio consentono di tooscale tooprocess un numero molto elevato di messaggi in un numero molto elevato di utenti e applicazioni.

## <a name="create-a-service-namespace"></a>Creare uno spazio dei nomi del servizio
toobegin utilizzando gli argomenti del Bus di servizio e le sottoscrizioni in Azure, è innanzitutto necessario creare uno spazio dei nomi, che fornisce un contenitore per l'indirizzamento delle risorse del Bus di servizio all'interno dell'applicazione.

toocreate uno spazio dei nomi:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
Verificare di avere installato hello [Azure SDK per Java] [ Azure SDK for Java] prima di compilare questo esempio. Se si usa Eclipse, è possibile installare hello [Azure Toolkit per Eclipse] [ Azure Toolkit for Eclipse] che include hello Azure SDK per Java. È quindi possibile aggiungere hello **Microsoft Azure Libraries for Java** tooyour progetto:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Aggiungere il seguente hello `import` file Java hello cima toohello istruzioni:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Aggiungere hello Azure Libraries for Java tooyour percorso di compilazione e includerlo in assembly di distribuzione del progetto.

## <a name="create-a-topic"></a>Creare un argomento
Per eseguire operazioni di gestione per gli argomenti del bus di servizio, è possibile usare la classe **ServiceBusContract**. Oggetto **ServiceBusContract** oggetto viene costruito con una configurazione appropriata che incapsula il token di firma di accesso condiviso con le autorizzazioni toomanage e hello **ServiceBusContract** classe è il punto unico di hello la comunicazione con Azure.

Hello **ServiceBusService** classe fornisce metodi toocreate, enumerare ed eliminare gli argomenti. Hello seguente esempio viene illustrato come un **ServiceBusService** oggetto può essere utilizzato toocreate un argomento denominato `TestTopic`, con uno spazio dei nomi denominato `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Sono disponibili metodi su **TopicInfo** che abilitano la proprietà di argomento hello da impostare (ad esempio: tooset hello predefinito time-to-live (TTL) valore toobe applicato toomessages inviati toohello argomento). Hello esempio seguente viene illustrato come toocreate un argomento denominato `TestTopic` con una dimensione massima di 5 GB:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Si noti che è possibile utilizzare hello **listTopics** metodo **ServiceBusContract** oggetti toocheck se un argomento con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.

## <a name="create-subscriptions"></a>Creare sottoscrizioni
Tootopics le sottoscrizioni vengono creati anche con hello **ServiceBusService** classe. Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi passati coda virtuale toohello della sottoscrizione.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Creare una sottoscrizione con filtro predefinito (MatchAll) hello
Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione. Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione. esempio Hello crea una sottoscrizione denominata "AllMessages" e utilizza hello predefinito **MatchAll** filtro.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Creare sottoscrizioni con i filtri
È anche possibile creare filtri che consentono di tooscope cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.

Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è il [SqlFilter][SqlFilter], che implementa un subset di SQL92. I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato. Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.

esempio Hello crea una sottoscrizione denominata `HighMessages` con un [SqlFilter] [ SqlFilter] oggetto che seleziona solo i messaggi con un oggetto personalizzato **MessageNumber** proprietà maggiore di 3:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un [SqlFilter] [ SqlFilter] oggetto che seleziona solo i messaggi che hanno un **MessageNumber** proprietà minore o uguale too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Quando viene inviato un messaggio ora troppo`TestTopic`, verrà sempre recapitata tooreceivers sottoscritto toohello `AllMessages` sottoscrizione e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` (sottoscrizioni seconda il contenuto del messaggio).

## <a name="send-messages-tooa-topic"></a>Inviare l'argomento tooa messaggi
un argomento del Bus di servizio tooa messaggio toosend, l'applicazione otterrà un **ServiceBusContract** oggetto. Hello codice seguente viene illustrato come un messaggio per hello toosend `TestTopic` argomento creato in precedenza all'interno di hello `HowToSample` dello spazio dei nomi:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

I messaggi inviati gli argomenti del Bus tooService sono istanze di [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage][BrokeredMessage]* oggetti dispongono di un set di metodi standard (ad esempio **setLabel** e **TimeToLive**), un dizionario usato toohold personalizzato proprietà specifiche dell'applicazione e un corpo di dati applicazione arbitrari. Un'applicazione può impostare il corpo di hello del messaggio passando qualsiasi oggetto serializzabile al costruttore di hello del [BrokeredMessage][BrokeredMessage], hello appropriato e **DataContractSerializer ** potranno quindi essere oggetto di hello tooserialize utilizzato. In alternativa, è possibile specificare un oggetto **java.io.InputStream**.

Hello esempio seguente viene illustrato come test toosend cinque messaggi toothe `TestTopic` **MessageSender** sono stati ottenuti nel frammento di codice hello precedente.
Si noti come hello **MessageNumber** valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (per stabilire le sottoscrizioni che ricevano):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è previsto un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento. Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.

## <a name="how-tooreceive-messages-from-a-subscription"></a>La modalità tooreceive dei messaggi da una sottoscrizione
tooreceive messaggi da una sottoscrizione, utilizzare un **ServiceBusContract** oggetto. I messaggi ricevuti possono essere usati in due modalità diverse: **ReceiveAndDelete** e **PeekLock**.

Quando si utilizza hello **ReceiveAndDelete** , la modalità di ricezione è un'operazione singola cattura -, ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio, contrassegna il messaggio hello come usato e lo restituisce toothe applicazione. **ReceiveAndDelete** modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione. Poiché il Bus di servizio verrà contrassegnato il messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

In **PeekLock** , la modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando **eliminare** nel messaggio ricevuto. Quando il Bus di servizio rileva hello **eliminare** chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dall'argomento hello.

Hello esempio riportato di seguito viene illustrato come è possibile ricevere messaggi e trasformati utilizzando **PeekLock** modalità (non hello predefinita). Hello esempio riportato di seguito esegue un ciclo ed elabora i messaggi di hello "HighMessages" sottoscrizione e quindi viene chiuso quando non sono presenti ulteriori messaggi (in alternativa, Impossibile impostare toowait per i nuovi messaggi).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Come si blocca toohandle applicazione e i messaggi illeggibili
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **unlockMessage** metodo sul messaggio ricevuto (anziché hello **deleteMessage** (metodo)). Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di argomento hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno dell'argomento, e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima il timeout di blocco scade (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **deleteMessage** richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata. Spesso si tratta di **almeno una volta elaborazione**, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello **getMessageId** metodo di messaggio hello che rimangono costante tra i tentativi di recapito.

## <a name="delete-topics-and-subscriptions"></a>Eliminare argomenti e sottoscrizioni
Hello argomenti toodelete modo primario e le sottoscrizioni è toouse un **ServiceBusContract** oggetto. L'eliminazione di un argomento eliminerà anche le sottoscrizioni che sono registrate con l'argomento hello. Le sottoscrizioni possono essere eliminate anche in modo indipendente.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code del Bus di servizio, argomenti e sottoscrizioni] [ Service Bus queues, topics, and subscriptions] per ulteriori informazioni.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
