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
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="d5b11-104">La modalità di code toouse Bus di servizio con Java</span><span class="sxs-lookup"><span data-stu-id="d5b11-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="d5b11-105">Questo articolo viene descritto come toouse code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d5b11-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="d5b11-106">esempi di Hello sono scritti in Java e usano hello [Azure SDK per Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d5b11-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="d5b11-107">Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="d5b11-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="d5b11-108">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="d5b11-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="d5b11-109">Verificare di avere installato hello [Azure SDK per Java] [ Azure SDK for Java] prima di compilare questo esempio.</span><span class="sxs-lookup"><span data-stu-id="d5b11-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="d5b11-110">Se si usa Eclipse, è possibile installare hello [Azure Toolkit per Eclipse] [ Azure Toolkit for Eclipse] che include hello Azure SDK per Java.</span><span class="sxs-lookup"><span data-stu-id="d5b11-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="d5b11-111">È quindi possibile aggiungere hello **Microsoft Azure Libraries for Java** tooyour progetto:</span><span class="sxs-lookup"><span data-stu-id="d5b11-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="d5b11-112">Aggiungere il seguente hello `import` file Java hello cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="d5b11-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="d5b11-113">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="d5b11-113">Create a queue</span></span>
<span data-ttu-id="d5b11-114">Per eseguire operazioni di gestione per le code del bus di servizio, è possibile usare la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="d5b11-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="d5b11-115">Oggetto **ServiceBusContract** oggetto viene costruito con una configurazione appropriata che incapsula il token di firma di accesso condiviso con le autorizzazioni toomanage e hello **ServiceBusContract** classe è il punto unico di hello la comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b11-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="d5b11-116">Hello **ServiceBusService** classe fornisce metodi toocreate, enumerare ed eliminare code.</span><span class="sxs-lookup"><span data-stu-id="d5b11-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="d5b11-117">Hello di esempio seguente viene illustrato come un **ServiceBusService** oggetto può essere utilizzato toocreate una coda denominata `TestQueue`, con uno spazio dei nomi denominato `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="d5b11-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

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

<span data-ttu-id="d5b11-118">Sono disponibili metodi su `QueueInfo` che consentono di proprietà di hello coda toobe ottimizzati (ad esempio: tooset hello predefinito time-to-live (TTL) valore toobe applicato toomessages inviati toohello coda).</span><span class="sxs-lookup"><span data-stu-id="d5b11-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="d5b11-119">Hello esempio seguente viene illustrato come toocreate una coda denominata `TestQueue` con una dimensione massima di 5 GB:</span><span class="sxs-lookup"><span data-stu-id="d5b11-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="d5b11-120">Si noti che è possibile utilizzare hello `listQueues` metodo **ServiceBusContract** oggetti toocheck se una coda con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="d5b11-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="d5b11-121">Messaggi tooa coda di invio</span><span class="sxs-lookup"><span data-stu-id="d5b11-121">Send messages tooa queue</span></span>
<span data-ttu-id="d5b11-122">l'applicazione di una coda di Service Bus di messaggi tooa toosend, otterrà un **ServiceBusContract** oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5b11-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="d5b11-123">Hello seguente codice mostra come un messaggio per hello toosend `TestQueue` coda creata in precedenza in hello `HowToSample` dello spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="d5b11-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

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

<span data-ttu-id="d5b11-124">I messaggi inviati a e ricevuti dal Bus di servizio code sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="d5b11-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="d5b11-125">[BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di proprietà standard (ad esempio [etichetta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un dizionario usato toohold personalizzato proprietà specifiche dell'applicazione e un corpo di dati applicazione arbitrari.</span><span class="sxs-lookup"><span data-stu-id="d5b11-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="d5b11-126">Un'applicazione può impostare il corpo di hello del messaggio hello passando qualsiasi oggetto serializzabile al costruttore di hello di hello [BrokeredMessage][BrokeredMessage], e verrà quindi usata serializzatore appropriato hello oggetto hello tooserialize.</span><span class="sxs-lookup"><span data-stu-id="d5b11-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="d5b11-127">In alternativa, è possibile specificare un oggetto **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="d5b11-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="d5b11-128">Hello esempio seguente viene illustrato come test toosend cinque messaggi toothe `TestQueue` **MessageSender** sono stati ottenuti nel frammento di codice precedente hello:</span><span class="sxs-lookup"><span data-stu-id="d5b11-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

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

<span data-ttu-id="d5b11-129">Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="d5b11-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="d5b11-130">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="d5b11-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="d5b11-131">Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda.</span><span class="sxs-lookup"><span data-stu-id="d5b11-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="d5b11-132">Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="d5b11-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="d5b11-133">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="d5b11-133">Receive messages from a queue</span></span>
<span data-ttu-id="d5b11-134">Hello primario aspetto tooreceive dei messaggi da una coda è toouse un **ServiceBusContract** oggetto.</span><span class="sxs-lookup"><span data-stu-id="d5b11-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="d5b11-135">I messaggi ricevuti possono essere usati in due modalità diverse: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="d5b11-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="d5b11-136">Quando si utilizza hello **ReceiveAndDelete** , la modalità di ricezione è un'operazione singola cattura -, ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio in una coda, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5b11-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="d5b11-137">**ReceiveAndDelete** modalità (modalità predefinita di hello) è il modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="d5b11-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="d5b11-138">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d5b11-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="d5b11-139">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="d5b11-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="d5b11-140">In **PeekLock** , la modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="d5b11-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="d5b11-141">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5b11-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="d5b11-142">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando **eliminare** nel messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="d5b11-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="d5b11-143">Quando il Bus di servizio rileva hello **eliminare** chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="d5b11-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="d5b11-144">Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando **PeekLock** modalità (non hello predefinita).</span><span class="sxs-lookup"><span data-stu-id="d5b11-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="d5b11-145">esegue un ciclo infinito Hello esempio riportato di seguito ed elabora i messaggi man mano che arrivano nel nostro `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="d5b11-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="d5b11-146">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="d5b11-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="d5b11-147">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="d5b11-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="d5b11-148">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **unlockMessage** metodo sul messaggio ricevuto (anziché hello **deleteMessage** (metodo)).</span><span class="sxs-lookup"><span data-stu-id="d5b11-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="d5b11-149">Questa condizione provoca hello toounlock Bus di servizio dei messaggi in coda hello e renderlo disponibile toobe nuovamente ricevuto sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="d5b11-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="d5b11-150">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno della coda, e se un'applicazione hello avrà esito negativo tooprocess hello messaggio prima della scadenza del timeout di blocco (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e rende disponibili toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="d5b11-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="d5b11-151">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **deleteMessage** richiesta viene eseguita, il messaggio hello è applicazione toohello consegnati nuovamente quando viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="d5b11-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="d5b11-152">Spesso si tratta di *almeno una volta elaborazione*; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="d5b11-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="d5b11-153">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="d5b11-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="d5b11-154">Questa operazione viene spesso eseguita utilizzando hello **getMessageId** (metodo) del messaggio hello, che rimane costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="d5b11-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5b11-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5b11-155">Next Steps</span></span>
<span data-ttu-id="d5b11-156">Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="d5b11-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="d5b11-157">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="d5b11-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
