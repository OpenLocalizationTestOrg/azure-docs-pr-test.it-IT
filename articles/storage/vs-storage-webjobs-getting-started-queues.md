---
title: Introduzione all'archiviazione code e ai Servizi connessi di Visual Studio (progetti processo Web) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione di accodamento di Azure in un progetto WebJob dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio.
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
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="997c0-103">Introduzione all'archiviazione di accodamento di Azure e ai servizi relativi a Visual Studio (progetti WebJob)</span><span class="sxs-lookup"><span data-stu-id="997c0-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="997c0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="997c0-104">Overview</span></span>
<span data-ttu-id="997c0-105">Questo articolo descrive come iniziare a usare l'archiviazione code di Azure in un progetto di tipo processo Web di Azure in Visual Studio dopo avere creato o fatto riferimento a un account di archiviazione di Azure usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="997c0-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="997c0-106">Quando si aggiunge un account di archiviazione a un progetto WebJob tramite la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio, vengono installati i pacchetti NuGet di archiviazione di Azure appropriati, i riferimenti .NET appropriati vengono aggiunti al progetto e le stringhe di connessione per l'account di archiviazione vengono aggiornate nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="997c0-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="997c0-107">Questo articolo fornisce esempi di codice C# che illustrano come usare Azure WebJobs SDK versione 1.x con il servizio di archiviazione di accodamento di Azure.</span><span class="sxs-lookup"><span data-stu-id="997c0-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="997c0-108">Il servizio di archiviazione di accodamento di Azure consente di archiviare grandi quantità di messaggi ai quali è possibile accedere da qualsiasi parte del mondo mediante chiamate autenticate tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="997c0-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="997c0-109">La dimensione massima di un singolo messaggio della coda è di 64 KB e una coda può contenere milioni di messaggi, nei limiti della capacità complessiva di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="997c0-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="997c0-110">Per altre informazioni, vedere [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="997c0-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="997c0-111">Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="997c0-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="997c0-112">Come attivare una funzione quando viene ricevuto un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="997c0-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="997c0-113">Per scrivere una funzione che viene chiamata da WebJobs SDK quando viene ricevuto un messaggio di coda, usare l'attributo **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="997c0-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="997c0-114">Il costruttore dell'attributo accetta un parametro di stringa che specifica il nome della coda di cui eseguire il polling.</span><span class="sxs-lookup"><span data-stu-id="997c0-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="997c0-115">Per informazioni su come impostare il nome della coda in modo dinamico, vedere l'argomento relativo a [come impostare le opzioni di configurazione](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="997c0-116">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="997c0-116">String queue messages</span></span>
<span data-ttu-id="997c0-117">Nell'esempio seguente, la coda contiene una stringa di messaggio, in modo che l'attributo **QueueTrigger** venga applicato a un parametro di stringa denominato **logMessage** che include il contenuto del messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="997c0-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="997c0-118">La funzione [scrive un messaggio di log nel dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="997c0-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="997c0-119">Oltre a **string**, il parametro può essere una matrice di byte, un oggetto **CloudQueueMessage** o un oggetto POCO definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="997c0-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="997c0-120">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="997c0-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="997c0-121">Nell'esempio seguente, il messaggio in coda contiene JSON per un oggetto **BlobInformation** che include una proprietà **BlobName**.</span><span class="sxs-lookup"><span data-stu-id="997c0-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="997c0-122">L'SDK deserializza automaticamente l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="997c0-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="997c0-123">L'SDK usa il pacchetto [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) per serializzare e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="997c0-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="997c0-124">Se si creano messaggi di coda in un programma che non usa WebJobs SDK, è possibile scrivere codice simile a quello del seguente esempio per creare un messaggio di coda POCO analizzabile dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="997c0-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="997c0-125">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="997c0-125">Async functions</span></span>
<span data-ttu-id="997c0-126">La seguente funzione asincrona [scrive un log nel dashboard](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="997c0-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="997c0-127">Le funzioni asincrone possono usare un [token di annullamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), come illustrato nel seguente esempio che copia un BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="997c0-128">Per una spiegazione del segnaposto **queueTrigger**, vedere la sezione relativa ai [BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message).</span><span class="sxs-lookup"><span data-stu-id="997c0-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="997c0-129">Tipi usati dall'attributo QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="997c0-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="997c0-130">È possibile usare **QueueTrigger** con i seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="997c0-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="997c0-131">**string**</span><span class="sxs-lookup"><span data-stu-id="997c0-131">**string**</span></span>
* <span data-ttu-id="997c0-132">Tipo POCO serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="997c0-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="997c0-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="997c0-133">**byte[]**</span></span>
* <span data-ttu-id="997c0-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="997c0-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="997c0-135">Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="997c0-135">Polling algorithm</span></span>
<span data-ttu-id="997c0-136">L'SDK implementa un algoritmo di backoff esponenziale casuale per ridurre l'effetto del polling delle code inattive sui costi delle transazioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="997c0-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="997c0-137">Quando viene trovato un messaggio, l'SDK attende due secondi e controlla la presenza di un altro messaggio. Quando non viene trovato alcun messaggio, rimane in attesa per circa quattro secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="997c0-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="997c0-138">Dopo alcuni tentativi non riusciti per ottenere un messaggio nella coda, il tempo di attesa continua ad aumentare finché non raggiunge il tempo massimo di attesa, che per impostazione predefinita è di un minuto.</span><span class="sxs-lookup"><span data-stu-id="997c0-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="997c0-139">[Il tempo di attesa massimo è configurabile](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="997c0-140">Più istanze</span><span class="sxs-lookup"><span data-stu-id="997c0-140">Multiple instances</span></span>
<span data-ttu-id="997c0-141">Se l'app Web viene eseguita in più istanze, in ogni computer i processi Web verranno eseguiti in modalità continua e ogni computer attenderà i trigger e proverà a eseguire le funzioni.</span><span class="sxs-lookup"><span data-stu-id="997c0-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="997c0-142">Poiché in alcuni scenari è possibile che per questo motivo alcune funzioni elaborino gli stessi dati due volte, le funzioni dovrebbero essere idempotent (scritte in modo tale che, anche se chiamate più volte con gli stessi dati di input, non generano risultati duplicati).</span><span class="sxs-lookup"><span data-stu-id="997c0-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="997c0-143">Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="997c0-143">Parallel execution</span></span>
<span data-ttu-id="997c0-144">Se si dispongono di più funzioni in ascolto in code diverse, l'SDK le chiamerà in parallelo quando i messaggi vengono ricevuti simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="997c0-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="997c0-145">Lo stesso vale quando si ricevono più messaggi per una singola coda.</span><span class="sxs-lookup"><span data-stu-id="997c0-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="997c0-146">Per impostazione predefinita, l'SDK ottiene un batch di 16 messaggi in coda alla volta ed esegue la funzione che li elabora in parallelo.</span><span class="sxs-lookup"><span data-stu-id="997c0-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="997c0-147">[La dimensione del batch è configurabile](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="997c0-148">Quando il numero elaborato viene ridotto alla metà della dimensione del batch, l'SDK ottiene un altro batch e inizia l'elaborazione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="997c0-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="997c0-149">Di conseguenza, il numero massimo di messaggi simultanei elaborati per ogni funzione è pari a una volta e mezza la dimensione del batch.</span><span class="sxs-lookup"><span data-stu-id="997c0-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="997c0-150">Questo limite si applica separatamente a ogni funzione caratterizzata da un attributo **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="997c0-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="997c0-151">Se non si vuole avviare l'esecuzione parallela per i messaggi ricevuti su una coda, impostare le dimensioni del batch su 1.</span><span class="sxs-lookup"><span data-stu-id="997c0-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="997c0-152">Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="997c0-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="997c0-153">Con l'aggiunta di parametri alla firma del metodo, è possibile ottenere le proprietà del messaggio seguenti:</span><span class="sxs-lookup"><span data-stu-id="997c0-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="997c0-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="997c0-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="997c0-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="997c0-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="997c0-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="997c0-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="997c0-157">**string** queueTrigger (contiene il testo del messaggio)</span><span class="sxs-lookup"><span data-stu-id="997c0-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="997c0-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="997c0-158">**string** id</span></span>
* <span data-ttu-id="997c0-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="997c0-159">**string** popReceipt</span></span>
* <span data-ttu-id="997c0-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="997c0-160">**int** dequeueCount</span></span>

<span data-ttu-id="997c0-161">Per lavorare direttamente con l'API del servizio di archiviazione di Azure, è anche possibile aggiungere un parametro **CloudStorageAccount** .</span><span class="sxs-lookup"><span data-stu-id="997c0-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="997c0-162">Nell'esempio seguente tutti questi metadati vengono scritti in un log applicazione INFO.</span><span class="sxs-lookup"><span data-stu-id="997c0-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="997c0-163">Nell'esempio, gli attributi logMessage e queueTrigger includono il contenuto del messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="997c0-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="997c0-164">Ecco un log di esempio scritto dal codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="997c0-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="997c0-165">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="997c0-165">Graceful shutdown</span></span>
<span data-ttu-id="997c0-166">Una funzione che viene eseguita in un processo Web continuo può accettare un parametro **CancellationToken** che consente al sistema operativo di notificare la funzione quando il processo Web sta per essere terminato.</span><span class="sxs-lookup"><span data-stu-id="997c0-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="997c0-167">È possibile usare questa notifica per assicurarsi che la funzione non termini in modo imprevisto lasciando i dati in uno stato incoerente.</span><span class="sxs-lookup"><span data-stu-id="997c0-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="997c0-168">L'esempio seguente illustra come controllare la chiusura imminente di un processo Web in una funzione.</span><span class="sxs-lookup"><span data-stu-id="997c0-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="997c0-169">**Nota:** è possibile che il dashboard non mostri correttamente lo stato e il risultato delle funzioni che sono state interrotte.</span><span class="sxs-lookup"><span data-stu-id="997c0-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="997c0-170">Per altre informazioni, vedere l'articolo sull' [arresto normale dei processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="997c0-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="997c0-171">Come creare un messaggio di coda durante l'elaborazione di un messaggio di coda</span><span class="sxs-lookup"><span data-stu-id="997c0-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="997c0-172">Per scrivere una funzione che crea un nuovo messaggio di coda, usare l'attributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="997c0-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="997c0-173">Come per l'attributo **QueueTrigger**, si passa il nome della coda come stringa oppure è possibile [configurare dinamicamente il nome della coda](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="997c0-174">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="997c0-174">String queue messages</span></span>
<span data-ttu-id="997c0-175">Il seguente esempio di codice non asincrono crea nella coda denominata "outputqueue" un nuovo messaggio di coda con lo stesso contenuto del messaggio di coda ricevuto nella coda denominata "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="997c0-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="997c0-176">Per le funzioni asincrone, usare **IAsyncCollector<T>** come illustrato più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="997c0-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="997c0-177">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="997c0-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="997c0-178">Per creare un messaggio di coda contenente un oggetto POCO anziché una stringa, passare il tipo POCO come parametro di output al costruttore dell'attributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="997c0-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="997c0-179">L'SDK deserializza automaticamente l'oggetto in JSON.</span><span class="sxs-lookup"><span data-stu-id="997c0-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="997c0-180">Viene sempre creato un messaggio in coda, anche se l'oggetto è null.</span><span class="sxs-lookup"><span data-stu-id="997c0-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="997c0-181">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="997c0-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="997c0-182">Per creare più messaggi, impostare il tipo di parametro per la coda di output **ICollector<T>** o **IAsyncCollector<T>**, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="997c0-183">Ogni messaggio in coda viene creato immediatamente quando viene chiamato il metodo **Add** .</span><span class="sxs-lookup"><span data-stu-id="997c0-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="997c0-184">Tipi usati dall'attributo Queue</span><span class="sxs-lookup"><span data-stu-id="997c0-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="997c0-185">È possibile usare l'attributo **Queue** nei seguenti tipi di parametri:</span><span class="sxs-lookup"><span data-stu-id="997c0-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="997c0-186">**out string** (crea il messaggio di coda se il valore del parametro è diverso da null quando termina la funzione)</span><span class="sxs-lookup"><span data-stu-id="997c0-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="997c0-187">**out byte** (funziona come **string**)</span><span class="sxs-lookup"><span data-stu-id="997c0-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="997c0-188">**out CloudQueueMessage** (funziona come **string**)</span><span class="sxs-lookup"><span data-stu-id="997c0-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="997c0-189">**out POCO** (tipo serializzabile, crea un messaggio con un oggetto null se il parametro è null quando termina la funzione)</span><span class="sxs-lookup"><span data-stu-id="997c0-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="997c0-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="997c0-190">**ICollector**</span></span>
* <span data-ttu-id="997c0-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="997c0-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="997c0-192">**CloudQueue** (per la creazione manuale dei messaggi direttamente con l'API di archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="997c0-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="997c0-193">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="997c0-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="997c0-194">Se è necessario eseguire alcune operazioni nella funzione prima di usare un attributo di WebJobs SDK come **Queue**, **Blob** o **Table**, è possibile usare l'interfaccia **IBinder**.</span><span class="sxs-lookup"><span data-stu-id="997c0-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="997c0-195">Nell'esempio seguente viene accettato un messaggio di coda di input e creato un nuovo messaggio con lo stesso contenuto in una coda di output.</span><span class="sxs-lookup"><span data-stu-id="997c0-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="997c0-196">Il nome della coda di output viene impostato dal codice nel corpo della funzione.</span><span class="sxs-lookup"><span data-stu-id="997c0-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="997c0-197">L'interfaccia **IBinder** può essere usata anche con gli attributi **Table** e **Blob**.</span><span class="sxs-lookup"><span data-stu-id="997c0-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="997c0-198">Come leggere e scrivere BLOB e tabelle durante l'elaborazione di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="997c0-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="997c0-199">Gli attributi **Blob** e **Table** consentono di leggere e scrivere BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="997c0-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="997c0-200">Gli esempi in questa sezione si applicano ai BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="997c0-201">Per esempi di codice che illustrano come attivare processi quando i BLOB vengono creati o aggiornati, vedere [Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) e per esempi di codice che leggono e scrivono tabelle, vedere [Come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="997c0-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="997c0-202">Messaggi di coda stringa che attivano operazioni BLOB</span><span class="sxs-lookup"><span data-stu-id="997c0-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="997c0-203">Per un messaggio in coda che contiene una stringa, **queueTrigger** è un segnaposto che è possibile usare nel parametro **blobPath** dell'attributo **Blob** che include il contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="997c0-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="997c0-204">Nell'esempio seguente vengono utilizzati oggetti **Stream** per leggere e scrivere i BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="997c0-205">Il messaggio di coda è il nome di un BLOB presente nel contenitore textblobs.</span><span class="sxs-lookup"><span data-stu-id="997c0-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="997c0-206">Una copia del BLOB con "-new" aggiunto al nome viene creata nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="997c0-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="997c0-207">Il costruttore dell'attributo **Blob** usa un parametro **blobPath** che specifica il contenitore e il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="997c0-208">Per altre informazioni su questo segnaposto, vedere [Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="997c0-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="997c0-209">Quando l'attributo decora un oggetto **Stream**, un altro parametro del costruttore specifica la modalità **FileAccess** come lettura, scrittura o lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="997c0-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="997c0-210">Nell'esempio seguente viene utilizzato un oggetto **CloudBlockBlob** per eliminare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="997c0-211">Il messaggio di coda è il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="997c0-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="997c0-212">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="997c0-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="997c0-213">Per un oggetto POCO archiviato nel formato JSON nel messaggio della coda, è possibile usare i segnaposto che denominano le proprietà dell'oggetto nel parametro **blobPath** dell'attributo **Queue**.</span><span class="sxs-lookup"><span data-stu-id="997c0-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="997c0-214">È anche possibile usare nomi di proprietà dei metadati di coda come segnaposto.</span><span class="sxs-lookup"><span data-stu-id="997c0-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="997c0-215">Vedere [Ottenere i metadati della coda o del messaggio in coda](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="997c0-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="997c0-216">Il seguente esempio copia un BLOB in un nuovo BLOB con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="997c0-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="997c0-217">Il messaggio di coda è un oggetto **BlobInformation** che include le proprietà **BlobName** e **BlobNameWithoutExtension**.</span><span class="sxs-lookup"><span data-stu-id="997c0-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="997c0-218">I nomi delle proprietà vengono usati come segnaposto nel percorso BLOB per gli attributi **Blob** .</span><span class="sxs-lookup"><span data-stu-id="997c0-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="997c0-219">L'SDK usa il pacchetto [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) per serializzare e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="997c0-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="997c0-220">Se si creano messaggi di coda in un programma che non usa WebJobs SDK, è possibile scrivere codice simile a quello del seguente esempio per creare un messaggio di coda POCO analizzabile dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="997c0-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="997c0-221">Se è necessario eseguire alcune operazioni nella funzione prima di associare un BLOB a un oggetto, è possibile usare l'attributo nel corpo della funzione, come mostrato in [Usare gli attributi di WebJobs SDK nel corpo di una funzione](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="997c0-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="997c0-222">Tipi con cui è possibile usare l'attributo Blob</span><span class="sxs-lookup"><span data-stu-id="997c0-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="997c0-223">L'attributo **Blob** può essere usato con i seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="997c0-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="997c0-224">**Stream** (lettura o scrittura, specificata tramite il parametro del costruttore FileAccess)</span><span class="sxs-lookup"><span data-stu-id="997c0-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="997c0-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="997c0-225">**TextReader**</span></span>
* <span data-ttu-id="997c0-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="997c0-226">**TextWriter**</span></span>
* <span data-ttu-id="997c0-227">**string** (lettura)</span><span class="sxs-lookup"><span data-stu-id="997c0-227">**string** (read)</span></span>
* <span data-ttu-id="997c0-228">**out string** (scrittura; crea un BLOB solo se il parametro di stringa è diverso da null quando la funzione restituisce un valore)</span><span class="sxs-lookup"><span data-stu-id="997c0-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="997c0-229">POCO (lettura)</span><span class="sxs-lookup"><span data-stu-id="997c0-229">POCO (read)</span></span>
* <span data-ttu-id="997c0-230">out POCO (scrittura; crea sempre un BLOB come oggetto null se il parametro POCO è null quando la funzione restituisce un valore)</span><span class="sxs-lookup"><span data-stu-id="997c0-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="997c0-231">**CloudBlobStream** (scrittura)</span><span class="sxs-lookup"><span data-stu-id="997c0-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="997c0-232">**ICloudBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="997c0-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="997c0-233">**CloudBlockBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="997c0-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="997c0-234">**CloudPageBlob** (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="997c0-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="997c0-235">Come gestire i messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="997c0-235">How to handle poison messages</span></span>
<span data-ttu-id="997c0-236">I messaggi il cui contenuto comporta l'esito negativo di una funzione sono denominati *messaggi non elaborabili*.</span><span class="sxs-lookup"><span data-stu-id="997c0-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="997c0-237">Quando la funzione non riesce, il messaggio in coda non viene eliminato e infine viene prelevato, causando la ripetizione del ciclo.</span><span class="sxs-lookup"><span data-stu-id="997c0-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="997c0-238">L'SDK può interrompere automaticamente il ciclo dopo un numero limitato di iterazioni oppure è possibile farlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="997c0-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="997c0-239">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="997c0-239">Automatic poison message handling</span></span>
<span data-ttu-id="997c0-240">L'SDK chiamerà una funzione fino a 5 volte per elaborare un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="997c0-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="997c0-241">Se il quinto tentativo non riesce, il messaggio viene spostato in una coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="997c0-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="997c0-242">È possibile vedere come configurare il numero massimo di tentativi nell'argomento relativo a [come impostare le opzioni di configurazione](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="997c0-243">La coda non elaborabile è denominata *{nomecodaoriginale}*-poison.</span><span class="sxs-lookup"><span data-stu-id="997c0-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="997c0-244">È possibile scrivere una funzione per elaborare i messaggi dalla coda non elaborabile archiviandoli o inviando una notifica della necessità di un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="997c0-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="997c0-245">Nell'esempio seguente, la funzione **CopyBlob** non riesce quando un messaggio della coda contiene il nome di un BLOB inesistente.</span><span class="sxs-lookup"><span data-stu-id="997c0-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="997c0-246">In questo caso, il messaggio viene spostato dalla coda copyblobqueue alla coda non elaborabile copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="997c0-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="997c0-247">**ProcessPoisonMessage** registra quindi il messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="997c0-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="997c0-248">Nella figura seguente viene illustrato l'output di console di queste funzioni quando viene elaborato un messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="997c0-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Output di console per la gestione dei messaggi non elaborabili](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="997c0-250">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="997c0-250">Manual poison message handling</span></span>
<span data-ttu-id="997c0-251">È possibile ottenere il numero di volte in cui un messaggio è stato selezionato per l'elaborazione aggiungendo un parametro **int** denominato **dequeueCount** alla funzione.</span><span class="sxs-lookup"><span data-stu-id="997c0-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="997c0-252">Sarà quindi possibile controllare il conteggio di rimozione dalla coda nel codice della funzione ed eseguire la gestione dei messaggi non elaborabili quando il numero supera una certa soglia, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="997c0-253">come impostare le opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="997c0-253">How to set configuration options</span></span>
<span data-ttu-id="997c0-254">È possibile usare il tipo **JobHostConfiguration** per impostare le opzioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="997c0-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="997c0-255">Impostare le stringhe di connessione SDK nel codice.</span><span class="sxs-lookup"><span data-stu-id="997c0-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="997c0-256">Configurare le impostazioni di **QueueTrigger** , ad esempio il conteggio rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="997c0-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="997c0-257">Ottenere i nomi delle code dalla configurazione.</span><span class="sxs-lookup"><span data-stu-id="997c0-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="997c0-258">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="997c0-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="997c0-259">Impostare le stringhe di connessione SDK nel codice per poter usare i propri nomi di stringa di connessione nei file di configurazione o nelle variabili di ambiente, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="997c0-260">Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="997c0-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="997c0-261">È possibile configurare le seguenti impostazioni valide per l'elaborazione del messaggio di coda:</span><span class="sxs-lookup"><span data-stu-id="997c0-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="997c0-262">Numero massimo di messaggi in coda che vengono prelevati contemporaneamente per l'esecuzione in parallelo (il valore predefinito è 16).</span><span class="sxs-lookup"><span data-stu-id="997c0-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="997c0-263">Numero massimo di tentativi prima che un messaggio nella coda venga inviato a una coda non elaborabile (il valore predefinito è 5).</span><span class="sxs-lookup"><span data-stu-id="997c0-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="997c0-264">Tempo massimo di attesa prima di eseguire nuovamente il polling quando una coda è vuota (il valore predefinito è 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="997c0-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="997c0-265">L'esempio seguente illustra come configurare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="997c0-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="997c0-266">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="997c0-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="997c0-267">A volte si desidera specificare un nome di coda, un nome di BLOB o un contenitore oppure un nome di tabella nel codice anziché impostarlo come hardcoded.</span><span class="sxs-lookup"><span data-stu-id="997c0-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="997c0-268">È ad esempio possibile specificare il nome della coda per **QueueTrigger** in una variabile di ambiente o in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="997c0-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="997c0-269">A tale scopo, passare un oggetto **NameResolver** al tipo **JobHostConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="997c0-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="997c0-270">Includere segnaposto speciali racchiusi tra segni di percentuale (%) nei parametri del costruttore dell'attributo di SDK e il codice **NameResolver** specifica i valori effettivi da usare in sostituzione di questi segnaposto.</span><span class="sxs-lookup"><span data-stu-id="997c0-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="997c0-271">Si supponga, ad esempio, di voler usare una coda denominata logqueuetest nell'ambiente di test e una coda denominata logqueueprod nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="997c0-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="997c0-272">Invece di un nome di coda hardcoded, è preferibile specificare il nome di una voce nella raccolta **appSettings** caratterizzata dal nome della coda effettivo.</span><span class="sxs-lookup"><span data-stu-id="997c0-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="997c0-273">Se la chiave **appSettings** è logqueue, la funzione potrebbe essere simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="997c0-274">La classe **NameResolver** potrebbe quindi ottenere il nome della coda dalla raccolta **appSettings**, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="997c0-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="997c0-275">È possibile passare la classe **NameResolver** all'oggetto **JobHost**, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="997c0-276">**Nota:** i nomi di coda, tabella e BLOB vengono risolti ogni volta che viene chiamata una funzione, ma i nomi di contenitore di BLOB vengono risolti solo all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="997c0-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="997c0-277">Non è possibile modificare il nome del contenitore di BLOB durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="997c0-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="997c0-278">Come attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="997c0-278">How to trigger a function manually</span></span>
<span data-ttu-id="997c0-279">Per attivare manualmente una funzione, usare il metodo **Call** o **CallAsync** sull'oggetto **JobHost** e l'attributo **NoAutomaticTrigger** nella funzione, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="997c0-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="997c0-280">Come scrivere i log</span><span class="sxs-lookup"><span data-stu-id="997c0-280">How to write logs</span></span>
<span data-ttu-id="997c0-281">Il dashboard visualizza i log in due posizioni: la pagina del processo Web e la pagina di una particolare chiamata al processo Web.</span><span class="sxs-lookup"><span data-stu-id="997c0-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Log nella pagina del processo Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="997c0-284">L'output dei metodi Console chiamati in una funzione o nel metodo **Main()** viene visualizzato nella pagina Dashboard del WebJob, non nella pagina di una chiamata a un metodo specifico.</span><span class="sxs-lookup"><span data-stu-id="997c0-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="997c0-285">L'output dell'oggetto TextWriter ottenuto da un parametro nella firma del metodo viene visualizzato nella pagina Dashboard di una chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="997c0-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="997c0-286">L'output di Console non può essere collegato a una chiamata a un metodo particolare perché Console è a thread singolo, mentre potrebbero essere in esecuzione più funzioni di processo contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="997c0-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="997c0-287">Per questo motivo l'SDK fornisce a ogni chiamata di funzione il proprio oggetto writer di log univoco.</span><span class="sxs-lookup"><span data-stu-id="997c0-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="997c0-288">Per scrivere [log di traccia dell'applicazione](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), usare **Console.Out** (crea log contrassegnati come INFO) e **Console.Error** (crea log contrassegnati come ERROR).</span><span class="sxs-lookup"><span data-stu-id="997c0-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="997c0-289">In alternativa, è possibile usare [Trace o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), che fornisce livelli dettagliati, di avviso e critici, oltre ai livelli di informazioni e di errore.</span><span class="sxs-lookup"><span data-stu-id="997c0-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="997c0-290">I log di traccia dell'applicazione vengono visualizzati nei file di log dell'app Web, nelle tabelle di Azure o nei BLOB di Azure a seconda di come è configurata l'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="997c0-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="997c0-291">Come per tutti gli output di Console, anche i 100 registri applicazioni più recenti vengono visualizzati nella pagina Dashboard del processo Web e non nella pagina di una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="997c0-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="997c0-292">L'output di Console viene visualizzato nel dashboard solo se il programma viene eseguito in un processo Web di Azure e non se il programma viene eseguito localmente o in un altro ambiente.</span><span class="sxs-lookup"><span data-stu-id="997c0-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="997c0-293">È possibile disabilitare la registrazione impostando la stringa di connessione del dashboard su Null.</span><span class="sxs-lookup"><span data-stu-id="997c0-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="997c0-294">Per altre informazioni, vedere l'argomento relativo a [come impostare le opzioni di configurazione](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="997c0-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="997c0-295">Nell'esempio seguente vengono illustrati diversi modi per scrivere log:</span><span class="sxs-lookup"><span data-stu-id="997c0-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="997c0-296">Nel dashboard di WebJobs SDK viene visualizzato l'output dell'oggetto **TextWriter** quando si visita la pagina relativa a una chiamata di funzione specifica e si fa clic su **Attiva/Disattiva output**:</span><span class="sxs-lookup"><span data-stu-id="997c0-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Collegamento della chiamata](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="997c0-299">Nel dashboard di WebJobs SDK le 100 righe più recenti dell'output di Console vengono visualizzate quando si visita la pagina relativa al processo Web (non alla chiamata di funzione) e si fa clic su **Attiva/Disattiva output**.</span><span class="sxs-lookup"><span data-stu-id="997c0-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Attiva/Disattiva Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="997c0-301">In un processo Web continuo, i log dell'applicazione vengono visualizzati in /data/jobs/continuous/*{nomeprocessoweb}*/job_log.txt nel file system dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="997c0-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="997c0-302">In un BLOB di Azure, l'aspetto dei registri applicazione è simile al seguente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="997c0-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="997c0-303">In una tabella di Azure i log **Console.Out** e **Console.Error** hanno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="997c0-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Log delle informazioni nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log degli errori nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="997c0-306">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="997c0-306">Next steps</span></span>
<span data-ttu-id="997c0-307">Questo articolo ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di code di Azure.</span><span class="sxs-lookup"><span data-stu-id="997c0-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="997c0-308">Per altre informazioni su come usare Processi Web di Azure e WebJobs SDK, vedere le [risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="997c0-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

