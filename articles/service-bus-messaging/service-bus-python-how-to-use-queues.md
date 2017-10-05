---
title: Come usare le code del bus di servizio di Azure con Python | Microsoft Docs
description: Informazioni su come usare le code del bus di servizio da Python.
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
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="50490-103">Come usare le code del bus di servizio con Python</span><span class="sxs-lookup"><span data-stu-id="50490-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="50490-104">Questo articolo illustra come usare le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="50490-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="50490-105">Gli esempi sono scritti in Python e usano il [pacchetto del bus di servizio di Azure per Python][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="50490-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="50490-106">Gli scenari illustrati includono la **creazione di code, l'invio e la ricezione di messaggi** e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="50490-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="50490-107">Per installare Python oppure il [pacchetto del bus di servizio di Azure per Python][Python Azure Service Bus package], vedere la [guida all'installazione di Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="50490-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="50490-108">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="50490-108">Create a queue</span></span>
<span data-ttu-id="50490-109">L'oggetto **ServiceBusService** consente di usare le code.</span><span class="sxs-lookup"><span data-stu-id="50490-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="50490-110">Aggiungere il seguente codice all'inizio di ogni file Python da cui si desidera accedere al bus di servizio a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="50490-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="50490-111">Il codice seguente consente di creare un oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="50490-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="50490-112">Sostituire, `mynamespace`, `sharedaccesskeyname` e `sharedaccesskey` con lo spazio dei nomi e il nome e il valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="50490-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="50490-113">I valori relativi al nome e al valore della chiave di firma di accesso condiviso sono disponibili nelle informazioni di connessione del [portale di Azure][Azure portal] o nel pannello **Proprietà** di Visual Studio quando si seleziona lo spazio dei nomi del bus di servizio in Esplora server, come illustrato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="50490-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="50490-114">Il metodo `create_queue` supporta anche opzioni aggiuntive che consentono di eseguire l'override delle impostazioni predefinite delle code, come ad esempio la durata (TTL) dei messaggi o la dimensione massima della coda.</span><span class="sxs-lookup"><span data-stu-id="50490-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="50490-115">L'esempio seguente illustra come impostare la dimensione massima della coda su 5 GB e il valore TTL su 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="50490-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="50490-116">Inviare messaggi a una coda</span><span class="sxs-lookup"><span data-stu-id="50490-116">Send messages to a queue</span></span>
<span data-ttu-id="50490-117">Per inviare un messaggio a una coda del bus di servizio, l'applicazione chiama il metodo `send_queue_message` per l'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="50490-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="50490-118">L'esempio seguente illustra come inviare un messaggio di prova alla coda denominata `taskqueue` usando `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="50490-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="50490-119">Le code del bus di servizio supportano messaggi di dimensioni fino a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e fino a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="50490-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="50490-120">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="50490-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="50490-121">Non esiste alcun limite al numero di messaggi mantenuti in una coda, mentre è prevista una limitazione alla dimensione totale dei messaggi di una coda.</span><span class="sxs-lookup"><span data-stu-id="50490-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="50490-122">Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="50490-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="50490-123">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="50490-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="50490-124">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="50490-124">Receive messages from a queue</span></span>
<span data-ttu-id="50490-125">I messaggi vengono ricevuti da una coda tramite il metodo `receive_queue_message` per l'oggetto **ServiceBusService**:</span><span class="sxs-lookup"><span data-stu-id="50490-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="50490-126">I messaggi vengono eliminati dalla coda non appena vengono letti, quando il parametro `peek_lock` è impostato su **False**.</span><span class="sxs-lookup"><span data-stu-id="50490-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="50490-127">È possibile leggere e bloccare il messaggio senza eliminarlo dalla coda impostando il parametro `peek_lock` su **True**.</span><span class="sxs-lookup"><span data-stu-id="50490-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="50490-128">Il comportamento di lettura ed eliminazione del messaggio nell'ambito dell'operazione di ricezione costituisce il modello più semplice ed è adatto per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="50490-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="50490-129">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="50490-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="50490-130">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="50490-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="50490-131">Se il parametro `peek_lock` è impostato su **True**, l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="50490-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="50490-132">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50490-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="50490-133">Dopo aver elaborato il messaggio, o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione esegue la seconda fase del processo di ricezione chiamando il metodo **delete** per l'oggetto **Message**.</span><span class="sxs-lookup"><span data-stu-id="50490-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="50490-134">Il metodo **delete** contrassegna il messaggio come usato e lo rimuove dalla coda.</span><span class="sxs-lookup"><span data-stu-id="50490-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="50490-135">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="50490-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="50490-136">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="50490-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="50490-137">Se un'applicazione ricevitore non è in grado di elaborare il messaggio per un qualsiasi motivo, può chiamare il metodo **unlock** per l'oggetto **Message**.</span><span class="sxs-lookup"><span data-stu-id="50490-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="50490-138">In questo modo, il bus di servizio sbloccherà il messaggio nella coda rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="50490-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="50490-139">Al messaggio bloccato nella coda è inoltre associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="50490-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="50490-140">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio ma prima della chiamata del metodo **delete**, il messaggio verrà nuovamente recapitato all'applicazione al riavvio.</span><span class="sxs-lookup"><span data-stu-id="50490-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="50490-141">Questo processo di elaborazione viene spesso definito di tipo **At-Least-Once**, per indicare che ogni messaggio verrà elaborato almeno una volta ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="50490-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="50490-142">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva all'applicazione per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="50490-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="50490-143">A tale scopo viene spesso usata la proprietà **MessageId** del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="50490-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50490-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50490-144">Next steps</span></span>
<span data-ttu-id="50490-145">Dopo aver appreso le nozioni di base sulle code del bus di servizio, vedere gli articoli seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="50490-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="50490-146">[Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="50490-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

