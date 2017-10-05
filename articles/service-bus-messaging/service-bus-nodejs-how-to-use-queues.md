---
title: Come usare le code del bus di servizio in Node.js | Microsoft Docs
description: Informazioni su come usare le code del bus di servizio in Azure da un'app Node.js.
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
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="70af1-103">Come usare le code del bus di servizio con Node.js</span><span class="sxs-lookup"><span data-stu-id="70af1-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="70af1-104">Questo articolo illustra come usare le code del bus di servizio con Node.js.</span><span class="sxs-lookup"><span data-stu-id="70af1-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="70af1-105">Gli esempi sono scritti in JavaScript e utilizzano il modulo Node.js di Azure.</span><span class="sxs-lookup"><span data-stu-id="70af1-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="70af1-106">Gli scenari presentati includono la **creazione di code**, l'**invio e la ricezione di messaggi** e l'**eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="70af1-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="70af1-107">Per altre informazioni sulle code, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="70af1-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="70af1-108">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="70af1-108">Create a Node.js application</span></span>
<span data-ttu-id="70af1-109">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="70af1-109">Create a blank Node.js application.</span></span> <span data-ttu-id="70af1-110">Per istruzioni su come creare un'applicazione Node.js, vedere [Creare un'app Web Node.js nel servizio app di Azure][Create and deploy a Node.js application to an Azure Website] oppure [Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure][Node.js Cloud Service] con Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70af1-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="70af1-111">Configurare l'applicazione per l'uso del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="70af1-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="70af1-112">Per usare il bus di servizio di Azure, scaricare e usare il pacchetto Azure Node.js</span><span class="sxs-lookup"><span data-stu-id="70af1-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="70af1-113">che include un set di librerie di riferimento che comunicano con i servizi REST del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="70af1-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="70af1-114">Usare Node Package Manager (NPM) per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="70af1-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="70af1-115">Usare la finestra di comando **Windows PowerShell per Node.js** per passare alla cartella **c:\\node\\sbqueues\\WebRole1** in cui è stata creata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="70af1-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="70af1-116">Digitare **npm install azure** nella finestra di comando, che dovrebbe restituire un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="70af1-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

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
3. <span data-ttu-id="70af1-117">È possibile eseguire manualmente il comando **ls** per verificare che sia stata creata una cartella **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="70af1-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="70af1-118">All'interno di tale cartella individuare il pacchetto **azure**, che contiene le librerie necessarie per accedere alle code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="70af1-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="70af1-119">Importare il modulo</span><span class="sxs-lookup"><span data-stu-id="70af1-119">Import the module</span></span>
<span data-ttu-id="70af1-120">Usando il Blocco note o un altro editor di testo, aggiungere quanto segue alla parte superiore del file **server.js** dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="70af1-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="70af1-121">Configurare una connessione del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="70af1-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="70af1-122">Il modulo di Azure legge la variabile di ambiente `AZURE_SERVICEBUS_CONNECTION_STRING` per ottenere le informazioni necessarie per la connessione al bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="70af1-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="70af1-123">Se questa variabile di ambiente non è impostata, è necessario specificare le informazioni relative all'account durante la chiamata di `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="70af1-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="70af1-124">Per un esempio di impostazione delle variabili di ambiente in un file di configurazione per un servizio cloud di Azure, vedere [Creazione di un'applicazione Web Node.js con Archiviazione][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="70af1-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="70af1-125">Per un esempio di impostazione delle variabili di ambiente nel [portale di Azure][Azure portal] per un sito Web di Azure, vedere [Node.js Web Application with Storage][Node.js Web Application with Storage] (Applicazione Web Node.js con Archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="70af1-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="70af1-126">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="70af1-126">Create a queue</span></span>
<span data-ttu-id="70af1-127">L'oggetto **ServiceBusService** consente di usare le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="70af1-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="70af1-128">Il codice seguente consente di creare un oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="70af1-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="70af1-129">Aggiungerlo nella parte superiore del file **server.js** dopo l'istruzione per importare il modulo Azure:</span><span class="sxs-lookup"><span data-stu-id="70af1-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="70af1-130">Chiamando `createQueueIfNotExists` nell'oggetto **ServiceBusService**, viene restituita la coda specificata, se esistente, oppure viene creata una nuova coda con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="70af1-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="70af1-131">Il codice seguente usa `createQueueIfNotExists` per connettersi alla coda denominata `myqueue` o crearla:</span><span class="sxs-lookup"><span data-stu-id="70af1-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="70af1-132">Il metodo `createServiceBusService` supporta anche opzioni aggiuntive che consentono di eseguire l'override delle impostazioni predefinite delle code, come la durata (TTL) dei messaggi o le dimensioni massime della coda.</span><span class="sxs-lookup"><span data-stu-id="70af1-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="70af1-133">Il seguente esempio illustra come impostare la dimensione massima della coda su 5 GB e una durata (TTL) di 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="70af1-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="70af1-134">Filtri</span><span class="sxs-lookup"><span data-stu-id="70af1-134">Filters</span></span>
<span data-ttu-id="70af1-135">Le operazioni di filtro facoltative possono essere applicate alle operazioni eseguite usando **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="70af1-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="70af1-136">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con la firma:</span><span class="sxs-lookup"><span data-stu-id="70af1-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="70af1-137">Dopo avere eseguito la pre-elaborazione sulle opzioni della richiesta, il metodo deve chiamare `next` passando un callback con la seguente firma:</span><span class="sxs-lookup"><span data-stu-id="70af1-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="70af1-138">Dopo l'elaborazione di `returnObject` (ossia della risposta della richiesta al server), questo callback deve richiamare `next`, se esistente, per continuare a elaborare altri filtri oppure richiamare semplicemente `finalCallback` per terminare la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="70af1-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="70af1-139">In Azure SDK per Node.js sono inclusi due filtri che implementano la logica di ripetizione dei tentativi, `ExponentialRetryPolicyFilter` e `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="70af1-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="70af1-140">Il codice seguente crea un oggetto `ServiceBusService` che usa `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="70af1-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="70af1-141">Inviare messaggi a una coda</span><span class="sxs-lookup"><span data-stu-id="70af1-141">Send messages to a queue</span></span>
<span data-ttu-id="70af1-142">Per inviare un messaggio a una coda del bus di servizio, l'applicazione chiama il metodo `sendQueueMessage` per l'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="70af1-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="70af1-143">I messaggi inviati e ricevuti dalle code del bus di servizio sono oggetti **BrokeredMessage** e includono un set di proprietà standard, ad esempio **Label** e **TimeToLive**, un dizionario usato per contenere le proprietà personalizzate specifiche dell'applicazione e un corpo di dati arbitrari dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70af1-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="70af1-144">Un'applicazione può impostare il corpo del messaggio passando una stringa come messaggio.</span><span class="sxs-lookup"><span data-stu-id="70af1-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="70af1-145">Le proprietà standard necessarie vengono popolate con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="70af1-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="70af1-146">L'esempio seguente illustra come inviare un messaggio di prova alla coda denominata `myqueue` usando `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="70af1-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="70af1-147">Le code del bus di servizio supportano messaggi di dimensioni fino a 256 KB nel [livello Standard](service-bus-premium-messaging.md) e fino a 1 MB nel [livello Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="70af1-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="70af1-148">Le dimensioni massime dell'intestazione, che include le proprietà standard e personalizzate dell'applicazione, non possono superare 64 KB.</span><span class="sxs-lookup"><span data-stu-id="70af1-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="70af1-149">Non esiste alcun limite al numero di messaggi mantenuti in una coda, mentre è prevista una limitazione alla dimensione totale dei messaggi di una coda.</span><span class="sxs-lookup"><span data-stu-id="70af1-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="70af1-150">Questa dimensione della coda viene definita al momento della creazione, con un limite massimo di 5 GB.</span><span class="sxs-lookup"><span data-stu-id="70af1-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="70af1-151">Per altre informazioni sulle quote, vedere [Quote del bus di servizio][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="70af1-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="70af1-152">Ricevere messaggi da una coda</span><span class="sxs-lookup"><span data-stu-id="70af1-152">Receive messages from a queue</span></span>
<span data-ttu-id="70af1-153">I messaggi vengono ricevuti da una coda usando il metodo `receiveQueueMessage` nell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="70af1-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="70af1-154">Per impostazione predefinita, i messaggi vengono eliminati dalla coda non appena vengono letti. È tuttavia possibile leggere (visualizzare) e bloccare il messaggio senza eliminarlo dalla coda impostando il parametro facoltativo `isPeekLock` su **true**.</span><span class="sxs-lookup"><span data-stu-id="70af1-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="70af1-155">Il comportamento predefinito di lettura ed eliminazione del messaggio nell'ambito dell'operazione di ricezione costituisce il modello più semplice ed è adatto per scenari in cui un'applicazione può tollerare la mancata elaborazione di un messaggio in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="70af1-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="70af1-156">Per comprendere meglio questo meccanismo, si consideri uno scenario in cui il consumer invia la richiesta di ricezione e viene arrestato in modo anomalo prima dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="70af1-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="70af1-157">Poiché il bus di servizio contrassegna il messaggio come utilizzato, quando l'applicazione viene riavviata e inizia a utilizzare nuovamente i messaggi, il messaggio utilizzato prima dell'arresto anomalo risulterà perso.</span><span class="sxs-lookup"><span data-stu-id="70af1-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="70af1-158">Se il parametro `isPeekLock` è impostato su **true**, l'operazione di ricezione viene suddivisa in due fasi, in modo da consentire il supporto di applicazioni che non possono tollerare messaggi mancanti.</span><span class="sxs-lookup"><span data-stu-id="70af1-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="70af1-159">Quando il bus di servizio riceve una richiesta, individua il messaggio successivo da usare, lo blocca per impedirne la ricezione da parte di altri consumer e quindi lo restituisce all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70af1-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="70af1-160">Dopo aver elaborato il messaggio o averlo archiviato in modo affidabile per una successiva elaborazione, l'applicazione esegue la seconda fase del processo di ricezione chiamando il metodo `deleteMessage` e specificando il messaggio da eliminare come parametro.</span><span class="sxs-lookup"><span data-stu-id="70af1-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="70af1-161">Il metodo `deleteMessage` contrassegna il messaggio come utilizzato e lo rimuove dalla coda.</span><span class="sxs-lookup"><span data-stu-id="70af1-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="70af1-162">L'esempio seguente illustra come ricevere ed elaborare messaggi usando `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="70af1-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="70af1-163">L'esempio prima di tutto riceve ed elimina un messaggio, quindi riceve un messaggio con `isPeekLock` impostato su **true** e infine elimina il messaggio con `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="70af1-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="70af1-164">Come gestire arresti anomali e messaggi illeggibili dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="70af1-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="70af1-165">Il bus di servizio fornisce funzionalità per il ripristino gestito automaticamente in caso di errori nell'applicazione o di problemi di elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="70af1-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="70af1-166">Se un'applicazione ricevente non riesce a elaborare il messaggio per qualsiasi motivo, può chiamare il metodo `unlockMessage` nell'oggetto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="70af1-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="70af1-167">In questo modo, il bus di servizio sbloccherà il messaggio nella coda rendendolo nuovamente disponibile per la ricezione da parte della stessa o da un'altra applicazione consumer.</span><span class="sxs-lookup"><span data-stu-id="70af1-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="70af1-168">Al messaggio bloccato nella coda è inoltre associato un timeout. Se l'applicazione non riesce a elaborare il messaggio prima della scadenza del timeout, ad esempio a causa di un arresto anomalo, il bus di servizio sbloccherà automaticamente il messaggio rendendolo nuovamente disponibile per la ricezione.</span><span class="sxs-lookup"><span data-stu-id="70af1-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="70af1-169">In caso di arresto anomalo dell'applicazione dopo l'elaborazione del messaggio ma prima della chiamata del metodo `deleteMessage`, il messaggio verrà nuovamente recapitato all'applicazione al riavvio.</span><span class="sxs-lookup"><span data-stu-id="70af1-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="70af1-170">Questo processo di elaborazione viene spesso definito di tipo *At-Least-Once*, per indicare che ogni messaggio verrà elaborato almeno una volta ma che in determinate situazioni potrà essere recapitato una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="70af1-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="70af1-171">Se lo scenario non tollera la doppia elaborazione, gli sviluppatori dovranno aggiungere logica aggiuntiva all'applicazione per gestire il secondo recapito del messaggio.</span><span class="sxs-lookup"><span data-stu-id="70af1-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="70af1-172">A tale scopo viene spesso usata la proprietà **MessageId** del messaggio, che rimane costante in tutti i tentativi di recapito.</span><span class="sxs-lookup"><span data-stu-id="70af1-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70af1-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70af1-173">Next steps</span></span>
<span data-ttu-id="70af1-174">Per altre informazioni sulle code, vedere le risorse seguenti.</span><span class="sxs-lookup"><span data-stu-id="70af1-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="70af1-175">[Code, argomenti e sottoscrizioni del bus di servizio][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="70af1-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="70af1-176">Repository [Azure SDK per Node][Azure SDK for Node] su GitHub</span><span class="sxs-lookup"><span data-stu-id="70af1-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="70af1-177">Centro per sviluppatori di Node.js</span><span class="sxs-lookup"><span data-stu-id="70af1-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
