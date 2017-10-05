---
title: Come usare il servizio di archiviazione code di Azure con WebJobs SDK
description: Informazioni su come usare il servizio di archiviazione code di Azure con WebJobs SDK. Creare ed eliminare code, inserire, visualizzare, ottenere ed eliminare messaggi dalla coda e altro ancora.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="50540-104">Come usare il servizio di archiviazione code di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="50540-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="50540-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="50540-105">Overview</span></span>
<span data-ttu-id="50540-106">Questa guida fornisce esempi di codice C# che illustrano come usare Azure WebJobs SDK versione 1.x con il servizio di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="50540-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="50540-107">Nella guida si presuppone che si sappia come [creare un progetto processo Web in Visual Studio con stringhe di connessione che puntano all'account di archiviazione](websites-dotnet-webjobs-sdk-get-started.md) o a [più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="50540-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="50540-108">La maggior parte dei frammenti di codice mostra solo le funzioni, non il codice che crea l'oggetto `JobHost` come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="50540-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="50540-109">La guida include i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="50540-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="50540-110">Come attivare una funzione quando viene ricevuto un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="50540-111">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="50540-111">String queue messages</span></span>
  * <span data-ttu-id="50540-112">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="50540-112">POCO queue messages</span></span>
  * <span data-ttu-id="50540-113">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="50540-113">Async functions</span></span>
  * <span data-ttu-id="50540-114">Tipi usati dall'attributo QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="50540-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="50540-115">Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="50540-115">Polling algorithm</span></span>
  * <span data-ttu-id="50540-116">Più istanze</span><span class="sxs-lookup"><span data-stu-id="50540-116">Multiple instances</span></span>
  * <span data-ttu-id="50540-117">Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="50540-117">Parallel execution</span></span>
  * <span data-ttu-id="50540-118">Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="50540-119">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="50540-119">Graceful shutdown</span></span>
