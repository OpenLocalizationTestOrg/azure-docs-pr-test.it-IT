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
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Come toouse l'archiviazione delle code da PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra come gli scenari comuni di tooperform usando hello servizio di archiviazione code di Azure. esempi di Hello vengono scritte tramite le classi da hello Windows SDK per PHP. Hello coperti scenari includono inserimento, visualizzazione, recupero e l'eliminazione di messaggi in coda, nonché creazione e l'eliminazione di code.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creare un'applicazione PHP
Hello solo requisito per la creazione di un'applicazione PHP che accede l'archiviazione delle code di Azure è hello che fanno riferimento a classi di hello Azure SDK per PHP all'interno del codice. È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo dell'applicazione, inclusi il blocco note.

In questa guida si useranno le funzionalità del Servizio di accodamento che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.

## <a name="get-hello-azure-client-libraries"></a>Recuperare le librerie Client di hello Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurare l'archiviazione delle code di tooaccess applicazione
hello toouse API per l'archiviazione delle code di Azure, è necessario:

1. File di riferimento hello autoloader utilizzando hello [require_once] istruzione.
2. Fare riferimento a tutte le eventuali classi utilizzabili.

Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServicesBuilder** classe.

> [!NOTE]
> In questo esempio (e altri esempi in questo articolo) si presuppone di aver installato le librerie Client di PHP hello per Azure tramite creazione. Se è stato installato manualmente le librerie di hello, sarà necessario tooreference hello `WindowsAzure.php` autoloader file.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo le classi di hello necessari per tooexecute esempio hello verranno fatto riferimento.

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
tooinstantiate un client di archiviazione della coda di Azure, è innanzitutto necessario una stringa di connessione valido. formato stringa di connessione del servizio coda hello Hello è come indicato di seguito.

Per accedere a un servizio attivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Per l'accesso all'archiviazione di emulatore hello:

```php
UseDevelopmentStorage=true
```

toocreate qualsiasi client del servizio di Azure, è necessario hello toouse **ServicesBuilder** classe. È possibile utilizzare una delle seguenti tecniche hello:

* Passare la connessione hello tooit direttamente di stringa.
* Utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:
  * Per impostazione predefinita, viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali
  * È possibile aggiungere nuove origini estendendo hello **ConnectionStringSource** classe.

Per esempi di hello descritti di seguito, la stringa di connessione hello verrà passata direttamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Creare una coda
Oggetto **QueueRestProxy** oggetto consente di creare una coda utilizzando hello **createQueue** metodo. Quando si crea una coda, è possibile impostare le opzioni nella coda di hello, ma non è necessario. (hello di esempio seguente viene illustrato come tooset metadati in una coda.)

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
> Non basarsi sulla distinzione maiuscole/minuscole nelle chiavi di metadati. Tutte le chiavi vengono lette dal servizio hello in lettere minuscole.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Aggiungere una coda di messaggi tooa
utilizzare una coda di messaggi tooa, tooadd **QueueRestProxy -> createMessage**. metodo Hello accetta il nome di coda hello, testo del messaggio hello e opzioni di messaggio (che sono facoltative).

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

## <a name="peek-at-hello-next-message"></a>Leggere il messaggio hello successivo
È possibile anche visualizzare un messaggio (o i messaggi) nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello chiamando **QueueRestProxy -> peekMessages**. Per impostazione predefinita, hello **peekMessage** metodo restituisce un singolo messaggio, ma è possibile modificare tale valore utilizzando hello **PeekMessagesOptions -> setNumberOfMessages** metodo.

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

## <a name="de-queue-hello-next-message"></a>Annullato l'accodamento messaggio successivo hello
Il codice consente di rimuovere un messaggio da una coda in due passaggi. In primo luogo, si chiama **QueueRestProxy -> listMessages**, rendendo hello messaggio invisibile tooany altro codice che legge dalla coda hello. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi. (Se il messaggio hello non viene eliminato in questo periodo di tempo, sarà nuovamente visibile nella coda di hello.) toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare **QueueRestProxy -> deleteMessage**. Questo processo in due passaggi della rimozione di un messaggio assicura che quando il tooprocess ha esito negativo di codice un messaggio a causa di un errore toohardware o software, un'altra istanza del codice è possibile ottenere hello stesso messaggio e provare nuovamente. Il codice chiama **deleteMessage** subito dopo il messaggio hello è stato elaborato.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Modificare il contenuto di hello di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello chiamando **QueueRestProxy -> updateMessage**. Se il messaggio hello rappresenta un'attività di lavoro, è possibile utilizzare questo stato hello tooupdate della funzionalità dell'attività di lavoro hello. Hello seguente codice aggiorna il messaggio di coda hello con nuovo contenuto e imposta tooextend timeout di visibilità hello un'altra 60 secondi. In questo modo lo stato di hello del lavoro che è associata a messaggi hello e offre un'altra toocontinue minuto lavorando messaggio hello al client hello. È possibile utilizzare flussi di lavoro di più passaggi tootrack questa tecnica per i messaggi della coda, senza la necessità di toostart dall'inizio di hello se un passaggio di elaborazione non riesce a causa di un errore toohardware o software. In genere, è consigliabile mantenere un numero di tentativi anche, e se hello messaggio viene ripetuto più  *n*  volte, è possibile eliminare. In questo modo è possibile evitare che un messaggio attivi un errore dell'applicazione ogni volta che viene elaborato.

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

## <a name="additional-options-for-de-queuing-messages"></a>Opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi. In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di visibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. esempio di codice seguente Hello utilizza hello **getMessages** messaggi tooget 16 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo **for** . Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.

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

## <a name="get-queue-length"></a>Recuperare la lunghezza della coda
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Hello **QueueRestProxy -> getQueueMetadata** metodo richiede metadati tooreturn di hello coda del servizio sulla coda hello. Chiamare il metodo hello **getApproximateMessageCount** metodo su hello ha restituito l'oggetto fornisce un conteggio del numero di messaggi è in una coda. conteggio Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo che il servizio di Accodamento di hello risponde tooyour richiesta.

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

## <a name="delete-a-queue"></a>Eliminare una coda
chiamate di una coda e tutti i messaggi hello in essa contenuti, toodelete hello **QueueRestProxy -> deleteQueue** metodo.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code di Azure, seguire questi toolearn collegamenti sulle attività più complesse di archiviazione:

* Visitare hello [blog del Team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).

Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

