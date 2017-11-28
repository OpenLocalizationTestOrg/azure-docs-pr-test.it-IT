---
title: aaaGetting avviato con l'archiviazione delle code e Visual Studio (progetti processi Web) di servizi connessi | Documenti Microsoft
description: Come tooget iniziare a usare l'archiviazione delle code di Azure in un progetto processo Web dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi.
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="c208d-103">Introduzione all'archiviazione di accodamento di Azure e ai servizi relativi a Visual Studio (progetti WebJob)</span><span class="sxs-lookup"><span data-stu-id="c208d-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c208d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c208d-104">Overview</span></span>
<span data-ttu-id="c208d-105">Questo articolo viene descritto come ottenere avviato mediante Azure coda di archiviazione in un progetto processo Web di Visual Studio Azure dopo aver creato o riferimento a un account di archiviazione di Azure tramite hello Visual Studio **aggiungere servizi connessi** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c208d-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="c208d-106">Quando si aggiunge un progetto di processo Web tooa account di archiviazione usando Visual Studio hello **aggiungere servizi connessi** finestra di dialogo, sono installati pacchetti NuGet di archiviazione di Azure appropriati hello, riferimenti .NET appropriati hello vengono aggiuntivo toohello progetto e stringhe di connessione per l'account di archiviazione hello vengono aggiornate nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="c208d-107">In questo articolo vengono forniti esempi di codice c# che mostrano come toouse hello Azure WebJobs SDK versione 1. x con il servizio di archiviazione di Azure coda hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="c208d-108">Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c208d-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c208d-109">Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c208d-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="c208d-110">Per altre informazioni, vedere [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="c208d-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="c208d-111">Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="c208d-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="c208d-112">Come tootrigger una funzione quando viene ricevuto un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="c208d-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="c208d-113">chiama una funzione che hello WebJobs SDK toowrite quando viene ricevuto un messaggio nella coda, utilizzare hello **QueueTrigger** attributo.</span><span class="sxs-lookup"><span data-stu-id="c208d-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="c208d-114">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello di hello coda toopoll.</span><span class="sxs-lookup"><span data-stu-id="c208d-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="c208d-115">toosee come tooset hello nome della coda in modo dinamico, estrarre [come opzioni di configurazione tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c208d-116">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="c208d-116">String queue messages</span></span>
<span data-ttu-id="c208d-117">Nell'esempio seguente di hello, hello coda contiene una stringa di messaggio, pertanto **QueueTrigger** tooa applicato parametro di stringa denominato **logMessage** che comprende il contenuto di hello del messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="c208d-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="c208d-118">funzione Hello [scrive un toohello messaggio log Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="c208d-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="c208d-119">Oltre a **stringa**, il parametro hello può essere una matrice di byte, un **CloudQueueMessage** oggetto o un POCO definiti.</span><span class="sxs-lookup"><span data-stu-id="c208d-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c208d-120">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c208d-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c208d-121">Nell'esempio seguente di hello, messaggio della coda contiene JSON per un **BlobInformation** oggetto che include un **BlobName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="c208d-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="c208d-122">Hello SDK deserializza automaticamente oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="c208d-123">Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="c208d-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c208d-124">Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.</span><span class="sxs-lookup"><span data-stu-id="c208d-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="c208d-125">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="c208d-125">Async functions</span></span>
<span data-ttu-id="c208d-126">Hello seguente funzione async [scrive un toohello log Dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="c208d-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="c208d-127">Le funzioni asincrone potrebbero richiedere un [token di annullamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), come illustrato nell'esempio che consente di copiare un blob seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="c208d-128">(Per una spiegazione di hello **queueTrigger** segnaposto, vedere hello [BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sezione.)</span><span class="sxs-lookup"><span data-stu-id="c208d-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="c208d-129">Attributo di tipi hello QueueTrigger funziona con</span><span class="sxs-lookup"><span data-stu-id="c208d-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="c208d-130">È possibile utilizzare **QueueTrigger** con hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="c208d-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="c208d-131">**string**</span><span class="sxs-lookup"><span data-stu-id="c208d-131">**string**</span></span>
* <span data-ttu-id="c208d-132">Tipo POCO serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="c208d-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="c208d-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="c208d-133">**byte[]**</span></span>
* <span data-ttu-id="c208d-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="c208d-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="c208d-135">Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="c208d-135">Polling algorithm</span></span>
<span data-ttu-id="c208d-136">Hello SDK implementa un effetto di hello esponenziale Backoff algoritmo casuali tooreduce di inattività della coda del polling sui costi delle transazioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c208d-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="c208d-137">Quando viene trovato un messaggio, hello SDK attende due secondi e ne controlla la presenza di un altro messaggio. Quando viene trovato alcun messaggio rimane in attesa circa quattro secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="c208d-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="c208d-138">Dopo i tentativi non riusciti successivi tooget un messaggio nella coda, il tempo di attesa hello continua tooincrease finché raggiunge il tempo di attesa massimo hello, il minuto tooone valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="c208d-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="c208d-139">[Hello tempo di attesa massimo è configurabile](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="c208d-140">Più istanze</span><span class="sxs-lookup"><span data-stu-id="c208d-140">Multiple instances</span></span>
<span data-ttu-id="c208d-141">Se l'app web viene eseguito su più istanze, viene eseguito un processi Web continui in ogni computer e ogni computer tenterà di attesa per i trigger e funzioni toorun.</span><span class="sxs-lookup"><span data-stu-id="c208d-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="c208d-142">Funzioni toosome elaborazione hello due volte, in alcuni scenari, che questo può causare stessi dati funzioni devono essere idempotenti (scritto in modo che chiama ripetutamente con stessi dati di input non producono hello duplicare risultati).</span><span class="sxs-lookup"><span data-stu-id="c208d-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="c208d-143">Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="c208d-143">Parallel execution</span></span>
<span data-ttu-id="c208d-144">Se si dispongono di più funzioni in attesa in code diverse, hello SDK verrà chiamarli in parallelo quando vengono ricevuti i messaggi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c208d-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="c208d-145">Hello stesso vale quando vengono ricevuti più messaggi per una singola coda.</span><span class="sxs-lookup"><span data-stu-id="c208d-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="c208d-146">Per impostazione predefinita, hello SDK riceve un batch di messaggi in coda 16 alla volta ed esegue funzione hello elaborarli in parallelo.</span><span class="sxs-lookup"><span data-stu-id="c208d-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="c208d-147">[dimensioni del batch Hello sono configurabile](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="c208d-148">Quando il numero di hello elaborato Ottiene verso il basso toohalf della dimensione di batch di hello, hello SDK riceve un altro batch e inizia l'elaborazione di tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="c208d-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="c208d-149">Numero massimo di hello simultanee messaggi vengano elaborati per ogni funzione pertanto è dimensioni di batch di una volta e mezza hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="c208d-150">Questo limite si applica separatamente tooeach funzione che ha un **QueueTrigger** attributo.</span><span class="sxs-lookup"><span data-stu-id="c208d-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="c208d-151">Se non si desidera l'esecuzione parallela per i messaggi ricevuti su una coda, impostare too1 dimensioni di batch hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="c208d-152">Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="c208d-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="c208d-153">È possibile ottenere hello seguenti proprietà di messaggio mediante l'aggiunta di firma del metodo toohello parametri:</span><span class="sxs-lookup"><span data-stu-id="c208d-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="c208d-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="c208d-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="c208d-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="c208d-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="c208d-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="c208d-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="c208d-157">**string** queueTrigger (contiene il testo del messaggio)</span><span class="sxs-lookup"><span data-stu-id="c208d-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="c208d-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="c208d-158">**string** id</span></span>
* <span data-ttu-id="c208d-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="c208d-159">**string** popReceipt</span></span>
* <span data-ttu-id="c208d-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="c208d-160">**int** dequeueCount</span></span>

<span data-ttu-id="c208d-161">Se si desidera toowork direttamente con hello API di archiviazione di Azure, è inoltre possibile aggiungere un **CloudStorageAccount** parametro.</span><span class="sxs-lookup"><span data-stu-id="c208d-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="c208d-162">Hello nell'esempio seguente vengono tutti il registro applicazioni di metadati tooan INFO.</span><span class="sxs-lookup"><span data-stu-id="c208d-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="c208d-163">Nell'esempio hello logMessage sia queueTrigger contenuto hello di messaggio della coda hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="c208d-164">Di seguito è riportato un log di esempio scritto dal codice di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="c208d-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="c208d-165">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="c208d-165">Graceful shutdown</span></span>
<span data-ttu-id="c208d-166">Una funzione che viene eseguito in un processo Web continuo può accettare un **CancellationToken** parametro che consente di hello toonotify hello funzione del sistema operativo quando hello processo Web sta toobe terminato.</span><span class="sxs-lookup"><span data-stu-id="c208d-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="c208d-167">È possibile utilizzare questo toomake di notifica che la funzione hello non causare l'interruzione imprevista in modo che i dati rimane in uno stato incoerente.</span><span class="sxs-lookup"><span data-stu-id="c208d-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="c208d-168">Hello seguente esempio viene illustrato come toocheck imminente chiusura processo Web in una funzione.</span><span class="sxs-lookup"><span data-stu-id="c208d-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="c208d-169">**Nota:** hello Dashboard potrebbe non visualizzare correttamente hello stato e l'output di funzioni che è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="c208d-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="c208d-170">Per altre informazioni, vedere l'articolo sull' [arresto normale dei processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="c208d-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="c208d-171">Come toocreate una coda dei messaggi durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="c208d-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="c208d-172">una funzione che crea un nuovo messaggio, utilizzare hello toowrite **coda** attributo.</span><span class="sxs-lookup"><span data-stu-id="c208d-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="c208d-173">Ad esempio **QueueTrigger**, si passa il nome della coda hello sotto forma di stringa oppure è possibile [impostare dinamicamente il nome di coda hello](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c208d-174">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="c208d-174">String queue messages</span></span>
<span data-ttu-id="c208d-175">Hello non asincrona nell'esempio di codice seguente crea un nuovo messaggio nella coda di hello denominato "outputqueue" con stesso contenuto sotto forma di messaggio della coda di hello ricevuto nella coda di hello denominata "inputqueue" hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="c208d-176">Per le funzioni asincrone, usare **IAsyncCollector<T>** come illustrato più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c208d-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c208d-177">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c208d-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c208d-178">tipo di un messaggio nella coda che contiene un POCO anziché una stringa, passata hello POCO toocreate come un toohello di parametro di output **coda** costruttore di attributo.</span><span class="sxs-lookup"><span data-stu-id="c208d-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="c208d-179">Hello SDK serializza automaticamente tooJSON oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="c208d-180">Viene sempre creato un messaggio nella coda, anche se l'oggetto hello è null.</span><span class="sxs-lookup"><span data-stu-id="c208d-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="c208d-181">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="c208d-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="c208d-182">toocreate più messaggi, rendere il tipo di parametro hello per coda di output di hello **ICollector<T>**  o **IAsyncCollector<T>**, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="c208d-183">Ogni messaggio della coda viene creato immediatamente quando hello **Aggiungi** metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="c208d-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="c208d-184">Tipi di attributo coda hello funziona con</span><span class="sxs-lookup"><span data-stu-id="c208d-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="c208d-185">È possibile utilizzare hello **coda** attributo hello seguenti tipi di parametro:</span><span class="sxs-lookup"><span data-stu-id="c208d-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="c208d-186">**stringa** (Crea messaggio della coda se il valore del parametro è diverso da null quando la funzione hello termina)</span><span class="sxs-lookup"><span data-stu-id="c208d-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="c208d-187">**out byte** (funziona come **string**)</span><span class="sxs-lookup"><span data-stu-id="c208d-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="c208d-188">**out CloudQueueMessage** (funziona come **string**)</span><span class="sxs-lookup"><span data-stu-id="c208d-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="c208d-189">**out POCO** (un tipo serializzabile, crea un messaggio con un oggetto null, se il parametro hello è null quando la funzione hello termina)</span><span class="sxs-lookup"><span data-stu-id="c208d-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="c208d-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="c208d-190">**ICollector**</span></span>
* <span data-ttu-id="c208d-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="c208d-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="c208d-192">**CloudQueue** (per la creazione di messaggi manualmente utilizzando hello API di archiviazione di Azure direttamente)</span><span class="sxs-lookup"><span data-stu-id="c208d-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="c208d-193">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="c208d-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="c208d-194">Se è necessario toodo alcune funzionano nella funzione prima di utilizzare un attributo WebJobs SDK, ad esempio **coda**, **Blob**, o **tabella**, è possibile utilizzare hello **IBinder** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="c208d-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="c208d-195">Hello di esempio seguente accetta un messaggio della coda di input e crea un nuovo messaggio con stesso contenuto in una coda di output di hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="c208d-196">nome della coda output Hello viene impostata dal codice nel corpo di hello della funzione hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="c208d-197">Hello **IBinder** interfaccia può essere utilizzata anche con hello **tabella** e **Blob** attributi.</span><span class="sxs-lookup"><span data-stu-id="c208d-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="c208d-198">Come tooread e scrittura BLOB e tabelle durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="c208d-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="c208d-199">Hello **Blob** e **tabella** gli attributi consentono di tooread e scrivere i BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="c208d-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="c208d-200">esempi di Hello in questa sezione si applicano tooblobs.</span><span class="sxs-lookup"><span data-stu-id="c208d-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="c208d-201">Per esempi di codice che mostrano come tootrigger elabora quando BLOB vengono creati o aggiornati, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e per esempi di codice che leggono e scrivono le tabelle, vedere [come toouse tabelle di Azure archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c208d-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="c208d-202">Messaggi di coda stringa che attivano operazioni BLOB</span><span class="sxs-lookup"><span data-stu-id="c208d-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="c208d-203">Per un messaggio nella coda che contiene una stringa, **queueTrigger** è un segnaposto che è possibile utilizzare in hello **Blob** dell'attributo **blobPath** parametro che contiene il contenuto di hello di messaggio Hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="c208d-204">Hello seguente utilizza **flusso** oggetti BLOB tooread e di scrittura.</span><span class="sxs-lookup"><span data-stu-id="c208d-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="c208d-205">messaggio della coda di Hello è il nome di hello di un blob nel contenitore textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="c208d-206">Una copia di blob hello con "-new" nome toohello accodato viene creato in hello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="c208d-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c208d-207">Hello **Blob** attributo costruttore accetta un **blobPath** parametro che specifica il nome di blob e contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="c208d-208">Per ulteriori informazioni su questo segnaposto, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c208d-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="c208d-209">Quando attributo hello decora un **flusso** dell'oggetto, un altro parametro di costruttore specifica hello **FileAccess** modalità come lettura, scrittura o lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="c208d-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="c208d-210">Hello esempio seguente viene utilizzato un **CloudBlockBlob** oggetto toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="c208d-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="c208d-211">messaggio della coda di Hello è il nome di hello del blob hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c208d-212">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c208d-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c208d-213">Per POCO archiviato in formato JSON in messaggio hello in coda, è possibile utilizzare i segnaposto di nome di proprietà dell'oggetto hello in hello **coda** dell'attributo **blobPath** parametro.</span><span class="sxs-lookup"><span data-stu-id="c208d-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="c208d-214">È anche possibile usare nomi di proprietà dei metadati di coda come segnaposto.</span><span class="sxs-lookup"><span data-stu-id="c208d-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="c208d-215">Vedere [Ottenere i metadati della coda o del messaggio in coda](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="c208d-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="c208d-216">Hello esempio copia un blob tooa nuovo blob con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="c208d-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="c208d-217">messaggio della coda di Hello è un **BlobInformation** oggetto che include **BlobName** e **BlobNameWithoutExtension** proprietà.</span><span class="sxs-lookup"><span data-stu-id="c208d-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="c208d-218">i nomi delle proprietà Hello vengono utilizzati come segnaposto nel percorso blob hello per hello **Blob** attributi.</span><span class="sxs-lookup"><span data-stu-id="c208d-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c208d-219">Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="c208d-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c208d-220">Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.</span><span class="sxs-lookup"><span data-stu-id="c208d-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="c208d-221">Se è necessario toodo alcuni nella funzione prima di associare un oggetto tooan blob, è possibile utilizzare attributo hello nel corpo di hello della funzione hello, come illustrato nella [attributi utilizzare WebJobs SDK nel corpo di una funzione di hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="c208d-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="c208d-222">Tipi di dati hello Blob di attributo con</span><span class="sxs-lookup"><span data-stu-id="c208d-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="c208d-223">Hello **Blob** attributo può essere utilizzato con hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="c208d-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="c208d-224">**Flusso** (lettura o scrittura, specificato utilizzando il parametro di costruttore FileAccess hello)</span><span class="sxs-lookup"><span data-stu-id="c208d-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="c208d-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="c208d-225">**TextReader**</span></span>
* <span data-ttu-id="c208d-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="c208d-226">**TextWriter**</span></span>
* <span data-ttu-id="c208d-227">**string** (lettura)</span><span class="sxs-lookup"><span data-stu-id="c208d-227">**string** (read)</span></span>
* <span data-ttu-id="c208d-228">**stringa** (scrittura; crea un blob solo se il parametro di stringa hello è non null quando viene restituita la funzione hello)</span><span class="sxs-lookup"><span data-stu-id="c208d-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="c208d-229">POCO (lettura)</span><span class="sxs-lookup"><span data-stu-id="c208d-229">POCO (read)</span></span>
* <span data-ttu-id="c208d-230">out POCO (scrivere; sempre creato un blob, come oggetto null se il parametro POCO è null quando viene restituita la funzione hello)</span><span class="sxs-lookup"><span data-stu-id="c208d-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="c208d-231">**CloudBlobStream** (scrittura)</span><span class="sxs-lookup"><span data-stu-id="c208d-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="c208d-232">**ICloudBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="c208d-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="c208d-233">**CloudBlockBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="c208d-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="c208d-234">**CloudPageBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="c208d-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="c208d-235">Come messaggi non elaborabili toohandle</span><span class="sxs-lookup"><span data-stu-id="c208d-235">How toohandle poison messages</span></span>
<span data-ttu-id="c208d-236">Messaggi il cui contenuto provoca un toofail funzione sono denominati *messaggi non elaborabili*.</span><span class="sxs-lookup"><span data-stu-id="c208d-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="c208d-237">Quando la funzione hello non riesce, il messaggio di coda hello non viene eliminato e infine viene prelevato nuovamente, causando hello ciclo toobe ripetuto.</span><span class="sxs-lookup"><span data-stu-id="c208d-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="c208d-238">Hello SDK automaticamente in grado di interrompere il ciclo di hello dopo un numero limitato di iterazioni o è possibile farlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="c208d-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="c208d-239">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="c208d-239">Automatic poison message handling</span></span>
<span data-ttu-id="c208d-240">Hello SDK chiama una funzione di too5 volte tooprocess un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="c208d-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="c208d-241">Se non riesce try quinto hello, messaggio hello è la coda non elaborabile spostato tooa.</span><span class="sxs-lookup"><span data-stu-id="c208d-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="c208d-242">È possibile vedere come tooconfigure hello numero massimo di tentativi in [come opzioni di configurazione tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="c208d-243">coda non elaborabile Hello è denominata *{originalqueuename}*-messaggi non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="c208d-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="c208d-244">È possibile scrivere messaggi tooprocess un funzione dalla coda non elaborabile hello registrarle o inviando una notifica che è necessario un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="c208d-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="c208d-245">In seguito hello esempio hello **CopyBlob** function ha esito negativo quando un messaggio nella coda contiene il nome di hello di un blob che non esiste.</span><span class="sxs-lookup"><span data-stu-id="c208d-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="c208d-246">In questo caso, il messaggio hello viene spostato dalla hello copyblobqueue toohello copyblobqueue poison coda.</span><span class="sxs-lookup"><span data-stu-id="c208d-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="c208d-247">Hello **ProcessPoisonMessage** quindi registri hello messaggi non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="c208d-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="c208d-248">Hello figura seguente Mostra output di console da queste funzioni durante l'elaborazione di un messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="c208d-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Output di console per la gestione dei messaggi non elaborabili](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="c208d-250">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="c208d-250">Manual poison message handling</span></span>
<span data-ttu-id="c208d-251">È possibile ottenere un numero di volte in cui è stato selezionato un messaggio per l'elaborazione di hello aggiungendo un **int** parametro denominato **dequeueCount** tooyour funzione.</span><span class="sxs-lookup"><span data-stu-id="c208d-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="c208d-252">È possibile quindi controllo hello numero nel codice della funzione di rimozione dalla coda ed eseguire la propria gestione di messaggio non elaborabile quando il numero di hello supera una soglia, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="c208d-253">Come le opzioni di configurazione tooset</span><span class="sxs-lookup"><span data-stu-id="c208d-253">How tooset configuration options</span></span>
<span data-ttu-id="c208d-254">È possibile utilizzare hello **JobHostConfiguration** hello tooset tipo le opzioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="c208d-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="c208d-255">Impostare le stringhe di connessione SDK hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="c208d-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="c208d-256">Configurare le impostazioni di **QueueTrigger** , ad esempio il conteggio rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="c208d-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="c208d-257">Ottenere i nomi delle code dalla configurazione.</span><span class="sxs-lookup"><span data-stu-id="c208d-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="c208d-258">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="c208d-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="c208d-259">L'impostazione di stringhe di connessione SDK hello nel codice consente si toouse i propri nomi di stringa di connessione nel file di configurazione o le variabili di ambiente, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="c208d-260">Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="c208d-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="c208d-261">È possibile configurare hello seguendo le impostazioni che si applicano toohello l'elaborazione del messaggio della coda:</span><span class="sxs-lookup"><span data-stu-id="c208d-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="c208d-262">numero massimo di messaggi in coda che vengono prelevati contemporaneamente toobe eseguite in parallelo Hello (valore predefinito è 16).</span><span class="sxs-lookup"><span data-stu-id="c208d-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="c208d-263">Hello numero massimo di tentativi prima che un messaggio nella coda venga inviato coda non elaborabile tooa (valore predefinito è 5).</span><span class="sxs-lookup"><span data-stu-id="c208d-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="c208d-264">tempo di attesa massimo Hello prima polling nuovamente quando una coda è vuota (valore predefinito è 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="c208d-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="c208d-265">Hello seguente esempio viene illustrato come tooconfigure queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="c208d-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="c208d-266">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="c208d-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="c208d-267">Talvolta si desidera toospecify un nome di coda, un nome di blob o contenitore o una tabella di nome in codice anziché a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="c208d-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="c208d-268">Ad esempio, è consigliabile toospecify hello nome della coda **QueueTrigger** in una variabile di ambiente o i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c208d-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="c208d-269">È possibile farlo tramite il passaggio di un **NameResolver** oggetto toohello **JobHostConfiguration** tipo.</span><span class="sxs-lookup"><span data-stu-id="c208d-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="c208d-270">Si includono segnaposto speciale racchiusi tra segni di percentuale (%) nei parametri di costruttore di attributo WebJobs SDK e **NameResolver** codice specifica toobe valori effettivi hello utilizzato al posto di questi segnaposto.</span><span class="sxs-lookup"><span data-stu-id="c208d-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="c208d-271">Ad esempio, si supponga che si desidera toouse una coda denominata logqueuetest nell'ambiente di test hello e uno denominato logqueueprod nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="c208d-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="c208d-272">Anziché un nome di coda a livello di codice, si desidera nome hello toospecify di una voce in hello **appSettings** raccolta aventi il nome di coda effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="c208d-273">Se hello **appSettings** chiave logqueue, la funzione potrebbe essere analogo al seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="c208d-274">Il **NameResolver** classe quindi è stato possibile ottenere il nome della coda hello da **appSettings** come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c208d-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="c208d-275">Si passa hello **NameResolver** classe toohello **JobHost** come mostrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="c208d-276">**Nota:** coda, tabella e i nomi di blob vengono risolti ogni volta che viene chiamata una funzione, ma i nomi dei contenitori blob vengono risolti solo quando viene avviata un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="c208d-277">È possibile modificare il nome di contenitore blob mentre è in esecuzione il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="c208d-278">Come una funzione tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="c208d-278">How tootrigger a function manually</span></span>
<span data-ttu-id="c208d-279">una funzione tootrigger manualmente, utilizzare hello **chiamare** o **CallAsync** metodo hello **JobHost** oggetto e hello **NoAutomaticTrigger** attributo nella funzione hello, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="c208d-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a><span data-ttu-id="c208d-280">Modalità di registrazione toowrite</span><span class="sxs-lookup"><span data-stu-id="c208d-280">How toowrite logs</span></span>
<span data-ttu-id="c208d-281">Hello Dashboard Mostra i registri in due posizioni: la pagina hello per processo Web hello e hello per una chiamata a un particolare processo Web.</span><span class="sxs-lookup"><span data-stu-id="c208d-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Log nella pagina del processo Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="c208d-284">Output dei metodi di Console che si chiama una funzione o hello **Main ()** metodo verrà visualizzato nella pagina Dashboard hello per hello processo Web, non nella pagina hello per una chiamata di metodo specifico.</span><span class="sxs-lookup"><span data-stu-id="c208d-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="c208d-285">Verrà visualizzato l'output dall'oggetto TextWriter hello che si ottiene da un parametro nella firma del metodo nella pagina Dashboard hello per una chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="c208d-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="c208d-286">Output della console non può essere chiamata al metodo particolare tooa collegato perché hello Console è a thread singolo, mentre molte funzioni di processo potrebbero essere in esecuzione hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c208d-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="c208d-287">Per tale motivo hello SDK fornisce a ogni chiamata di funzione con il proprio oggetto writer di log univoco.</span><span class="sxs-lookup"><span data-stu-id="c208d-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="c208d-288">toowrite [registri di traccia delle applicazioni](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilizzare **console** (Crea registri contrassegnati come INFO) e **Console.Error** (Crea log contrassegnato come errore).</span><span class="sxs-lookup"><span data-stu-id="c208d-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="c208d-289">In alternativa, è toouse [traccia o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), che fornisce Verbose, avviso, e i livelli di tooInfo aggiunta e di errore critico.</span><span class="sxs-lookup"><span data-stu-id="c208d-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="c208d-290">Registri di traccia delle applicazioni vengono visualizzati nel file di log di hello web app, le tabelle di Azure, o oggetti BLOB di Azure a seconda di come si configura l'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c208d-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="c208d-291">Come nel caso di tutti gli output di Console, i registri applicazione 100 più recente di hello vengono inoltre visualizzati nella pagina Dashboard hello hello processo Web, la pagina di hello non per una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="c208d-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="c208d-292">Output della console viene visualizzato in hello Dashboard solo se il programma hello è in esecuzione in un processo Web di Azure, non se il programma hello viene eseguito localmente o in altri ambienti di rete.</span><span class="sxs-lookup"><span data-stu-id="c208d-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="c208d-293">È possibile disabilitare la registrazione impostando hello Dashboard connessione stringa toonull.</span><span class="sxs-lookup"><span data-stu-id="c208d-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="c208d-294">Per ulteriori informazioni, vedere [come opzioni di configurazione tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c208d-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="c208d-295">Hello esempio seguente vengono illustrati vari modi toowrite log:</span><span class="sxs-lookup"><span data-stu-id="c208d-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="c208d-296">Nel Dashboard di processi Web SDK hello, hello output di hello **TextWriter** viene visualizzato quando si passa toohello pagina per una particolare chiamata di funzione e selezionarla oggetti **attiva/disattiva Output**:</span><span class="sxs-lookup"><span data-stu-id="c208d-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Collegamento della chiamata](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="c208d-299">Nel Dashboard di processi Web SDK hello, righe hello 100 più recente della Console l'output Mostra backup quando accede pagina toohello per hello processo Web (non per la chiamata di funzione hello) e selezionare **attiva/disattiva Output**.</span><span class="sxs-lookup"><span data-stu-id="c208d-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Attiva/Disattiva Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="c208d-301">In un processo Web continuo, log applicazioni visualizzati nella/dati processi/continua/*{webjobname}*/job_log.txt nel file system di hello web app.</span><span class="sxs-lookup"><span data-stu-id="c208d-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="c208d-302">In un'applicazione hello blob di Azure registri simile al seguente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, errore, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="c208d-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="c208d-303">In un hello tabella Azure **console** e **Console.Error** registri è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c208d-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Log delle informazioni nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log degli errori nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="c208d-306">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c208d-306">Next steps</span></span>
<span data-ttu-id="c208d-307">In questo articolo ha fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di code di Azure.</span><span class="sxs-lookup"><span data-stu-id="c208d-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="c208d-308">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse della documentazione di processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c208d-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

