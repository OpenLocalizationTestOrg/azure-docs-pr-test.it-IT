---
title: Come usare gli argomenti del bus di servizio con PHP | Documentazione Microsoft
description: Informazioni su come usare gli argomenti del bus di servizio con PHP in Azure.
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
ms.openlocfilehash: afa9efcb6335786198021ec81dd087287c39bda9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="5cb50-103">Come usare gli argomenti e le sottoscrizioni del bus di servizio con PHP</span><span class="sxs-lookup"><span data-stu-id="5cb50-103">How to use Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="5cb50-104">In questo articolo verrà descritto come usare gli argomenti e le sottoscrizioni del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-104">This article shows you how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="5cb50-105">Gli esempi sono scritti in PHP e usano [Azure SDK per PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5cb50-105">The samples are written in PHP and use the [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="5cb50-106">Gli scenari presentati includono **la creazione di argomenti e sottoscrizioni**, **la creazione di filtri per le sottoscrizioni**, **l’invio di messaggi a un argomento**, **la ricezione di messaggi da una sottoscrizione** e **l’eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="5cb50-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="5cb50-107">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="5cb50-107">Create a PHP application</span></span>
<span data-ttu-id="5cb50-108">Per creare un'applicazione PHP che acceda al servizio BLOB di Azure, è sufficiente fare riferimento alle classi in [Azure SDK per PHP](../php-download-sdk.md) dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="5cb50-108">The only requirement for creating a PHP application that accesses the Azure Blob service is to reference classes in the [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="5cb50-109">Per creare l'applicazione, è possibile usare qualsiasi strumento di sviluppo o il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="5cb50-109">You can use any development tools to create your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb50-110">L'installazione di PHP deve avere anche l'[estensione OpenSSL](http://php.net/openssl) installata e abilitata.</span><span class="sxs-lookup"><span data-stu-id="5cb50-110">Your PHP installation must also have the [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="5cb50-111">Questo articolo illustra come usare le funzionalità del servizio che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb50-111">This article describes how to use service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="5cb50-112">Acquisire le librerie client di Azure</span><span class="sxs-lookup"><span data-stu-id="5cb50-112">Get the Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="5cb50-113">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5cb50-113">Configure your application to use Service Bus</span></span>
<span data-ttu-id="5cb50-114">Per usare le API del bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="5cb50-114">To use the Service Bus APIs:</span></span>

1. <span data-ttu-id="5cb50-115">Fare riferimento al file autoloader mediante l'istruzione [require_once][require-once].</span><span class="sxs-lookup"><span data-stu-id="5cb50-115">Reference the autoloader file using the [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="5cb50-116">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="5cb50-116">Reference any classes you might use.</span></span>

<span data-ttu-id="5cb50-117">Nell'esempio seguente viene indicato come includere il file autoloader e fare riferimento alla classe **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="5cb50-117">The following example shows how to include the autoloader file and reference the **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb50-118">Questo esempio (e in altri esempi in questo articolo) presuppone che siano state installate le librerie client PHP per Azure tramite Composer.</span><span class="sxs-lookup"><span data-stu-id="5cb50-118">This example (and other examples in this article) assumes you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="5cb50-119">Se le librerie sono state installate manualmente o come pacchetto PEAR, è necessario fare riferimento al file autoloader **WindowsAzure.php**.</span><span class="sxs-lookup"><span data-stu-id="5cb50-119">If you installed the libraries manually or as a PEAR package, you must reference the **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="5cb50-120">Nei seguenti esempi l'istruzione `require_once` verrà sempre visualizzata, ma si fa riferimento solo alle classi necessarie per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-120">In the following examples, the `require_once` statement will always be shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="5cb50-121">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5cb50-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="5cb50-122">Per creare un'istanza di un client del bus di servizio, è necessario innanzitutto disporre di una stringa di connessione valida nel seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5cb50-122">To instantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="5cb50-123">Dove `Endpoint` è in genere nel formato `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-123">Where `Endpoint` is typically of the format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="5cb50-124">Per creare un client del servizio Azure, è necessario usare la classe `ServicesBuilder`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-124">To create any Azure service client you must use the `ServicesBuilder` class.</span></span> <span data-ttu-id="5cb50-125">È possibile:</span><span class="sxs-lookup"><span data-stu-id="5cb50-125">You can:</span></span>

* <span data-ttu-id="5cb50-126">Passare la stringa di connessione direttamente.</span><span class="sxs-lookup"><span data-stu-id="5cb50-126">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="5cb50-127">utilizzare **CloudConfigurationManager (CCM)** per cercare la stringa di connessione in più origini esterne:</span><span class="sxs-lookup"><span data-stu-id="5cb50-127">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="5cb50-128">Per impostazione predefinita viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali.</span><span class="sxs-lookup"><span data-stu-id="5cb50-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="5cb50-129">È possibile aggiungere nuove origini estendendo la classe `ConnectionStringSource`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-129">You can add new sources by extending the `ConnectionStringSource` class.</span></span>

<span data-ttu-id="5cb50-130">Per gli esempi illustrati in questo articolo, la stringa di connessione viene passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="5cb50-130">For the examples outlined here, the connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="5cb50-131">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="5cb50-131">Create a topic</span></span>
<span data-ttu-id="5cb50-132">È possibile eseguire operazioni di gestione per gli argomenti del bus di servizio usando la classe `ServiceBusRestProxy`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-132">You can perform management operations for Service Bus topics via the `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="5cb50-133">Un oggetto `ServiceBusRestProxy` è costruito tramite il metodo factory `ServicesBuilder::createServiceBusService` con una stringa di connessione appropriata che incapsula le autorizzazioni di token per gestirlo.</span><span class="sxs-lookup"><span data-stu-id="5cb50-133">A `ServiceBusRestProxy` object is constructed via the `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates the token permissions to manage it.</span></span>

<span data-ttu-id="5cb50-134">L'esempio seguente mostra come creare un'istanza di `ServiceBusRestProxy` e chiamare il metodo `ServiceBusRestProxy->createTopic` per creare un argomento denominato `mytopic` in uno spazio dei nomi `MySBNamespace`:</span><span class="sxs-lookup"><span data-stu-id="5cb50-134">The following example shows how to instantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` to create a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

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
> <span data-ttu-id="5cb50-135">È possibile usare il metodo `listTopics` negli oggetti `ServiceBusRestProxy` per verificare se in uno spazio dei nomi del servizio esiste già un argomento con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="5cb50-135">You can use the `listTopics` method on `ServiceBusRestProxy` objects to check if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="5cb50-136">Creare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5cb50-136">Create a subscription</span></span>
<span data-ttu-id="5cb50-137">È possibile creare le sottoscrizioni di un argomento con il metodo `ServiceBusRestProxy->createSubscription`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-137">Topic subscriptions are also created with the `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="5cb50-138">Le sottoscrizioni sono denominate e possono includere un filtro facoltativo che limita l'insieme dei messaggi passati alla coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-138">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="5cb50-139">Creare una sottoscrizione con il filtro (MatchAll) predefinito</span><span class="sxs-lookup"><span data-stu-id="5cb50-139">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="5cb50-140">Il filtro **MatchAll** è il filtro predefinito e viene usato se non vengono specificati altri filtri durante la creazione di una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-140">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="5cb50-141">Quando si usa il filtro **MatchAll**, tutti i messaggi pubblicati nell'argomento vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-141">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="5cb50-142">Nell'esempio seguente viene creata una sottoscrizione denominata 'mysubscription' e viene usato il filtro predefinito **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="5cb50-142">The following example creates a subscription named 'mysubscription' and uses the default **MatchAll** filter.</span></span>

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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="5cb50-143">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="5cb50-143">Create subscriptions with filters</span></span>
<span data-ttu-id="5cb50-144">È anche possibile configurare filtri che consentono di specificare quali messaggi inviati a un argomento devono essere presenti in una specifica sottoscrizione dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="5cb50-144">You can also set up filters that enable you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="5cb50-145">Il tipo di filtro più flessibile tra quelli supportati dalle sottoscrizioni è [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="5cb50-145">The most flexible type of filter supported by subscriptions is the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="5cb50-146">I filtri SQL agiscono sulle proprietà dei messaggi pubblicati nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="5cb50-146">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="5cb50-147">Per altre informazioni su SqlFilters, vedere la sezione relativa alla [proprietà SqlFilter.SqlExpression][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="5cb50-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="5cb50-148">Ogni regola in una sottoscrizione elabora i messaggi in arrivo indipendentemente, aggiungendo i messaggi risultanti alla sottoscrizione stessa.</span><span class="sxs-lookup"><span data-stu-id="5cb50-148">Each rule on a subscription processes incoming messages independently, adding their result messages to the subscription.</span></span> <span data-ttu-id="5cb50-149">Ogni nuova sottoscrizione presenta anche un oggetto **Rule** predefinito con un filtro che aggiunge tutti i messaggi dall'argomento alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from the topic to the subscription.</span></span> <span data-ttu-id="5cb50-150">Per ricevere solo messaggi corrispondenti al filtro in uso, è necessario rimuovere la regola predefinita.</span><span class="sxs-lookup"><span data-stu-id="5cb50-150">To receive only messages matching your filter, you must remove the default rule.</span></span> <span data-ttu-id="5cb50-151">È possibile rimuovere la regola predefinita usando il metodo `ServiceBusRestProxy->deleteRule`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-151">You can remove the default rule by using the `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="5cb50-152">L'esempio seguente crea una sottoscrizione denominata `HighMessages` con un filtro **SqlFilter** che seleziona solo i messaggi in cui il valore della proprietà `MessageNumber` personalizzata è maggiore di 3.</span><span class="sxs-lookup"><span data-stu-id="5cb50-152">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="5cb50-153">Per informazioni su come aggiungere proprietà personalizzate ai messaggi, vedere [Inviare messaggi a un argomento](#send-messages-to-a-topic).</span><span class="sxs-lookup"><span data-stu-id="5cb50-153">See [Send messages to a topic](#send-messages-to-a-topic) for information about adding custom properties to messages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="5cb50-154">Si noti che questo codice richiede l'uso di uno spazio dei nomi aggiuntivo: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-154">Note that this code requires the use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="5cb50-155">Analogamente, l'esempio seguente crea una sottoscrizione denominata `LowMessages` con un filtro `SqlFilter` che seleziona solo i messaggi in cui il valore della proprietà `MessageNumber` è minore o uguale a 3.</span><span class="sxs-lookup"><span data-stu-id="5cb50-155">Similarly, the following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal to 3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="5cb50-156">A questo punto, quando viene inviato un messaggio all'argomento `mytopic`, viene sempre recapitato ai ricevitori con sottoscrizione `mysubscription` e recapitato selettivamente ai ricevitori con sottoscrizioni `HighMessages` e `LowMessages`, a seconda del contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-156">Now, when a message is sent to the `mytopic` topic, it is always delivered to receivers subscribed to the `mysubscription` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="5cb50-157">Inviare messaggi a un argomento</span><span class="sxs-lookup"><span data-stu-id="5cb50-157">Send messages to a topic</span></span>
<span data-ttu-id="5cb50-158">Per inviare un messaggio a un argomento del bus di servizio, l'applicazione chiama il metodo `ServiceBusRestProxy->sendTopicMessage`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-158">To send a message to a Service Bus topic, your application calls the `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="5cb50-159">Il codice seguente illustra come inviare un messaggio all'argomento `mytopic` creato prima nello spazio dei nomi del servizio `MySBNamespace`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-159">The following code shows how to send a message to the `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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

<span data-ttu-id="5cb50-160">I messaggi inviati ad argomenti del bus di servizio sono istanze della classe [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="5cb50-160">Messages sent to Service Bus topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5cb50-161">Gli oggetti [BrokeredMessage][BrokeredMessage] includono un set di proprietà e metodi standard, nonché proprietà usate per contenere proprietà personalizzate specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used to hold custom application-specific properties.</span></span> <span data-ttu-id="5cb50-162">L'esempio seguente illustra come inviare 5 messaggi di prova all'argomento `mytopic` creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5cb50-162">The following example shows how to send 5 test messages to the `mytopic` topic previously created.</span></span> <span data-ttu-id="5cb50-163">Il metodo `setProperty` viene usato per aggiungere una proprietà personalizzata (`MessageNumber`) a ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-163">The `setProperty` method is used to add a custom property (`MessageNumber`) to each message.</span></span> <span data-ttu-id="5cb50-164">Si noti che il valore della proprietà `MessageNumber` varia per ogni messaggio, consentendo di determinare quali sottoscrizioni lo riceveranno, come descritto nella sezione [Creare una sottoscrizione](#create-a-subscription):</span><span class="sxs-lookup"><span data-stu-id="5cb50-164">Note that the `MessageNumber` property value varies on each message (you can use this value to determine which subscriptions receive it, as shown in the [Create a subscription](#create-a-subscription) section):</span></span>

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

<span data-ttu-id="5cb50-165">Gli argomenti del bus di servizio supportano messaggi di dimensioni massime pari a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e pari a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5cb50-165">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5cb50-166">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="5cb50-166">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5cb50-167">Non esiste alcun limite al numero di messaggi mantenuti in un argomento, mentre è prevista una limitazione alla dimensione totale dei messaggi di un argomento.</span><span class="sxs-lookup"><span data-stu-id="5cb50-167">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="5cb50-168">Il limite massimo delle dimensioni di un argomento è 5 GB.</span><span class="sxs-lookup"><span data-stu-id="5cb50-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="5cb50-169">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="5cb50-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="5cb50-170">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5cb50-170">Receive messages from a subscription</span></span>
<span data-ttu-id="5cb50-171">Il modo ideale per ricevere i messaggi da una sottoscrizione prevede l'uso di un metodo `ServiceBusRestProxy->receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-171">The best way to receive messages from a subscription is to use a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="5cb50-172">Le modalità di ricezione dei messaggi sono due: [*ReceiveAndDelete* e *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="5cb50-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="5cb50-173">**PeekLock** è la modalità predefinita.</span><span class="sxs-lookup"><span data-stu-id="5cb50-173">**PeekLock** is the default.</span></span>

<span data-ttu-id="5cb50-174">Quando si usa la modalità [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode), l'operazione di ricezione viene eseguita in un'unica fase. Quando infatti il bus di servizio riceve una richiesta di lettura relativa a un messaggio in una sottoscrizione, lo contrassegna come usato e lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-174">When using the [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="5cb50-175">La modalità [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * costituisce il modello più semplice ed è adatta per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="5cb50-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="5cb50-176">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="5cb50-177">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="5cb50-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="5cb50-178">Nella modalità [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) predefinita l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="5cb50-178">In the default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5cb50-179">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="5cb50-180">Dopo aver elaborato il messaggio, o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione completa la seconda fase del processo di ricezione passando il messaggio ricevuto a `ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by passing the received message to `ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="5cb50-181">Quando il bus di servizio vede la chiamata `deleteMessage`, contrassegna il messaggio come utilizzato e lo rimuove dalla coda.</span><span class="sxs-lookup"><span data-stu-id="5cb50-181">When Service Bus sees the `deleteMessage` call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="5cb50-182">L'esempio seguente illustra come ricevere ed elaborare un messaggio usando la modalità [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) (predefinita).</span><span class="sxs-lookup"><span data-stu-id="5cb50-182">The following example shows how to receive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (the default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode to PeekLock (default is ReceiveAndDelete)
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5cb50-183">Procedura: Gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5cb50-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="5cb50-184">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-184">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5cb50-185">Se un'applicazione ricevente non è in grado di elaborare il messaggio per un qualsiasi motivo, può chiamare il metodo `unlockMessage` anziché `deleteMessage` sul messaggio ricevuto.</span><span class="sxs-lookup"><span data-stu-id="5cb50-185">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the received message (instead of the `deleteMessage` method).</span></span> <span data-ttu-id="5cb50-186">In questo modo, il bus di servizio sbloccherà il messaggio nella coda rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="5cb50-186">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5cb50-187">Al messaggio bloccato nella coda è inoltre associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="5cb50-187">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="5cb50-188">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio, ma prima dell'invio della richiesta `deleteMessage`, il messaggio verrà nuovamente recapitato all'applicazione al riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="5cb50-188">In the event that the application crashes after processing the message but before the `deleteMessage` request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="5cb50-189">Questo processo di elaborazione viene spesso definito di tipo *At-Least-Once*, per indicare che ogni messaggio verrà elaborato almeno una volta, ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="5cb50-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="5cb50-190">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva alle applicazioni per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="5cb50-190">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to applications to handle duplicate message delivery.</span></span> <span data-ttu-id="5cb50-191">A tale scopo viene spesso usato il metodo `getMessageId` del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="5cb50-191">This is often achieved using the `getMessageId` method of the message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="5cb50-192">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="5cb50-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="5cb50-193">Per eliminare un argomento o una sottoscrizione, usare rispettivamente il metodo `ServiceBusRestProxy->deleteTopic` o `ServiceBusRestProxy->deleteSubscripton`.</span><span class="sxs-lookup"><span data-stu-id="5cb50-193">To delete a topic or a subscription, use the `ServiceBusRestProxy->deleteTopic` or the `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="5cb50-194">Si noti che, se si elimina un argomento, vengono eliminate anche tutte le sottoscrizioni registrate con l'argomento.</span><span class="sxs-lookup"><span data-stu-id="5cb50-194">Note that deleting a topic also deletes any subscriptions that are registered with the topic.</span></span>

<span data-ttu-id="5cb50-195">L'esempio seguente illustra come eliminare un argomento denominato `mytopic` e le relative sottoscrizioni registrate.</span><span class="sxs-lookup"><span data-stu-id="5cb50-195">The following example shows how to delete a topic named `mytopic` and its registered subscriptions.</span></span>

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

<span data-ttu-id="5cb50-196">È possibile eliminare una sottoscrizione in modo indipendente usando il metodo `deleteSubscription`:</span><span class="sxs-lookup"><span data-stu-id="5cb50-196">By using the `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="5cb50-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5cb50-197">Next steps</span></span>
<span data-ttu-id="5cb50-198">A questo punto, dopo aver appreso le nozioni di base delle code del bus di servizio, vedere [Code, argomenti e sottoscrizioni][Queues, topics, and subscriptions] per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="5cb50-198">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
