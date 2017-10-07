---
title: Accoda aaaHow toouse Bus di servizio con PHP | Documenti Microsoft
description: Informazioni su come code di toouse Bus di servizio in Azure. Gli esempi di codice sono scritti in PHP.
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
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="182e2-104">La modalità di code toouse Bus di servizio con PHP</span><span class="sxs-lookup"><span data-stu-id="182e2-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="182e2-105">Questa guida illustra come toouse code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="182e2-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="182e2-106">esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="182e2-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="182e2-107">Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="182e2-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="182e2-108">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="182e2-108">Create a PHP application</span></span>
<span data-ttu-id="182e2-109">Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio Blob di Azure hello è hello che fanno riferimento a delle classi in hello [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="182e2-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="182e2-110">È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo, l'applicazione o il blocco note.</span><span class="sxs-lookup"><span data-stu-id="182e2-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="182e2-111">L'installazione di PHP deve inoltre disporre hello [estensione OpenSSL](http://php.net/openssl) installato e abilitato.</span><span class="sxs-lookup"><span data-stu-id="182e2-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="182e2-112">In questa guida si useranno le funzionalità del servizio che possono essere chiamate da un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="182e2-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="182e2-113">Recuperare le librerie client di Azure hello</span><span class="sxs-lookup"><span data-stu-id="182e2-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="182e2-114">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="182e2-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="182e2-115">coda di Service Bus hello toouse API, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="182e2-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="182e2-116">File di riferimento autoloader hello utilizzando hello [require_once] [ require_once] istruzione.</span><span class="sxs-lookup"><span data-stu-id="182e2-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="182e2-117">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="182e2-117">Reference any classes you might use.</span></span>

<span data-ttu-id="182e2-118">Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="182e2-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="182e2-119">In questo esempio (e altri esempi in questo articolo) presuppone installate le librerie Client di PHP hello per Azure tramite creazione.</span><span class="sxs-lookup"><span data-stu-id="182e2-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="182e2-120">Se è installato librerie hello manualmente o come un pacchetto di PERA, è necessario fare riferimento hello **WindowsAzure.php** autoloader file.</span><span class="sxs-lookup"><span data-stu-id="182e2-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="182e2-121">Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="182e2-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="182e2-122">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="182e2-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="182e2-123">tooinstantiate un client del Bus di servizio, è necessario disporre prima di tutto una stringa di connessione valido nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="182e2-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="182e2-124">Dove `Endpoint` è in genere in formato di hello `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="182e2-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="182e2-125">toocreate qualsiasi client di servizio di Azure, è necessario utilizzare hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="182e2-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="182e2-126">È possibile:</span><span class="sxs-lookup"><span data-stu-id="182e2-126">You can:</span></span>

* <span data-ttu-id="182e2-127">Passare la connessione hello tooit direttamente di stringa.</span><span class="sxs-lookup"><span data-stu-id="182e2-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="182e2-128">Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="182e2-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="182e2-129">Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="182e2-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="182e2-130">È possibile aggiungere nuove origini estendendo hello `ConnectionStringSource` classe</span><span class="sxs-lookup"><span data-stu-id="182e2-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="182e2-131">Per esempi di hello descritti di seguito, la stringa di connessione hello viene passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="182e2-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="182e2-132">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="182e2-132">Create a queue</span></span>
<span data-ttu-id="182e2-133">È possibile eseguire operazioni di gestione per le code del Bus di servizio tramite hello `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="182e2-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="182e2-134">Oggetto `ServiceBusRestProxy` oggetto viene costruito tramite hello `ServicesBuilder::createServiceBusService` metodo factory con una stringa di connessione appropriata che incapsula toomanage autorizzazioni token hello è.</span><span class="sxs-lookup"><span data-stu-id="182e2-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="182e2-135">Hello seguente esempio viene illustrato come tooinstantiate un `ServiceBusRestProxy` e chiamare `ServiceBusRestProxy->createQueue` toocreate una coda denominata `myqueue` all'interno di un `MySBNamespace` spazio dei nomi servizio:</span><span class="sxs-lookup"><span data-stu-id="182e2-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

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
> <span data-ttu-id="182e2-136">È possibile utilizzare hello `listQueues` metodo `ServiceBusRestProxy` oggetti toocheck se una coda con un nome specificato esiste già all'interno di uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="182e2-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="182e2-137">Messaggi tooa coda di invio</span><span class="sxs-lookup"><span data-stu-id="182e2-137">Send messages tooa queue</span></span>
<span data-ttu-id="182e2-138">una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `ServiceBusRestProxy->sendQueueMessage` metodo.</span><span class="sxs-lookup"><span data-stu-id="182e2-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="182e2-139">Hello seguente codice mostra come toosend toohello un messaggio `myqueue` coda creata in precedenza all'interno di `MySBNamespace` dello spazio dei nomi di servizio.</span><span class="sxs-lookup"><span data-stu-id="182e2-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="182e2-140">I messaggi inviate troppo (e ricevute da) code di Service Bus sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="182e2-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="182e2-141">[BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di metodi e proprietà che sono proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati applicazione arbitrari standard.</span><span class="sxs-lookup"><span data-stu-id="182e2-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="182e2-142">Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="182e2-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="182e2-143">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="182e2-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="182e2-144">Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda.</span><span class="sxs-lookup"><span data-stu-id="182e2-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="182e2-145">Il limite massimo della dimensione di una coda è di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="182e2-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="182e2-146">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="182e2-146">Receive messages from a queue</span></span>

<span data-ttu-id="182e2-147">migliore modalità tooreceive messaggi Hello da una coda è toouse un `ServiceBusRestProxy->receiveQueueMessage` metodo.</span><span class="sxs-lookup"><span data-stu-id="182e2-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="182e2-148">È possibile ricevere i messaggi in due modi diversi: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) e [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="182e2-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="182e2-149">**PeekLock** hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="182e2-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="182e2-150">Quando si utilizza [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modalità di ricezione è un'operazione singola cattura; vale a dire quando Bus di servizio riceve una richiesta di lettura per un messaggio in una coda, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="182e2-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="182e2-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="182e2-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="182e2-152">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="182e2-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="182e2-153">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="182e2-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="182e2-154">Predefinita hello [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modalità di ricezione di un messaggio diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="182e2-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="182e2-155">Quando Service Bus riceve una richiesta, trova hello successivo messaggio toobe utilizzata, blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="182e2-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="182e2-156">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione, passando il messaggio hello ricevuto troppo`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="182e2-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="182e2-157">Quando il Bus di servizio rileva hello `deleteMessage` chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="182e2-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="182e2-158">Hello seguente esempio viene illustrato come tooreceive ed elaborare un messaggio utilizzando [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modalità (hello predefinita).</span><span class="sxs-lookup"><span data-stu-id="182e2-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="182e2-159">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="182e2-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="182e2-160">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="182e2-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="182e2-161">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo sul messaggio ricevuto (anziché hello `deleteMessage` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="182e2-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="182e2-162">Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="182e2-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="182e2-163">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="182e2-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="182e2-164">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="182e2-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="182e2-165">Spesso si tratta di *almeno una volta che* l'elaborazione; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="182e2-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="182e2-166">Se hello scenario non tollera la doppia elaborazione, quindi l'aggiunta di ulteriori logica tooapplications toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="182e2-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="182e2-167">Questa operazione viene spesso eseguita utilizzando hello `getMessageId` metodo del messaggio hello, che rimane costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="182e2-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="182e2-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="182e2-168">Next steps</span></span>
<span data-ttu-id="182e2-169">Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="182e2-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="182e2-170">Per ulteriori informazioni, visitare anche hello [Centro sviluppatori PHP](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="182e2-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


