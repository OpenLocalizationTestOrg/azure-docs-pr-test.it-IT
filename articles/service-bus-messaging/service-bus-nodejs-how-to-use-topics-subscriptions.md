---
title: Usare argomenti e sottoscrizioni del bus di servizio di Azure con Node.js | Microsoft Docs
description: Informazioni su come usare le sottoscrizioni e gli argomenti del bus di servizio in Azure da un'app Node.js.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 24ae9b80f75531c5e4a84c3b4a6666a6f8a83d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="885a2-103">Come usare gli argomenti e le sottoscrizioni del bus di servizio con Node.js</span><span class="sxs-lookup"><span data-stu-id="885a2-103">How to Use Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="885a2-104">Questa guida descrive come usare gli argomenti e le sottoscrizioni del bus di servizio da applicazioni Node.js.</span><span class="sxs-lookup"><span data-stu-id="885a2-104">This guide describes how to use Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="885a2-105">Gli scenari presentati includono la **creazione di argomenti e sottoscrizioni**, la **creazione di filtri per le sottoscrizioni**, l'**invio di messaggi** a un argomento, la **ricezione di messaggi da una sottoscrizione** e l'**eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="885a2-105">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="885a2-106">Per altre informazioni su argomenti e sottoscrizioni, vedere la sezione [Passaggi successivi](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="885a2-106">For more information about topics and subscriptions, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="885a2-107">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="885a2-107">Create a Node.js application</span></span>
<span data-ttu-id="885a2-108">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="885a2-108">Create a blank Node.js application.</span></span> <span data-ttu-id="885a2-109">Per istruzioni sulla creazione di un'applicazione Node.js, vedere [Creare un'app Web Node.js nel servizio app di Azure] oppure [Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure][Node.js Cloud Service] con Windows PowerShell o Sito Web con WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="885a2-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to an Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="885a2-110">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="885a2-110">Configure your application to use Service Bus</span></span>
<span data-ttu-id="885a2-111">Per usare il bus di servizio, scaricare il pacchetto Azure Node.js,</span><span class="sxs-lookup"><span data-stu-id="885a2-111">To use Service Bus, download the Node.js Azure package.</span></span> <span data-ttu-id="885a2-112">che include un set di librerie di riferimento che comunicano con i servizi REST del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="885a2-112">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="885a2-113">Usare Node Package Manager (NPM) per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="885a2-113">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="885a2-114">Usare un'interfaccia della riga di comando come **PowerShell** (Windows,) **Terminal** (Mac,) o **Bash** (Unix) e spostarsi nella cartella in cui è stata creata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="885a2-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="885a2-115">Digitare **npm install azure** nella finestra di comando, che dovrebbe restituire l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="885a2-115">Type **npm install azure** in the command window, which should result in the following output:</span></span>

   ```
       azure@0.7.5 node_modules\azure
   ├── dateformat@1.0.2-1.2.3
   ├── xmlbuilder@0.4.2
   ├── node-uuid@1.2.0
   ├── mime@1.2.9
   ├── underscore@1.4.4
   ├── validator@1.1.1
   ├── tunnel@0.0.2
   ├── wns@0.5.3
   ├── xml2js@0.2.7 (sax@0.5.2)
   └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
   ```
