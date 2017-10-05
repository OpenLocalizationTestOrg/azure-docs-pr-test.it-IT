---
title: Come usare l'archiviazione code da Python | Microsoft Docs
description: Informazioni su come usare il servizio di accodamento di Azure da Python per creare ed eliminare code e per inserire, visualizzare ed eliminare messaggi.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 1ad3ba6853edda93034b84996823262cb017c71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="a4f14-103">Come usare l'archiviazione di accodamento da Python</span><span class="sxs-lookup"><span data-stu-id="a4f14-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="a4f14-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4f14-104">Overview</span></span>
<span data-ttu-id="a4f14-105">In questa guida viene illustrato come eseguire scenari comuni del servizio di archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f14-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="a4f14-106">Gli esempi sono scritti in Python e usano [Microsoft Azure Storage SDK per Python].</span><span class="sxs-lookup"><span data-stu-id="a4f14-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="a4f14-107">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre alla **creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="a4f14-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="a4f14-108">Per altre informazioni sulle code, fare riferimento alla sezione [Passaggi successivi].</span><span class="sxs-lookup"><span data-stu-id="a4f14-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="a4f14-109">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="a4f14-109">How To: Create a Queue</span></span>
<span data-ttu-id="a4f14-110">L'oggetto **QueueService** consente di utilizzare le code.</span><span class="sxs-lookup"><span data-stu-id="a4f14-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="a4f14-111">Il codice seguente consente di creare un oggetto **QueueService** .</span><span class="sxs-lookup"><span data-stu-id="a4f14-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="a4f14-112">Aggiungere il codice seguente vicino all'inizio del file Python da cui si desidera accedere all'archiviazione di Azure a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="a4f14-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="a4f14-113">Il codice seguente consente di creare un oggetto **QueueService** usando il nome dell'account di archiviazione e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="a4f14-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="a4f14-114">Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="a4f14-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="a4f14-115">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="a4f14-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="a4f14-116">Per inserire un messaggio in una coda, usare il metodo **put\_message** per creare un nuovo messaggio e aggiungerlo alla coda.</span><span class="sxs-lookup"><span data-stu-id="a4f14-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="a4f14-117">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="a4f14-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="a4f14-118">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **peek\_messages**.</span><span class="sxs-lookup"><span data-stu-id="a4f14-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="a4f14-119">Per impostazione predefinita, **peek\_messages** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4f14-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="a4f14-120">Procedura: Rimuovere messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="a4f14-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="a4f14-121">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a4f14-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="a4f14-122">Per impostazione predefinita, chiamando **get\_messages**, si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="a4f14-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="a4f14-123">Un messaggio restituito da **get\_messages** diventa invisibile a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="a4f14-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="a4f14-124">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="a4f14-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="a4f14-125">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **delete\_message**.</span><span class="sxs-lookup"><span data-stu-id="a4f14-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="a4f14-126">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio abbia esito negativo a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="a4f14-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="a4f14-127">Il codice chiama **delete\_message** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4f14-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="a4f14-128">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="a4f14-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="a4f14-129">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="a4f14-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="a4f14-130">In secondo luogo, è possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4f14-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="a4f14-131">Nell'esempio di codice seguente viene usato il metodo **get\_messages** per recuperare 16 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="a4f14-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="a4f14-132">Quindi, ogni messaggio viene elaborato con un ciclo for.</span><span class="sxs-lookup"><span data-stu-id="a4f14-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="a4f14-133">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="a4f14-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="a4f14-134">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="a4f14-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="a4f14-135">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="a4f14-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="a4f14-136">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questa funzionalità per aggiornarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="a4f14-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="a4f14-137">La coda seguente usa il metodo **update\_message** per aggiornare un messaggio.</span><span class="sxs-lookup"><span data-stu-id="a4f14-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="a4f14-138">Il timeout di visibilità è impostato su 0. Ciò significa che il messaggio viene visualizzato immediatamente e il contenuto viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="a4f14-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="a4f14-139">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="a4f14-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="a4f14-140">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="a4f14-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="a4f14-141">Il metodo **get\_queue\_metadata** chiede al servizio di accodamento di restituire i metadati relativi alla coda e **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="a4f14-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="a4f14-142">Il risultato è solo approssimativo, poiché è possibile aggiungere o rimuovere messaggi dopo la risposta del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="a4f14-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="a4f14-143">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="a4f14-143">How To: Delete a Queue</span></span>
<span data-ttu-id="a4f14-144">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **delete\_queue**.</span><span class="sxs-lookup"><span data-stu-id="a4f14-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="a4f14-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4f14-145">Next Steps</span></span>
<span data-ttu-id="a4f14-146">A questo punto, dopo avere appreso le nozioni di base dell'archiviazione code, visitare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a4f14-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="a4f14-147">Centro per sviluppatori di Python</span><span class="sxs-lookup"><span data-stu-id="a4f14-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="a4f14-148">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a4f14-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a4f14-149">[Blog del team di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="a4f14-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="a4f14-150">[Microsoft Azure Storage SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="a4f14-150">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="a4f14-151">[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="a4f14-151">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="a4f14-152">[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="a4f14-152">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>