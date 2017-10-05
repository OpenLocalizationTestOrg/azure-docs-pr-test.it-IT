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
ms.openlocfilehash: b978b65bb3b717362697a41510c5b2b4d057cf1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="91f0a-104">Come usare l'archiviazione di accodamento da Ruby</span><span class="sxs-lookup"><span data-stu-id="91f0a-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="91f0a-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="91f0a-105">Overview</span></span>
<span data-ttu-id="91f0a-106">In questa guida viene illustrato come eseguire scenari comuni del servizio di archiviazione di accodamento di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="91f0a-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="91f0a-107">Gli esempi sono scritti usando l'API Ruby di Azure.</span><span class="sxs-lookup"><span data-stu-id="91f0a-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="91f0a-108">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre alla **creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="91f0a-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="91f0a-109">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="91f0a-109">Create a Ruby Application</span></span>
<span data-ttu-id="91f0a-110">Creare un'applicazione Ruby.</span><span class="sxs-lookup"><span data-stu-id="91f0a-110">Create a Ruby application.</span></span> <span data-ttu-id="91f0a-111">Per istruzioni, vedere l'articolo relativo all' [applicazione Web Ruby on Rails in una macchina virtuale di Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="91f0a-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="91f0a-112">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="91f0a-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="91f0a-113">Per utilizzare l'archiviazione di Azure, è necessario scaricare e utilizzare il pacchetto Ruby Azure, che comprende un set di librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="91f0a-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="91f0a-114">Utilizzare RubyGems per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="91f0a-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="91f0a-115">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="91f0a-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="91f0a-116">Digitare "gem install azure" nella finestra di comando per installare la gemma e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="91f0a-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="91f0a-117">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="91f0a-117">Import the package</span></span>
<span data-ttu-id="91f0a-118">Usando l'editor di testo preferito aggiungere quanto segue alla parte superiore del file Ruby dove si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="91f0a-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="91f0a-119">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="91f0a-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="91f0a-120">Il modulo di Azure leggerà le variabili di ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS_KEY** per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="91f0a-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="91f0a-121">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account prima di utilizzare **Azure::QueueService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="91f0a-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="91f0a-122">Per ottenere questi valori da un account di archiviazione classico o di Resource Manager nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="91f0a-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="91f0a-123">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91f0a-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="91f0a-124">Passare all'account di archiviazione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="91f0a-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="91f0a-125">Nel pannello Impostazioni a destra fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="91f0a-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="91f0a-126">Nel pannello Chiavi di accesso visualizzato notare la chiave di accesso 1 e la chiave di accesso 2.</span><span class="sxs-lookup"><span data-stu-id="91f0a-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="91f0a-127">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="91f0a-127">You can use either of these.</span></span> 
5. <span data-ttu-id="91f0a-128">Fare clic sull'icona Copia per copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="91f0a-128">Click the copy icon to copy the key to the clipboard.</span></span> 

