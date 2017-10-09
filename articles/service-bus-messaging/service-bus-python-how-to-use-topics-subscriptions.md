---
title: gli argomenti del Bus di servizio di Azure toouse aaaHow con Python | Documenti Microsoft
description: Informazioni su come toouse Azure Service Bus argomenti e sottoscrizioni da Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="2d896-103">Il Bus di servizio toouse argomenti e sottoscrizioni con Python</span><span class="sxs-lookup"><span data-stu-id="2d896-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="2d896-104">Questo articolo viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="2d896-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="2d896-105">esempi di Hello sono scritti in Python e utilizzare hello [pacchetto Python di Azure SDK][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="2d896-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="2d896-106">Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="2d896-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="2d896-107">Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="2d896-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="2d896-108">Se è necessario tooinstall Python o hello [pacchetto Python Azure][Azure Python package], vedere hello [Guida all'installazione di Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="2d896-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="2d896-109">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="2d896-109">Create a topic</span></span>
<span data-ttu-id="2d896-110">Hello **ServiceBusService** consente toowork con argomenti.</span><span class="sxs-lookup"><span data-stu-id="2d896-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="2d896-111">Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera accedere tooprogrammatically Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="2d896-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="2d896-112">Hello codice seguente viene creata una **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="2d896-113">Sostituire `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` con lo spazio dei nomi effettivo e il nome e il valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="2d896-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="2d896-114">È possibile ottenere i valori hello per nome della chiave SAS hello e il valore da hello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="2d896-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="2d896-115">Hello `create_topic` metodo supporta inoltre opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio dimensioni argomento toolive o massimo in fase di messaggio.</span><span class="sxs-lookup"><span data-stu-id="2d896-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="2d896-116">Hello esempio seguente imposta hello massima dell'argomento dimensioni too5 GB e un valore di (durata TTL) toolive ora di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="2d896-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="2d896-117">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="2d896-117">Create subscriptions</span></span>
<span data-ttu-id="2d896-118">Tootopics le sottoscrizioni vengono creati anche con hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="2d896-119">Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2d896-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="2d896-120">Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello toowhich argomento sono state sottoscritte, vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="2d896-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="2d896-121">Creare una sottoscrizione con filtro predefinito (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="2d896-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="2d896-122">Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2d896-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="2d896-123">Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="2d896-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="2d896-124">esempio Hello crea una sottoscrizione denominata `AllMessages` e utilizza hello predefinito **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="2d896-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="2d896-125">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="2d896-125">Create subscriptions with filters</span></span>
<span data-ttu-id="2d896-126">È inoltre possibile definire filtri che consentono di toospecify cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="2d896-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="2d896-127">Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è un **SqlFilter**, che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="2d896-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="2d896-128">I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato.</span><span class="sxs-lookup"><span data-stu-id="2d896-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="2d896-129">Per ulteriori informazioni sulle espressioni hello che può essere utilizzato con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.</span><span class="sxs-lookup"><span data-stu-id="2d896-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="2d896-130">È possibile aggiungere filtri tooa sottoscrizione utilizzando hello **creare\_regola** metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="2d896-131">Questo metodo consente tooadd nuovi filtri tooan sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2d896-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2d896-132">Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è necessario innanzitutto rimuovere filtro predefinito hello o hello **MatchAll** sostituirà gli altri filtri che è possibile specificare.</span><span class="sxs-lookup"><span data-stu-id="2d896-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="2d896-133">È possibile rimuovere una regola predefinita hello utilizzando hello `delete_rule` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="2d896-134">esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `messagenumber` maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="2d896-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="2d896-135">Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un **SqlFilter** che seleziona solo i messaggi che hanno un `messagenumber` proprietà minore o uguale too3:</span><span class="sxs-lookup"><span data-stu-id="2d896-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="2d896-136">A questo punto, quando viene inviato un messaggio troppo`mytopic` viene sempre recapitato tooreceivers sottoscritto toohello **AllMessages** sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello **HighMessages**  e **LowMessages** le sottoscrizioni dell'argomento (a seconda di contenuto del messaggio hello).</span><span class="sxs-lookup"><span data-stu-id="2d896-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="2d896-137">Inviare l'argomento tooa messaggi</span><span class="sxs-lookup"><span data-stu-id="2d896-137">Send messages tooa topic</span></span>
<span data-ttu-id="2d896-138">un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare hello `send_topic_message` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="2d896-139">Hello esempio seguente viene illustrato come test toosend cinque messaggi troppo`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="2d896-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="2d896-140">Si noti che hello `messagenumber` valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (ciò determina le sottoscrizioni che ricevano):</span><span class="sxs-lookup"><span data-stu-id="2d896-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="2d896-141">Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="2d896-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="2d896-142">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="2d896-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="2d896-143">Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento.</span><span class="sxs-lookup"><span data-stu-id="2d896-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="2d896-144">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="2d896-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="2d896-145">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="2d896-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="2d896-146">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="2d896-146">Receive messages from a subscription</span></span>
<span data-ttu-id="2d896-147">I messaggi vengono ricevuti da una sottoscrizione utilizzando hello `receive_subscription_message` metodo hello **ServiceBusService** oggetto:</span><span class="sxs-lookup"><span data-stu-id="2d896-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="2d896-148">I messaggi vengono eliminati dalla sottoscrizione hello quando vengono letti quando hello parametro `peek_lock` è troppo**False**.</span><span class="sxs-lookup"><span data-stu-id="2d896-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="2d896-149">È possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dall'impostazione parametro hello `peek_lock` troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="2d896-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="2d896-150">Hello comportamento di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="2d896-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="2d896-151">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2d896-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="2d896-152">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2d896-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="2d896-153">Se hello `peek_lock` parametro è impostato troppo**True**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="2d896-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="2d896-154">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d896-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="2d896-155">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `delete` metodo hello **messaggio** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="2d896-156">Hello `delete` metodo contrassegna il messaggio hello come usato e la rimuove dalla sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="2d896-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="2d896-157">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="2d896-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="2d896-158">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="2d896-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="2d896-159">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlock` metodo hello **messaggio** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2d896-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="2d896-160">Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di sottoscrizione hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="2d896-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="2d896-161">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di sottoscrizione hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e lo rende disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="2d896-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="2d896-162">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `delete` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia.</span><span class="sxs-lookup"><span data-stu-id="2d896-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="2d896-163">Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="2d896-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="2d896-164">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="2d896-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="2d896-165">Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="2d896-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="2d896-166">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="2d896-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="2d896-167">Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="2d896-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="2d896-168">Hello riportato di seguito come argomento di hello toodelete denominati `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="2d896-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="2d896-169">L'eliminazione di un argomento elimina anche le sottoscrizioni che sono registrate con l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="2d896-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="2d896-170">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="2d896-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="2d896-171">Hello codice seguente viene illustrato come toodelete una sottoscrizione denominata `HighMessages` da hello `mytopic` argomento:</span><span class="sxs-lookup"><span data-stu-id="2d896-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="2d896-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d896-172">Next steps</span></span>
<span data-ttu-id="2d896-173">Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="2d896-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="2d896-174">Vedere [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="2d896-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="2d896-175">Informazioni di riferimento per [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="2d896-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
