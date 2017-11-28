---
title: le code di aaaHow toouse Bus di servizio in Node.js | Documenti Microsoft
description: Informazioni su come code toouse Bus di servizio in Azure da un'app Node.js.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="5393a-103">La modalità di code toouse Bus di servizio con Node.js</span><span class="sxs-lookup"><span data-stu-id="5393a-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="5393a-104">In questo articolo viene descritto come toouse Bus di servizio code con Node.js.</span><span class="sxs-lookup"><span data-stu-id="5393a-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="5393a-105">esempi di Hello scritte in JavaScript e usare il modulo di Node.js Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="5393a-106">Hello scenari trattati includono **la creazione delle code**, **inviando e ricevendo messaggi**, e **l'eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="5393a-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="5393a-107">Per ulteriori informazioni sulle code, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="5393a-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="5393a-108">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="5393a-108">Create a Node.js application</span></span>
<span data-ttu-id="5393a-109">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="5393a-109">Create a blank Node.js application.</span></span> <span data-ttu-id="5393a-110">Per istruzioni su come toocreate un'applicazione Node.js, vedere [creare e distribuire un tooan di applicazione del sito Web di Azure Node.js][Create and deploy a Node.js application tooan Azure Website], o [servizio Cloud Node.js] [ Node.js Cloud Service] tramite Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5393a-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5393a-111">Configurare il toouse applicazione Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="5393a-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5393a-112">toouse Service Bus di Azure, scaricare e usare il pacchetto di Node.js Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="5393a-113">Il pacchetto include un set di librerie che comunicano con servizi di Service Bus REST hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="5393a-114">Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="5393a-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="5393a-115">Hello utilizzare **Windows PowerShell per Node.js** toohello toonavigate finestra di comando **c:\\nodo\\sbqueues\\WebRole1** cartella in cui è stato creato il applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="5393a-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="5393a-116">Tipo **npm installare azure** nella finestra di comando hello, che dovrebbe restituire seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="5393a-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="5393a-117">È possibile eseguire manualmente hello **ls** comando tooverify che un **node_modules** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="5393a-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="5393a-118">All'interno di tale hello Trova cartella **azure** pacchetto che contiene le librerie di hello necessarie tooaccess code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5393a-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="5393a-119">Modulo di importazione hello</span><span class="sxs-lookup"><span data-stu-id="5393a-119">Import hello module</span></span>
<span data-ttu-id="5393a-120">Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="5393a-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="5393a-121">Configurare una connessione del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="5393a-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="5393a-122">modulo di Azure Hello legge la variabile di ambiente hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informazioni necessarie tooconnect tooService Bus.</span><span class="sxs-lookup"><span data-stu-id="5393a-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="5393a-123">Se questa variabile di ambiente non è impostata, è necessario specificare le informazioni sull'account hello quando si chiama `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="5393a-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="5393a-124">Per un esempio di impostazione delle variabili di ambiente di hello in un file di configurazione per un servizio Cloud di Azure, vedere [servizio Cloud Node.js con archiviazione][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="5393a-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="5393a-125">Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure] [ Azure portal] per un sito Web di Azure, vedere [applicazione Web Node.js con archiviazione] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="5393a-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="5393a-126">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="5393a-126">Create a queue</span></span>
<span data-ttu-id="5393a-127">Hello **ServiceBusService** consente toowork con le code del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5393a-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="5393a-128">Hello codice seguente viene creata una **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="5393a-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="5393a-129">Aggiungerlo parte superiore di hello di hello **server.js** file hello tooimport di istruzione hello modulo di Azure:</span><span class="sxs-lookup"><span data-stu-id="5393a-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="5393a-130">Chiamando `createQueueIfNotExists` su hello **ServiceBusService** oggetto, viene creata una nuova coda con il nome specificato hello o hello specificato coda viene restituita (se presente).</span><span class="sxs-lookup"><span data-stu-id="5393a-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="5393a-131">codice Hello seguente usa `createQueueIfNotExists` toocreate o connettersi coda toohello denominata `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="5393a-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="5393a-132">Hello `createServiceBusService` metodo supporta inoltre opzioni aggiuntive, che consentono di impostazioni di coda toooverride predefinite, ad esempio dimensioni toolive o massimo in una coda in fase di messaggio.</span><span class="sxs-lookup"><span data-stu-id="5393a-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="5393a-133">Hello esempio seguente imposta GB too5 dimensioni massime della coda di hello e un valore di (durata TTL) toolive ora di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="5393a-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="5393a-134">Filtri</span><span class="sxs-lookup"><span data-stu-id="5393a-134">Filters</span></span>
<span data-ttu-id="5393a-135">Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="5393a-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="5393a-136">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:</span><span class="sxs-lookup"><span data-stu-id="5393a-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="5393a-137">Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, è necessario chiamare il metodo hello `next`, passando un callback con hello seguente firma:</span><span class="sxs-lookup"><span data-stu-id="5393a-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="5393a-138">In questo callback e dopo l'elaborazione hello `returnObject` (hello risposta dal server di hello richiesta toohello), deve richiamare il callback di hello `next` se esiste toocontinue l'elaborazione di altri filtri, o semplicemente richiamare `finalCallback`, che termina chiamata del servizio Hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="5393a-139">Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="5393a-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="5393a-140">Hello codice seguente viene creata una `ServiceBusService` oggetto che utilizza hello `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="5393a-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="5393a-141">Messaggi tooa coda di invio</span><span class="sxs-lookup"><span data-stu-id="5393a-141">Send messages tooa queue</span></span>
<span data-ttu-id="5393a-142">una coda di Service Bus di messaggi tooa toosend, l'applicazione chiama hello `sendQueueMessage` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="5393a-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="5393a-143">I messaggi inviati troppo (e ricevuti da) Bus di servizio, le code sono **BrokeredMessage** oggetti e di disporre di un set di proprietà standard (ad esempio **etichetta** e **TimeToLive**), dizionario di proprietà specifiche dell'applicazione personalizzate usate toohold e un corpo di dati applicazione arbitrari.</span><span class="sxs-lookup"><span data-stu-id="5393a-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="5393a-144">Un'applicazione può impostare il corpo di hello del messaggio hello passando una stringa come messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="5393a-145">Le proprietà standard necessarie vengono popolate con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="5393a-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="5393a-146">Hello esempio seguente viene illustrato come toosend una coda toohello test denominati `myqueue` utilizzando `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="5393a-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="5393a-147">Le code del Bus di servizio supportano una dimensione massima di 256 KB in hello [livello Standard](service-bus-premium-messaging.md) hello a 1 MB e [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5393a-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5393a-148">intestazione Hello, che include standard hello e le proprietà personalizzate dell'applicazione, può avere una dimensione massima di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="5393a-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5393a-149">Non è previsto alcun limite per il numero di hello di messaggi contenuti in una coda, ma è un limite alla dimensione totale di hello di messaggi hello mantenuto da una coda.</span><span class="sxs-lookup"><span data-stu-id="5393a-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="5393a-150">Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="5393a-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="5393a-151">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="5393a-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="5393a-152">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="5393a-152">Receive messages from a queue</span></span>
<span data-ttu-id="5393a-153">I messaggi vengono ricevuti da una coda utilizzando hello `receiveQueueMessage` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="5393a-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="5393a-154">Per impostazione predefinita, i messaggi vengono eliminati dalla coda di hello quando vengono letti; Tuttavia, è possibile leggere (anteprima) e bloccare il messaggio hello senza eliminarla dalla coda hello dal parametro facoltativo hello impostazione `isPeekLock` troppo**true**.</span><span class="sxs-lookup"><span data-stu-id="5393a-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="5393a-155">Hello il comportamento predefinito di lettura e l'eliminazione del messaggio hello come parte di hello l'operazione di ricezione è il modello più semplice di hello e adatto per scenari in cui un'applicazione in grado di tollerare non elabora un messaggio di evento hello di un errore.</span><span class="sxs-lookup"><span data-stu-id="5393a-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5393a-156">toounderstand, si consideri uno scenario in cui problemi relativi ai consumer hello hello di ricezione richiesta e quindi si blocca prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5393a-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5393a-157">Poiché verrà contrassegnato messaggio come usato, quindi quando un'applicazione hello viene riavviata e inizia a usare nuovamente i messaggi hello del Bus di servizio, risulterà perso messaggio hello che è stato consumato toohello precedente arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="5393a-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5393a-158">Se hello `isPeekLock` parametro è impostato troppo**true**, hello ricezione diventa un'operazione in due fasi, che rende possibile toosupport applicazioni che non sono in grado di tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="5393a-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5393a-159">Quando il Bus di servizio riceve una richiesta, individua hello successivo messaggio toobe utilizzati Blocca tooprevent altri consumer di ricezione e lo restituisce quindi toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="5393a-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5393a-160">Dopo l'applicazione hello completa l'elaborazione messaggio hello o archiviarlo in modo affidabile per l'elaborazione futura, completa hello seconda fase di hello ricevere processo chiamando `deleteMessage` (metodo) e fornendo toobe messaggio hello eliminato come parametro.</span><span class="sxs-lookup"><span data-stu-id="5393a-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="5393a-161">Hello `deleteMessage` metodo contrassegna il messaggio hello come usato e la rimuove dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="5393a-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="5393a-162">Hello esempio seguente viene illustrato come tooreceive ed elaborare messaggi utilizzando `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="5393a-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="5393a-163">Hello esempio riceve un messaggio viene eliminato e quindi riceve un messaggio utilizzando `isPeekLock` impostare troppo**true**, quindi Elimina hello messaggio utilizzando `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="5393a-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5393a-164">Come si blocca toohandle applicazione e i messaggi illeggibili</span><span class="sxs-lookup"><span data-stu-id="5393a-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="5393a-165">Bus di servizio offre funzionalità toohelp che normalmente possibile correggere gli errori nell'applicazione o problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="5393a-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5393a-166">Se un'applicazione ricevente è in grado di tooprocess hello messaggio per qualche motivo, quindi è possibile chiamare hello `unlockMessage` metodo hello **ServiceBusService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="5393a-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="5393a-167">Ciò causerà Bus di servizio toounlock il messaggio nella coda di hello e renderlo disponibile toobe nuovamente ricevuto, sia da hello stesso consumo dell'applicazione o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="5393a-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5393a-168">È inoltre disponibile un timeout associato a un messaggio bloccato all'interno di coda hello e se hello ha esito negativo dell'applicazione hello tooprocess hello messaggio prima della scadenza del timeout (ad esempio, se si blocca l'applicazione hello), quindi il Bus di servizio sbloccherà il messaggio hello e renderlo disponibile toobe nuovamente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="5393a-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5393a-169">In hello evento hello applicazione si blocca dopo l'elaborazione messaggio hello ma prima di hello `deleteMessage` metodo viene chiamato, quindi il messaggio hello sarà applicazione toohello consegnati nuovamente quando si riavvia.</span><span class="sxs-lookup"><span data-stu-id="5393a-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5393a-170">Spesso si tratta di *almeno una volta elaborazione*, vale a dire, ogni messaggio verrà elaborato almeno una volta ma in hello determinate situazioni potrebbe essere recapitato nuovamente stesso messaggio.</span><span class="sxs-lookup"><span data-stu-id="5393a-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5393a-171">Se hello scenario non tollera la doppia elaborazione, gli sviluppatori di applicazioni devono aggiungere logica aggiuntiva tootheir applicazione toohandle duplicato il recapito dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="5393a-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="5393a-172">Questa operazione viene spesso eseguita utilizzando hello **MessageId** proprietà di messaggio hello che rimangono costante tra i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="5393a-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5393a-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5393a-173">Next steps</span></span>
<span data-ttu-id="5393a-174">toolearn più sulle code, vedere hello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="5393a-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="5393a-175">[Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="5393a-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="5393a-176">Repository [Azure SDK per Node][Azure SDK for Node] su GitHub</span><span class="sxs-lookup"><span data-stu-id="5393a-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="5393a-177">Centro per sviluppatori di Node.js</span><span class="sxs-lookup"><span data-stu-id="5393a-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
