---
title: Accoda aaaHow toouse Azure Service Bus con Python | Documenti Microsoft
description: Informazioni su come code di toouse Azure Service Bus da Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="25294-103">La modalità di code toouse Bus di servizio con Python</span><span class="sxs-lookup"><span data-stu-id="25294-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="25294-104">Questo articolo viene descritto come toouse code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="25294-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="25294-105">esempi di Hello sono scritti in Python e utilizzare hello [pacchetto Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="25294-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="25294-106">Hello scenari trattati includono **la creazione delle code, inviando e ricevendo messaggi**, e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="25294-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="25294-107">tooinstall Python o hello [pacchetto Python Azure Service Bus][Python Azure Service Bus package], vedere hello [Guida all'installazione di Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="25294-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="25294-108">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="25294-108">Create a queue</span></span>
<span data-ttu-id="25294-109">Hello **ServiceBusService** consente toowork con le code.</span><span class="sxs-lookup"><span data-stu-id="25294-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="25294-110">Aggiungere hello codice superiore hello di qualsiasi file Python in cui si desidera accedere tooprogrammatically Bus di servizio seguente:</span><span class="sxs-lookup"><span data-stu-id="25294-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="25294-111">Hello codice seguente viene creata una **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="25294-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="25294-112">Sostituire, `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` con lo spazio dei nomi e il nome e il valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="25294-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="25294-113">Hello valori per nome hello SAS e il valore sono reperibile in hello [portale di Azure] [ Azure portal] informazioni di connessione, o in Visual Studio hello **proprietà** riquadro durante la selezione Hello dello spazio dei nomi Service Bus in Esplora Server (come illustrato nella sezione precedente hello).</span><span class="sxs-lookup"><span data-stu-id="25294-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="25294-114">Hello `create_queue` metodo supporta inoltre opzioni aggiuntive, che consentono di impostazioni di coda toooverride predefinite, ad esempio messaggio toolive TTL (time) o dimensione massima della coda.</span><span class="sxs-lookup"><span data-stu-id="25294-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="25294-115">Hello esempio seguente imposta GB too5 dimensioni massime della coda di hello e minuto too1 valore TTL di hello:</span><span class="sxs-lookup"><span data-stu-id="25294-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="25294-116">Messaggi tooa coda di invio</span><span class="sxs-lookup"><span data-stu-id="25294-116">Send messages tooa queue</span></span>
<span data-ttu-id="25294-117">una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `send_queue_message` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="25294-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="25294-118">Hello esempio seguente viene illustrato come toosend una coda toohello test denominati `taskqueue` utilizzando `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="25294-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="25294-119">Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="25294-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="25294-120">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="25294-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="25294-121">Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda.</span><span class="sxs-lookup"><span data-stu-id="25294-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="25294-122">Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="25294-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="25294-123">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="25294-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="25294-124">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="25294-124">Receive messages from a queue</span></span>
<span data-ttu-id="25294-125">I messaggi vengono ricevuti da una coda utilizzando hello `receive_queue_message` metodo hello **ServiceBusService** oggetto:</span><span class="sxs-lookup"><span data-stu-id="25294-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="25294-126">I messaggi vengono eliminati dalla coda di hello quando vengono letti quando hello parametro `peek_lock` è troppo**False**.</span><span class="sxs-lookup"><span data-stu-id="25294-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="25294-127">È possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dall'impostazione parametro hello `peek_lock` troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="25294-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="25294-128">Hello comportamento di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="25294-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="25294-129">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="25294-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="25294-130">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="25294-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="25294-131">Se hello `peek_lock` parametro è impostato troppo**True**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="25294-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="25294-132">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="25294-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="25294-133">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione dal chiamante hello **eliminare** metodo hello **messaggio** oggetto.</span><span class="sxs-lookup"><span data-stu-id="25294-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="25294-134">Hello **eliminare** metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="25294-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="25294-135">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="25294-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="25294-136">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="25294-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="25294-137">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello **sbloccare** metodo hello **messaggio** oggetto.</span><span class="sxs-lookup"><span data-stu-id="25294-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="25294-138">Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="25294-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="25294-139">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se hello ha esito negativo dell'applicazione hello tooprocess hello messaggio prima della scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="25294-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="25294-140">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello **eliminare** metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia.</span><span class="sxs-lookup"><span data-stu-id="25294-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="25294-141">Spesso si tratta di **almeno una volta elaborazione**, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="25294-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="25294-142">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="25294-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="25294-143">Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="25294-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25294-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25294-144">Next steps</span></span>
<span data-ttu-id="25294-145">Ora che si è appreso i concetti di base di hello di code del Bus di servizio, vedere questi toolearn articoli più.</span><span class="sxs-lookup"><span data-stu-id="25294-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="25294-146">[Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="25294-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

