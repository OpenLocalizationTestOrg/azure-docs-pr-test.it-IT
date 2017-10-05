---
title: Come usare l'archiviazione code da PHP | Microsoft Docs
description: Informazioni su come usare il servizio di accodamento di Azure per creare ed eliminare code e per inserire, visualizzare ed eliminare messaggi. Gli esempi sono scritti in PHP.
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="45a99-104">Come usare l'archiviazione di accodamento da PHP</span><span class="sxs-lookup"><span data-stu-id="45a99-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="45a99-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="45a99-105">Overview</span></span>
<span data-ttu-id="45a99-106">Questa guida illustra diversi scenari di utilizzo comuni del servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="45a99-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="45a99-107">Gli esempi sono scritti utilizzando le classi di Windows SDK per PHP</span><span class="sxs-lookup"><span data-stu-id="45a99-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="45a99-108">Gli scenari presentati includono l'inserimento, la visualizzazione, il recupero e l'eliminazione dei messaggi in coda, oltre alle procedure di creazione ed eliminazione di code.</span><span class="sxs-lookup"><span data-stu-id="45a99-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="45a99-109">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="45a99-109">Create a PHP application</span></span>
<span data-ttu-id="45a99-110">Per creare un'applicazione PHP che accede al Servizio di accodamento di Azure, è sufficiente fare riferimento alle classi di Azure SDK per PHP dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="45a99-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="45a99-111">Per creare l'applicazione, è possibile usare qualsiasi strumento di sviluppo, incluso il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="45a99-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="45a99-112">In questa guida si useranno le funzionalità del Servizio di accodamento che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="45a99-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="45a99-113">Acquisire le librerie client di Azure</span><span class="sxs-lookup"><span data-stu-id="45a99-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="45a99-114">Configurare l'applicazione per l'accesso all'archiviazione di accodamento</span><span class="sxs-lookup"><span data-stu-id="45a99-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="45a99-115">Per utilizzare le API per l'archiviazione di accodamento di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="45a99-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="45a99-116">Fare riferimento al file autoloader mediante l'istruzione [require_once].</span><span class="sxs-lookup"><span data-stu-id="45a99-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="45a99-117">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="45a99-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="45a99-118">Nell'esempio seguente viene indicato come includere il file autoloader e fare riferimento alla classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="45a99-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="45a99-119">In questo esempio (e in altri esempi in questo articolo) si presuppone che siano state installate le librerie client PHP per Azure tramite Composer.</span><span class="sxs-lookup"><span data-stu-id="45a99-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="45a99-120">Se le librerie sono state installate manualmente, sarà necessario fare riferimento al file autoloader `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="45a99-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="45a99-121">Nei seguenti esempi l'istruzione `require_once` verrà sempre visualizzata, ma si farà riferimento solo alle classi necessarie per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="45a99-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="45a99-122">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45a99-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="45a99-123">Per creare un'istanza di un client del Servizio di accodamento di Azure, è necessario innanzitutto disporre di una stringa di connessione valida.</span><span class="sxs-lookup"><span data-stu-id="45a99-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="45a99-124">Il formato della stringa di connessione del servizio di accodamento è:</span><span class="sxs-lookup"><span data-stu-id="45a99-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="45a99-125">Per accedere a un servizio attivo:</span><span class="sxs-lookup"><span data-stu-id="45a99-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="45a99-126">Per accedere alla memoria dell'emulatore:</span><span class="sxs-lookup"><span data-stu-id="45a99-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="45a99-127">Per creare un client di servizio di Azure, è necessario usare la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="45a99-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="45a99-128">È possibile utilizzare le tecniche seguenti:</span><span class="sxs-lookup"><span data-stu-id="45a99-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="45a99-129">Passare la stringa di connessione direttamente.</span><span class="sxs-lookup"><span data-stu-id="45a99-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="45a99-130">Utilizzare **CloudConfigurationManager (CCM)** per cercare la stringa di connessione in più origini esterne:</span><span class="sxs-lookup"><span data-stu-id="45a99-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="45a99-131">Per impostazione predefinita, viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="45a99-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="45a99-132">è possibile aggiungere nuove origini estendendo la classe **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="45a99-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="45a99-133">Per gli esempi illustrati in questo articolo, la stringa di connessione verrà passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="45a99-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="45a99-134">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="45a99-134">Create a queue</span></span>
<span data-ttu-id="45a99-135">Un oggetto **QueueRestProxy** consente di creare una coda usando il metodo **createQueue**.</span><span class="sxs-lookup"><span data-stu-id="45a99-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="45a99-136">Quando si crea una coda, è possibile impostare le opzioni per la coda, anche se tale operazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="45a99-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="45a99-137">Nell'esempio seguente viene illustrato come impostare i metadati in una coda.</span><span class="sxs-lookup"><span data-stu-id="45a99-137">(The example below shows how to set metadata on a queue.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="45a99-138">Non basarsi sulla distinzione maiuscole/minuscole nelle chiavi di metadati.</span><span class="sxs-lookup"><span data-stu-id="45a99-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="45a99-139">Il servizio legge tutte le chiavi come scritte in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="45a99-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="45a99-140">Aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="45a99-140">Add a message to a queue</span></span>
<span data-ttu-id="45a99-141">Per aggiungere un messaggio a una coda, usare **QueueRestProxy->createMessage**.</span><span class="sxs-lookup"><span data-stu-id="45a99-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="45a99-142">Il metodo utilizza il nome della coda, il testo del messaggio e le opzioni messaggio (facoltative).</span><span class="sxs-lookup"><span data-stu-id="45a99-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="45a99-143">Visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="45a99-143">Peek at the next message</span></span>
<span data-ttu-id="45a99-144">È possibile visualizzare il messaggio (o i messaggi successivi) in cima a una coda senza rimuoverlo dalla coda chiamando il metodo **QueueRestProxy->peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="45a99-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="45a99-145">Per impostazione predefinita, il metodo **peekMessage** restituisce un solo messaggio, ma è possibile modificare tale valore con il metodo **PeekMessagesOptions->setNumberOfMessages**.</span><span class="sxs-lookup"><span data-stu-id="45a99-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="45a99-146">Rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="45a99-146">De-queue the next message</span></span>
<span data-ttu-id="45a99-147">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="45a99-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="45a99-148">Chiamare **QueueRestProxy->listMessages** per rendere il messaggio invisibile a tutte le altre letture del codice dalla coda.</span><span class="sxs-lookup"><span data-stu-id="45a99-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="45a99-149">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="45a99-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="45a99-150">(Se il messaggio non viene eliminato in questo periodo di tempo, diventerà nuovamente visibile nella coda.) Per completare la rimozione del messaggio dalla coda, è necessario chiamare **QueueRestProxy->deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="45a99-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="45a99-151">Questo processo in due passaggi di rimozione di un messaggio assicura che, qualora l'elaborazione di un messaggio abbia esito negativo a causa di errori hardware o software, un'altra istanza del codice sia in grado di ottenere lo stesso messaggio e di riprovare.</span><span class="sxs-lookup"><span data-stu-id="45a99-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="45a99-152">Il codice chiama **deleteMessage** immediatamente dopo l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="45a99-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="45a99-153">Cambiare il contenuto di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="45a99-153">Change the contents of a queued message</span></span>
<span data-ttu-id="45a99-154">È possibile modificare il contenuto di un messaggio inserito nella coda chiamando **QueueRestProxy->updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="45a99-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="45a99-155">Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questa funzionalità per aggiornarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="45a99-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="45a99-156">Il codice seguente consente di aggiornare il messaggio in coda con nuovo contenuto e di impostarne il timeout di visibilità per prolungarlo di altri 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="45a99-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="45a99-157">In questo modo lo stato del lavoro associato al messaggio viene salvato e il client ha a disposizione un altro minuto per continuare l'elaborazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="45a99-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="45a99-158">È possibile usare questa tecnica per tenere traccia di flussi di lavoro composti da più passaggi nei messaggi in coda, senza la necessità di ricominciare dall'inizio se un passaggio di elaborazione non riesce a causa di errori hardware o software.</span><span class="sxs-lookup"><span data-stu-id="45a99-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="45a99-159">In genere, è consigliabile mantenere anche un conteggio dei tentativi, in modo da eliminare i messaggi per cui vengono effettuati più di *n* tentativi.</span><span class="sxs-lookup"><span data-stu-id="45a99-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="45a99-160">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="45a99-160">This protects against a message that triggers an application error each time it is processed.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="45a99-161">Opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="45a99-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="45a99-162">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="45a99-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="45a99-163">Innanzitutto, è possibile recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="45a99-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="45a99-164">In secondo luogo, è possibile impostare un timeout di visibilità più lungo o più breve assegnando al codice più o meno tempo per l'elaborazione completa di ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="45a99-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="45a99-165">Nell'esempio di codice seguente viene utilizzato il metodo **getMessages** per recuperare 16 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="45a99-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="45a99-166">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="45a99-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="45a99-167">Per ogni messaggio, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="45a99-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a><span data-ttu-id="45a99-168">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="45a99-168">Get queue length</span></span>
<span data-ttu-id="45a99-169">È possibile ottenere una stima sul numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="45a99-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="45a99-170">Il metodo **QueueRestProxy->getQueueMetadata** chiede al servizio di accodamento di restituire i metadati relativi alla coda.</span><span class="sxs-lookup"><span data-stu-id="45a99-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="45a99-171">La chiamata al metodo **getApproximateMessageCount** sull'oggetto restituito fornisce il numero di messaggi presenti in una coda.</span><span class="sxs-lookup"><span data-stu-id="45a99-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="45a99-172">Il conteggio è solo approssimativo, poiché è possibile aggiungere o rimuovere messaggi dopo la risposta del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="45a99-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a><span data-ttu-id="45a99-173">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="45a99-173">Delete a queue</span></span>
<span data-ttu-id="45a99-174">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **QueueRestProxy->deleteQueue**.</span><span class="sxs-lookup"><span data-stu-id="45a99-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="45a99-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45a99-175">Next steps</span></span>
<span data-ttu-id="45a99-176">A questo punto, dopo aver appreso le nozioni di base sull'archiviazione delle code, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="45a99-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="45a99-177">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="45a99-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="45a99-178">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="45a99-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

