---
title: Come usare gli argomenti del bus di servizio (Ruby) | Microsoft Docs
description: Informazioni su come usare le sottoscrizioni e gli argomenti del bus di servizio in Azure. Gli esempi di codice sono scritti per applicazioni Ruby.
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
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="ca70d-104">Come usare gli argomenti e le sottoscrizioni del bus di servizio con Ruby</span><span class="sxs-lookup"><span data-stu-id="ca70d-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ca70d-105">Questo articolo descrive come usare gli argomenti e le sottoscrizioni del bus di servizio da applicazioni Ruby.</span><span class="sxs-lookup"><span data-stu-id="ca70d-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="ca70d-106">Gli scenari illustrati includono **creazione di argomenti e sottoscrizioni, creazione di filtri per le sottoscrizioni, invio di messaggi** a un argomento, **ricezione di messaggi da una sottoscrizione** ed **eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="ca70d-107">Per altre informazioni sugli argomenti e sulle sottoscrizioni, vedere la sezione [Passaggi successivi](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="ca70d-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="ca70d-108">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="ca70d-108">Create a topic</span></span>
<span data-ttu-id="ca70d-109">L'oggetto **Azure::ServiceBusService** consente di usare argomenti.</span><span class="sxs-lookup"><span data-stu-id="ca70d-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="ca70d-110">Il codice seguente crea un oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-111">Per creare un argomento, usare il metodo `create_topic()`.</span><span class="sxs-lookup"><span data-stu-id="ca70d-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="ca70d-112">L'esempio seguente crea un argomento o visualizza gli eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="ca70d-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="ca70d-113">È anche possibile passare un oggetto **Azure::ServiceBus::Topic** con opzioni aggiuntive, che consente di eseguire l'override delle impostazioni degli argomenti predefinite, ad esempio la durata dei messaggi o la dimensione massima della coda.</span><span class="sxs-lookup"><span data-stu-id="ca70d-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="ca70d-114">L'esempio seguente illustra come impostare la dimensione massima della coda su 5 GB e una durata di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="ca70d-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="ca70d-115">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="ca70d-115">Create subscriptions</span></span>
<span data-ttu-id="ca70d-116">Le sottoscrizioni di un argomento vengono create anche con l'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-117">Le sottoscrizioni sono denominate e possono includere un filtro facoltativo che limita il set di messaggi recapitati alla coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="ca70d-118">Le sottoscrizioni sono persistenti e continueranno a esistere fintanto che esse, o l'argomento a cui sono associate, non vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="ca70d-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="ca70d-119">Se l'applicazione contiene la logica per la creazione di una sottoscrizione, è innanzitutto necessario verificare se la sottoscrizione esiste già usando il metodo getSubscription.</span><span class="sxs-lookup"><span data-stu-id="ca70d-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="ca70d-120">Creare una sottoscrizione con il filtro (MatchAll) predefinito</span><span class="sxs-lookup"><span data-stu-id="ca70d-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="ca70d-121">Il filtro **MatchAll** è il filtro predefinito e viene usato se non vengono specificati altri filtri durante la creazione di una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ca70d-122">Quando si usa il filtro **MatchAll**, tutti i messaggi pubblicati nell'argomento vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="ca70d-123">Nell'esempio seguente viene creata una sottoscrizione denominata "all-messages" e viene usato il filtro predefinito **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ca70d-124">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="ca70d-124">Create subscriptions with filters</span></span>
<span data-ttu-id="ca70d-125">È anche possibile definire i filtri che consentono di specificare quali messaggi inviati a un argomento devono essere presenti in una specifica sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="ca70d-126">Il tipo di filtro più flessibile tra quelli supportati dalle sottoscrizioni è **Azure::ServiceBus::SqlFilter**, che implementa un sottoinsieme di SQL92.</span><span class="sxs-lookup"><span data-stu-id="ca70d-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="ca70d-127">I filtri SQL agiscono sulle proprietà dei messaggi pubblicati nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="ca70d-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="ca70d-128">Per altri dettagli sulle espressioni che è possibile usare con un filtro SQL, esaminare la sintassi di [SqlFilter](service-bus-messaging-sql-filter.md).</span><span class="sxs-lookup"><span data-stu-id="ca70d-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="ca70d-129">È possibile aggiungere filtri a una sottoscrizione usando il metodo `create_rule()` dell'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-130">Questo metodo consente di aggiungere nuovi filtri a una sottoscrizione esistente.</span><span class="sxs-lookup"><span data-stu-id="ca70d-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="ca70d-131">Poiché il filtro predefinito viene applicato automaticamente a tutte le nuove sottoscrizioni, è necessario prima rimuovere il filtro predefinito, altrimenti **MatchAll** eseguirà l'override di qualsiasi altro filtro specificato.</span><span class="sxs-lookup"><span data-stu-id="ca70d-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="ca70d-132">È possibile rimuovere la regola predefinita tramite il metodo `delete_rule()` nell'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="ca70d-133">Nell'esempio seguente viene creata una sottoscrizione denominata "high-messages" con **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi in cui il valore della proprietà personalizzata `message_number` è maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="ca70d-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="ca70d-134">Analogamente, l'esempio seguente crea una sottoscrizione denominata `low-messages` con un filtro **Azure::ServiceBus::SqlFilter** che seleziona solo i messaggi in cui il valore della proprietà `message_number` è minore o uguale a 3:</span><span class="sxs-lookup"><span data-stu-id="ca70d-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

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

