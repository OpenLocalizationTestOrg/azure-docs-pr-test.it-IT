---
title: aaaHow toouse archiviazione delle code da Node.js | Documenti Microsoft
description: Informazioni su come toouse hello Azure coda servizio toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in Node.js.
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
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="7d792-104">Come toouse archiviazione delle code da Node.js</span><span class="sxs-lookup"><span data-stu-id="7d792-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="7d792-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7d792-105">Overview</span></span>
<span data-ttu-id="7d792-106">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello servizio di Accodamento di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d792-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="7d792-107">esempi di Hello vengono scritti utilizzando hello API Node.js.</span><span class="sxs-lookup"><span data-stu-id="7d792-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="7d792-108">Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.</span><span class="sxs-lookup"><span data-stu-id="7d792-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="7d792-109">Creazione di un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="7d792-109">Create a Node.js Application</span></span>
<span data-ttu-id="7d792-110">Creare un'applicazione Node.js vuota.</span><span class="sxs-lookup"><span data-stu-id="7d792-110">Create a blank Node.js application.</span></span> <span data-ttu-id="7d792-111">Per istruzioni di creazione di un'applicazione Node.js, vedere [creare un'app web Node.js in Azure App Service], [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js] utilizzando Windows PowerShell o [ Compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="7d792-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="7d792-112">Configurare l'applicazione tooAccess archiviazione</span><span class="sxs-lookup"><span data-stu-id="7d792-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="7d792-113">toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="7d792-114">Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="7d792-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="7d792-115">Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), passare toohello cartella in cui è stato creato l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="7d792-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="7d792-116">Tipo **npm installare archiviazione di azure** nella finestra di comando hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="7d792-117">Output del comando hello è simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7d792-117">Output from hello command is similar toohello following example.</span></span>
 
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

3. <span data-ttu-id="7d792-118">È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="7d792-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="7d792-119">Questa cartella si troverà hello **archiviazione di azure** pacchetto che contiene le librerie di hello necessarie per accedere all'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7d792-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="7d792-120">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="7d792-120">Import hello package</span></span>
<span data-ttu-id="7d792-121">Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello superiore di **server.js** file dell'applicazione hello in cui si intende toouse archiviazione:</span><span class="sxs-lookup"><span data-stu-id="7d792-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="7d792-122">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7d792-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="7d792-123">modulo Hello azure verrà lette le variabili di ambiente hello AZURE\_archiviazione\_ACCOUNT e AZURE\_archiviazione\_accesso\_chiave o AZURE\_archiviazione\_connessione \_Stringa per le informazioni necessarie tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d792-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7d792-124">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="7d792-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="7d792-125">Per un esempio di impostazione delle variabili di ambiente hello in hello [portale Azure](https://portal.azure.com) per un sito Web di Azure, vedere [app web Node. js utilizzando hello del servizio tabelle di Azure].</span><span class="sxs-lookup"><span data-stu-id="7d792-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="7d792-126">Procedura: creare una coda</span><span class="sxs-lookup"><span data-stu-id="7d792-126">How To: Create a Queue</span></span>
<span data-ttu-id="7d792-127">Hello codice seguente viene creata una **QueueService** oggetto, che consente di toowork con le code.</span><span class="sxs-lookup"><span data-stu-id="7d792-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="7d792-128">Hello utilizzare **createQueueIfNotExists** metodo, che restituisce la coda specificata hello se già esistente o crea una nuova coda con il nome specificato hello se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="7d792-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="7d792-129">Se viene creata la coda hello, `result.created` è true.</span><span class="sxs-lookup"><span data-stu-id="7d792-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="7d792-130">Se non esiste, la coda hello `result.created` è false.</span><span class="sxs-lookup"><span data-stu-id="7d792-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="7d792-131">Filtri</span><span class="sxs-lookup"><span data-stu-id="7d792-131">Filters</span></span>
<span data-ttu-id="7d792-132">Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="7d792-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="7d792-133">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:</span><span class="sxs-lookup"><span data-stu-id="7d792-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="7d792-134">Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti" passaggio di un callback con hello seguente firma:</span><span class="sxs-lookup"><span data-stu-id="7d792-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="7d792-135">In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare finalCallback tooend in caso contrario di hello chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="7d792-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="7d792-136">Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="7d792-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="7d792-137">Hello seguito creato un **QueueService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="7d792-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="7d792-138">Procedura: inserire un messaggio in una coda</span><span class="sxs-lookup"><span data-stu-id="7d792-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="7d792-139">un messaggio in una coda, utilizzare hello tooinsert **createMessage** per creare un nuovo messaggio e aggiungerlo toohello coda.</span><span class="sxs-lookup"><span data-stu-id="7d792-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="7d792-140">Procedura: Leggere hello messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="7d792-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="7d792-141">È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peekMessages** metodo.</span><span class="sxs-lookup"><span data-stu-id="7d792-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="7d792-142">Per impostazione predefinita, **peekMessages** visualizza un singolo messaggio.</span><span class="sxs-lookup"><span data-stu-id="7d792-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="7d792-143">Hello `result` contiene il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="7d792-144">Utilizzando **peekMessages** quando non sono presenti messaggi nella coda di hello non restituirà un errore, tuttavia non verrà restituito alcun messaggio.</span><span class="sxs-lookup"><span data-stu-id="7d792-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="7d792-145">Procedura: Rimozione dalla coda hello messaggio successivo</span><span class="sxs-lookup"><span data-stu-id="7d792-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="7d792-146">L'elaborazione di un messaggio prevede un processo a due fasi:</span><span class="sxs-lookup"><span data-stu-id="7d792-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="7d792-147">Rimozione dalla coda il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="7d792-148">Eliminare il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-148">Delete hello message.</span></span>

