---
title: Come usare l'archiviazione code da Ruby | Microsoft Docs
description: Informazioni su come usare il servizio di accodamento di Azure per creare ed eliminare code e per inserire, visualizzare ed eliminare messaggi. Gli esempi sono scritti in Ruby.
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b1a7dd36af6c45bf085342cdf9c1c926a5040792
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="64a52-104">Come usare l'archiviazione di accodamento da Ruby</span><span class="sxs-lookup"><span data-stu-id="64a52-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="64a52-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="64a52-105">Overview</span></span>
<span data-ttu-id="64a52-106">In questa guida viene illustrato come eseguire scenari comuni del servizio di archiviazione di accodamento di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="64a52-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="64a52-107">Gli esempi sono scritti usando l'API Ruby di Azure.</span><span class="sxs-lookup"><span data-stu-id="64a52-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="64a52-108">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre alla **creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="64a52-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="64a52-109">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="64a52-109">Create a Ruby Application</span></span>
<span data-ttu-id="64a52-110">Creare un'applicazione Ruby.</span><span class="sxs-lookup"><span data-stu-id="64a52-110">Create a Ruby application.</span></span> <span data-ttu-id="64a52-111">Per istruzioni, vedere l'articolo relativo all' [applicazione Web Ruby on Rails in una macchina virtuale di Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="64a52-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="64a52-112">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="64a52-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="64a52-113">Per utilizzare l'archiviazione di Azure, è necessario scaricare e utilizzare il pacchetto Ruby Azure, che comprende un set di librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="64a52-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="64a52-114">Utilizzare RubyGems per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="64a52-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="64a52-115">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="64a52-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="64a52-116">Digitare "gem install azure" nella finestra di comando per installare la gemma e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="64a52-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="64a52-117">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="64a52-117">Import the package</span></span>
<span data-ttu-id="64a52-118">Usando l'editor di testo preferito aggiungere quanto segue alla parte superiore del file Ruby dove si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="64a52-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="64a52-119">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="64a52-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="64a52-120">Il modulo di Azure leggerà le variabili di ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS_KEY** per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="64a52-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="64a52-121">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account prima di utilizzare **Azure::QueueService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="64a52-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="64a52-122">Per ottenere questi valori da un account di archiviazione classico o di Resource Manager nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="64a52-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="64a52-123">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64a52-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64a52-124">Passare all'account di archiviazione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="64a52-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="64a52-125">Nel pannello Impostazioni a destra fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="64a52-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="64a52-126">Nel pannello Chiavi di accesso visualizzato notare la chiave di accesso 1 e la chiave di accesso 2.</span><span class="sxs-lookup"><span data-stu-id="64a52-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="64a52-127">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="64a52-127">You can use either of these.</span></span> 
5. <span data-ttu-id="64a52-128">Fare clic sull'icona Copia per copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="64a52-128">Click the copy icon to copy the key to the clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="64a52-129">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="64a52-129">How To: Create a Queue</span></span>
<span data-ttu-id="64a52-130">La coda seguente crea un oggetto **Azure::QueueService** che consente di usare le code.</span><span class="sxs-lookup"><span data-stu-id="64a52-130">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="64a52-131">Usare il metodo **create_queue()** per creare una coda con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="64a52-131">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="64a52-132">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="64a52-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="64a52-133">Per inserire un messaggio in una coda, usare il metodo **create_message()** per creare un nuovo messaggio e aggiungerlo alla coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-133">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="64a52-134">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="64a52-134">How To: Peek at the Next Message</span></span>
<span data-ttu-id="64a52-135">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **peek\_messages()** .</span><span class="sxs-lookup"><span data-stu-id="64a52-135">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="64a52-136">Per impostazione predefinita, **peek\_messages()** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="64a52-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="64a52-137">È anche possibile specificare il numero di messaggi che si desidera visualizzare.</span><span class="sxs-lookup"><span data-stu-id="64a52-137">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="64a52-138">Procedura: rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="64a52-138">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="64a52-139">È possibile rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="64a52-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="64a52-140">Per impostazione predefinita, chiamando **list\_messages()** si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-140">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="64a52-141">È anche possibile specificare il numero di messaggi che si desidera ottenere.</span><span class="sxs-lookup"><span data-stu-id="64a52-141">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="64a52-142">I messaggi restituiti da **list\_messages()** diventano invisibili a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-142">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="64a52-143">Passare il timeout di visibilità in secondi come parametro.</span><span class="sxs-lookup"><span data-stu-id="64a52-143">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="64a52-144">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="64a52-144">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="64a52-145">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio abbia esito negativo a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="64a52-145">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="64a52-146">Il codice chiama **delete\_message()** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="64a52-146">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="64a52-147">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="64a52-147">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="64a52-148">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-148">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="64a52-149">Il codice seguente usa il metodo **update_message()** per aggiornare un messaggio.</span><span class="sxs-lookup"><span data-stu-id="64a52-149">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="64a52-150">Il metodo restituirà una tupla contenente il Pop Receipt del messaggio in coda e un valore di data e ora UTC che rappresenta il momento in cui il messaggio sarà visibile nella coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-150">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="64a52-151">Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="64a52-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="64a52-152">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="64a52-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="64a52-153">È possibile recuperare un batch di messaggi.</span><span class="sxs-lookup"><span data-stu-id="64a52-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="64a52-154">È possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="64a52-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="64a52-155">Nell'esempio di codice seguente viene utilizzato il metodo **list\_messages()** per recuperare 15 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="64a52-155">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="64a52-156">Quindi, ogni messaggio viene stampato ed eliminato.</span><span class="sxs-lookup"><span data-stu-id="64a52-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="64a52-157">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="64a52-157">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="64a52-158">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="64a52-158">How To: Get the Queue Length</span></span>
<span data-ttu-id="64a52-159">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-159">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="64a52-160">Il metodo **get\_queue\_metadata()** chiede al servizio di accodamento di restituire il conteggio approssimativo dei messaggi e i metadati relativi alla coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-160">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="64a52-161">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="64a52-161">How To: Delete a Queue</span></span>
<span data-ttu-id="64a52-162">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **delete\_queue()** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="64a52-162">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="64a52-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64a52-163">Next Steps</span></span>
<span data-ttu-id="64a52-164">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione di accodamento, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="64a52-164">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="64a52-165">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="64a52-165">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="64a52-166">Archivio [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="64a52-166">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="64a52-167">Per un confronto tra il Servizio di accodamento di Azure discusso in questo articolo e le code del bus di servizio di Azure discusse nell'articolo [Come usare le code del bus di servizio](/develop/ruby/how-to-guides/service-bus-queues/) vedere [Analogie e differenze tra le code di Azure e le code del bus di servizio](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="64a52-167">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>