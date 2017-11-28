---
title: gli argomenti del Bus di servizio toouse aaaHow (Ruby) | Documenti Microsoft
description: Informazioni su come toouse Bus di servizio di argomenti e sottoscrizioni in Azure. Gli esempi di codice sono scritti per applicazioni Ruby.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="b369a-104">Il Bus di servizio toouse argomenti e sottoscrizioni con Ruby</span><span class="sxs-lookup"><span data-stu-id="b369a-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="b369a-105">Questo articolo viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni dalle applicazioni Ruby.</span><span class="sxs-lookup"><span data-stu-id="b369a-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="b369a-106">Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni, la creazione di filtri di sottoscrizione, l'invio di messaggi** argomento tooa **la ricezione di messaggi da una sottoscrizione**, e  **l'eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="b369a-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="b369a-107">Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="b369a-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="b369a-108">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="b369a-108">Create a topic</span></span>
<span data-ttu-id="b369a-109">Hello **Azure::ServiceBusService** consente toowork con argomenti.</span><span class="sxs-lookup"><span data-stu-id="b369a-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="b369a-110">Hello codice seguente viene creato un **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-111">un argomento, toocreate utilizzare hello `create_topic()` metodo.</span><span class="sxs-lookup"><span data-stu-id="b369a-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="b369a-112">Hello di esempio seguente crea un argomento o stampa se sono presenti errori di hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="b369a-113">È inoltre possibile passare un **Azure::ServiceBus::Topic** oggetto con opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio dimensioni toolive o massimo in una coda in fase di messaggio.</span><span class="sxs-lookup"><span data-stu-id="b369a-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="b369a-114">Hello esempio seguente viene illustrata l'impostazione massima della coda hello dimensioni too5 GB e l'ora too1 toolive minuto:</span><span class="sxs-lookup"><span data-stu-id="b369a-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="b369a-115">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="b369a-115">Create subscriptions</span></span>
<span data-ttu-id="b369a-116">Le sottoscrizioni dell'argomento vengono inoltre create con hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-117">Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b369a-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="b369a-118">Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello argomento sono associati, vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="b369a-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="b369a-119">Se l'applicazione contiene la logica toocreate una sottoscrizione, deve verificare se hello sottoscrizione esiste già con metodo getSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="b369a-120">Creare una sottoscrizione con filtro predefinito (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="b369a-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="b369a-121">Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b369a-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="b369a-122">Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="b369a-123">esempio Hello crea una sottoscrizione denominata "tutti i messaggi" e utilizza hello predefinito **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="b369a-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="b369a-124">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="b369a-124">Create subscriptions with filters</span></span>
<span data-ttu-id="b369a-125">È inoltre possibile definire filtri che consentono di toospecify cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione specifica.</span><span class="sxs-lookup"><span data-stu-id="b369a-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="b369a-126">tipo di filtro supportato dalle sottoscrizioni più flessibile Hello è hello **Azure::ServiceBus::SqlFilter**, che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="b369a-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="b369a-127">I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato.</span><span class="sxs-lookup"><span data-stu-id="b369a-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="b369a-128">Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter](service-bus-messaging-sql-filter.md) sintassi.</span><span class="sxs-lookup"><span data-stu-id="b369a-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="b369a-129">È possibile aggiungere filtri tooa sottoscrizione utilizzando hello `create_rule()` metodo hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-130">Questo metodo consente tooadd nuovi filtri tooan sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b369a-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="b369a-131">Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è innanzitutto necessario rimuovere filtro predefinito hello o hello **MatchAll** sostituirà gli altri filtri che è possibile specificare.</span><span class="sxs-lookup"><span data-stu-id="b369a-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="b369a-132">È possibile rimuovere una regola predefinita hello utilizzando hello `delete_rule()` metodo hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="b369a-133">esempio Hello crea una sottoscrizione denominata "alta messaggi" con un **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `message_number` maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="b369a-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="b369a-134">Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `low-messages` con un **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi che hanno un `message_number` proprietà minore o uguale too3:</span><span class="sxs-lookup"><span data-stu-id="b369a-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="b369a-135">Quando viene inviato un messaggio ora troppo`test-topic`, è sempre essere recapitato tooreceivers sottoscritto toohello `all-messages` sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello `high-messages` e `low-messages` (sottoscrizioni di argomento in base al contenuto del messaggio hello).</span><span class="sxs-lookup"><span data-stu-id="b369a-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="b369a-136">Inviare l'argomento tooa messaggi</span><span class="sxs-lookup"><span data-stu-id="b369a-136">Send messages tooa topic</span></span>
<span data-ttu-id="b369a-137">un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare hello `send_topic_message()` metodo hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-138">I messaggi inviati gli argomenti del Bus tooService sono istanze di hello **Azure::ServiceBus::BrokeredMessage** oggetti.</span><span class="sxs-lookup"><span data-stu-id="b369a-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="b369a-139">**Azure::ServiceBus::BrokeredMessage** oggetti dispongono di un set di proprietà standard (ad esempio `label` e `time_to_live`), un dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="b369a-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="b369a-140">Un'applicazione può impostare il corpo di hello del messaggio hello passando un toohello valore stringa `send_topic_message()` necessari (metodo) e le proprietà standard verranno popolate dai valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b369a-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="b369a-141">Hello esempio seguente viene illustrato come test toosend cinque messaggi troppo`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="b369a-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="b369a-142">Si noti che hello `message_number` valore della proprietà personalizzata di ogni messaggio varia iterazione hello del ciclo di hello (ciò determina la sottoscrizione riceve):</span><span class="sxs-lookup"><span data-stu-id="b369a-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="b369a-143">Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="b369a-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="b369a-144">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="b369a-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="b369a-145">Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento.</span><span class="sxs-lookup"><span data-stu-id="b369a-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="b369a-146">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="b369a-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="b369a-147">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="b369a-147">Receive messages from a subscription</span></span>
<span data-ttu-id="b369a-148">I messaggi vengono ricevuti da una sottoscrizione utilizzando hello `receive_subscription_message()` metodo hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-149">Per impostazione predefinita, i messaggi sono read(peak) e bloccato senza eliminarla dalla sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="b369a-150">È possibile leggere ed eliminare il messaggio hello dalla sottoscrizione hello dall'impostazione hello `peek_lock` opzione troppo**false**.</span><span class="sxs-lookup"><span data-stu-id="b369a-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="b369a-151">comportamento predefinito di Hello rende hello durante la lettura e l'eliminazione di un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="b369a-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b369a-152">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="b369a-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="b369a-153">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `delete_subscription_message()` (metodo) e fornendo toobe messaggio hello eliminato come parametro.</span><span class="sxs-lookup"><span data-stu-id="b369a-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="b369a-154">Hello `delete_subscription_message()` metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="b369a-155">Se hello `:peek_lock` parametro è impostato troppo**false**, durante la lettura e l'eliminazione del messaggio hello diventa modello più semplice hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="b369a-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="b369a-156">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b369a-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="b369a-157">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b369a-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="b369a-158">Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="b369a-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="b369a-159">esempio Hello innanzitutto riceve ed elimina un messaggio da hello `low-messages` sottoscrizione utilizzando `:peek_lock` impostare troppo**false**, quindi riceve un altro messaggio da hello `high-messages` e quindi Elimina hello messaggio utilizzando `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="b369a-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="b369a-160">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="b369a-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="b369a-161">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="b369a-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="b369a-162">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlock_subscription_message()` metodo hello **Azure::ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b369a-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="b369a-163">Questa condizione provoca hello toounlock Bus di servizio all'interno di sottoscrizione hello del messaggio e renderlo disponibile toobe nuovamente ricevuto sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="b369a-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="b369a-164">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di sottoscrizione hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="b369a-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="b369a-165">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `delete_subscription_message()` metodo viene chiamato, il messaggio hello è applicazione toohello consegnati nuovamente quando viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="b369a-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="b369a-166">Spesso si tratta di *almeno una volta elaborazione*; ovvero, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="b369a-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="b369a-167">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="b369a-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="b369a-168">Questa logica viene spesso ottenuta utilizzando hello `message_id` proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="b369a-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="b369a-169">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="b369a-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="b369a-170">Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="b369a-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="b369a-171">Hello riportato di seguito come argomento di hello toodelete denominati `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="b369a-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="b369a-172">L'eliminazione di un argomento elimina anche le sottoscrizioni che sono registrate con l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="b369a-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="b369a-173">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="b369a-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="b369a-174">Hello codice seguente viene illustrato come sottoscrizione hello toodelete denominati `high-messages` da hello `test-topic` argomento:</span><span class="sxs-lookup"><span data-stu-id="b369a-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="b369a-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b369a-175">Next steps</span></span>
<span data-ttu-id="b369a-176">Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="b369a-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="b369a-177">Vedere [Code, argomenti e sottoscrizioni](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="b369a-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="b369a-178">Materiale di riferimento dell'API per [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="b369a-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="b369a-179">Visitare hello [Azure SDK per Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b369a-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