<span data-ttu-id="7d792-149">Utilizzare un messaggio, toodequeue **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="7d792-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="7d792-150">In questo modo, i messaggi hello invisibile nella coda di hello, pertanto nessun altro client possa elaborarli.</span><span class="sxs-lookup"><span data-stu-id="7d792-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="7d792-151">Dopo l'applicazione ha elaborato un messaggio, chiamare **deleteMessage** toodelete dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="7d792-152">Hello di esempio seguente ottiene un messaggio, quindi eliminarlo:</span><span class="sxs-lookup"><span data-stu-id="7d792-152">hello following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="7d792-153">Per impostazione predefinita, un messaggio è nascosto solo per 30 secondi, trascorso il quale è visibile tooother client.</span><span class="sxs-lookup"><span data-stu-id="7d792-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="7d792-154">È possibile specificare un valore diverso usando `options.visibilityTimeout` con **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="7d792-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="7d792-155">Utilizzando **getMessages** quando non sono presenti messaggi nella coda di hello non restituirà un errore, tuttavia non verrà restituito alcun messaggio.</span><span class="sxs-lookup"><span data-stu-id="7d792-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="7d792-156">Procedura: Modificare il contenuto di hello di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="7d792-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="7d792-157">È possibile modificare il contenuto di hello di un messaggio sul posto nel hello coda tramite **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="7d792-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="7d792-158">Hello di esempio seguente aggiorna il testo hello di un messaggio:</span><span class="sxs-lookup"><span data-stu-id="7d792-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="7d792-159">Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="7d792-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="7d792-160">È possibile personalizzare il recupero di messaggi da una coda in due modi:</span><span class="sxs-lookup"><span data-stu-id="7d792-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="7d792-161">`options.numOfMessages`-Recuperare un batch di messaggi (in alto too32).</span><span class="sxs-lookup"><span data-stu-id="7d792-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="7d792-162">`options.visibilityTimeout` - consente di impostare un timeout di invisibilità più lungo o più breve.</span><span class="sxs-lookup"><span data-stu-id="7d792-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="7d792-163">esempio Hello utilizza hello **getMessages** messaggi tooget 15 metodo in un'unica chiamata.</span><span class="sxs-lookup"><span data-stu-id="7d792-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="7d792-164">Quindi, ogni messaggio viene elaborato con un ciclo for.</span><span class="sxs-lookup"><span data-stu-id="7d792-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="7d792-165">Imposta inoltre hello invisibilità timeout toofive in minuti per tutti i messaggi restituiti da questo metodo.</span><span class="sxs-lookup"><span data-stu-id="7d792-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="7d792-166">Procedura: Recuperare hello lunghezza coda</span><span class="sxs-lookup"><span data-stu-id="7d792-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="7d792-167">Hello **getQueueMetadata** restituisce i metadati sulla coda di hello, ad esempio il numero approssimativo di messaggi in attesa nella coda di hello hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="7d792-168">Procedura: Elenco di code</span><span class="sxs-lookup"><span data-stu-id="7d792-168">How To: List Queues</span></span>
<span data-ttu-id="7d792-169">un elenco di code, utilizzare tooretrieve **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="7d792-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="7d792-170">tooretrieve un elenco filtrato tramite un prefisso specifico, utilizzare **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="7d792-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="7d792-171">Se non è possibile restituire tutte le code, `result.continuationToken` può essere utilizzato come primo parametro di hello **listQueuesSegmented** o hello secondo parametro di **listQueuesSegmentedWithPrefix** tooretrieve altri risultati.</span><span class="sxs-lookup"><span data-stu-id="7d792-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="7d792-172">Procedura: eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="7d792-172">How To: Delete a Queue</span></span>
<span data-ttu-id="7d792-173">toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **deleteQueue** metodo hello dell'oggetto di coda.</span><span class="sxs-lookup"><span data-stu-id="7d792-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="7d792-174">utilizzare tutti i messaggi da una coda senza eliminarla, tooclear **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="7d792-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="7d792-175">Procedura: usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="7d792-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="7d792-176">Le firme di accesso condiviso (SAS) sono un tooqueues di accesso granulare tooprovide in modo sicuro senza fornire il nome account di archiviazione o chiavi.</span><span class="sxs-lookup"><span data-stu-id="7d792-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="7d792-177">Firma di accesso condiviso è spesso le code di tooyour accesso tooprovide utilizzati limitate, ad esempio per consentire a un'app mobile toosubmit messaggi.</span><span class="sxs-lookup"><span data-stu-id="7d792-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="7d792-178">Un'applicazione attendibile, ad esempio un servizio basato su cloud genera una firma di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **QueueService**e fornisce tooan applicazione non attendibile o semi-trusted.</span><span class="sxs-lookup"><span data-stu-id="7d792-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="7d792-179">Si prenda ad esempio un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7d792-179">For example, a mobile app.</span></span> <span data-ttu-id="7d792-180">Hello firma di accesso condiviso viene generato utilizzando un criterio, che descrive l'avvio di hello e fine in cui hello firma di accesso condiviso è valido, nonché hello titolare SAS toohello concesso livello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7d792-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="7d792-181">Hello di esempio seguente genera un nuovo criterio di accesso condiviso che consente la coda toohello SAS titolare tooadd messaggi hello e scade 100 minuti dopo il tempo di hello che viene creato.</span><span class="sxs-lookup"><span data-stu-id="7d792-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="7d792-182">Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare SAS hello tenta anche coda hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7d792-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="7d792-183">Hello applicazione client, quindi Usa hello SAS con **QueueServiceWithSAS** operazioni tooperform coda hello.</span><span class="sxs-lookup"><span data-stu-id="7d792-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="7d792-184">Hello di esempio seguente si connette toohello coda e crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="7d792-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="7d792-185">Poiché hello firma di accesso condiviso è stato generato con Aggiungi accesso, se un tentativo sono stato apportato tooread, aggiornare o eliminare i messaggi, verrebbe restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="7d792-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="7d792-186">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="7d792-186">Access control lists</span></span>
<span data-ttu-id="7d792-187">È inoltre possibile utilizzare un criterio di accesso hello tooset elenco di controllo di accesso (ACL) per una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="7d792-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="7d792-188">Ciò è utile se si desidera tooallow coda hello di più client tooaccess, ma forniscono criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="7d792-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="7d792-189">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="7d792-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="7d792-190">Hello di esempio seguente definisce due criteri; uno per "user1" e uno per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="7d792-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="7d792-191">Hello seguente esempio ottiene hello gli ACL per **myqueue**, quindi vengono aggiunti nuovi criteri hello utilizzando **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="7d792-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="7d792-192">Risultato:</span><span class="sxs-lookup"><span data-stu-id="7d792-192">This approach allows:</span></span>

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

<span data-ttu-id="7d792-193">Una volta hello che ACL è stato impostato, è quindi possibile creare una firma di accesso condiviso in base all'ID di hello per un criterio.</span><span class="sxs-lookup"><span data-stu-id="7d792-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="7d792-194">Hello di esempio seguente crea una nuova firma di accesso condiviso per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="7d792-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="7d792-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d792-195">Next Steps</span></span>
<span data-ttu-id="7d792-196">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="7d792-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="7d792-197">Visitare hello [Blog del Team di archiviazione Azure][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="7d792-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="7d792-198">Visitare hello [Azure Storage SDK per nodo] [ Azure Storage SDK for Node] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d792-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[creare un'app web Node.js in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[app web Node. js utilizzando hello del servizio tabelle di Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