<span data-ttu-id="91f0a-129">Per ottenere questi valori da un account di archiviazione classico nel portale di Azure classico:</span><span class="sxs-lookup"><span data-stu-id="91f0a-129">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="91f0a-130">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="91f0a-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="91f0a-131">Passare all'account di archiviazione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="91f0a-131">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="91f0a-132">Fare clic su **GESTISCI CHIAVI DI ACCESSO** nella parte inferiore del riquadro di spostamento.</span><span class="sxs-lookup"><span data-stu-id="91f0a-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="91f0a-133">Nella finestra di dialogo popup saranno visualizzati il nome dell'account di archiviazione, la chiave di accesso primaria e la chiave di accesso secondaria.</span><span class="sxs-lookup"><span data-stu-id="91f0a-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="91f0a-134">Per la chiave di accesso è possibile usare sia la chiave primaria che secondaria.</span><span class="sxs-lookup"><span data-stu-id="91f0a-134">For access key, you can use either the primary one or the secondary one.</span></span> 
5. <span data-ttu-id="91f0a-135">Fare clic sull'icona Copia per copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="91f0a-135">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="91f0a-136">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="91f0a-136">How To: Create a Queue</span></span>
<span data-ttu-id="91f0a-137">La coda seguente crea un oggetto **Azure::QueueService** che consente di usare le code.</span><span class="sxs-lookup"><span data-stu-id="91f0a-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="91f0a-138">Usare il metodo **create_queue()** per creare una coda con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="91f0a-138">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="91f0a-139">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="91f0a-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="91f0a-140">Per inserire un messaggio in una coda, usare il metodo **create_message()** per creare un nuovo messaggio e aggiungerlo alla coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="91f0a-141">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="91f0a-141">How To: Peek at the Next Message</span></span>
<span data-ttu-id="91f0a-142">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **peek\_messages()** .</span><span class="sxs-lookup"><span data-stu-id="91f0a-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="91f0a-143">Per impostazione predefinita, **peek\_messages()** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="91f0a-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="91f0a-144">È anche possibile specificare il numero di messaggi che si desidera visualizzare.</span><span class="sxs-lookup"><span data-stu-id="91f0a-144">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="91f0a-145">Procedura: rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="91f0a-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="91f0a-146">È possibile rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="91f0a-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="91f0a-147">Per impostazione predefinita, chiamando **list\_messages()** si ottiene il messaggio successivo in una coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-147">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="91f0a-148">È anche possibile specificare il numero di messaggi che si desidera ottenere.</span><span class="sxs-lookup"><span data-stu-id="91f0a-148">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="91f0a-149">I messaggi restituiti da **list\_messages()** diventano invisibili a qualsiasi altro codice che legge i messaggi dalla stessa coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="91f0a-150">Passare il timeout di visibilità in secondi come parametro.</span><span class="sxs-lookup"><span data-stu-id="91f0a-150">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="91f0a-151">Per completare la rimozione del messaggio dalla coda, è necessario chiamare anche **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="91f0a-151">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="91f0a-152">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio abbia esito negativo a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="91f0a-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="91f0a-153">Il codice chiama **delete\_message()** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="91f0a-153">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="91f0a-154">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="91f0a-154">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="91f0a-155">È possibile cambiare il contenuto di un messaggio inserito nella coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-155">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="91f0a-156">Il codice seguente usa il metodo **update_message()** per aggiornare un messaggio.</span><span class="sxs-lookup"><span data-stu-id="91f0a-156">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="91f0a-157">Il metodo restituirà una tupla contenente il Pop Receipt del messaggio in coda e un valore di data e ora UTC che rappresenta il momento in cui il messaggio sarà visibile nella coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="91f0a-158">Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="91f0a-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="91f0a-159">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="91f0a-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="91f0a-160">È possibile recuperare un batch di messaggi.</span><span class="sxs-lookup"><span data-stu-id="91f0a-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="91f0a-161">È possibile impostare un timeout di invisibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="91f0a-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="91f0a-162">Nell'esempio di codice seguente viene utilizzato il metodo **list\_messages()** per recuperare 15 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="91f0a-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="91f0a-163">Quindi, ogni messaggio viene stampato ed eliminato.</span><span class="sxs-lookup"><span data-stu-id="91f0a-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="91f0a-164">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="91f0a-164">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="91f0a-165">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="91f0a-165">How To: Get the Queue Length</span></span>
<span data-ttu-id="91f0a-166">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-166">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="91f0a-167">Il metodo **get\_queue\_metadata()** chiede al servizio di accodamento di restituire il conteggio approssimativo dei messaggi e i metadati relativi alla coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="91f0a-168">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="91f0a-168">How To: Delete a Queue</span></span>
<span data-ttu-id="91f0a-169">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **delete\_queue()** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="91f0a-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="91f0a-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91f0a-170">Next Steps</span></span>
<span data-ttu-id="91f0a-171">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione di accodamento, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="91f0a-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="91f0a-172">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="91f0a-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="91f0a-173">Archivio [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="91f0a-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="91f0a-174">Per un confronto tra il Servizio di accodamento di Azure discusso in questo articolo e le code del bus di servizio di Azure discusse nell'articolo [Come usare le code del bus di servizio](/develop/ruby/how-to-guides/service-bus-queues/) vedere [Analogie e differenze tra le code di Azure e le code del bus di servizio](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="91f0a-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>