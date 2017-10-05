---
title: Come usare l'archiviazione code da Node.js | Microsoft Docs
description: Informazioni su come usare il servizio di accodamento di Azure per creare ed eliminare code e per inserire, visualizzare ed eliminare messaggi. Gli esempi sono scritti in Node.js.
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 15c1d3cb6eac8fc14837277c4a4275dea91701cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="6dad7-104">Come usare l'archiviazione di accodamento da Node.js</span><span class="sxs-lookup"><span data-stu-id="6dad7-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="6dad7-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6dad7-105">Overview</span></span>
<span data-ttu-id="6dad7-106">In questa guida viene illustrato come eseguire scenari comuni del Servizio di accodamento di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6dad7-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="6dad7-107">Gli esempi sono scritti usando l'API Node.js.</span><span class="sxs-lookup"><span data-stu-id="6dad7-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="6dad7-108">Gli scenari illustrati includono **inserimento**, **visualizzazione**, **recupero** ed **eliminazione** dei messaggi in coda, oltre alla **creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="6dad7-109">Creazione di un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="6dad7-109">Create a Node.js Application</span></span>
<span data-ttu-id="6dad7-110">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="6dad7-110">Create a blank Node.js application.</span></span> <span data-ttu-id="6dad7-111">Per istruzioni sulla creazione di un'applicazione Node.js, vedere [Creare un'app Web Node.js nel servizio app di Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) con Windows PowerShell, o [Creazione e distribuzione di un sito Web Node.js in Azure con WebMatrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="6dad7-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="6dad7-112">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="6dad7-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="6dad7-113">Per usare l'archiviazione di Azure, è necessario scaricare Azure Storage SDK per Node.js, che comprende un set di pratiche librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="6dad7-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="6dad7-114">Usare Node Package Manager (NPM) per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="6dad7-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="6dad7-115">Usare un'interfaccia della riga di comando come **PowerShell** (Windows,) **Terminal** (Mac,) o **Bash** (Unix) e spostarsi nella cartella in cui è stata creata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="6dad7-116">Digitare **npm install azure-storage** nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="6dad7-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="6dad7-117">L'output da questo comando sarà simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="6dad7-117">Output from the command is similar to the following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="6dad7-118">È possibile eseguire manualmente il comando **ls** per verificare che sia stata creata una cartella **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="6dad7-119">All'interno di questa cartella si trova il pacchetto **azure-storage** , che contiene le librerie necessarie per accedere all'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6dad7-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="6dad7-120">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="6dad7-120">Import the package</span></span>
<span data-ttu-id="6dad7-121">Utilizzando il Blocco note o un altro editor di testo, aggiungere quanto segue alla parte superiore del file **server.js** dell'applicazione dove si intende utilizzare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="6dad7-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="6dad7-122">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6dad7-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="6dad7-123">I modulo di Azure leggerà le variabili di ambiente AZURE\_STORAGE\_ACCOUNT e AZURE\_STORAGE\_ACCESS\_KEY, o AZURE\_STORAGE\_CONNECTION\_STRING per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6dad7-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="6dad7-124">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account quando si chiama **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="6dad7-125">Per un esempio di impostazione delle variabili di ambiente nel [portale di Azure](https://portal.azure.com) per un sito Web di Azure, vedere [App Web Node.js con il servizio tabelle di Azure].</span><span class="sxs-lookup"><span data-stu-id="6dad7-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="6dad7-126">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="6dad7-126">How To: Create a Queue</span></span>
<span data-ttu-id="6dad7-127">La coda seguente crea un oggetto **QueueService** che consente di utilizzare le code.</span><span class="sxs-lookup"><span data-stu-id="6dad7-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="6dad7-128">Utilizzare il metodo **createQueueIfNotExists** che restituisce la coda specificata se esiste già o, in caso contrario, crea una nuova coda con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="6dad7-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="6dad7-129">Se la coda viene creata, `result.created` è true.</span><span class="sxs-lookup"><span data-stu-id="6dad7-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="6dad7-130">Se la coda esiste già, `result.created` è false.</span><span class="sxs-lookup"><span data-stu-id="6dad7-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="6dad7-131">Filtri</span><span class="sxs-lookup"><span data-stu-id="6dad7-131">Filters</span></span>
<span data-ttu-id="6dad7-132">Le operazioni di filtro facoltative possono essere applicate alle operazioni eseguite usando **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="6dad7-133">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con la firma:</span><span class="sxs-lookup"><span data-stu-id="6dad7-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="6dad7-134">Dopo avere eseguito la pre-elaborazione sulle opzioni della richiesta, il metodo deve chiamare "next" passando un callback con la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="6dad7-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="6dad7-135">In questo callback, e dopo l'elaborazione del returnObject (la risposta della richiesta al server), il callback deve richiamare "next", se questo esiste, per continuare a elaborare altri filtri oppure semplicemente richiamare finalCallback per concludere la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="6dad7-136">In Azure SDK per Node.js sono inclusi due filtri che implementano la logica di ripetizione dei tentativi. Sono **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="6dad7-137">Il codice seguente consente di creare un oggetto **QueueService** che usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="6dad7-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="6dad7-138">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="6dad7-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="6dad7-139">Per inserire un messaggio in una coda, utilizzare il metodo **createMessage** per creare un nuovo messaggio e aggiungerlo alla coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="6dad7-140">Procedura: visualizzare il messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="6dad7-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="6dad7-141">È possibile visualizzare il messaggio successivo di una coda senza rimuoverlo dalla coda chiamando il metodo **peekMessages** .</span><span class="sxs-lookup"><span data-stu-id="6dad7-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="6dad7-142">Per impostazione predefinita, **peekMessages** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="6dad7-143">`result` contiene il messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="6dad7-144">Se si usa **peekMessages** in assenza di messaggi nella coda, non viene visualizzato un errore, ma non vengono restituiti messaggi.</span><span class="sxs-lookup"><span data-stu-id="6dad7-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="6dad7-145">Procedura: rimuovere il messaggio successivo dalla coda</span><span class="sxs-lookup"><span data-stu-id="6dad7-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="6dad7-146">L'elaborazione di un messaggio prevede un processo a due fasi:</span><span class="sxs-lookup"><span data-stu-id="6dad7-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="6dad7-147">Rimozione del messaggio dalla coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-147">Dequeue the message.</span></span>
2. <span data-ttu-id="6dad7-148">Eliminazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-148">Delete the message.</span></span>

<span data-ttu-id="6dad7-149">Per rimuovere un messaggio dalla coda usare **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="6dad7-150">Il messaggio viene reso invisibile nella coda, quindi nessun altro client può elaborarlo.</span><span class="sxs-lookup"><span data-stu-id="6dad7-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="6dad7-151">Dopo che l'applicazione ha elaborato il messaggio, chiamare **deleteMessage** per eliminarlo dalla coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="6dad7-152">Nell'esempio seguente il messaggio viene prima richiamato, quindi eliminato:</span><span class="sxs-lookup"><span data-stu-id="6dad7-152">The following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="6dad7-153">Per impostazione predefinita, un messaggio viene nascosto solo per 30 secondi, dopo i quali torna visibile agli altri client.</span><span class="sxs-lookup"><span data-stu-id="6dad7-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="6dad7-154">È possibile specificare un valore diverso usando `options.visibilityTimeout` con **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="6dad7-155">Se si usa **getMessages** in assenza di messaggi nella coda, non viene visualizzato un errore, ma non vengono restituiti messaggi.</span><span class="sxs-lookup"><span data-stu-id="6dad7-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="6dad7-156">Procedura: cambiare il contenuto di un messaggio accodato</span><span class="sxs-lookup"><span data-stu-id="6dad7-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="6dad7-157">È possibile cambiare il contenuto di un messaggio inserito nella coda con **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="6dad7-158">Nell'esempio seguente viene aggiornato il testo di un messaggio:</span><span class="sxs-lookup"><span data-stu-id="6dad7-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="6dad7-159">Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="6dad7-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="6dad7-160">È possibile personalizzare il recupero di messaggi da una coda in due modi:</span><span class="sxs-lookup"><span data-stu-id="6dad7-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="6dad7-161">`options.numOfMessages` - consente di recuperare un batch di messaggi (massimo 32).</span><span class="sxs-lookup"><span data-stu-id="6dad7-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="6dad7-162">`options.visibilityTimeout` - consente di impostare un timeout di invisibilità più lungo o più breve.</span><span class="sxs-lookup"><span data-stu-id="6dad7-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="6dad7-163">Nell'esempio seguente viene usato il metodo **getMessages** per recuperare 15 messaggi con una sola chiamata.</span><span class="sxs-lookup"><span data-stu-id="6dad7-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="6dad7-164">Quindi, ogni messaggio viene elaborato con un ciclo for.</span><span class="sxs-lookup"><span data-stu-id="6dad7-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="6dad7-165">Per tutti i messaggi restituiti dal metodo, inoltre, il timeout di invisibilità viene impostato su cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="6dad7-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="6dad7-166">Procedura: recuperare la lunghezza delle code</span><span class="sxs-lookup"><span data-stu-id="6dad7-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="6dad7-167">**getQueueMetadata** restituisce metadati relativi alla coda, includendo il numero approssimativo di messaggi in attesa nella coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="6dad7-168">Procedura: Elenco di code</span><span class="sxs-lookup"><span data-stu-id="6dad7-168">How To: List Queues</span></span>
<span data-ttu-id="6dad7-169">Per recuperare un elenco di code, usare **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="6dad7-170">Per recuperare un elenco filtrato in base a uno specifico prefisso, usare **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="6dad7-171">Se non possono essere restituite tutte le code, è possibile usare `result.continuationToken` come primo parametro di **listQueuesSegmented** o secondo parametro di **listQueuesSegmentedWithPrefix** per recuperare più risultati.</span><span class="sxs-lookup"><span data-stu-id="6dad7-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="6dad7-172">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="6dad7-172">How To: Delete a Queue</span></span>
<span data-ttu-id="6dad7-173">Per eliminare una coda e tutti i messaggi che contiene, chiamare il metodo **deleteQueue** sull'oggetto coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="6dad7-174">Per deselezionare tutti i messaggi da una coda senza eliminarla, usare **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="6dad7-175">Procedura: usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="6dad7-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="6dad7-176">Le firme di accesso condiviso rappresentano un modo sicuro per fornire accesso granulare alle code senza specificare il nome o le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6dad7-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="6dad7-177">Le firme di accesso condiviso vengono spesso usate per fornire accesso limitato alle code, ad esempio per consentire a un'app per dispositivi mobili di inviare messaggi.</span><span class="sxs-lookup"><span data-stu-id="6dad7-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="6dad7-178">Un'applicazione attendibile, ad esempio un servizio basato sul cloud, genera una firma di accesso condiviso tramite il metodo **generateSharedAccessSignature** dell'oggetto **QueueService** e la fornisce a un'applicazione non attendibile o parzialmente attendibile.</span><span class="sxs-lookup"><span data-stu-id="6dad7-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="6dad7-179">Si prenda ad esempio un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="6dad7-179">For example, a mobile app.</span></span> <span data-ttu-id="6dad7-180">La firma di accesso condiviso viene generata tramite un criterio che indica le date di inizio e di fine del periodo di validità della firma, nonché il livello di accesso concesso al titolare della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="6dad7-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="6dad7-181">Nell'esempio seguente viene generato un nuovo criterio di accesso condiviso che consentirà al titolare della firma di accesso condiviso di aggiungere i messaggi alla coda e che scadrà 100 minuti dopo la data di creazione.</span><span class="sxs-lookup"><span data-stu-id="6dad7-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="6dad7-182">Si noti che è necessario fornire anche le informazioni sull'host, in quanto sono necessarie quando il titolare della firma di accesso condiviso tenta di accedere alla coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="6dad7-183">L'applicazione client usa quindi la firma di accesso condiviso con il metodo **QueueServiceWithSAS** per eseguire operazioni sulla coda.</span><span class="sxs-lookup"><span data-stu-id="6dad7-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="6dad7-184">Nell'esempio seguente viene eseguita la connessione alla coda e viene creato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="6dad7-185">Poiché la firma di accesso condiviso è stata generata con accesso di aggiunta, se si tentasse di leggere, aggiornare o eliminare i messaggi verrebbe restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="6dad7-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="6dad7-186">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="6dad7-186">Access control lists</span></span>
<span data-ttu-id="6dad7-187">Per impostare i criteri di accesso per una firma di accesso condiviso è anche possibile usare un elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="6dad7-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="6dad7-188">Questa soluzione è utile quando si vuole consentire a più client di accedere alla coda, impostando tuttavia criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="6dad7-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="6dad7-189">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="6dad7-190">L'esempio seguente definisce due criteri, uno per 'user1' e uno per 'user2':</span><span class="sxs-lookup"><span data-stu-id="6dad7-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="6dad7-191">Nell'esempio seguente viene recuperato l'elenco di controllo di accesso corrente per **myqueue** e vengono aggiunti i nuovi criteri tramite **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="6dad7-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="6dad7-192">Risultato:</span><span class="sxs-lookup"><span data-stu-id="6dad7-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="6dad7-193">Dopo avere impostato l'elenco di controllo di accesso, è possibile creare una firma di accesso condiviso in base all'ID di un criterio.</span><span class="sxs-lookup"><span data-stu-id="6dad7-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="6dad7-194">Nell'esempio seguente viene creata una nuova firma di accesso condiviso per 'user2':</span><span class="sxs-lookup"><span data-stu-id="6dad7-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="6dad7-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6dad7-195">Next Steps</span></span>
<span data-ttu-id="6dad7-196">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione di accodamento, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="6dad7-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="6dad7-197">Visitare il [Blog del team di Archiviazione di Azure][Blog del team di Archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="6dad7-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="6dad7-198">Vedere il repository [Azure Storage SDK per Node][Azure Storage SDK for Node] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="6dad7-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="6dad7-199">
[Creare un'app Web Node.js in Servizio app di Azure](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="6dad7-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="6dad7-200">[App Web Node.js con il servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="6dad7-200">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="6dad7-201">[Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="6dad7-201">[Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="6dad7-202">[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/ [Creazione e distribuzione di un'app Web Node.js in Azure con WebMatrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="6dad7-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