3. <span data-ttu-id="885a2-116">È possibile eseguire manualmente il comando **ls** per verificare che sia stata creata una cartella **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="885a2-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="885a2-117">In tale cartella trovare il pacchetto **azure**, che contiene le librerie necessarie per accedere agli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="885a2-117">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus topics.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="885a2-118">Importare il modulo</span><span class="sxs-lookup"><span data-stu-id="885a2-118">Import the module</span></span>
<span data-ttu-id="885a2-119">Usando il Blocco note o un altro editor di testo, aggiungere quanto segue alla parte superiore del file **server.js** dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="885a2-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="885a2-120">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="885a2-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="885a2-121">Il modulo di Azure legge le variabile di ambiente `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` per ottenere le informazioni necessarie per la connessione al bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="885a2-121">The Azure module reads the environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required to connect to Service Bus.</span></span> <span data-ttu-id="885a2-122">Se queste variabili di ambiente non sono impostate, è necessario specificare le informazioni relative all'account durante la chiamata di `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="885a2-122">If these environment variables are not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="885a2-123">Per un esempio di impostazione delle variabili di ambiente per un servizio cloud di Azure, vedere [Servizio cloud Node.js con Archiviazione][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="885a2-123">For an example of setting the environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="885a2-124">Per un esempio di impostazione delle variabili di ambiente per un sito Web di Azure, vedere [Creazione di un'applicazione Web Node.js con Archiviazione][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="885a2-124">For an example of setting the environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="885a2-125">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="885a2-125">Create a topic</span></span>
<span data-ttu-id="885a2-126">L'oggetto **ServiceBusService** consente di usare gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="885a2-126">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="885a2-127">Il codice seguente consente di creare un oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="885a2-128">Aggiungerlo nella parte superiore del file **server.js** dopo l'istruzione per l'importazione del modulo azure:</span><span class="sxs-lookup"><span data-stu-id="885a2-128">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="885a2-129">Chiamando `createTopicIfNotExists` nell'oggetto **ServiceBusService**, verrà restituito l'argomento specificato, se esistente, oppure verrà creato un nuovo argomento con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="885a2-129">By calling `createTopicIfNotExists` on the **ServiceBusService** object, the specified topic will be returned (if it exists,) or a new topic with the specified name will be created.</span></span> <span data-ttu-id="885a2-130">Il codice seguente usa `createTopicIfNotExists` per connettersi all'argomento denominato `MyTopic` o crearlo:</span><span class="sxs-lookup"><span data-stu-id="885a2-130">The following code uses `createTopicIfNotExists` to create or connect to the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="885a2-131">Il metodo `createServiceBusService` supporta anche opzioni aggiuntive che consentono di eseguire l'override delle impostazioni predefinite degli argomenti, come la durata (TTL) dei messaggi o le dimensioni massime dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="885a2-131">The `createServiceBusService` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="885a2-132">L'esempio seguente illustra come impostare la dimensione massima dell'argomento su 5 GB con una durata di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="885a2-132">The following example sets the maximum topic size to 5GB with a time to live of 1 minute:</span></span>

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="885a2-133">Filtri</span><span class="sxs-lookup"><span data-stu-id="885a2-133">Filters</span></span>
<span data-ttu-id="885a2-134">Le operazioni di filtro facoltative possono essere applicate alle operazioni eseguite usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-134">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="885a2-135">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con la firma:</span><span class="sxs-lookup"><span data-stu-id="885a2-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="885a2-136">Dopo aver eseguito la pre-elaborazione sulle opzioni della richiesta, il metodo chiama `next` passando un callback con la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="885a2-136">After performing preprocessing on the request options, the method calls `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="885a2-137">Dopo l'elaborazione di `returnObject` (ossia della risposta della richiesta al server), questo callback deve richiamare next, se esistente, per continuare a elaborare altri filtri o in caso contrario richiamare `finalCallback` per terminare la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="885a2-137">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or invoke `finalCallback` otherwise, to end the service invocation.</span></span>

<span data-ttu-id="885a2-138">In Azure SDK per Node.js sono inclusi due filtri che implementano la logica di ripetizione dei tentativi. Sono **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="885a2-138">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="885a2-139">Il codice seguente consente di creare un oggetto **ServiceBusService** che usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="885a2-139">The following creates a **ServiceBusService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="885a2-140">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="885a2-140">Create subscriptions</span></span>
<span data-ttu-id="885a2-141">È possibile creare le sottoscrizioni di un argomento anche con l'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-141">Topic subscriptions are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="885a2-142">Le sottoscrizioni sono denominate e possono includere un filtro facoltativo che limita il set di messaggi recapitati alla coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="885a2-142">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="885a2-143">Le sottoscrizioni sono persistenti e continueranno a esistere fintanto che esse, o l'argomento a cui sono associate, non vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="885a2-143">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="885a2-144">Se l'applicazione contiene la logica per la creazione di una sottoscrizione, è prima di tutto necessario verificare se la sottoscrizione esiste già usando il metodo `getSubscription`.</span><span class="sxs-lookup"><span data-stu-id="885a2-144">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="885a2-145">Creare una sottoscrizione con il filtro (MatchAll) predefinito</span><span class="sxs-lookup"><span data-stu-id="885a2-145">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="885a2-146">Il filtro **MatchAll** è il filtro predefinito e viene usato se non vengono specificati altri filtri durante la creazione di una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="885a2-146">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="885a2-147">Quando si usa il filtro **MatchAll**, tutti i messaggi pubblicati nell'argomento vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="885a2-147">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="885a2-148">Nell'esempio seguente viene creata una sottoscrizione denominata "AllMessages" e viene usato il filtro predefinito **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="885a2-148">The following example creates a subscription named 'AllMessages' and uses the default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="885a2-149">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="885a2-149">Create subscriptions with filters</span></span>
<span data-ttu-id="885a2-150">È anche possibile creare filtri che consentono di definire l'ambito dei messaggi inviati a un argomento che devono essere visualizzati in una specifica sottoscrizione dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="885a2-150">You can also create filters that allow you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="885a2-151">Il tipo di filtro più flessibile tra quelli supportati dalle sottoscrizioni è **SqlFilter**, che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="885a2-151">The most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="885a2-152">I filtri SQL agiscono sulle proprietà dei messaggi pubblicati nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="885a2-152">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="885a2-153">Per altri dettagli sulle espressioni che è possibile usare con un filtro SQL, esaminare la sintassi di [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="885a2-153">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="885a2-154">È possibile aggiungere filtri a una sottoscrizione con il metodo `createRule` dell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-154">Filters can be added to a subscription by using the `createRule` method of the **ServiceBusService** object.</span></span> <span data-ttu-id="885a2-155">Questo metodo consente di aggiungere nuovi filtri a una sottoscrizione esistente.</span><span class="sxs-lookup"><span data-stu-id="885a2-155">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="885a2-156">Poiché il filtro predefinito viene applicato automaticamente a tutte le nuove sottoscrizioni, è necessario prima di tutto rimuovere il filtro predefinito, altrimenti **MatchAll** eseguirà l'override di qualsiasi altro filtro specificato.</span><span class="sxs-lookup"><span data-stu-id="885a2-156">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="885a2-157">È possibile rimuovere la regola predefinita con il metodo `deleteRule` dell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-157">You can remove the default rule by using the `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="885a2-158">L'esempio seguente crea una sottoscrizione denominata `HighMessages` con un filtro **SqlFilter** che seleziona solo i messaggi che hanno una proprietà `messagenumber` personalizzata con valore maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="885a2-158">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="885a2-159">Analogamente, l'esempio seguente crea una sottoscrizione denominata `LowMessages` con un filtro **SqlFilter** che seleziona solo i messaggi che hanno una proprietà `messagenumber` con valore minore o uguale a 3:</span><span class="sxs-lookup"><span data-stu-id="885a2-159">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

<span data-ttu-id="885a2-160">Un messaggio inviato a `MyTopic` verrà sempre recapitato ai ricevitori con sottoscrizione all'argomento `AllMessages` e recapitato selettivamente ai ricevitori con sottoscrizioni agli argomenti `HighMessages` e `LowMessages` (a seconda del contenuto del messaggio).</span><span class="sxs-lookup"><span data-stu-id="885a2-160">When a message is now sent to `MyTopic`, it will always be delivered to receivers subscribed to the `AllMessages` topic subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` topic subscriptions (depending upon the message content).</span></span>

## <a name="how-to-send-messages-to-a-topic"></a><span data-ttu-id="885a2-161">Come inviare messaggi a un argomento</span><span class="sxs-lookup"><span data-stu-id="885a2-161">How to send messages to a topic</span></span>
<span data-ttu-id="885a2-162">Per inviare un messaggio a un argomento del bus di servizio, l'applicazione deve usare il metodo `sendTopicMessage` dell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-162">To send a message to a Service Bus topic, your application must use the `sendTopicMessage` method of the **ServiceBusService** object.</span></span>
<span data-ttu-id="885a2-163">I messaggi inviati ad argomenti del bus di servizio sono oggetti **BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="885a2-163">Messages sent to Service Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="885a2-164">Gli oggetti **BrokeredMessage** includono un set di proprietà standard, ad esempio `Label` e `TimeToLive`, un dizionario usato per contenere le proprietà personalizzate specifiche dell'applicazione e un corpo di dati di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="885a2-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="885a2-165">Un'applicazione può impostare il corpo del messaggio passando un valore stringa a `sendTopicMessage` e popolare le proprietà standard necessarie con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="885a2-165">An application can set the body of the message by passing a string value to the `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="885a2-166">Il seguente esempio illustra come inviare cinque messaggi di test a `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="885a2-166">The following example demonstrates how to send five test messages to `MyTopic`.</span></span> <span data-ttu-id="885a2-167">Si noti che il valore della proprietà `messagenumber` di ogni messaggio varia nell'iterazione del ciclo, determinando quali sottoscrizioni lo riceveranno:</span><span class="sxs-lookup"><span data-stu-id="885a2-167">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

<span data-ttu-id="885a2-168">Gli argomenti del bus di servizio supportano messaggi di dimensioni massime fino a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e fino a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="885a2-168">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="885a2-169">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="885a2-169">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="885a2-170">Non esiste alcun limite al numero di messaggi mantenuti in un argomento, mentre è prevista una limitazione alla dimensione totale dei messaggi di un argomento.</span><span class="sxs-lookup"><span data-stu-id="885a2-170">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="885a2-171">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="885a2-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="885a2-172">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="885a2-172">Receive messages from a subscription</span></span>
<span data-ttu-id="885a2-173">I messaggi vengono ricevuti da una sottoscrizione usando il metodo `receiveSubscriptionMessage` nell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="885a2-174">Per impostazione predefinita, i messaggi vengono eliminati dalla sottoscrizione non appena vengono letti. È tuttavia possibile leggere (visualizzare) e bloccare il messaggio senza eliminarlo dalla sottoscrizione impostando il parametro facoltativo `isPeekLock` su **true**.</span><span class="sxs-lookup"><span data-stu-id="885a2-174">By default, messages are deleted from the subscription as they are read; however, you can read (peek) and lock the message without deleting it from the subscription by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="885a2-175">Il comportamento predefinito di lettura ed eliminazione del messaggio nell'ambito dell'operazione di ricezione costituisce il modello più semplice ed è adatto per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="885a2-175">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="885a2-176">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="885a2-176">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="885a2-177">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="885a2-177">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="885a2-178">Se il parametro `isPeekLock` è impostato su **true**, l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="885a2-178">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="885a2-179">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="885a2-179">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span>
<span data-ttu-id="885a2-180">Dopo aver elaborato il messaggio, o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione esegue la seconda fase del processo di ricezione chiamando il metodo **deleteMessage** e specificando il messaggio da eliminare come parametro.</span><span class="sxs-lookup"><span data-stu-id="885a2-180">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **deleteMessage** method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="885a2-181">Il metodo **deleteMessage** contrassegna il messaggio come usato e lo rimuove dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="885a2-181">The **deleteMessage** method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="885a2-182">L'esempio seguente illustra come ricevere ed elaborare messaggi tramite `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="885a2-182">The following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="885a2-183">L'esempio prima di tutto riceve ed elimina un messaggio dalla sottoscrizione "LowMessages" e quindi riceve un messaggio dalla sottoscrizione "HighMessages" con il parametro `isPeekLock` impostato su true.</span><span class="sxs-lookup"><span data-stu-id="885a2-183">The example first receives and deletes a message from the 'LowMessages' subscription, and then receives a message from the 'HighMessages' subscription using `isPeekLock` set to true.</span></span> <span data-ttu-id="885a2-184">Elimina infine il messaggio usando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="885a2-184">It then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="885a2-185">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="885a2-185">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="885a2-186">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="885a2-186">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="885a2-187">Se un'applicazione ricevente non riesce a elaborare il messaggio per qualsiasi motivo, può chiamare il metodo `unlockMessage` nell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="885a2-187">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="885a2-188">In questo modo, il bus di servizio sbloccherà il messaggio nella sottoscrizione rendendolo nuovamente disponibile per la ricezione da parte della stessa applicazione consumer o da un'altra.</span><span class="sxs-lookup"><span data-stu-id="885a2-188">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="885a2-189">Al messaggio bloccato nella sottoscrizione è anche associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="885a2-189">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="885a2-190">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio ma prima della chiamata del metodo `deleteMessage`, il messaggio verrà nuovamente recapitato all'applicazione al riavvio.</span><span class="sxs-lookup"><span data-stu-id="885a2-190">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="885a2-191">Questo processo di elaborazione viene spesso definito di tipo *At-Least-Once*, per indicare che ogni messaggio verrà elaborato almeno una volta ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="885a2-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="885a2-192">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva all'applicazione per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="885a2-192">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="885a2-193">A tale scopo viene spesso usata la proprietà **MessageId** del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="885a2-193">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="885a2-194">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="885a2-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="885a2-195">Gli argomenti e le sottoscrizioni sono persistenti e devono essere eliminati in modo esplicito nel [portale di Azure][Azure portal] oppure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="885a2-195">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="885a2-196">L'esempio seguente illustra come eliminare l'argomento denominato `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="885a2-196">The following example demonstrates how to delete the topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="885a2-197">Se si elimina un argomento, verranno eliminate anche tutte le sottoscrizioni registrate con l'argomento.</span><span class="sxs-lookup"><span data-stu-id="885a2-197">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="885a2-198">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="885a2-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="885a2-199">L'esempio seguente illustra come eliminare una sottoscrizione denominata `HighMessages` dall'argomento `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="885a2-199">The following example shows how to delete a subscription named `HighMessages` from the `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="885a2-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="885a2-200">Next Steps</span></span>
<span data-ttu-id="885a2-201">A questo punto, dopo aver appreso le nozioni di base degli argomenti del bus di servizio, usare i seguenti collegamenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="885a2-201">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="885a2-202">Vedere [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="885a2-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="885a2-203">Informazioni di riferimento sulle API per [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="885a2-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="885a2-204">Visitare il repository [Azure SDK per Node][Azure SDK for Node] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="885a2-204">Visit the [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Creare un'app Web Node.js nel servizio app di Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
