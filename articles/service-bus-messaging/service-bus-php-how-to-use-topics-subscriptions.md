---
title: gli argomenti del Bus di servizio toouse aaaHow con PHP | Documenti Microsoft
description: Informazioni su come argomenti del Bus di servizio toouse con PHP in Azure.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="ca6e7-103">Il Bus di servizio toouse argomenti e sottoscrizioni con PHP</span><span class="sxs-lookup"><span data-stu-id="ca6e7-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ca6e7-104">In questo articolo illustra come toouse Bus di servizio di argomenti e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="ca6e7-105">esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="ca6e7-106">Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **invio argomento tooa messaggi**, **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="ca6e7-107">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="ca6e7-107">Create a PHP application</span></span>
<span data-ttu-id="ca6e7-108">Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio Blob di Azure hello è classi tooreference hello [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="ca6e7-109">È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo, l'applicazione o il blocco note.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="ca6e7-110">L'installazione di PHP deve inoltre disporre hello [estensione OpenSSL](http://php.net/openssl) installato e abilitato.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="ca6e7-111">In questo articolo viene descritto come toouse funzionalità che può essere chiamata all'interno di un'applicazione PHP in locale o nel codice in esecuzione all'interno di un ruolo web di Azure, un ruolo di lavoro o un sito Web del servizio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="ca6e7-112">Recuperare le librerie client di Azure hello</span><span class="sxs-lookup"><span data-stu-id="ca6e7-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="ca6e7-113">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ca6e7-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="ca6e7-114">hello toouse API del Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="ca6e7-115">File di riferimento autoloader hello utilizzando hello [require_once] [ require-once] istruzione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="ca6e7-116">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-116">Reference any classes you might use.</span></span>

<span data-ttu-id="ca6e7-117">Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServiceBusService** classe.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="ca6e7-118">In questo esempio (e altri esempi in questo articolo) presuppone installate le librerie Client di PHP hello per Azure tramite creazione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="ca6e7-119">Se è installato librerie hello manualmente o come un pacchetto di PERA, è necessario fare riferimento hello **WindowsAzure.php** autoloader file.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="ca6e7-120">In hello seguono esempi, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="ca6e7-121">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="ca6e7-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="ca6e7-122">tooinstantiate un client del Bus di servizio è necessario avere una stringa di connessione valido nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="ca6e7-123">Dove `Endpoint` è in genere in formato di hello `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="ca6e7-124">toocreate qualsiasi client di servizio di Azure, è necessario utilizzare hello `ServicesBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="ca6e7-125">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-125">You can:</span></span>

* <span data-ttu-id="ca6e7-126">Passare la connessione hello tooit direttamente di stringa.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="ca6e7-127">Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="ca6e7-128">Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="ca6e7-129">È possibile aggiungere nuove origini estendendo hello `ConnectionStringSource` classe.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="ca6e7-130">Per esempi di hello descritti di seguito, la stringa di connessione hello viene passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="ca6e7-131">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="ca6e7-131">Create a topic</span></span>
<span data-ttu-id="ca6e7-132">È possibile eseguire operazioni di gestione per gli argomenti del Bus di servizio tramite hello `ServiceBusRestProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="ca6e7-133">Oggetto `ServiceBusRestProxy` oggetto viene costruito tramite hello `ServicesBuilder::createServiceBusService` metodo factory con una stringa di connessione appropriata che incapsula toomanage autorizzazioni token hello è.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="ca6e7-134">Hello seguente esempio viene illustrato come tooinstantiate un `ServiceBusRestProxy` e chiamare `ServiceBusRestProxy->createTopic` toocreate un argomento denominato `mytopic` all'interno di un `MySBNamespace` dello spazio dei nomi:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> <span data-ttu-id="ca6e7-135">È possibile utilizzare hello `listTopics` metodo `ServiceBusRestProxy` oggetti toocheck se un argomento con un nome specificato esiste già all'interno di uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="ca6e7-136">Creare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ca6e7-136">Create a subscription</span></span>
<span data-ttu-id="ca6e7-137">Le sottoscrizioni dell'argomento vengono inoltre create con hello `ServiceBusRestProxy->createSubscription` metodo.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="ca6e7-138">Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi passati coda virtuale toohello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ca6e7-139">Creare una sottoscrizione con filtro predefinito (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="ca6e7-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ca6e7-140">Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ca6e7-141">Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="ca6e7-142">esempio Hello crea una sottoscrizione denominata 'mysubscription' e utilizza hello predefinito **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ca6e7-143">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="ca6e7-143">Create subscriptions with filters</span></span>
<span data-ttu-id="ca6e7-144">È inoltre possibile impostare i filtri che consentono di toospecify cui i messaggi inviati tooa argomento deve trovarsi all'interno di una sottoscrizione di argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="ca6e7-145">tipo di filtro supportato dalle sottoscrizioni più flessibile Hello è hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="ca6e7-146">I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ca6e7-147">Per altre informazioni su SqlFilters, vedere la sezione relativa alla [proprietà SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="ca6e7-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="ca6e7-148">Ogni regola su una sottoscrizione elabora i messaggi in ingresso in modo indipendente, aggiungere la sottoscrizione a pagamento risultato toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="ca6e7-149">Inoltre, ogni nuova sottoscrizione ha un valore predefinito **regola** oggetto con un filtro che consente di aggiungere tutti i messaggi dalla sottoscrizione di toohello argomento hello.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="ca6e7-150">tooreceive solo i messaggi che corrispondono al filtro, è necessario rimuovere la regola predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="ca6e7-151">È possibile rimuovere una regola predefinita hello utilizzando hello `ServiceBusRestProxy->deleteRule` metodo.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="ca6e7-152">esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `MessageNumber` maggiore di 3.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="ca6e7-153">Vedere [argomento tooa di trasmissione messaggi](#send-messages-to-a-topic) per informazioni sull'aggiunta di proprietà personalizzate toomessages.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="ca6e7-154">Si noti che questo codice richiede l'uso di hello di uno spazio dei nomi aggiuntivo: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="ca6e7-155">Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un `SqlFilter` che seleziona solo i messaggi che hanno un `MessageNumber` proprietà minore o uguale too3.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="ca6e7-156">A questo punto, quando viene inviato un messaggio toohello `mytopic` argomento, viene sempre recapitato tooreceivers sottoscritto toohello `mysubscription` sottoscrizione e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` (sottoscrizioni in base al contenuto del messaggio hello).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="ca6e7-157">Inviare l'argomento tooa messaggi</span><span class="sxs-lookup"><span data-stu-id="ca6e7-157">Send messages tooa topic</span></span>
<span data-ttu-id="ca6e7-158">un argomento del Bus di servizio tooa messaggio toosend, l'applicazione chiama hello `ServiceBusRestProxy->sendTopicMessage` metodo.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="ca6e7-159">Hello seguente codice mostra come toosend toohello un messaggio `mytopic` argomento creato in precedenza all'interno di `MySBNamespace` dello spazio dei nomi di servizio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

<span data-ttu-id="ca6e7-160">I messaggi inviati gli argomenti del Bus tooService sono istanze di hello [BrokeredMessage] [ BrokeredMessage] classe.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="ca6e7-161">[BrokeredMessage] [ BrokeredMessage] oggetti dispongono di un set di metodi e proprietà standard, nonché le proprietà che possono essere proprietà specifiche dell'applicazione personalizzate toohold utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="ca6e7-162">Hello esempio seguente viene illustrato come test toosend 5 messaggi toohello `mytopic` argomento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="ca6e7-163">Hello `setProperty` metodo è usato tooadd una proprietà personalizzata (`MessageNumber`) tooeach messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="ca6e7-164">Si noti che hello `MessageNumber` valore della proprietà varia per ogni messaggio (è possibile utilizzare questo valore toodetermine ricevano le sottoscrizioni, come illustrato nell'hello [creare una sottoscrizione](#create-a-subscription) sezione):</span><span class="sxs-lookup"><span data-stu-id="ca6e7-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="ca6e7-165">Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ca6e7-166">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ca6e7-167">Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ca6e7-168">Il limite massimo delle dimensioni di un argomento è 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="ca6e7-169">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="ca6e7-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ca6e7-170">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ca6e7-170">Receive messages from a subscription</span></span>
<span data-ttu-id="ca6e7-171">migliore modalità tooreceive messaggi Hello da una sottoscrizione è toouse un `ServiceBusRestProxy->receiveSubscriptionMessage` metodo.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="ca6e7-172">Le modalità di ricezione dei messaggi sono due: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="ca6e7-173">**PeekLock** hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="ca6e7-174">Quando si utilizza hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) , la modalità di ricezione è un'operazione singola cattura; ovvero quando il Bus di servizio riceve una richiesta di lettura per un messaggio in una sottoscrizione, contrassegna il messaggio hello come usato e lo restituisce toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="ca6e7-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modalità modello più semplice di hello ed è adatta per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ca6e7-176">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ca6e7-177">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ca6e7-178">Predefinita hello [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità di ricezione di un messaggio diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ca6e7-179">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ca6e7-180">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello processo di ricezione, passando il messaggio hello ricevuto troppo`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="ca6e7-181">Quando il Bus di servizio rileva hello `deleteMessage` chiamata, verrà contrassegnare il messaggio hello come usato e rimuoverlo dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="ca6e7-182">Hello seguente esempio viene illustrato come tooreceive ed elaborare un messaggio utilizzando [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modalità (hello predefinita).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ca6e7-183">Procedura: Gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="ca6e7-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ca6e7-184">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ca6e7-185">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo sul messaggio ricevuto (anziché hello `deleteMessage` (metodo)).</span><span class="sxs-lookup"><span data-stu-id="ca6e7-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="ca6e7-186">Ciò causerà messaggio hello toounlock di Bus di servizio all'interno di coda hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ca6e7-187">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima hello scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello automaticamente e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="ca6e7-188">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` richiesta inviata, quindi messaggio hello sarà applicazione toohello consegnati nuovamente quando viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ca6e7-189">Spesso si tratta di *almeno una volta che* l'elaborazione; ovvero, ogni messaggio viene elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ca6e7-190">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tooapplications toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="ca6e7-191">Questa operazione viene spesso eseguita utilizzando hello `getMessageId` metodo del messaggio hello, che rimane costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ca6e7-192">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="ca6e7-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="ca6e7-193">toodelete un argomento o una sottoscrizione, utilizzare hello `ServiceBusRestProxy->deleteTopic` o hello `ServiceBusRestProxy->deleteSubscripton` metodi, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="ca6e7-194">Si noti che anche l'eliminazione di un argomento Elimina le sottoscrizioni che sono registrate con l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="ca6e7-195">Hello esempio seguente viene illustrato come toodelete un argomento denominato `mytopic` e le relative sottoscrizioni registrate.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

<span data-ttu-id="ca6e7-196">Utilizzando hello `deleteSubscription` metodo, è possibile eliminare una sottoscrizione in modo indipendente:</span><span class="sxs-lookup"><span data-stu-id="ca6e7-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="ca6e7-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca6e7-197">Next steps</span></span>
<span data-ttu-id="ca6e7-198">Dopo aver appreso nozioni di base di hello di code del Bus di servizio, vedere [code, argomenti e sottoscrizioni] [ Queues, topics, and subscriptions] per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="ca6e7-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
