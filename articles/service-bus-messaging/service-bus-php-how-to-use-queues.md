---
title: Come usare le code del bus di servizio con PHP | Microsoft Docs
description: Informazioni su come usare le code del bus di servizio in Azure. Gli esempi di codice sono scritti in PHP.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3514812f7f087582035dad5d9a4d620652aa4da9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-php"></a><span data-ttu-id="e3d69-104">Come usare le code del bus di servizio con PHP</span><span class="sxs-lookup"><span data-stu-id="e3d69-104">How to use Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="e3d69-105">Questa guida illustra come usare le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="e3d69-105">This guide shows you how to use Service Bus queues.</span></span> <span data-ttu-id="e3d69-106">Gli esempi sono scritti in PHP e usano [Azure SDK per PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e3d69-106">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="e3d69-107">Gli scenari presentati includono **la creazione di code**, **l'invio e la ricezione di messaggi** e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="e3d69-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e3d69-108">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="e3d69-108">Create a PHP application</span></span>
<span data-ttu-id="e3d69-109">Per creare un'applicazione PHP che acceda al servizio BLOB di Azure, è sufficiente fare riferimento alle classi in [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="e3d69-109">The only requirement for creating a PHP application that accesses the Azure Blob service is the referencing of classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="e3d69-110">Per creare l'applicazione, è possibile usare qualsiasi strumento di sviluppo o il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="e3d69-110">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d69-111">L'installazione di PHP deve avere anche l'[estensione OpenSSL](http://php.net/openssl) installata e abilitata.</span><span class="sxs-lookup"><span data-stu-id="e3d69-111">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="e3d69-112">In questa guida si useranno le funzionalità del servizio che possono essere chiamate da un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d69-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="e3d69-113">Acquisire le librerie client di Azure</span><span class="sxs-lookup"><span data-stu-id="e3d69-113">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="e3d69-114">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e3d69-114">Configure your application to use Service Bus</span></span>
<span data-ttu-id="e3d69-115">Per usare le API delle code del bus di servizio, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="e3d69-115">To use the Service Bus queue APIs, do the following:</span></span>

1. <span data-ttu-id="e3d69-116">Fare riferimento al file autoloader mediante l'istruzione [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="e3d69-116">Reference the autoloader file using the [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="e3d69-117">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="e3d69-117">Reference any classes you might use.</span></span>

<span data-ttu-id="e3d69-118">Nell'esempio seguente viene indicato come includere il file autoloader e fare riferimento alla classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-118">The following example shows how to include the autoloader file and reference the `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d69-119">Questo esempio (e in altri esempi in questo articolo) presuppone che siano state installate le librerie client PHP per Azure tramite Composer.</span><span class="sxs-lookup"><span data-stu-id="e3d69-119">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e3d69-120">Se le librerie sono state installate manualmente o come pacchetto PEAR, è necessario fare riferimento al file autoloader **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="e3d69-120">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="e3d69-121">Nei seguenti esempi l'istruzione `require_once` verrà sempre visualizzata, ma si fa riferimento solo alle classi necessarie per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e3d69-121">In the examples below, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="e3d69-122">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="e3d69-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="e3d69-123">Per creare un'istanza di un client del bus di servizio, è necessario innanzitutto disporre di una stringa di connessione valida nel seguente formato:</span><span class="sxs-lookup"><span data-stu-id="e3d69-123">To instantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="e3d69-124">Dove `Endpoint` è in genere nel formato `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-124">Where `Endpoint` is typically of the format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="e3d69-125">Per creare un client del servizio Azure, è necessario usare la classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-125">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="e3d69-126">È possibile:</span><span class="sxs-lookup"><span data-stu-id="e3d69-126">You can:</span></span>

* <span data-ttu-id="e3d69-127">Passare la stringa di connessione direttamente.</span><span class="sxs-lookup"><span data-stu-id="e3d69-127">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="e3d69-128">utilizzare **CloudConfigurationManager (CCM)** per cercare la stringa di connessione in più origini esterne:</span><span class="sxs-lookup"><span data-stu-id="e3d69-128">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="e3d69-129">Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="e3d69-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="e3d69-130">È possibile aggiungere nuove origini estendendo la classe `ConnectionStringSource`</span><span class="sxs-lookup"><span data-stu-id="e3d69-130">You can add new sources by extending the `ConnectionStringSource` class</span></span>

