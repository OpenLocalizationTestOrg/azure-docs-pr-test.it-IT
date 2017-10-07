---
title: aaaHow toouse Azure Service Bus argomenti e sottoscrizioni con Node.js | Documenti Microsoft
description: Informazioni su come toouse Bus di servizio di argomenti e sottoscrizioni in Azure da un'app Node.js.
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
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a><span data-ttu-id="362e6-103">Il Bus di servizio tooUse argomenti e sottoscrizioni con Node.js</span><span class="sxs-lookup"><span data-stu-id="362e6-103">How tooUse Service Bus topics and subscriptions with Node.js</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="362e6-104">Questa guida viene descritto come toouse Bus di servizio di argomenti e sottoscrizioni dalle applicazioni Node.js.</span><span class="sxs-lookup"><span data-stu-id="362e6-104">This guide describes how toouse Service Bus topics and subscriptions from Node.js applications.</span></span> <span data-ttu-id="362e6-105">Hello scenari trattati includono **la creazione di argomenti e sottoscrizioni**, **creazione filtri di sottoscrizione**, **l'invio di messaggi** tooa argomento **ricezione i messaggi da una sottoscrizione**, e **l'eliminazione di argomenti e sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="362e6-105">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="362e6-106">Per ulteriori informazioni su argomenti e sottoscrizioni, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="362e6-106">For more information about topics and subscriptions, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="362e6-107">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="362e6-107">Create a Node.js application</span></span>
<span data-ttu-id="362e6-108">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="362e6-108">Create a blank Node.js application.</span></span> <span data-ttu-id="362e6-109">Per istruzioni sulla creazione di un'applicazione Node.js, vedere [creare e distribuire un tooan di applicazione del sito Web di Azure Node.js], [servizio Cloud Node.js] [ Node.js Cloud Service] utilizzando Windows PowerShell o il sito Web con WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="362e6-109">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooan Azure Web Site], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or Web Site with WebMatrix.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="362e6-110">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="362e6-110">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="362e6-111">toouse Service Bus, scaricare il pacchetto di Node.js Azure hello.</span><span class="sxs-lookup"><span data-stu-id="362e6-111">toouse Service Bus, download hello Node.js Azure package.</span></span> <span data-ttu-id="362e6-112">Il pacchetto include un set di librerie che comunicano con servizi di Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="362e6-112">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="362e6-113">Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="362e6-113">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="362e6-114">Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), passare toohello cartella in cui è stato creato l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="362e6-114">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="362e6-115">Tipo **npm installare azure** nella finestra di comando hello, che dovrebbe restituire hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="362e6-115">Type **npm install azure** in hello command window, which should result in hello following output:</span></span>

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
3. <span data-ttu-id="362e6-116">È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="362e6-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="362e6-117">All'interno di tale cartella è possibile trovare il **azure** pacchetto che contiene le librerie di hello necessarie tooaccess argomenti del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="362e6-117">Inside that folder find the **azure** package, which contains hello libraries you need tooaccess Service Bus topics.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="362e6-118">Modulo di importazione hello</span><span class="sxs-lookup"><span data-stu-id="362e6-118">Import hello module</span></span>
<span data-ttu-id="362e6-119">Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="362e6-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="362e6-120">Configurare una stringa di connessione per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="362e6-120">Set up a Service Bus connection</span></span>
<span data-ttu-id="362e6-121">Hello Azure modulo legge le variabili di ambiente hello `AZURE_SERVICEBUS_NAMESPACE` e `AZURE_SERVICEBUS_ACCESS_KEY` per le informazioni necessarie tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="362e6-121">hello Azure module reads hello environment variables `AZURE_SERVICEBUS_NAMESPACE` and `AZURE_SERVICEBUS_ACCESS_KEY` for information required tooconnect tooService Bus.</span></span> <span data-ttu-id="362e6-122">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="362e6-122">If these environment variables are not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="362e6-123">Per un esempio di impostazione delle variabili di ambiente hello per un servizio Cloud di Azure, vedere [servizio Cloud Node.js con archiviazione][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="362e6-123">For an example of setting hello environment variables for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="362e6-124">Per un esempio di impostazione delle variabili di ambiente hello per un sito Web di Azure, vedere [applicazione Web Node.js con archiviazione][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="362e6-124">For an example of setting hello environment variables for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="362e6-125">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="362e6-125">Create a topic</span></span>
<span data-ttu-id="362e6-126">Hello **ServiceBusService** consente toowork con argomenti.</span><span class="sxs-lookup"><span data-stu-id="362e6-126">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="362e6-127">Il codice seguente consente di creare un oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="362e6-127">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="362e6-128">Aggiungerlo nella parte superiore di hello **server.js** file, dopo il modulo di hello istruzione tooimport hello azure:</span><span class="sxs-lookup"><span data-stu-id="362e6-128">Add it near the top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="362e6-129">Chiamando `createTopicIfNotExists` su hello **ServiceBusService** oggetto, verrà creato un nuovo argomento con il nome specificato hello o hello specificato verrà restituito l'argomento (se presente).</span><span class="sxs-lookup"><span data-stu-id="362e6-129">By calling `createTopicIfNotExists` on hello **ServiceBusService** object, hello specified topic will be returned (if it exists,) or a new topic with hello specified name will be created.</span></span> <span data-ttu-id="362e6-130">codice Hello seguente usa `createTopicIfNotExists` toocreate o connettersi toohello argomento denominato `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="362e6-130">hello following code uses `createTopicIfNotExists` toocreate or connect toohello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

<span data-ttu-id="362e6-131">Hello `createServiceBusService` metodo supporta inoltre opzioni aggiuntive, che consentono di determinare le impostazioni dell'argomento predefinito toooverride, ad esempio durata messaggio o la dimensione massima dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="362e6-131">hello `createServiceBusService` method also supports additional options, which enable you toooverride default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="362e6-132">Hello esempio seguente imposta too5GB di dimensione massima dell'argomento hello con un tempo toolive di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="362e6-132">hello following example sets hello maximum topic size too5GB with a time toolive of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="362e6-133">Filtri</span><span class="sxs-lookup"><span data-stu-id="362e6-133">Filters</span></span>
<span data-ttu-id="362e6-134">Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="362e6-134">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="362e6-135">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:</span><span class="sxs-lookup"><span data-stu-id="362e6-135">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="362e6-136">Dopo l'esecuzione di pre-elaborazione sulle opzioni di richiesta di hello, hello chiamate al metodo `next`, passando un callback con hello seguente firma:</span><span class="sxs-lookup"><span data-stu-id="362e6-136">After performing preprocessing on hello request options, hello method calls `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="362e6-137">In questo callback e dopo l'elaborazione hello `returnObject` (hello risposta dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o richiamare `finalCallback` hello tooend in caso contrario, chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="362e6-137">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or invoke `finalCallback` otherwise, tooend hello service invocation.</span></span>

<span data-ttu-id="362e6-138">Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="362e6-138">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="362e6-139">Hello seguito creato un **ServiceBusService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="362e6-139">hello following creates a **ServiceBusService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a><span data-ttu-id="362e6-140">Creare sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="362e6-140">Create subscriptions</span></span>
<span data-ttu-id="362e6-141">Le sottoscrizioni dell'argomento vengono inoltre create con hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-141">Topic subscriptions are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="362e6-142">Le sottoscrizioni sono denominate e possono avere un filtro facoltativo che limita il set di hello di messaggi recapitati coda virtuale toohello della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="362e6-142">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="362e6-143">Le sottoscrizioni sono permanenti e continueranno tooexist finché uno non o hello argomento sono associati, vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="362e6-143">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="362e6-144">Se l'applicazione contiene la logica toocreate una sottoscrizione, deve verificare se hello sottoscrizione esiste già con il `getSubscription` metodo.</span><span class="sxs-lookup"><span data-stu-id="362e6-144">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using the `getSubscription` method.</span></span>
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="362e6-145">Creare una sottoscrizione con filtro predefinito (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="362e6-145">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="362e6-146">Hello **MatchAll** filtro è hello predefinito che viene utilizzato se viene specificato alcun filtro quando viene creata una nuova sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="362e6-146">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="362e6-147">Quando hello **MatchAll** filtro viene utilizzato, l'argomento di toohello pubblicati tutti i messaggi vengono inseriti nella coda virtuale della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="362e6-147">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="362e6-148">esempio Hello crea una sottoscrizione denominata 'AllMessages' e utilizza hello predefinito **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="362e6-148">hello following example creates a subscription named 'AllMessages' and uses hello default **MatchAll** filter.</span></span>

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="362e6-149">Creare sottoscrizioni con i filtri</span><span class="sxs-lookup"><span data-stu-id="362e6-149">Create subscriptions with filters</span></span>
<span data-ttu-id="362e6-150">È anche possibile creare filtri che consentono di tooscope cui i messaggi inviati tooa argomento visualizzati all'interno di una sottoscrizione di argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="362e6-150">You can also create filters that allow you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="362e6-151">Hello più flessibile il tipo di filtro supportato dalle sottoscrizioni è il **SqlFilter**, che implementa un subset di SQL92.</span><span class="sxs-lookup"><span data-stu-id="362e6-151">hello most flexible type of filter supported by subscriptions is the **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="362e6-152">I filtri SQL operano sulle proprietà hello dei messaggi hello argomento toohello pubblicato.</span><span class="sxs-lookup"><span data-stu-id="362e6-152">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="362e6-153">Per ulteriori informazioni sulle espressioni hello che possono essere utilizzate con un filtro SQL, vedere hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintassi.</span><span class="sxs-lookup"><span data-stu-id="362e6-153">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="362e6-154">È possibile aggiungere filtri tooa sottoscrizione utilizzando hello `createRule` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-154">Filters can be added tooa subscription by using hello `createRule` method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="362e6-155">Questo metodo consente di aggiungere nuovi filtri tooan sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="362e6-155">This method allows you to add new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="362e6-156">Poiché il filtro predefinito hello viene applicato automaticamente tooall nuove sottoscrizioni, è necessario innanzitutto rimuovere filtro predefinito hello o **MatchAll** sostituirà gli altri filtri che è possibile specificare.</span><span class="sxs-lookup"><span data-stu-id="362e6-156">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="362e6-157">È possibile rimuovere una regola predefinita hello utilizzando hello `deleteRule` metodo il **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-157">You can remove hello default rule by using hello `deleteRule` method of the **ServiceBusService** object.</span></span>
>
>

<span data-ttu-id="362e6-158">esempio Hello crea una sottoscrizione denominata `HighMessages` con un **SqlFilter** che seleziona solo i messaggi con un oggetto personalizzato `messagenumber` maggiore di 3:</span><span class="sxs-lookup"><span data-stu-id="362e6-158">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

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

<span data-ttu-id="362e6-159">Analogamente, hello esempio seguente viene creata una sottoscrizione denominata `LowMessages` con un **SqlFilter** che seleziona solo i messaggi che hanno un `messagenumber` proprietà minore o uguale too3:</span><span class="sxs-lookup"><span data-stu-id="362e6-159">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

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

<span data-ttu-id="362e6-160">Quando viene inviato un messaggio ora troppo`MyTopic`, sempre essere recapitato ricevitori sottoscritti toohello `AllMessages` sottoscrizione dell'argomento e recapitati in modo selettivo tooreceivers sottoscritto toohello `HighMessages` e `LowMessages` le sottoscrizioni dell'argomento (in base al contenuto del messaggio hello).</span><span class="sxs-lookup"><span data-stu-id="362e6-160">When a message is now sent too`MyTopic`, it will always be delivered to receivers subscribed toohello `AllMessages` topic subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="how-toosend-messages-tooa-topic"></a><span data-ttu-id="362e6-161">La modalità toosend dei messaggi tooa argomento</span><span class="sxs-lookup"><span data-stu-id="362e6-161">How toosend messages tooa topic</span></span>
<span data-ttu-id="362e6-162">un argomento del Bus di servizio tooa messaggio toosend, l'applicazione deve usare il `sendTopicMessage` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-162">toosend a message tooa Service Bus topic, your application must use the `sendTopicMessage` method of hello **ServiceBusService** object.</span></span>
<span data-ttu-id="362e6-163">I messaggi inviati sono argomenti del Bus tooService **BrokeredMessage** oggetti.</span><span class="sxs-lookup"><span data-stu-id="362e6-163">Messages sent tooService Bus topics are **BrokeredMessage** objects.</span></span>
<span data-ttu-id="362e6-164">**BrokeredMessage** oggetti dispongono di un set di proprietà standard (ad esempio `Label` e `TimeToLive`), un dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="362e6-164">**BrokeredMessage** objects have a set of standard properties (such as `Label` and `TimeToLive`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="362e6-165">Un'applicazione può impostare il corpo di hello del messaggio hello passando un valore di stringa a messaggi hello `sendTopicMessage` e le necessarie proprietà standard verranno popolate dai valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="362e6-165">An application can set hello body of hello message by passing a string value to hello `sendTopicMessage` and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="362e6-166">Hello esempio seguente viene illustrato come toosend cinque messaggi di prova per `MyTopic`.</span><span class="sxs-lookup"><span data-stu-id="362e6-166">hello following example demonstrates how toosend five test messages to `MyTopic`.</span></span> <span data-ttu-id="362e6-167">Si noti che hello `messagenumber` valore della proprietà di ogni messaggio varia iterazione hello del ciclo di hello (per stabilire le sottoscrizioni che ricevano):</span><span class="sxs-lookup"><span data-stu-id="362e6-167">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

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

<span data-ttu-id="362e6-168">Argomenti del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="362e6-168">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="362e6-169">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="362e6-169">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="362e6-170">Non è previsto alcun limite per il numero di hello di messaggi contenuti in un argomento, ma è un limite alla dimensione totale di hello di messaggi hello utilizzate da un argomento.</span><span class="sxs-lookup"><span data-stu-id="362e6-170">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="362e6-171">Questa dimensione dell'argomento viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="362e6-171">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="362e6-172">Ricevere messaggi da una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="362e6-172">Receive messages from a subscription</span></span>
<span data-ttu-id="362e6-173">I messaggi vengono ricevuti da una sottoscrizione tramite il `receiveSubscriptionMessage` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-173">Messages are received from a subscription using the `receiveSubscriptionMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="362e6-174">Per impostazione predefinita, i messaggi vengono eliminati dalla sottoscrizione hello quando vengono letti; Tuttavia, è possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla sottoscrizione hello dal parametro facoltativo hello impostazione `isPeekLock` troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="362e6-174">By default, messages are deleted from hello subscription as they are read; however, you can read (peek) and lock hello message without deleting it from hello subscription by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="362e6-175">comportamento predefinito di Hello di lettura e l'eliminazione del messaggio hello come parte dell'operazione di ricezione è il modello più semplice di hello ed è ideale per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="362e6-175">hello default behavior of reading and deleting hello message as part of the receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="362e6-176">toounderstand, si consideri uno scenario in cui il hello problemi consumer di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="362e6-176">toounderstand this, consider a scenario in which the consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="362e6-177">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="362e6-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="362e6-178">Se hello `isPeekLock` parametro è impostato troppo**true**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="362e6-178">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="362e6-179">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="362e6-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span>
<span data-ttu-id="362e6-180">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase del processo di ricezione chiamando **deleteMessage** (metodo) e fornendo il toobe messaggio eliminato come parametro.</span><span class="sxs-lookup"><span data-stu-id="362e6-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of the receive process by calling **deleteMessage** method and providing the message toobe deleted as a parameter.</span></span> <span data-ttu-id="362e6-181">Hello **deleteMessage** metodo contrassegna il messaggio hello come usato, ma verrà rimosso dalla sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="362e6-181">hello **deleteMessage** method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="362e6-182">Hello esempio seguente viene illustrato come è possibile ricevere messaggi e trasformati utilizzando `receiveSubscriptionMessage`.</span><span class="sxs-lookup"><span data-stu-id="362e6-182">hello following example demonstrates how messages can be received and processed using `receiveSubscriptionMessage`.</span></span> <span data-ttu-id="362e6-183">Hello esempio riceve Elimina un messaggio dalla sottoscrizione 'LowMessages' hello e viene ricevuto un messaggio dalla sottoscrizione di 'HighMessages' hello utilizzando `isPeekLock` impostare tootrue.</span><span class="sxs-lookup"><span data-stu-id="362e6-183">hello example first receives and deletes a message from hello 'LowMessages' subscription, and then receives a message from hello 'HighMessages' subscription using `isPeekLock` set tootrue.</span></span> <span data-ttu-id="362e6-184">Elimina quindi il messaggio hello utilizzando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="362e6-184">It then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="362e6-185">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="362e6-185">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="362e6-186">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="362e6-186">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="362e6-187">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo il **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="362e6-187">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="362e6-188">Ciò causerà Bus di servizio toounlock il messaggio all'interno di sottoscrizione hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="362e6-188">This will cause Service Bus toounlock the message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="362e6-189">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno della sottoscrizione, e se un'applicazione hello ha esito negativo messaggio hello tooprocess prima il timeout di blocco hello scade (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio Sblocca messaggio hello automaticamente e lo rende disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="362e6-189">There is also a timeout associated with a message locked within the subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="362e6-190">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia.</span><span class="sxs-lookup"><span data-stu-id="362e6-190">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="362e6-191">Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="362e6-191">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="362e6-192">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="362e6-192">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="362e6-193">Questa operazione viene spesso eseguita mediante il **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="362e6-193">This is often achieved using the **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="362e6-194">Eliminare argomenti e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="362e6-194">Delete topics and subscriptions</span></span>
<span data-ttu-id="362e6-195">Argomenti e sottoscrizioni sono persistenti e deve essere in modo esplicito tramite hello eliminato [portale di Azure] [ Azure portal] o a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="362e6-195">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span>
<span data-ttu-id="362e6-196">Hello esempio seguente viene illustrato come argomento di hello toodelete denominati `MyTopic`:</span><span class="sxs-lookup"><span data-stu-id="362e6-196">hello following example demonstrates how toodelete hello topic named `MyTopic`:</span></span>

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

<span data-ttu-id="362e6-197">L'eliminazione di un argomento eliminerà anche le sottoscrizioni che sono registrate con l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="362e6-197">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="362e6-198">Le sottoscrizioni possono essere eliminate anche in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="362e6-198">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="362e6-199">Nell'esempio seguente viene illustrato come toodelete una sottoscrizione denominata `HighMessages` da hello `MyTopic` argomento:</span><span class="sxs-lookup"><span data-stu-id="362e6-199">The following example shows how toodelete a subscription named `HighMessages` from hello `MyTopic` topic:</span></span>

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a><span data-ttu-id="362e6-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="362e6-200">Next Steps</span></span>
<span data-ttu-id="362e6-201">Ora che si è appreso i concetti di base di hello di argomenti del Bus di servizio, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="362e6-201">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="362e6-202">Vedere [Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="362e6-202">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="362e6-203">Informazioni di riferimento sulle API per [SqlFilter][SqlFilter].</span><span class="sxs-lookup"><span data-stu-id="362e6-203">API reference for [SqlFilter][SqlFilter].</span></span>
* <span data-ttu-id="362e6-204">Visitare hello [Azure SDK per nodo] [ Azure SDK for Node] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="362e6-204">Visit hello [Azure SDK for Node][Azure SDK for Node] repository on GitHub.</span></span>

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Creare e distribuire un tooan applicazione Node.js sito Web di Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
