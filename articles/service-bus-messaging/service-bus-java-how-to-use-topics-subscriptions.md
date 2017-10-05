---
title: Come usare gli argomenti del bus di servizio di Azure con Java | Microsoft Docs
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
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="dda03-103">Come usare gli argomenti e le sottoscrizioni del bus di servizio con Java</span><span class="sxs-lookup"><span data-stu-id="dda03-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="dda03-104">Questa guida descrive come usare gli argomenti e le sottoscrizioni del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="dda03-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="dda03-105">Gli esempi sono scritti in Java e usano [Azure SDK per Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="dda03-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="dda03-106">Gli scenari presentati includono **la creazione di argomenti e sottoscrizioni**, **la creazione di filtri per le sottoscrizioni**, **l’invio di messaggi a un argomento**, **la ricezione di messaggi da una sottoscrizione** e **l’eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="dda03-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="dda03-107">Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?</span><span class="sxs-lookup"><span data-stu-id="dda03-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="dda03-108">Gli argomenti e le sottoscrizioni del bus di servizio supportano un modello di comunicazione con messaggistica di *pubblicazione-sottoscrizione* .</span><span class="sxs-lookup"><span data-stu-id="dda03-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="dda03-109">Quando si usano gli argomenti e le sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente l'uno con l'altro, ma scambiano messaggi tramite un argomento, che agisce da intermediario.</span><span class="sxs-lookup"><span data-stu-id="dda03-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![Concetti relativi agli argomenti](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="dda03-111">Diversamente dalle code del bus di servizio, in cui ogni messaggio viene elaborato da un unico consumer, gli argomenti e le sottoscrizioni offrono una forma di comunicazione "uno a molti" tramite un modello di pubblicazione-sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dda03-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="dda03-112">È possibile registrare più sottoscrizioni a un argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="dda03-113">Quando un messaggio viene inviato a un argomento, viene reso disponibile affinché ogni sottoscrizione possa gestirlo o elaborarlo in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="dda03-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="dda03-114">La sottoscrizione a un argomento è simile a una coda virtuale che riceve copie dei messaggi che sono stati inviati all'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="dda03-115">È possibile registrare regole di filtro per un argomento in base alla sottoscrizione in modo da poter filtrare/limitare i messaggi a un argomento ricevuti dalle diverse sottoscrizioni degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="dda03-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="dda03-116">Gli argomenti e le sottoscrizioni del bus di servizio garantiscono scalabilità, consentendo di elaborare grandi quantità di messaggi tra un numero elevato di utenti e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="dda03-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="dda03-117">Creare uno spazio dei nomi del servizio</span><span class="sxs-lookup"><span data-stu-id="dda03-117">Create a service namespace</span></span>
<span data-ttu-id="dda03-118">Per iniziare a usare gli argomenti e le sottoscrizioni del bus di servizio in Azure, è innanzitutto necessario creare uno spazio dei nomi che fornisca un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dda03-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="dda03-119">Per creare uno spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="dda03-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="dda03-120">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="dda03-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="dda03-121">Assicurarsi di aver installato [Azure SDK per Java][Azure SDK for Java] prima di compilare questo esempio.</span><span class="sxs-lookup"><span data-stu-id="dda03-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="dda03-122">Se si usa Eclipse, è possibile installare [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] che include Azure SDK per Java.</span><span class="sxs-lookup"><span data-stu-id="dda03-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="dda03-123">È quindi possibile aggiungere le **librerie di Microsoft Azure per Java** al progetto:</span><span class="sxs-lookup"><span data-stu-id="dda03-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="dda03-124">Aggiungere le seguenti istruzioni `import` all'inizio del file Java:</span><span class="sxs-lookup"><span data-stu-id="dda03-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="dda03-125">Aggiungere le librerie di Azure per Java al percorso di compilazione e includerlo nell'assembly di distribuzione del progetto.</span><span class="sxs-lookup"><span data-stu-id="dda03-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="dda03-126">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="dda03-126">Create a topic</span></span>
<span data-ttu-id="dda03-127">Per eseguire operazioni di gestione per gli argomenti del bus di servizio, è possibile usare la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="dda03-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="dda03-128">Un oggetto **ServiceBusContract** è costruito con una configurazione appropriata che incapsula il token di firma di accesso condiviso con le autorizzazioni necessarie a gestirlo. La classe **ServiceBusContract** rappresenta l'unico punto di comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="dda03-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="dda03-129">La classe **ServiceBusService** definisce i metodi per creare, enumerare ed eliminare gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="dda03-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="dda03-130">L'esempio seguente illustra come usare un oggetto **ServiceBusService** per creare un argomento con il nome `TestTopic` e uno spazio dei nomi denominato `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="dda03-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="dda03-131">In **TopicInfo** sono disponibili metodi che consentono di impostare le proprietà dell'argomento, ad esempio il valore TTL predefinito da applicare ai messaggi inviati all'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="dda03-132">L'esempio seguente illustra come creare un argomento denominato `TestTopic` con una dimensione massima pari a 5 GB:</span><span class="sxs-lookup"><span data-stu-id="dda03-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="dda03-133">Si noti che è possibile usare il metodo **listTopics** su oggetti **ServiceBusContract** per verificare se in uno spazio dei nomi servizio esiste già un argomento con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="dda03-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="dda03-134">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="dda03-134">Create subscriptions</span></span>
<span data-ttu-id="dda03-135">È possibile creare le sottoscrizioni a un argomento anche tramite la classe **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="dda03-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="dda03-136">Le sottoscrizioni sono denominate e possono includere un filtro facoltativo che limita l'insieme dei messaggi passati alla coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dda03-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="dda03-137">Creare una sottoscrizione con il filtro (MatchAll) predefinito</span><span class="sxs-lookup"><span data-stu-id="dda03-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="dda03-138">Il filtro **MatchAll** è il filtro predefinito e viene usato se non vengono specificati altri filtri durante la creazione di una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dda03-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="dda03-139">Quando si usa il filtro **MatchAll**, tutti i messaggi pubblicati nell'argomento vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dda03-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="dda03-140">Nell'esempio seguente viene creata una sottoscrizione denominata "AllMessages" e viene usato il filtro **MatchAll** predefinito.</span><span class="sxs-lookup"><span data-stu-id="dda03-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="dda03-141">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="dda03-141">Create subscriptions with filters</span></span>
<span data-ttu-id="dda03-142">È anche possibile creare filtri che consentono di specificare i messaggi inviati a un argomento da visualizzare in una specifica sottoscrizione dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="dda03-143">Il tipo di filtro più flessibile tra quelli supportati dalle sottoscrizioni è [SqlFilter][SqlFilter], che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="dda03-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="dda03-144">I filtri SQL agiscono sulle proprietà dei messaggi pubblicati nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="dda03-145">Per altri dettagli sulle espressioni che è possibile usare con un filtro SQL, esaminare la sintassi di [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="dda03-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="dda03-146">L'esempio seguente crea una sottoscrizione denominata `HighMessages` con un oggetto [SqlFilter][SqlFilter] che seleziona solo i messaggi che hanno una proprietà **MessageNumber** personalizzata maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="dda03-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="dda03-147">Analogamente, l'esempio seguente crea una sottoscrizione denominata `LowMessages` con un oggetto [SqlFilter][SqlFilter] che seleziona solo i messaggi in cui il valore della proprietà **MessageNumber** è minore o uguale a 3:</span><span class="sxs-lookup"><span data-stu-id="dda03-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="dda03-148">Un messaggio inviato a `TestTopic` verrà sempre recapitato a destinatari con sottoscrizione a `AllMessages` e recapitato selettivamente a destinatari con sottoscrizioni a `HighMessages` e `LowMessages` (a seconda del contenuto del messaggio).</span><span class="sxs-lookup"><span data-stu-id="dda03-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="dda03-149">Inviare messaggi a un argomento</span><span class="sxs-lookup"><span data-stu-id="dda03-149">Send messages to a topic</span></span>
<span data-ttu-id="dda03-150">Per inviare un messaggio a un argomento del bus di servizio, l'applicazione ottiene un oggetto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="dda03-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="dda03-151">Il codice seguente illustra come inviare un messaggio all'argomento `TestTopic` creato in precedenza nello spazio dei nomi `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="dda03-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="dda03-152">I messaggi inviati ad argomenti del bus di servizio sono istanze della classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="dda03-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="dda03-153">Gli oggetti [BrokeredMessage][BrokeredMessage]* includono un set di metodi standard, ad esempio **setLabel** e **TimeToLive**, un dizionario usato per contenere le proprietà personalizzate specifiche dell'applicazione e un corpo di dati arbitrari dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dda03-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="dda03-154">Per impostare il corpo del messaggio, un'applicazione può passare qualsiasi oggetto serializzabile nel costruttore di [BrokeredMessage][BrokeredMessage]. In tal caso per serializzare l'oggetto, verrà usato l'oggetto **DataContractSerializer** appropriato.</span><span class="sxs-lookup"><span data-stu-id="dda03-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="dda03-155">In alternativa, è possibile specificare un oggetto **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="dda03-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="dda03-156">L'esempio seguente illustra come inviare cinque messaggi di prova all'oggetto `TestTopic` **MessageSender** ottenuto nel frammento di codice sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="dda03-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="dda03-157">Si noti come il valore della proprietà **MessageNumber** di ogni messaggio varia nell'iterazione del ciclo, determinando le sottoscrizioni che lo riceveranno:</span><span class="sxs-lookup"><span data-stu-id="dda03-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="dda03-158">Gli argomenti del bus di servizio supportano messaggi di dimensioni massime fino a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e fino a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="dda03-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="dda03-159">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="dda03-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="dda03-160">Non esiste alcun limite al numero di messaggi mantenuti in un argomento, mentre è previsto un limite alla dimensione totale dei messaggi di un argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="dda03-161">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="dda03-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="dda03-162">Come ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="dda03-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="dda03-163">Per ricevere i messaggi da una sottoscrizione, usare un oggetto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="dda03-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="dda03-164">I messaggi ricevuti possono essere usati in due modalità diverse: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="dda03-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="dda03-165">Quando si usa la modalità **ReceiveAndDelete**, l'operazione di ricezione viene eseguita in un'unica fase. Quando infatti il bus di servizio riceve la richiesta di lettura relativa a un messaggio, lo contrassegna come usato e lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dda03-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="dda03-166">La modalità **ReceiveAndDelete** costituisce il modello più semplice ed è adatta per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="dda03-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="dda03-167">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="dda03-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="dda03-168">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="dda03-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="dda03-169">Nella modalità **PeekLock** l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="dda03-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="dda03-170">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dda03-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="dda03-171">Dopo aver elaborato il messaggio o averlo archiviato in modo affidabile per successive elaborazioni, l'applicazione esegue la seconda fase del processo di ricezione chiamando **Delete** sul messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="dda03-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="dda03-172">Quando il bus di servizio vede la chiamata **Delete**, contrassegna il messaggio come usato e lo rimuove dall'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="dda03-173">Nell'esempio seguente viene illustrato come ricevere ed elaborare messaggi usando la modalità **PeekLock** non predefinita.</span><span class="sxs-lookup"><span data-stu-id="dda03-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="dda03-174">L'esempio seguente esegue un ciclo, elabora i messaggi nella sottoscrizione "HighMessages" e infine esce quando non vi sono più messaggi (in alternativa, l'esempio può essere impostato per attendere l'arrivo di nuovi messaggi).</span><span class="sxs-lookup"><span data-stu-id="dda03-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

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
            // Display the topic message.
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
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="dda03-175">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="dda03-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="dda03-176">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="dda03-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="dda03-177">Se un'applicazione ricevitore non è in grado di elaborare il messaggio per un qualsiasi motivo, può chiamare il metodo **unlockMessage**, anziché **deleteMessage**, per il messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="dda03-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="dda03-178">In questo modo, il bus di servizio sbloccherà il messaggio nell'argomento rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="dda03-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="dda03-179">Al messaggio bloccato nell'argomento è associato anche un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="dda03-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="dda03-180">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio ma prima dell'invio della richiesta **deleteMessage**, il messaggio verrà nuovamente recapitato all'applicazione al riavvio.</span><span class="sxs-lookup"><span data-stu-id="dda03-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="dda03-181">Questo processo di elaborazione viene spesso definito di tipo **At-Least-Once**, per indicare che ogni messaggio verrà elaborato almeno una volta ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="dda03-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="dda03-182">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva all'applicazione per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="dda03-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="dda03-183">A tale scopo viene spesso usato il metodo **getMessageId** del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="dda03-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="dda03-184">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="dda03-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="dda03-185">Per eliminare argomenti e sottoscrizioni si usa principalmente un oggetto **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="dda03-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="dda03-186">Se si elimina un argomento, verranno eliminate anche tutte le sottoscrizioni registrate con l'argomento.</span><span class="sxs-lookup"><span data-stu-id="dda03-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="dda03-187">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="dda03-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="dda03-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dda03-188">Next Steps</span></span>
<span data-ttu-id="dda03-189">A questo punto, dopo aver appreso le nozioni di base delle code del bus di servizio, per altre informazioni vedere [Code, argomenti e sottoscrizioni del bus di servizio][Service Bus queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="dda03-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
