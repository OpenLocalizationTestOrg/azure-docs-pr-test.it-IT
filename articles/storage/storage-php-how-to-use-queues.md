---
title: aaaHow toouse l'archiviazione delle code da PHP | Documenti Microsoft
description: Informazioni su come toouse hello coda di Azure storage service toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in PHP.
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
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="d2c51-104">Come toouse l'archiviazione delle code da PHP</span><span class="sxs-lookup"><span data-stu-id="d2c51-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d2c51-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d2c51-105">Overview</span></span>
<span data-ttu-id="d2c51-106">Questa guida illustra come gli scenari comuni di tooperform usando hello servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c51-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="d2c51-107">esempi di Hello vengono scritte tramite le classi da hello Windows SDK per PHP.</span><span class="sxs-lookup"><span data-stu-id="d2c51-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="d2c51-108">Hello coperti scenari includono inserimento, visualizzazione, recupero e l'eliminazione di messaggi in coda, nonché creazione e l'eliminazione di code.</span><span class="sxs-lookup"><span data-stu-id="d2c51-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="d2c51-109">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="d2c51-109">Create a PHP application</span></span>
<span data-ttu-id="d2c51-110">Hello solo requisito per la creazione di un'applicazione PHP che accede l'archiviazione delle code di Azure è hello che fanno riferimento a classi di hello Azure SDK per PHP all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="d2c51-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="d2c51-111">È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo dell'applicazione, inclusi il blocco note.</span><span class="sxs-lookup"><span data-stu-id="d2c51-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="d2c51-112">In questa guida si useranno le funzionalità del Servizio di accodamento che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c51-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="d2c51-113">Recuperare le librerie Client di hello Azure</span><span class="sxs-lookup"><span data-stu-id="d2c51-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="d2c51-114">Configurare l'archiviazione delle code di tooaccess applicazione</span><span class="sxs-lookup"><span data-stu-id="d2c51-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="d2c51-115">hello toouse API per l'archiviazione delle code di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d2c51-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="d2c51-116">File di riferimento hello autoloader utilizzando hello [require_once] istruzione.</span><span class="sxs-lookup"><span data-stu-id="d2c51-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="d2c51-117">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="d2c51-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="d2c51-118">Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="d2c51-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="d2c51-119">In questo esempio (e altri esempi in questo articolo) si presuppone di aver installato le librerie Client di PHP hello per Azure tramite creazione.</span><span class="sxs-lookup"><span data-stu-id="d2c51-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="d2c51-120">Se è stato installato manualmente le librerie di hello, sarà necessario tooreference hello `WindowsAzure.php` autoloader file.</span><span class="sxs-lookup"><span data-stu-id="d2c51-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="d2c51-121">Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo le classi di hello necessari per tooexecute esempio hello verranno fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="d2c51-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d2c51-122">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d2c51-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="d2c51-123">tooinstantiate un client di archiviazione della coda di Azure, è innanzitutto necessario una stringa di connessione valido.</span><span class="sxs-lookup"><span data-stu-id="d2c51-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="d2c51-124">formato stringa di connessione del servizio coda hello Hello è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d2c51-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="d2c51-125">Per accedere a un servizio attivo:</span><span class="sxs-lookup"><span data-stu-id="d2c51-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="d2c51-126">Per l'accesso all'archiviazione di emulatore hello:</span><span class="sxs-lookup"><span data-stu-id="d2c51-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="d2c51-127">toocreate qualsiasi client del servizio di Azure, è necessario hello toouse **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="d2c51-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="d2c51-128">È possibile utilizzare una delle seguenti tecniche hello:</span><span class="sxs-lookup"><span data-stu-id="d2c51-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="d2c51-129">Passare la connessione hello tooit direttamente di stringa.</span><span class="sxs-lookup"><span data-stu-id="d2c51-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="d2c51-130">Utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="d2c51-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="d2c51-131">Per impostazione predefinita, viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="d2c51-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="d2c51-132">È possibile aggiungere nuove origini estendendo hello **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="d2c51-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="d2c51-133">Per esempi di hello descritti di seguito, la stringa di connessione hello verrà passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="d2c51-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="d2c51-134">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="d2c51-134">Create a queue</span></span>
<span data-ttu-id="d2c51-135">Oggetto **QueueRestProxy** oggetto consente di creare una coda utilizzando hello **createQueue** metodo.</span><span class="sxs-lookup"><span data-stu-id="d2c51-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="d2c51-136">Quando si crea una coda, è possibile impostare le opzioni nella coda di hello, ma non è necessario.</span><span class="sxs-lookup"><span data-stu-id="d2c51-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="d2c51-137">(hello di esempio seguente viene illustrato come tooset metadati in una coda.)</span><span class="sxs-lookup"><span data-stu-id="d2c51-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="d2c51-138">Non basarsi sulla distinzione maiuscole/minuscole nelle chiavi di metadati.</span><span class="sxs-lookup"><span data-stu-id="d2c51-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="d2c51-139">Tutte le chiavi vengono lette dal servizio hello in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="d2c51-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="d2c51-140">Aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="d2c51-140">Add a message tooa queue</span></span>
<span data-ttu-id="d2c51-141">utilizzare una coda di messaggi tooa, tooadd **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="d2c51-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="d2c51-142">metodo Hello accetta il nome di coda hello, testo del messaggio hello e opzioni di messaggio (che sono facoltative).</span><span class="sxs-lookup"><span data-stu-id="d2c51-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="d2c51-143">Leggere il messaggio hello successivo</span><span class="sxs-lookup"><span data-stu-id="d2c51-143">Peek at hello next message</span></span>
<span data-ttu-id="d2c51-144">È possibile anche visualizzare un messaggio (o i messaggi) nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello chiamando **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="d2c51-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="d2c51-145">Per impostazione predefinita, hello **peekMessage** metodo restituisce un singolo messaggio, ma è possibile modificare tale valore utilizzando hello **PeekMessagesOptions -> setNumberOfMessages** metodo.</span><span class="sxs-lookup"><span data-stu-id="d2c51-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="d2c51-146">Annullato l'accodamento messaggio successivo hello</span><span class="sxs-lookup"><span data-stu-id="d2c51-146">De-queue hello next message</span></span>
<span data-ttu-id="d2c51-147">Il codice consente di rimuovere un messaggio da una coda in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="d2c51-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="d2c51-148">In primo luogo, si chiama **QueueRestProxy -> listMessages**, rendendo hello messaggio invisibile tooany altro codice che legge dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="d2c51-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="d2c51-149">Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="d2c51-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="d2c51-150">(Se il messaggio hello non viene eliminato in questo periodo di tempo, sarà nuovamente visibile nella coda di hello.) toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d2c51-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="d2c51-151">Questo processo in due passaggi della rimozione di un messaggio assicura che quando il tooprocess ha esito negativo di codice un messaggio a causa di un errore toohardware o software, un'altra istanza del codice è possibile ottenere hello stesso messaggio e provare nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d2c51-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="d2c51-152">Il codice chiama **deleteMessage** subito dopo il messaggio hello è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="d2c51-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="d2c51-153">Modificare il contenuto di hello di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="d2c51-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="d2c51-154">È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello chiamando **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="d2c51-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="d2c51-155">Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="d2c51-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="d2c51-156">Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e imposta tooextend timeout di visibilità hello un'altra 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="d2c51-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="d2c51-157">In questo modo lo stato di hello del lavoro che è associata a messaggi hello e offre un'altra toocontinue minuto lavorando messaggio hello al client hello.</span><span class="sxs-lookup"><span data-stu-id="d2c51-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="d2c51-158">È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="d2c51-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="d2c51-159">In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare.</span><span class="sxs-lookup"><span data-stu-id="d2c51-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d2c51-160">In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="d2c51-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="d2c51-161">Opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="d2c51-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="d2c51-162">È possibile personalizzare il recupero di messaggi da una coda in due modi.</span><span class="sxs-lookup"><span data-stu-id="d2c51-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d2c51-163">In primo luogo, è possibile ottenere un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="d2c51-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="d2c51-164">In secondo luogo, è possibile impostare un timeout di visibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="d2c51-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="d2c51-165">esempio di codice seguente Hello utilizza hello **getMessages** messaggi tooget 16 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="d2c51-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="d2c51-166">Quindi, ogni messaggio viene elaborato con un ciclo **for** .</span><span class="sxs-lookup"><span data-stu-id="d2c51-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="d2c51-167">Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="d2c51-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="d2c51-168">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="d2c51-168">Get queue length</span></span>
<span data-ttu-id="d2c51-169">È possibile ottenere una stima del numero di hello dei messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="d2c51-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="d2c51-170">Hello **QueueRestProxy -> getQueueMetadata** metodo richiede metadati tooreturn di hello coda del servizio sulla coda hello.</span><span class="sxs-lookup"><span data-stu-id="d2c51-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="d2c51-171">Chiamare il metodo hello **getApproximateMessageCount** metodo su hello ha restituito l'oggetto fornisce un conteggio del numero di messaggi è in una coda.</span><span class="sxs-lookup"><span data-stu-id="d2c51-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="d2c51-172">conteggio Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo che il servizio di Accodamento di hello risponde tooyour richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2c51-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="d2c51-173">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="d2c51-173">Delete a queue</span></span>
<span data-ttu-id="d2c51-174">chiamate di una coda e tutti i messaggi hello in essa contenuti, toodelete hello **QueueRestProxy -> deleteQueue** metodo.</span><span class="sxs-lookup"><span data-stu-id="d2c51-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d2c51-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2c51-175">Next steps</span></span>
<span data-ttu-id="d2c51-176">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code di Azure, seguire questi toolearn collegamenti sulle attività più complesse di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="d2c51-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="d2c51-177">Visitare hello [blog del Team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="d2c51-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="d2c51-178">Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d2c51-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

