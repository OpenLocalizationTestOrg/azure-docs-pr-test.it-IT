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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="7c956-103">Il Bus di servizio toouse argomenti e sottoscrizioni con Java</span><span class="sxs-lookup"><span data-stu-id="7c956-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7c956-104">Questa guida viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="7c956-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="7c956-105">esempi di Hello sono scritti in Java e usano hello [Azure SDK per Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="7c956-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="7c956-106">Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="7c956-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="7c956-107">Cosa sono gli argomenti e le sottoscrizioni del bus di servizio?</span><span class="sxs-lookup"><span data-stu-id="7c956-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="7c956-108">Gli argomenti e le sottoscrizioni del bus di servizio supportano un modello di comunicazione con messaggistica di *pubblicazione-sottoscrizione* .</span><span class="sxs-lookup"><span data-stu-id="7c956-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="7c956-109">Quando si usano gli argomenti e le sottoscrizioni, i componenti di un'applicazione distribuita non comunicano direttamente l'uno con l'altro, ma scambiano messaggi tramite un argomento, che agisce da intermediario.</span><span class="sxs-lookup"><span data-stu-id="7c956-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![Concetti relativi agli argomenti](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="7c956-111">Diversamente dalle code del bus di servizio, in cui ogni messaggio viene elaborato da un unico consumer, gli argomenti e le sottoscrizioni offrono una forma di comunicazione "uno a molti" tramite un modello di pubblicazione-sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c956-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="7c956-112">È possibile registrare l'argomento di tooa più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="7c956-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="7c956-113">Quando l'argomento tooa viene inviato un messaggio, viene quindi reso disponibile tooeach sottoscrizione toohandle o il processo in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="7c956-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="7c956-114">Un argomento tooa sottoscrizione simile a una coda virtuale che riceve copie dei messaggi hello inviati toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="7c956-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="7c956-115">Facoltativamente, è possibile registrare le regole di filtro per un argomento in una base per ogni sottoscrizione, che consente di toofilter o limitare l'argomento tooa i messaggi vengono ricevuti dal quale le sottoscrizioni dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="7c956-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="7c956-116">Le sottoscrizioni e gli argomenti del Bus di servizio consentono di tooscale tooprocess un numero molto elevato di messaggi in un numero molto elevato di utenti e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7c956-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="7c956-117">Creare uno spazio dei nomi del servizio</span><span class="sxs-lookup"><span data-stu-id="7c956-117">Create a service namespace</span></span>
<span data-ttu-id="7c956-118">toobegin utilizzando gli argomenti del Bus di servizio e le sottoscrizioni in Azure, è innanzitutto necessario creare uno spazio dei nomi, che fornisce un contenitore per l'indirizzamento delle risorse del Bus di servizio all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c956-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="7c956-119">toocreate uno spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="7c956-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="7c956-120">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="7c956-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="7c956-121">Verificare di avere installato hello [Azure SDK per Java] [ Azure SDK for Java] prima di compilare questo esempio.</span><span class="sxs-lookup"><span data-stu-id="7c956-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="7c956-122">Se si usa Eclipse, è possibile installare hello [Azure Toolkit per Eclipse] [ Azure Toolkit for Eclipse] che include hello Azure SDK per Java.</span><span class="sxs-lookup"><span data-stu-id="7c956-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="7c956-123">È quindi possibile aggiungere hello **Microsoft Azure Libraries for Java** tooyour progetto:</span><span class="sxs-lookup"><span data-stu-id="7c956-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="7c956-124">Aggiungere il seguente hello `import` file Java hello cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="7c956-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="7c956-125">Aggiungere hello Azure Libraries for Java tooyour percorso di compilazione e includerlo in assembly di distribuzione del progetto.</span><span class="sxs-lookup"><span data-stu-id="7c956-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="7c956-126">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="7c956-126">Create a topic</span></span>
<span data-ttu-id="7c956-127">Per eseguire operazioni di gestione per gli argomenti del bus di servizio, è possibile usare la classe **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="7c956-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="7c956-128">Oggetto **ServiceBusContract** oggetto viene costruito con una configurazione appropriata che incapsula il token di firma di accesso condiviso con le autorizzazioni toomanage e hello **ServiceBusContract** classe è il punto unico di hello la comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="7c956-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="7c956-129">Hello **ServiceBusService** classe fornisce metodi toocreate, enumerare ed eliminare gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="7c956-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="7c956-130">Hello seguente esempio viene illustrato come un **ServiceBusService** oggetto può essere utilizzato toocreate un argomento denominato `TestTopic`, con uno spazio dei nomi denominato `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="7c956-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="7c956-131">Sono disponibili metodi su **TopicInfo** che abilitano la proprietà di argomento hello da impostare (ad esempio: tooset hello predefinito time-to-live (TTL) valore toobe applicato toomessages inviati toohello argomento).</span><span class="sxs-lookup"><span data-stu-id="7c956-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="7c956-132">Hello esempio seguente viene illustrato come toocreate un argomento denominato `TestTopic` con una dimensione massima di 5 GB:</span><span class="sxs-lookup"><span data-stu-id="7c956-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="7c956-133">Si noti che è possibile utilizzare hello **listTopics** metodo **ServiceBusContract** oggetti toocheck se un argomento con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="7c956-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="7c956-134">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="7c956-134">Create subscriptions</span></span>
<span data-ttu-id="7c956-135">Tootopics le sottoscrizioni vengono creati anche con hello **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="7c956-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="7c956-136">Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi passati coda virtuale toohello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c956-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="7c956-137">Creare una sottoscrizione con filtro predefinito (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="7c956-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="7c956-138">Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c956-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7c956-139">Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c956-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="7c956-140">esempio Hello crea una sottoscrizione denominata "AllMessages" e utilizza hello predefinito **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="7c956-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7c956-141">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="7c956-141">Create subscriptions with filters</span></span>
<span data-ttu-id="7c956-142">È anche possibile creare filtri che consentono di tooscope cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="7c956-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="7c956-143">Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è il [SqlFilter][SqlFilter], che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="7c956-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="7c956-144">I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato.</span><span class="sxs-lookup"><span data-stu-id="7c956-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="7c956-145">Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.</span><span class="sxs-lookup"><span data-stu-id="7c956-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="7c956-146">esempio Hello crea una sottoscrizione denominata `HighMessages` con un [SqlFilter] [ SqlFilter] oggetto che seleziona solo i messaggi con un oggetto personalizzato **MessageNumber** proprietà maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="7c956-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

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

<span data-ttu-id="7c956-147">Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un [SqlFilter] [ SqlFilter] oggetto che seleziona solo i messaggi che hanno un **MessageNumber** proprietà minore o uguale too3:</span><span class="sxs-lookup"><span data-stu-id="7c956-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

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

<span data-ttu-id="7c956-148">Quando viene inviato un messaggio ora troppo`TestTopic`, verrà sempre recapitata tooreceivers sottoscritto toohello `AllMessages` sottoscrizione e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` (sottoscrizioni seconda il contenuto del messaggio).</span><span class="sxs-lookup"><span data-stu-id="7c956-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="7c956-149">Inviare l'argomento tooa messaggi</span><span class="sxs-lookup"><span data-stu-id="7c956-149">Send messages tooa topic</span></span>
<span data-ttu-id="7c956-150">un argomento del Bus di servizio tooa messaggio toosend, l'applicazione otterrà un **ServiceBusContract** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7c956-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="7c956-151">Hello codice seguente viene illustrato come un messaggio per hello toosend `TestTopic` argomento creato in precedenza all'interno di hello `HowToSample` dello spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="7c956-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="7c956-152">I messaggi inviati gli argomenti del Bus tooService sono istanze di [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="7c956-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="7c956-153">[BrokeredMessage][BrokeredMessage]* oggetti dispongono di un set di metodi standard (ad esempio **setLabel** e **TimeToLive**), un dizionario usato toohold personalizzato proprietà specifiche dell'applicazione e un corpo di dati applicazione arbitrari.</span><span class="sxs-lookup"><span data-stu-id="7c956-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="7c956-154">Un'applicazione può impostare il corpo di hello del messaggio passando qualsiasi oggetto serializzabile al costruttore di hello del [BrokeredMessage][BrokeredMessage], hello appropriato e **DataContractSerializer ** potranno quindi essere oggetto di hello tooserialize utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7c956-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="7c956-155">In alternativa, è possibile specificare un oggetto **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="7c956-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="7c956-156">Hello esempio seguente viene illustrato come test toosend cinque messaggi toothe `TestTopic` **MessageSender** sono stati ottenuti nel frammento di codice hello precedente.</span><span class="sxs-lookup"><span data-stu-id="7c956-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="7c956-157">Si noti come hello **MessageNumber** valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (per stabilire le sottoscrizioni che ricevano):</span><span class="sxs-lookup"><span data-stu-id="7c956-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="7c956-158">Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="7c956-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7c956-159">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="7c956-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7c956-160">Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è previsto un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento.</span><span class="sxs-lookup"><span data-stu-id="7c956-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="7c956-161">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="7c956-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="7c956-162">La modalità tooreceive dei messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7c956-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="7c956-163">tooreceive messaggi da una sottoscrizione, utilizzare un **ServiceBusContract** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7c956-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="7c956-164">I messaggi ricevuti possono essere usati in due modalità diverse: **ReceiveAndDelete** e **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="7c956-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="7c956-165">Quando si utilizza hello **ReceiveAndDelete** , la modalità di ricezione è un'operazione singola cattura -, ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio, contrassegna il messaggio hello come usato e lo restituisce toothe applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c956-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="7c956-166">**ReceiveAndDelete** modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="7c956-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="7c956-167">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7c956-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="7c956-168">Poiché il Bus di servizio verrà contrassegnato il messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7c956-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="7c956-169">In **PeekLock** , la modalità di ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="7c956-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7c956-170">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c956-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="7c956-171">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando **eliminare** nel messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="7c956-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="7c956-172">Quando il Bus di servizio rileva hello **eliminare** chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dall'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="7c956-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="7c956-173">Hello esempio riportato di seguito viene illustrato come è possibile ricevere messaggi e trasformati utilizzando **PeekLock** modalità (non hello predefinita).</span><span class="sxs-lookup"><span data-stu-id="7c956-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="7c956-174">Hello esempio riportato di seguito esegue un ciclo ed elabora i messaggi di hello "HighMessages" sottoscrizione e quindi viene chiuso quando non sono presenti ulteriori messaggi (in alternativa, Impossibile impostare toowait per i nuovi messaggi).</span><span class="sxs-lookup"><span data-stu-id="7c956-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7c956-175">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="7c956-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="7c956-176">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="7c956-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7c956-177">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **unlockMessage** metodo sul messaggio ricevuto (anziché hello **deleteMessage** (metodo)).</span><span class="sxs-lookup"><span data-stu-id="7c956-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="7c956-178">Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di argomento hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="7c956-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7c956-179">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno dell'argomento, e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima il timeout di blocco scade (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="7c956-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="7c956-180">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **deleteMessage** richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="7c956-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="7c956-181">Spesso si tratta di **almeno una volta elaborazione**, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="7c956-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="7c956-182">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="7c956-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="7c956-183">Questa operazione viene spesso eseguita utilizzando hello **getMessageId** metodo di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="7c956-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7c956-184">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="7c956-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="7c956-185">Hello argomenti toodelete modo primario e le sottoscrizioni è toouse un **ServiceBusContract** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7c956-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="7c956-186">L'eliminazione di un argomento eliminerà anche le sottoscrizioni che sono registrate con l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="7c956-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="7c956-187">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="7c956-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="7c956-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c956-188">Next Steps</span></span>
<span data-ttu-id="7c956-189">Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code del Bus di servizio, argomenti e sottoscrizioni] [ Service Bus queues, topics, and subscriptions] per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="7c956-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
