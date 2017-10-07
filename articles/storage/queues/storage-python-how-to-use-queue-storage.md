---
title: aaaHow toouse l'archiviazione delle code da Python | Documenti Microsoft
description: Informazioni come toouse hello servizio di Accodamento di Azure da toocreate Python ed eliminare le code e inserire, ottenere ed eliminare messaggi.
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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="6c58c-103">Come toouse l'archiviazione delle code da Python</span><span class="sxs-lookup"><span data-stu-id="6c58c-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6c58c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6c58c-104">Overview</span></span>
<span data-ttu-id="6c58c-105">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c58c-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="6c58c-106">esempi di Hello sono scritti in Python e utilizzare hello [Microsoft Azure Storage SDK per Python].</span><span class="sxs-lookup"><span data-stu-id="6c58c-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="6c58c-107">Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="6c58c-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="6c58c-108">Per ulteriori informazioni sulle code, vedere sezione toohello [passaggi successivi].</span><span class="sxs-lookup"><span data-stu-id="6c58c-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="6c58c-109">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-109">How To: Create a Queue</span></span>
<span data-ttu-id="6c58c-110">Hello **QueueService** oggetto consente di lavorare con le code.</span><span class="sxs-lookup"><span data-stu-id="6c58c-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="6c58c-111">Hello codice seguente viene creata una **QueueService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="6c58c-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="6c58c-112">Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="6c58c-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="6c58c-113">Hello codice seguente viene creata una **QueueService** oggetto utilizzando hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="6c58c-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="6c58c-114">Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="6c58c-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="6c58c-115">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="6c58c-116">un messaggio in una coda, utilizzare hello tooinsert **inserire\_messaggio** per creare un nuovo messaggio e aggiungerlo toohello coda.</span><span class="sxs-lookup"><span data-stu-id="6c58c-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="6c58c-117">Procedura: Leggere hello messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="6c58c-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="6c58c-118">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek\_messaggi** metodo.</span><span class="sxs-lookup"><span data-stu-id="6c58c-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="6c58c-119">Per impostazione predefinita, **peek\_messages** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="6c58c-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="6c58c-120">Procedura: Rimuovere messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="6c58c-121">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="6c58c-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="6c58c-122">Quando si chiama **ottenere\_messaggi**, si messaggio hello successivo in una coda per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6c58c-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="6c58c-123">Un messaggio restituito da **ottenere\_messaggi** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="6c58c-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="6c58c-124">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="6c58c-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="6c58c-125">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **eliminare\_messaggio**.</span><span class="sxs-lookup"><span data-stu-id="6c58c-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="6c58c-126">Questo processo in due passaggi della rimozione di un messaggio garantisce che quando il codice ha esito negativo tooprocess un messaggio a causa di un errore hardware o software, un'altra istanza del codice può ottenere lo stesso messaggio e riprovare.</span><span class="sxs-lookup"><span data-stu-id="6c58c-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="6c58c-127">Il codice chiama **eliminare\_messaggio** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="6c58c-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="6c58c-128">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="6c58c-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="6c58c-129">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="6c58c-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="6c58c-130">In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="6c58c-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="6c58c-131">codice Hello seguente viene utilizzata la **ottenere\_messaggi** messaggi tooget 16 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="6c58c-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="6c58c-132">Quindi, ogni messaggio viene elaborato con un ciclo for.</span><span class="sxs-lookup"><span data-stu-id="6c58c-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="6c58c-133">Imposta inoltre il timeout di invisibilità hello a cinque minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="6c58c-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="6c58c-134">Procedura: Modificare il contenuto di hello di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="6c58c-135">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="6c58c-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="6c58c-136">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questo tooupdate funzionalità lo stato dell'attività di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="6c58c-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="6c58c-137">codice Hello riportato di seguito utilizza hello **aggiornare\_messaggio** metodo tooupdate un messaggio.</span><span class="sxs-lookup"><span data-stu-id="6c58c-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="6c58c-138">timeout di visibilità Hello è impostato too0, vale a dire viene immediatamente visualizzato il messaggio e contenuto hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6c58c-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="6c58c-139">Procedura: Recuperare hello lunghezza coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="6c58c-140">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="6c58c-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="6c58c-141">Il **ottenere\_coda\_metadati** metodo richiede i metadati della coda del servizio tooreturn sulla coda hello hello e hello **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="6c58c-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="6c58c-142">risultato Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo che il servizio di Accodamento risponde tooyour richiesta.</span><span class="sxs-lookup"><span data-stu-id="6c58c-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="6c58c-143">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="6c58c-143">How To: Delete a Queue</span></span>
<span data-ttu-id="6c58c-144">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare\_coda** metodo.</span><span class="sxs-lookup"><span data-stu-id="6c58c-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="6c58c-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c58c-145">Next Steps</span></span>
<span data-ttu-id="6c58c-146">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="6c58c-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="6c58c-147">Centro per sviluppatori di Python</span><span class="sxs-lookup"><span data-stu-id="6c58c-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="6c58c-148">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6c58c-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="6c58c-149">[Blog del team di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="6c58c-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="6c58c-150">[Microsoft Azure Storage SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="6c58c-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python