<span data-ttu-id="ca70d-135">Un messaggio inviato a `test-topic` viene sempre recapitato ai ricevitori con sottoscrizione all'argomento `all-messages` e recapitato selettivamente ai ricevitori con sottoscrizioni agli argomenti `high-messages` e `low-messages` (a seconda del contenuto del messaggio).</span><span class="sxs-lookup"><span data-stu-id="ca70d-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="ca70d-136">Inviare messaggi a un argomento</span><span class="sxs-lookup"><span data-stu-id="ca70d-136">Send messages to a topic</span></span>
<span data-ttu-id="ca70d-137">Per inviare un messaggio a un argomento del bus di servizio, l'applicazione deve usare il metodo `send_topic_message()` nell'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-138">I messaggi inviati ad argomenti del bus di servizio sono istanze degli oggetti **Azure::ServiceBus::BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="ca70d-139">Gli oggetti **Azure::ServiceBus::BrokeredMessage** includono un insieme di proprietà standard, ad esempio `label` e `time_to_live`, un dizionario usato per mantenere le proprietà personalizzate specifiche dell'applicazione e un corpo di dati di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="ca70d-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="ca70d-140">Un'applicazione può impostare il corpo del messaggio passando un valore stringa al metodo `send_topic_message()` in modo da popolare le proprietà standard necessarie con valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="ca70d-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="ca70d-141">Il seguente esempio illustra come inviare cinque messaggi di test a `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ca70d-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="ca70d-142">Si noti come il valore della proprietà personalizzata `message_number` di ogni messaggio varia nell'iterazione del ciclo, determinando la sottoscrizione che lo riceverà:</span><span class="sxs-lookup"><span data-stu-id="ca70d-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="ca70d-143">Gli argomenti del bus di servizio supportano messaggi di dimensioni massime fino a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e fino a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ca70d-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ca70d-144">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ca70d-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ca70d-145">Non esiste alcun limite al numero di messaggi mantenuti in un argomento, mentre è prevista una limitazione alla dimensione totale dei messaggi di un argomento.</span><span class="sxs-lookup"><span data-stu-id="ca70d-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="ca70d-146">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ca70d-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ca70d-147">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ca70d-147">Receive messages from a subscription</span></span>
<span data-ttu-id="ca70d-148">I messaggi vengono ricevuti da una sottoscrizione tramite il metodo `receive_subscription_message()` per l'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-149">Per impostazione predefinita, i messaggi vengono letti (picco) e bloccati senza essere eliminati dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="ca70d-150">È possibile leggere ed eliminare il messaggio dalla sottoscrizione, impostando l'opzione `peek_lock` su **false**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="ca70d-151">In base al comportamento predefinito, la lettura e l'eliminazione vengono incluse in un'operazione di ricezione suddivisa in due fasi, in modo da consentire anche il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="ca70d-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ca70d-152">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="ca70d-153">Dopo aver elaborato il messaggio o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione esegue la seconda fase del processo di ricezione chiamando il metodo `delete_subscription_message()` e specificando il messaggio da eliminare come parametro.</span><span class="sxs-lookup"><span data-stu-id="ca70d-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="ca70d-154">Il metodo `delete_subscription_message()` contrassegna il messaggio come usato e lo rimuove dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="ca70d-155">Se il parametro `:peek_lock` è impostato su **false**, la lettura e l'eliminazione del messaggio costituiscono il modello più semplice, adatto a scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="ca70d-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="ca70d-156">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="ca70d-157">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="ca70d-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="ca70d-158">L'esempio seguente illustra come ricevere ed elaborare messaggi tramite `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="ca70d-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="ca70d-159">Nell'esempio viene prima ricevuto ed eliminato un messaggio dalla sottoscrizione `low-messages` tramite `:peek_lock` impostato su **false** e successivamente viene ricevuto da `high-messages` e poi eliminato un altro messaggio tramite `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="ca70d-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ca70d-160">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ca70d-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ca70d-161">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca70d-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ca70d-162">Se un'applicazione del ricevitore non è in grado di elaborare il messaggio per un qualsiasi motivo, può chiamare il metodo `unlock_subscription_message()` sull'oggetto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="ca70d-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ca70d-163">In questo modo, il bus di servizio sblocca il messaggio nella sottoscrizione rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="ca70d-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ca70d-164">Al messaggio bloccato nella sottoscrizione è anche associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="ca70d-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="ca70d-165">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio ma prima della chiamata del metodo `delete_subscription_message()`, il messaggio viene nuovamente recapitato all'applicazione al riavvio.</span><span class="sxs-lookup"><span data-stu-id="ca70d-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="ca70d-166">Questo processo di elaborazione viene spesso definito *At-Least-Once* per indicare che ogni messaggio verrà elaborato almeno una volta, ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="ca70d-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="ca70d-167">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva all'applicazione per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca70d-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="ca70d-168">A tale scopo viene spesso usata la proprietà `message_id` del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="ca70d-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ca70d-169">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="ca70d-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="ca70d-170">Gli argomenti e le sottoscrizioni sono persistenti e devono essere eliminati in modo esplicito nel [portale di Azure][Azure portal] oppure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="ca70d-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="ca70d-171">Il seguente esempio illustra come eliminare l'argomento denominato `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ca70d-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="ca70d-172">Se si elimina un argomento, vengono eliminate anche tutte le sottoscrizioni registrate con l'argomento.</span><span class="sxs-lookup"><span data-stu-id="ca70d-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="ca70d-173">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="ca70d-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="ca70d-174">Il codice seguente dimostra come eliminare la sottoscrizione denominata `high-messages` dall'argomento `test-topic`:</span><span class="sxs-lookup"><span data-stu-id="ca70d-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="ca70d-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca70d-175">Next steps</span></span>
<span data-ttu-id="ca70d-176">A questo punto, dopo aver appreso le nozioni di base degli argomenti del bus di servizio, usare i seguenti collegamenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="ca70d-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="ca70d-177">Vedere [Code, argomenti e sottoscrizioni](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="ca70d-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="ca70d-178">Materiale di riferimento dell'API per [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="ca70d-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="ca70d-179">Vedere il repository [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca70d-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
