---
title: Accoda aaaHow toouse Service Bus di Azure con Java | Documenti Microsoft
description: Informazioni su come code di toouse Bus di servizio in Azure. Gli esempi di codice sono scritti in Java.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>La modalità di code toouse Bus di servizio con Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Questo articolo viene descritto come toouse code del Bus di servizio. esempi di Hello sono scritti in Java e usano hello [Azure SDK per Java][Azure SDK for Java]. Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurare il toouse applicazione Bus di servizio
Verificare di avere installato hello [Azure SDK per Java] [ Azure SDK for Java] prima di compilare questo esempio. Se si usa Eclipse, è possibile installare hello [Azure Toolkit per Eclipse] [ Azure Toolkit for Eclipse] che include hello Azure SDK per Java. È quindi possibile aggiungere hello **Microsoft Azure Libraries for Java** tooyour progetto:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Aggiungere il seguente hello `import` file Java hello cima toohello istruzioni:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Creare una coda
Per eseguire operazioni di gestione per le code del bus di servizio, è possibile usare la classe **ServiceBusContract**. Oggetto **ServiceBusContract** oggetto viene costruito con una configurazione appropriata che incapsula il token di firma di accesso condiviso con le autorizzazioni toomanage e hello **ServiceBusContract** classe è il punto unico di hello la comunicazione con Azure.

Hello **ServiceBusService** classe fornisce metodi toocreate, enumerare ed eliminare code. Hello di esempio seguente viene illustrato come un **ServiceBusService** oggetto può essere utilizzato toocreate una coda denominata `TestQueue`, con uno spazio dei nomi denominato `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Sono disponibili metodi su `QueueInfo` che consentono di proprietà di hello coda toobe ottimizzati (ad esempio: tooset hello predefinito time-to-live (TTL) valore toobe applicato toomessages inviati toohello coda). Hello esempio seguente viene illustrato come toocreate una coda denominata `TestQueue` con una dimensione massima di 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Si noti che è possibile utilizzare hello `listQueues` metodo **ServiceBusContract** oggetti toocheck se una coda con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.

## <a name="send-messages-tooa-queue"></a>Messaggi tooa coda di invio
l'applicazione di una coda di Service Bus di messaggi tooa toosend, otterrà un **ServiceBusContract** oggetto. Hello seguente codice mostra come un messaggio per hello toosend `TestQueue` coda creata in precedenza in hello `HowToSample` dello spazio dei nomi:

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

I messaggi inviati a e ricevuti dal Bus di servizio code sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di proprietà standard (ad esempio [etichetta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dizionario usato toohold personalizzato proprietà specifiche dell'applicazione e un corpo di dati applicazione arbitrari. Un'applicazione può impostare il corpo di hello del messaggio hello passando qualsiasi oggetto serializzabile al costruttore di hello di hello [BrokeredMessage][BrokeredMessage], e verrà quindi usata serializzatore appropriato hello oggetto hello tooserialize. In alternativa, è possibile specificare un oggetto **java.IO.InputStream**.

Hello esempio seguente viene illustrato come test toosend cinque messaggi toothe `TestQueue` **MessageSender** sono stati ottenuti nel frammento di codice precedente hello:

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md). intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB. Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda. Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.

## <a name="receive-messages-from-a-queue"></a>Ricevere messaggi da una coda
Hello primario aspetto tooreceive dei messaggi da una coda è toouse un **ServiceBusContract** oggetto. I messaggi ricevuti possono essere usati in due modalità diverse: **ReceiveAndDelete** e **PeekLock**.

Quando si utilizza hello **ReceiveAndDelete** , la modalità di ricezione è un'operazione singola cattura -, ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio in una coda, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione. **ReceiveAndDelete** modalità (modalità predefinita di hello) è il modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore. toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.
Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.

In **PeekLock** , la modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti. Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione. Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando **eliminare** nel messaggio ricevuto. Quando il Bus di servizio rileva hello **eliminare** chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.

Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando **PeekLock** modalità (non hello predefinita). esegue un ciclo infinito Hello esempio riportato di seguito ed elabora i messaggi man mano che arrivano nel nostro `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
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
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
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
Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio. Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **unlockMessage** metodo sul messaggio ricevuto (anziché hello **deleteMessage** (metodo)). Questa condizione provoca hello toounlock Bus di servizio dei messaggi in coda hello e renderlo disponibile toobe nuovamente ricevuto sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.

È inoltre disponibile un timeout associato a un messaggio bloccato all'interno della coda, e se un'applicazione hello avrà esito negativo tooprocess hello messaggio prima della scadenza del timeout di blocco (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e rende disponibili toobe nuovamente ricevuto.

In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **deleteMessage** richiesta viene eseguita, il messaggio hello è applicazione toohello consegnati nuovamente quando viene riavviata. Spesso si tratta di *almeno una volta elaborazione*; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio. Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi. Questa operazione viene spesso eseguita utilizzando hello **getMessageId** (metodo) del messaggio hello, che rimane costante tra i tentativi di recapito.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.

Per ulteriori informazioni, vedere hello [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