<span data-ttu-id="e3d69-131">Per gli esempi illustrati in questo articolo, la stringa di connessione viene passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="e3d69-131">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="e3d69-132">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="e3d69-132">Create a queue</span></span>
<span data-ttu-id="e3d69-133">È possibile eseguire operazioni di gestione per le code del bus di servizio usando la classe `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-133">You can perform management operations for Service Bus queues via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="e3d69-134">Un oggetto `ServiceBusRestProxy` è costruito tramite il metodo factory `ServicesBuilder::createServiceBusService` con una stringa di connessione appropriata che incapsula le autorizzazioni di token per gestirlo.</span><span class="sxs-lookup"><span data-stu-id="e3d69-134">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="e3d69-135">L'esempio seguente mostra come creare un'istanza di `ServiceBusRestProxy` e chiamare il metodo `ServiceBusRestProxy->createQueue` per creare una coda denominata `myqueue` in uno spazio dei nomi del servizio `MySBNamespace`:</span><span class="sxs-lookup"><span data-stu-id="e3d69-135">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` to create a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="e3d69-136">È possibile usare il metodo `listQueues` negli oggetti `ServiceBusRestProxy` per verificare se in uno spazio dei nomi esiste già una coda con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="e3d69-136">You can use the `listQueues` method on `ServiceBusRestProxy` objects to check if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="e3d69-137">Inviare messaggi a una coda</span><span class="sxs-lookup"><span data-stu-id="e3d69-137">Send messages to a queue</span></span>
<span data-ttu-id="e3d69-138">Per inviare un messaggio a una coda del bus di servizio, l'applicazione chiama il metodo `ServiceBusRestProxy->sendQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-138">To send a message to a Service Bus queue, your application calls the `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="e3d69-139">Il seguente codice illustra come inviare un messaggio alla coda `myqueue` creata in precedenza all'interno dello spazio dei nomi del servizio `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-139">The following code shows how to send a message to the `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e3d69-140">I messaggi inviati e ricevuti dalle code del bus di servizio sono istanze della classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="e3d69-140">Messages sent to (and received from ) Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="e3d69-141">Gli oggetti [BrokeredMessage][BrokeredMessage] includono un set di proprietà e metodi standard usati per contenere le proprietà personalizzate specifiche dell'applicazione e un corpo di dati arbitrari dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3d69-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used to hold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="e3d69-142">Le code del bus di servizio supportano messaggi di dimensioni massime pari a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e pari a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e3d69-142">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e3d69-143">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="e3d69-143">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e3d69-144">Non esiste alcun limite al numero di messaggi mantenuti in una coda, mentre è prevista una limitazione alla dimensione totale dei messaggi di una coda.</span><span class="sxs-lookup"><span data-stu-id="e3d69-144">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="e3d69-145">Il limite massimo della dimensione di una coda è di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="e3d69-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="e3d69-146">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="e3d69-146">Receive messages from a queue</span></span>

<span data-ttu-id="e3d69-147">Il modo ideale per ricevere i messaggi da una coda prevede l'uso di un metodo `ServiceBusRestProxy->receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-147">The best way to receive messages from a queue is to use a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="e3d69-148">È possibile ricevere i messaggi in due modi diversi: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="e3d69-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="e3d69-149">**PeekLock** è la modalità predefinita.</span><span class="sxs-lookup"><span data-stu-id="e3d69-149">**PeekLock** is the default.</span></span>

<span data-ttu-id="e3d69-150">Quando si usa la modalità [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete), l'operazione di ricezione viene eseguita in un'unica fase. Quando infatti il bus di servizio riceve una richiesta di lettura per un messaggio in una coda, lo contrassegna come utilizzato e lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3d69-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="e3d69-151">La modalità [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) costituisce il modello più semplice ed è adatta per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="e3d69-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="e3d69-152">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e3d69-152">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="e3d69-153">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="e3d69-153">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="e3d69-154">Nella modalità [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) predefinita l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="e3d69-154">In the default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e3d69-155">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da utilizzare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3d69-155">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="e3d69-156">Dopo aver elaborato il messaggio, o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione completa la seconda fase del processo di ricezione passando il messaggio ricevuto a `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="e3d69-156">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="e3d69-157">Quando il bus di servizio vede la chiamata `deleteMessage`, contrassegna il messaggio come utilizzato e lo rimuove dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e3d69-157">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="e3d69-158">L'esempio seguente illustra come ricevere ed elaborare un messaggio usando la modalità [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) (predefinita).</span><span class="sxs-lookup"><span data-stu-id="e3d69-158">The following example shows how to receive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (the default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set the receive mode to PeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e3d69-159">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e3d69-159">How to handle application crashes and unreadable messages</span></span>

<span data-ttu-id="e3d69-160">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="e3d69-160">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e3d69-161">Se un'applicazione ricevente non è in grado di elaborare il messaggio per un qualsiasi motivo, può chiamare il metodo `unlockMessage` anziché `deleteMessage` sul messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="e3d69-161">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="e3d69-162">In questo modo, il bus di servizio sbloccherà il messaggio nella coda rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="e3d69-162">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e3d69-163">Al messaggio bloccato nella coda è inoltre associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="e3d69-163">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="e3d69-164">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio, ma prima dell'invio della richiesta `deleteMessage`, il messaggio verrà nuovamente recapitato all'applicazione al riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="e3d69-164">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="e3d69-165">Questo processo di elaborazione viene spesso definito di tipo *At-Least-Once*, per indicare che ogni messaggio verrà elaborato almeno una volta, ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="e3d69-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="e3d69-166">Se lo scenario non tollera la doppia elaborazione,è consigliabile aggiungere logica aggiuntiva alle applicazioni per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="e3d69-166">If the scenario cannot tolerate duplicate processing, then adding additional logic to applications to handle duplicate message delivery is recommended.</span></span> <span data-ttu-id="e3d69-167">A tale scopo viene spesso usato il metodo `getMessageId` del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="e3d69-167">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3d69-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3d69-168">Next steps</span></span>
<span data-ttu-id="e3d69-169">A questo punto, dopo aver appreso le nozioni di base delle code del bus di servizio, vedere [Code, argomenti e sottoscrizioni][Queues, topics, and subscriptions] per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="e3d69-169">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="e3d69-170">Per altre informazioni, vedere anche il [Centro per sviluppatori PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e3d69-170">For more information, also visit the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