* [<span data-ttu-id="50540-120">Come creare un messaggio in coda durante l'elaborazione di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="50540-121">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="50540-121">String queue messages</span></span>
  * <span data-ttu-id="50540-122">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="50540-122">POCO queue messages</span></span>
  * <span data-ttu-id="50540-123">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="50540-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="50540-124">Tipi usati dall'attributo Queue</span><span class="sxs-lookup"><span data-stu-id="50540-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="50540-125">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="50540-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="50540-126">Come leggere e scrivere BLOB durante l'elaborazione di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="50540-127">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="50540-127">String queue messages</span></span>
  * <span data-ttu-id="50540-128">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="50540-128">POCO queue messages</span></span>
  * <span data-ttu-id="50540-129">Tipi usati dall'attributo Blob</span><span class="sxs-lookup"><span data-stu-id="50540-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="50540-130">Come gestire i messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="50540-131">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="50540-132">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-132">Manual poison message handling</span></span>
* [<span data-ttu-id="50540-133">Come impostare le opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="50540-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="50540-134">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="50540-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="50540-135">Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="50540-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="50540-136">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="50540-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="50540-137">Come attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="50540-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="50540-138">Come scrivere i log</span><span class="sxs-lookup"><span data-stu-id="50540-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="50540-139">Come gestire gli errori e configurare i timeout</span><span class="sxs-lookup"><span data-stu-id="50540-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="50540-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50540-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="50540-141"><a id="trigger"></a> Come attivare una funzione quando viene ricevuto un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="50540-142">Per scrivere una funzione che viene chiamata da WebJobs SDK quando viene ricevuto un messaggio di coda, usare l'attributo `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="50540-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="50540-143">Il costruttore dell'attributo accetta un parametro di stringa che specifica il nome della coda di cui eseguire il polling.</span><span class="sxs-lookup"><span data-stu-id="50540-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="50540-144">È anche possibile [impostare il nome della coda in modo dinamico](#config).</span><span class="sxs-lookup"><span data-stu-id="50540-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="50540-145">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="50540-145">String queue messages</span></span>
<span data-ttu-id="50540-146">Nel seguente esempio la coda contiene un messaggio stringa in modo che l'attributo `QueueTrigger` venga applicato a un parametro di stringa denominato `logMessage` che include il contenuto del messaggio di coda.</span><span class="sxs-lookup"><span data-stu-id="50540-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="50540-147">La funzione [scrive un messaggio di log nel dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="50540-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="50540-148">Oltre a `string`, il parametro può essere una matrice di byte, un oggetto `CloudQueueMessage` o un oggetto POCO definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="50540-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="50540-149">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="50540-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="50540-150">Nel seguente esempio il messaggio di coda contiene JSON per un oggetto `BlobInformation` che include una proprietà `BlobName`.</span><span class="sxs-lookup"><span data-stu-id="50540-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="50540-151">L'SDK deserializza automaticamente l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="50540-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="50540-152">L'SDK usa il pacchetto [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) per serializzare e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="50540-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="50540-153">Se si creano messaggi di coda in un programma che non usa WebJobs SDK, è possibile scrivere codice simile a quello del seguente esempio per creare un messaggio di coda POCO analizzabile dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="50540-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="50540-154">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="50540-154">Async functions</span></span>
<span data-ttu-id="50540-155">La seguente funzione asincrona [scrive un log nel dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="50540-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="50540-156">Le funzioni asincrone possono usare un [token di annullamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), come illustrato nel seguente esempio che copia un BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="50540-157">(per una spiegazione del segnaposto `queueTrigger`, vedere la sezione [BLOB](#blobs)).</span><span class="sxs-lookup"><span data-stu-id="50540-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="50540-158"><a id="qtattributetypes"></a> Tipi usati dall'attributo QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="50540-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="50540-159">È possibile usare `QueueTrigger` con i seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="50540-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="50540-160">Tipo POCO serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="50540-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="50540-161"><a id="polling"></a> Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="50540-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="50540-162">L'SDK implementa un algoritmo di backoff esponenziale casuale per ridurre l'effetto del polling delle code inattive sui costi delle transazioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50540-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="50540-163">Quando viene trovato un messaggio, l'SDK attende due secondi e controlla la presenza di un altro messaggio. Quando non viene trovato alcun messaggio, rimane in attesa per circa quattro secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="50540-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="50540-164">Dopo alcuni tentativi non riusciti per ottenere un messaggio nella coda, il tempo di attesa continua ad aumentare finché non raggiunge il tempo massimo di attesa, che per impostazione predefinita è di un minuto.</span><span class="sxs-lookup"><span data-stu-id="50540-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="50540-165">[Il tempo di attesa massimo è configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="50540-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="50540-166"><a id="instances"></a> Più istanze</span><span class="sxs-lookup"><span data-stu-id="50540-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="50540-167">Se l'app Web viene eseguita in più istanze, in ogni computer i WebJob verranno eseguiti in modalità continua e ogni computer attenderà i trigger e proverà a eseguire le funzioni.</span><span class="sxs-lookup"><span data-stu-id="50540-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="50540-168">Il trigger delle code SDK di WebJobs impedisce automaticamente a una funzione di elaborare un messaggio di coda più volte. Le funzioni non devono essere scritte per essere idempotenti.</span><span class="sxs-lookup"><span data-stu-id="50540-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="50540-169">Tuttavia, se si desidera garantire che solo un'istanza di una funzione venga eseguita anche se sono presenti più istanze dell’app web host, è possibile utilizzare l’attributo `Singleton`.</span><span class="sxs-lookup"><span data-stu-id="50540-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="50540-170"><a id="parallel"></a> Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="50540-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="50540-171">Se si dispongono di più funzioni in ascolto in code diverse, l'SDK le chiamerà in parallelo quando i messaggi vengono ricevuti simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="50540-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="50540-172">Lo stesso vale quando si ricevono più messaggi per una singola coda.</span><span class="sxs-lookup"><span data-stu-id="50540-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="50540-173">Per impostazione predefinita, l'SDK ottiene un batch di 16 messaggi in coda alla volta ed esegue la funzione che li elabora in parallelo.</span><span class="sxs-lookup"><span data-stu-id="50540-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="50540-174">[La dimensione del batch è configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="50540-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="50540-175">Quando il numero elaborato viene ridotto alla metà della dimensione del batch, l'SDK ottiene un altro batch e inizia l'elaborazione dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="50540-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="50540-176">Di conseguenza, il numero massimo di messaggi simultanei elaborati per ogni funzione è pari a una volta e mezza la dimensione del batch.</span><span class="sxs-lookup"><span data-stu-id="50540-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="50540-177">Questo limite si applica separatamente a ogni funzione caratterizzata da un attributo `QueueTrigger` .</span><span class="sxs-lookup"><span data-stu-id="50540-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="50540-178">Se non si vuole avviare l'esecuzione parallela per i messaggi ricevuti su una coda, impostare le dimensioni del batch su 1.</span><span class="sxs-lookup"><span data-stu-id="50540-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="50540-179">Vedere anche **Maggiore controllo sull'elaborazione delle code** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="50540-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="50540-180"><a id="queuemetadata"></a>Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="50540-181">Con l'aggiunta di parametri alla firma del metodo, è possibile ottenere le proprietà del messaggio seguenti:</span><span class="sxs-lookup"><span data-stu-id="50540-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="50540-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="50540-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="50540-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="50540-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="50540-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="50540-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="50540-185">`string` queueTrigger (contiene il testo del messaggio)</span><span class="sxs-lookup"><span data-stu-id="50540-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="50540-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="50540-186">`string` id</span></span>
* <span data-ttu-id="50540-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="50540-187">`string` popReceipt</span></span>
* <span data-ttu-id="50540-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="50540-188">`int` dequeueCount</span></span>

<span data-ttu-id="50540-189">Se si desidera usare direttamente l'API di archiviazione di Azure, è anche possibile aggiungere un parametro `CloudStorageAccount` .</span><span class="sxs-lookup"><span data-stu-id="50540-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="50540-190">Nell'esempio seguente tutti questi metadati vengono scritti in un log applicazione INFO.</span><span class="sxs-lookup"><span data-stu-id="50540-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="50540-191">Nell'esempio, gli attributi logMessage e queueTrigger includono il contenuto del messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="50540-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="50540-192">Ecco un log di esempio scritto dal codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="50540-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="50540-193"><a id="graceful"></a>Arresto normale</span><span class="sxs-lookup"><span data-stu-id="50540-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="50540-194">Una funzione eseguita in un processo Web continuo può accettare un parametro `CancellationToken` che consente al sistema operativo di notificare alla funzione quando il processo Web sta per essere terminato.</span><span class="sxs-lookup"><span data-stu-id="50540-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="50540-195">È possibile usare questa notifica per assicurarsi che la funzione non termini in modo imprevisto lasciando i dati in uno stato incoerente.</span><span class="sxs-lookup"><span data-stu-id="50540-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="50540-196">L'esempio seguente illustra come controllare la chiusura imminente di un processo Web in una funzione.</span><span class="sxs-lookup"><span data-stu-id="50540-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="50540-197">**Nota:** è possibile che il dashboard non mostri correttamente lo stato e il risultato delle funzioni che sono state interrotte.</span><span class="sxs-lookup"><span data-stu-id="50540-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="50540-198">Per altre informazioni, vedere l'articolo sull' [arresto normale dei processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="50540-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="50540-199"><a id="createqueue"></a> Come creare un messaggio in coda durante l'elaborazione di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="50540-200">Per scrivere una funzione che crea un nuovo messaggio di coda, usare l'attributo `Queue` .</span><span class="sxs-lookup"><span data-stu-id="50540-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="50540-201">Come per l'attributo `QueueTrigger`, è possibile passare il nome della coda come stringa oppure [impostare dinamicamente il nome della coda](#config).</span><span class="sxs-lookup"><span data-stu-id="50540-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="50540-202">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="50540-202">String queue messages</span></span>
<span data-ttu-id="50540-203">Il seguente esempio di codice non asincrono crea nella coda denominata "outputqueue" un nuovo messaggio di coda con lo stesso contenuto del messaggio di coda ricevuto nella coda denominata "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="50540-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="50540-204">Per le funzioni asincrone, usare `IAsyncCollector<T>` come illustrato più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="50540-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="50540-205">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="50540-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="50540-206">Per creare un messaggio di coda contenente un oggetto POCO anziché una stringa, passare il tipo POCO come parametro di output al costruttore dell'attributo `Queue` .</span><span class="sxs-lookup"><span data-stu-id="50540-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="50540-207">L'SDK deserializza automaticamente l'oggetto in JSON.</span><span class="sxs-lookup"><span data-stu-id="50540-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="50540-208">Viene sempre creato un messaggio in coda, anche se l'oggetto è null.</span><span class="sxs-lookup"><span data-stu-id="50540-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="50540-209">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="50540-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="50540-210">Per creare più messaggi, impostare il tipo di parametro per la coda di output `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="50540-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="50540-211">Ogni messaggio di coda viene creato immediatamente quando viene chiamato il metodo `Add` .</span><span class="sxs-lookup"><span data-stu-id="50540-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="50540-212">Tipi usati dall'attributo Queue</span><span class="sxs-lookup"><span data-stu-id="50540-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="50540-213">È possibile usare l'attributo `Queue` nei seguenti tipi di parametri:</span><span class="sxs-lookup"><span data-stu-id="50540-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="50540-214">`out string` (crea il messaggio di coda se il valore del parametro è diverso da null quando termina la funzione)</span><span class="sxs-lookup"><span data-stu-id="50540-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="50540-215">`out byte[]` (funziona come `string`)</span><span class="sxs-lookup"><span data-stu-id="50540-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="50540-216">`out CloudQueueMessage` (funziona come `string`)</span><span class="sxs-lookup"><span data-stu-id="50540-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="50540-217">`out POCO` (tipo serializzabile, crea un messaggio con un oggetto null se il parametro è null quando termina la funzione)</span><span class="sxs-lookup"><span data-stu-id="50540-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="50540-218">`CloudQueue` (per la creazione manuale dei messaggi direttamente con l'API di archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="50540-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="50540-219"><a id="ibinder"></a>Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="50540-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="50540-220">Se è necessario eseguire alcune operazioni nella funzione prima di usare un attributo di WebJobs SDK come `Queue`, `Blob` o `Table`, è possibile usare l'interfaccia `IBinder`.</span><span class="sxs-lookup"><span data-stu-id="50540-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="50540-221">Nell'esempio seguente viene accettato un messaggio di coda di input e creato un nuovo messaggio con lo stesso contenuto in una coda di output.</span><span class="sxs-lookup"><span data-stu-id="50540-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="50540-222">Il nome della coda di output viene impostato dal codice nel corpo della funzione.</span><span class="sxs-lookup"><span data-stu-id="50540-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="50540-223">L'interfaccia `IBinder`può essere usata anche con gli attributi `Table` e `Blob`.</span><span class="sxs-lookup"><span data-stu-id="50540-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="50540-224"><a id="blobs"></a> Come leggere e scrivere BLOB e tabelle durante l'elaborazione di un messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="50540-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="50540-225">Gli attributi `Blob` e `Table` consentono di leggere e scrivere BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="50540-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="50540-226">Gli esempi in questa sezione si applicano ai BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="50540-227">Per esempi di codice che illustrano come attivare processi quando i BLOB vengono creati o aggiornati, vedere [Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) e per esempi di codice che leggono e scrivono tabelle, vedere [Come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="50540-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="50540-228">Messaggi di coda stringa che attivano operazioni BLOB</span><span class="sxs-lookup"><span data-stu-id="50540-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="50540-229">Per un messaggio di coda contenente una stringa, `queueTrigger` è un segnaposto che è possibile usare nel parametro `blobPath` dell'attributo `Blob` che include il contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="50540-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="50540-230">Il seguente esempio usa oggetti `Stream` per leggere e scrivere i BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="50540-231">Il messaggio di coda è il nome di un BLOB presente nel contenitore textblobs.</span><span class="sxs-lookup"><span data-stu-id="50540-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="50540-232">Una copia del BLOB con "-new" aggiunto al nome viene creata nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="50540-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="50540-233">Il costruttore dell'attributo `Blob` usa un parametro `blobPath` che specifica il contenitore e il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="50540-234">Per altre informazioni su questo segnaposto, vedere [Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="50540-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="50540-235">Quando l'attributo decora un oggetto `Stream`, un altro parametro del costruttore specifica la modalità `FileAccess` come lettura, scrittura o lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="50540-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="50540-236">Il seguente esempio usa un oggetto `CloudBlockBlob` per eliminare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="50540-237">Il messaggio di coda è il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="50540-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="50540-238"><a id="pocoblobs"></a> Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="50540-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="50540-239">Per un oggetto POCO archiviato come JSON nel messaggio di coda, è possibile usare i segnaposto che denominano le proprietà dell'oggetto nel parametro `blobPath` dell'attributo `Queue`.</span><span class="sxs-lookup"><span data-stu-id="50540-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="50540-240">È anche possibile usare [nomi di proprietà dei metadati di coda](#queuemetadata) come segnaposto.</span><span class="sxs-lookup"><span data-stu-id="50540-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="50540-241">Il seguente esempio copia un BLOB in un nuovo BLOB con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="50540-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="50540-242">Il messaggio di coda è un oggetto `BlobInformation` che include le proprietà  `BlobName` e `BlobNameWithoutExtension`.</span><span class="sxs-lookup"><span data-stu-id="50540-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="50540-243">I nomi delle proprietà vengono usati come segnaposto nel percorso BLOB per gli attributi `Blob` .</span><span class="sxs-lookup"><span data-stu-id="50540-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="50540-244">L'SDK usa il pacchetto [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) per serializzare e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="50540-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="50540-245">Se si creano messaggi di coda in un programma che non usa WebJobs SDK, è possibile scrivere codice simile a quello del seguente esempio per creare un messaggio di coda POCO analizzabile dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="50540-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="50540-246">Se è necessario eseguire alcune operazioni nella funzione prima di associare un BLOB a un oggetto, è possibile usare l'attributo nel corpo della funzione, [come mostrato in precedenza per l'attributo Queue](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="50540-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="50540-247"><a id="blobattributetypes"></a> Tipi con cui è possibile usare l'attributo Blob</span><span class="sxs-lookup"><span data-stu-id="50540-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="50540-248">L'attributo `Blob` può essere usato con i seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="50540-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="50540-249">`Stream` (lettura o scrittura, specificata tramite il parametro del costruttore FileAccess)</span><span class="sxs-lookup"><span data-stu-id="50540-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="50540-250">`string` (lettura)</span><span class="sxs-lookup"><span data-stu-id="50540-250">`string` (read)</span></span>
* <span data-ttu-id="50540-251">`out string` (scrittura; crea un BLOB solo se il parametro di stringa è diverso da null quando la funzione restituisce un valore)</span><span class="sxs-lookup"><span data-stu-id="50540-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="50540-252">POCO (lettura)</span><span class="sxs-lookup"><span data-stu-id="50540-252">POCO (read)</span></span>
* <span data-ttu-id="50540-253">out POCO (scrittura; crea sempre un BLOB come oggetto null se il parametro POCO è null quando la funzione restituisce un valore)</span><span class="sxs-lookup"><span data-stu-id="50540-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="50540-254">`CloudBlobStream` (scrittura)</span><span class="sxs-lookup"><span data-stu-id="50540-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="50540-255">`ICloudBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="50540-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="50540-256">`CloudBlockBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="50540-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="50540-257">`CloudPageBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="50540-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="50540-258"><a id="poison"></a> Come gestire i messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="50540-259">I messaggi il cui contenuto comporta l'esito negativo di una funzione sono denominati *messaggi non elaborabili*.</span><span class="sxs-lookup"><span data-stu-id="50540-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="50540-260">Quando la funzione non riesce, il messaggio in coda non viene eliminato e infine viene prelevato, causando la ripetizione del ciclo.</span><span class="sxs-lookup"><span data-stu-id="50540-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="50540-261">L'SDK può interrompere automaticamente il ciclo dopo un numero limitato di iterazioni oppure è possibile farlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="50540-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="50540-262">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-262">Automatic poison message handling</span></span>
<span data-ttu-id="50540-263">L'SDK chiamerà una funzione fino a 5 volte per elaborare un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="50540-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="50540-264">Se il quinto tentativo non riesce, il messaggio viene spostato in una coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="50540-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="50540-265">[Il numero massimo di tentativi è configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="50540-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="50540-266">La coda non elaborabile è denominata *{nomecodaoriginale}*-poison.</span><span class="sxs-lookup"><span data-stu-id="50540-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="50540-267">È possibile scrivere una funzione per elaborare i messaggi dalla coda non elaborabile archiviandoli o inviando una notifica della necessità di un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="50540-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="50540-268">Nel seguente esempio la funzione `CopyBlob` ha esito negativo quando un messaggio di coda contiene il nome di un BLOB inesistente.</span><span class="sxs-lookup"><span data-stu-id="50540-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="50540-269">In questo caso, il messaggio viene spostato dalla coda copyblobqueue alla coda non elaborabile copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="50540-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="50540-270">`ProcessPoisonMessage` registra quindi il messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="50540-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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

<span data-ttu-id="50540-271">Nella figura seguente viene illustrato l'output di console di queste funzioni quando viene elaborato un messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="50540-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Output di console per la gestione dei messaggi non elaborabili](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="50540-273">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="50540-273">Manual poison message handling</span></span>
<span data-ttu-id="50540-274">È possibile ottenere il numero di volte in cui un messaggio è stato selezionato per l'elaborazione aggiungendo alla funzione un parametro `int` denominato `dequeueCount`.</span><span class="sxs-lookup"><span data-stu-id="50540-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="50540-275">Sarà quindi possibile controllare il conteggio di rimozione dalla coda nel codice della funzione ed eseguire la gestione dei messaggi non elaborabili quando il numero supera una certa soglia, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="50540-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <span data-ttu-id="50540-276"><a id="config"></a> Come impostare le opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="50540-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="50540-277">È possibile usare il tipo `JobHostConfiguration` per impostare le seguenti opzioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="50540-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="50540-278">Impostare le stringhe di connessione SDK nel codice.</span><span class="sxs-lookup"><span data-stu-id="50540-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="50540-279">Configurare le impostazioni di `QueueTrigger` , ad esempio il conteggio rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="50540-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="50540-280">Ottenere i nomi delle code dalla configurazione.</span><span class="sxs-lookup"><span data-stu-id="50540-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="50540-281"><a id="setconnstr"></a>Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="50540-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="50540-282">Impostare le stringhe di connessione SDK nel codice per poter usare i propri nomi di stringa di connessione nei file di configurazione o nelle variabili di ambiente, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="50540-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="50540-283"><a id="configqueue"></a>Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="50540-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="50540-284">È possibile configurare le seguenti impostazioni valide per l'elaborazione del messaggio di coda:</span><span class="sxs-lookup"><span data-stu-id="50540-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="50540-285">Numero massimo di messaggi in coda che vengono prelevati contemporaneamente per l'esecuzione in parallelo (il valore predefinito è 16).</span><span class="sxs-lookup"><span data-stu-id="50540-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="50540-286">Numero massimo di tentativi prima che un messaggio nella coda venga inviato a una coda non elaborabile (il valore predefinito è 5).</span><span class="sxs-lookup"><span data-stu-id="50540-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="50540-287">Tempo massimo di attesa prima di eseguire nuovamente il polling quando una coda è vuota (il valore predefinito è 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="50540-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="50540-288">L'esempio seguente illustra come configurare queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="50540-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="50540-289"><a id="setnamesincode"></a>Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="50540-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="50540-290">A volte si desidera specificare un nome di coda, un nome di BLOB o un contenitore oppure un nome di tabella nel codice anziché impostarlo come hardcoded.</span><span class="sxs-lookup"><span data-stu-id="50540-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="50540-291">È ad esempio possibile specificare il nome della coda per `QueueTrigger` in una variabile di ambiente o in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="50540-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="50540-292">A tale scopo, passare un oggetto `NameResolver` al tipo `JobHostConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="50540-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="50540-293">Includere segnaposto speciali racchiusi tra segni di percentuale (%) nei parametri del costruttore dell'attributo di SDK e il codice `NameResolver` specifica i valori effettivi da usare in sostituzione di questi segnaposto.</span><span class="sxs-lookup"><span data-stu-id="50540-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="50540-294">Si supponga, ad esempio, di voler usare una coda denominata logqueuetest nell'ambiente di test e una coda denominata logqueueprod nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="50540-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="50540-295">Invece di impostare un nome di coda come hardcoded, è possibile specificare il nome di una voce nella raccolta `appSettings` con il nome effettivo della coda.</span><span class="sxs-lookup"><span data-stu-id="50540-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="50540-296">Se la chiave `appSettings` è logqueue, la funzione potrebbe essere simile al seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="50540-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="50540-297">La classe `NameResolver` può quindi ottenere il nome della coda da `appSettings`, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="50540-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="50540-298">Passare la classe `NameResolver` all'oggetto `JobHost`, come illustrato nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="50540-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="50540-299">**Nota:** i nomi di coda, tabella e BLOB vengono risolti ogni volta che viene chiamata una funzione, ma i nomi di contenitore di BLOB vengono risolti solo all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50540-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="50540-300">Non è possibile modificare il nome del contenitore di BLOB durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="50540-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="50540-301"><a id="manual"></a>Come attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="50540-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="50540-302">Per attivare manualmente una funzione, usare il metodo `Call` o `CallAsync` per l'oggetto `JobHost` e l'attributo `NoAutomaticTrigger` per la funzione, come illustrato nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="50540-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="50540-303"><a id="logs"></a>Come scrivere i log</span><span class="sxs-lookup"><span data-stu-id="50540-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="50540-304">Il dashboard visualizza i log in due posizioni: la pagina del processo Web e la pagina di una particolare chiamata al processo Web.</span><span class="sxs-lookup"><span data-stu-id="50540-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Log nella pagina del processo Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Log nella pagina di una chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="50540-307">L'output dei metodi Console chiamati in una funzione o nel metodo `Main()` viene visualizzato nella pagina Dashboard del WebJob, non nella pagina di una chiamata a un metodo specifico.</span><span class="sxs-lookup"><span data-stu-id="50540-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="50540-308">L'output dell'oggetto TextWriter ottenuto da un parametro nella firma del metodo viene visualizzato nella pagina Dashboard di una chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="50540-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="50540-309">L'output di Console non può essere collegato a una chiamata a un metodo particolare perché Console è a thread singolo, mentre potrebbero essere in esecuzione più funzioni di processo contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="50540-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="50540-310">Per questo motivo l'SDK fornisce a ogni chiamata di funzione il proprio oggetto writer di log univoco.</span><span class="sxs-lookup"><span data-stu-id="50540-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="50540-311">Per scrivere [log di traccia dell'applicazione](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), usare `Console.Out` (crea log contrassegnati come INFO) e `Console.Error` (crea log contrassegnati come ERROR).</span><span class="sxs-lookup"><span data-stu-id="50540-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="50540-312">In alternativa, è possibile usare [Trace o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), che fornisce livelli dettagliati, di avviso e critici, oltre ai livelli di informazioni e di errore.</span><span class="sxs-lookup"><span data-stu-id="50540-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="50540-313">I log di traccia dell'applicazione vengono visualizzati nei file di log dell'app Web, nelle tabelle di Azure o nei BLOB di Azure a seconda di come è configurata l'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="50540-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="50540-314">Come per tutti gli output di Console, anche i 100 registri applicazioni più recenti vengono visualizzati nella pagina Dashboard del processo Web e non nella pagina di una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="50540-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="50540-315">L'output di Console viene visualizzato nel dashboard solo se il programma viene eseguito in un processo Web di Azure e non se il programma viene eseguito localmente o in un altro ambiente.</span><span class="sxs-lookup"><span data-stu-id="50540-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="50540-316">Disabilitare la registrazione dei dashboard per scenari con velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="50540-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="50540-317">Per impostazione predefinita, l’SDK scrive i log nella memoria e questa attività potrebbe influire negativamente sulle prestazioni quando si elaborano numerosi messaggi.</span><span class="sxs-lookup"><span data-stu-id="50540-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="50540-318">Per disabilitare la registrazione, impostare la stringa di connessione dashboard su null, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="50540-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="50540-319">Nell'esempio seguente vengono illustrati diversi modi per scrivere log:</span><span class="sxs-lookup"><span data-stu-id="50540-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="50540-320">Nel dashboard di WebJobs SDK, l'output dell'oggetto `TextWriter` viene visualizzato quando si visita la pagina relativa a una chiamata di funzione specifica e si fa clic su **Attiva/Disattiva output**:</span><span class="sxs-lookup"><span data-stu-id="50540-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![Fare clic sul collegamento della chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Log nella pagina di una chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="50540-323">Nel dashboard di WebJobs SDK le 100 righe più recenti dell'output di Console vengono visualizzate quando si visita la pagina relativa al processo Web (non alla chiamata di funzione) e si fa clic su **Attiva/Disattiva output**.</span><span class="sxs-lookup"><span data-stu-id="50540-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Fare clic su Toggle Output](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="50540-325">In un processo Web continuo, i log dell'applicazione vengono visualizzati in /data/jobs/continuous/*{nomeprocessoweb}*/job_log.txt nel file system dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="50540-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="50540-326">In un BLOB di Azure, l'aspetto dei registri applicazione è simile al seguente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="50540-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="50540-327">In una tabella di Azure, i log `Console.Out` e `Console.Error` hanno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="50540-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Log delle informazioni nella tabella](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Log degli errori nella tabella](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="50540-330">Se si desidera collegare un proprio logger, vedere [questo esempio](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="50540-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="50540-331"><a id="errors"></a>Come gestire gli errori e configurare i timeout</span><span class="sxs-lookup"><span data-stu-id="50540-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="50540-332">WebJobs SDK include anche un attributo [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) che è possibile utilizzare per annullare una funzione se non viene completata entro un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="50540-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="50540-333">E se si desidera generare un avviso quando si verificano numerosi errori entro un periodo di tempo specificato, è possibile utilizzare l’attributo `ErrorTrigger` .</span><span class="sxs-lookup"><span data-stu-id="50540-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="50540-334">Ecco un [esempio ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="50540-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="50540-335">Anche in modo dinamico, è possibile disabilitare e abilitare le funzioni per controllare se possono essere attivate, utilizzando un'opzione di configurazione che potrebbe essere un'impostazione app o il nome della variabile dell’ambiente.</span><span class="sxs-lookup"><span data-stu-id="50540-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="50540-336">Per codici di esempio, vedere l’attributo `Disable` nel [repository degli esempi di WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="50540-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="50540-337"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50540-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="50540-338">Questa guida ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di code di Azure.</span><span class="sxs-lookup"><span data-stu-id="50540-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="50540-339">Per altre informazioni su come usare i processi Web di Azure e su WebJobs SDK, vedere le [risorse consigliate per i processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="50540-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
