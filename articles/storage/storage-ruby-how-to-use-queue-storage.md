---
title: aaaHow toouse archiviazione delle code da Ruby | Documenti Microsoft
description: Informazioni su come toouse hello Azure coda servizio toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in Ruby.
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
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="85ce8-104">Come l'archiviazione delle code da Ruby toouse</span><span class="sxs-lookup"><span data-stu-id="85ce8-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="85ce8-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="85ce8-105">Overview</span></span>
<span data-ttu-id="85ce8-106">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello del servizio di archiviazione di Accodamento di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="85ce8-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="85ce8-107">esempi di Hello vengono scritti utilizzando hello Ruby API di Azure.</span><span class="sxs-lookup"><span data-stu-id="85ce8-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="85ce8-108">Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="85ce8-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="85ce8-109">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="85ce8-109">Create a Ruby Application</span></span>
<span data-ttu-id="85ce8-110">Creare un'applicazione Ruby.</span><span class="sxs-lookup"><span data-stu-id="85ce8-110">Create a Ruby application.</span></span> <span data-ttu-id="85ce8-111">Per istruzioni, vedere l'articolo relativo all' [applicazione Web Ruby on Rails in una macchina virtuale di Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="85ce8-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="85ce8-112">Configurare l'applicazione tooAccess archiviazione</span><span class="sxs-lookup"><span data-stu-id="85ce8-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="85ce8-113">toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto di azure, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="85ce8-114">Utilizzare un pacchetto di hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="85ce8-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="85ce8-115">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="85ce8-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="85ce8-116">Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="85ce8-117">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="85ce8-117">Import hello package</span></span>
<span data-ttu-id="85ce8-118">Utilizzare un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:</span><span class="sxs-lookup"><span data-stu-id="85ce8-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="85ce8-119">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="85ce8-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="85ce8-120">modulo Hello azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_ACCESS_KEY** per le informazioni richieste tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="85ce8-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="85ce8-121">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::QueueService** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="85ce8-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="85ce8-122">tooobtain questi valori da un classico o Gestione risorse di archiviazione di account nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="85ce8-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="85ce8-123">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85ce8-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85ce8-124">Passare l'account di archiviazione toohello da toouse.</span><span class="sxs-lookup"><span data-stu-id="85ce8-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="85ce8-125">Nel pannello delle impostazioni hello in hello destra, fare clic su **chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="85ce8-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="85ce8-126">Nel pannello chiavi accesso hello che viene visualizzato, si noterà la chiave di accesso hello 1 e 2 di chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="85ce8-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="85ce8-127">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="85ce8-127">You can use either of these.</span></span> 
5. <span data-ttu-id="85ce8-128">Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.</span><span class="sxs-lookup"><span data-stu-id="85ce8-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="85ce8-129">tooobtain questi valori da un'archiviazione classico account nel portale di Azure classico hello:</span><span class="sxs-lookup"><span data-stu-id="85ce8-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="85ce8-130">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="85ce8-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="85ce8-131">Passare l'account di archiviazione toohello da toouse.</span><span class="sxs-lookup"><span data-stu-id="85ce8-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="85ce8-132">Fare clic su **GESTISCI CHIAVI di accesso** nella parte inferiore di hello del riquadro di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="85ce8-133">Nella finestra di dialogo a comparsa hello, si noterà nome account di archiviazione hello, chiave di accesso primaria e chiave di accesso secondaria.</span><span class="sxs-lookup"><span data-stu-id="85ce8-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="85ce8-134">Per la chiave di accesso, è possibile utilizzare hello primario o quello secondario hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="85ce8-135">Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.</span><span class="sxs-lookup"><span data-stu-id="85ce8-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="85ce8-136">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-136">How To: Create a Queue</span></span>
<span data-ttu-id="85ce8-137">Hello codice seguente viene creata una **Azure::QueueService** oggetto, che consente di toowork con le code.</span><span class="sxs-lookup"><span data-stu-id="85ce8-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="85ce8-138">Hello utilizzare **create_queue()** toocreate metodo una coda con hello nome specificato.</span><span class="sxs-lookup"><span data-stu-id="85ce8-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="85ce8-139">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="85ce8-140">un messaggio in una coda, utilizzare hello tooinsert **create_message()** metodo toocreate un nuovo messaggio e aggiungerla toohello coda.</span><span class="sxs-lookup"><span data-stu-id="85ce8-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="85ce8-141">Procedura: Leggere hello messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="85ce8-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="85ce8-142">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek\_messages()** metodo.</span><span class="sxs-lookup"><span data-stu-id="85ce8-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="85ce8-143">Per impostazione predefinita, **peek\_messages()** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="85ce8-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="85ce8-144">È inoltre possibile specificare il numero di messaggi desiderato toopeek.</span><span class="sxs-lookup"><span data-stu-id="85ce8-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="85ce8-145">Procedura: Rimozione dalla coda hello messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="85ce8-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="85ce8-146">È possibile rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="85ce8-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="85ce8-147">Quando si chiama **elenco\_messages()**, si messaggio hello successivo in una coda per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="85ce8-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="85ce8-148">È inoltre possibile specificare il numero di messaggi desiderato tooget.</span><span class="sxs-lookup"><span data-stu-id="85ce8-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="85ce8-149">i messaggi restituiti da Hello **elenco\_messages()** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="85ce8-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="85ce8-150">Passare nel timeout di visibilità hello in secondi come parametro.</span><span class="sxs-lookup"><span data-stu-id="85ce8-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="85ce8-151">toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="85ce8-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="85ce8-152">Questo processo in due passaggi della rimozione di un messaggio assicura che quando il tooprocess ha esito negativo di codice un messaggio a causa di un errore toohardware o software, un'altra istanza del codice è possibile ottenere hello stesso messaggio e provare nuovamente.</span><span class="sxs-lookup"><span data-stu-id="85ce8-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="85ce8-153">Il codice chiama **eliminare\_message()** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="85ce8-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="85ce8-154">Procedura: Modificare il contenuto di hello di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="85ce8-155">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="85ce8-156">codice Hello riportato di seguito utilizza hello **update_message()** metodo tooupdate un messaggio.</span><span class="sxs-lookup"><span data-stu-id="85ce8-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="85ce8-157">metodo Hello restituirà una tupla che contiene di ricezione pop del messaggio della coda di hello hello e un valore di tempo data UTC che rappresenta quando il messaggio hello sarà visibile nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="85ce8-158">Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="85ce8-159">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="85ce8-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="85ce8-160">È possibile recuperare un batch di messaggi.</span><span class="sxs-lookup"><span data-stu-id="85ce8-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="85ce8-161">È possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="85ce8-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="85ce8-162">esempio di codice seguente Hello utilizza hello **elenco\_messages()** messaggi tooget 15 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="85ce8-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="85ce8-163">Quindi, ogni messaggio viene stampato ed eliminato.</span><span class="sxs-lookup"><span data-stu-id="85ce8-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="85ce8-164">Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="85ce8-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="85ce8-165">Procedura: Recuperare hello lunghezza coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="85ce8-166">È possibile ottenere una stima del numero di hello di messaggi nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="85ce8-167">Hello **ottenere\_coda\_metadata()** metodo chiede hello coda conteggio approssimativo dei messaggi di servizio tooreturn hello e i metadati sulla coda hello.</span><span class="sxs-lookup"><span data-stu-id="85ce8-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="85ce8-168">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="85ce8-168">How To: Delete a Queue</span></span>
<span data-ttu-id="85ce8-169">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamata hello **eliminare\_Queue** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="85ce8-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="85ce8-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85ce8-170">Next Steps</span></span>
<span data-ttu-id="85ce8-171">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="85ce8-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="85ce8-172">Visitare hello [blog del Team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="85ce8-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="85ce8-173">Visitare hello [Azure SDK per Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository in GitHub</span><span class="sxs-lookup"><span data-stu-id="85ce8-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="85ce8-174">Per un confronto tra hello servizio di Accodamento Azure descritti in questo articolo e code di Azure Service Bus descritti in hello [come toouse code di Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) articolo, vedere [code di Azure e code di Service Bus: confronto e Differenza](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="85ce8-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
