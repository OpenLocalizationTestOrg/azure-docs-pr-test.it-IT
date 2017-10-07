---
title: aaaHow toouse l'archiviazione delle code di Azure con hello WebJobs SDK
description: Informazioni su come toouse Azure coda di archiviazione con hello WebJobs SDK. Creare ed eliminare code, inserire, visualizzare, ottenere ed eliminare messaggi dalla coda e altro ancora.
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
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="b34bd-104">Coda di archiviazione con hello WebJobs SDK come toouse Azure</span><span class="sxs-lookup"><span data-stu-id="b34bd-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="b34bd-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b34bd-105">Overview</span></span>
<span data-ttu-id="b34bd-106">Questa guida vengono forniti esempi di codice c# che mostrano come toouse hello Azure WebJobs SDK versione 1. x con il servizio di archiviazione di Azure coda hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="b34bd-107">Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o troppo[più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="b34bd-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="b34bd-108">La maggior parte dei frammenti di codice hello Mostra solo le funzioni, hello non codice che crea hello `JobHost` oggetto come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="b34bd-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="b34bd-109">Guida di Hello include hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="b34bd-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="b34bd-110">Come tootrigger una funzione quando viene ricevuto un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="b34bd-111">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-111">String queue messages</span></span>
  * <span data-ttu-id="b34bd-112">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="b34bd-112">POCO queue messages</span></span>
  * <span data-ttu-id="b34bd-113">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="b34bd-113">Async functions</span></span>
  * <span data-ttu-id="b34bd-114">Attributo di tipi hello QueueTrigger funziona con</span><span class="sxs-lookup"><span data-stu-id="b34bd-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="b34bd-115">Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="b34bd-115">Polling algorithm</span></span>
  * <span data-ttu-id="b34bd-116">Più istanze</span><span class="sxs-lookup"><span data-stu-id="b34bd-116">Multiple instances</span></span>
  * <span data-ttu-id="b34bd-117">Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="b34bd-117">Parallel execution</span></span>
  * <span data-ttu-id="b34bd-118">Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="b34bd-119">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="b34bd-119">Graceful shutdown</span></span>
* [<span data-ttu-id="b34bd-120">Come toocreate una coda dei messaggi durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="b34bd-121">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-121">String queue messages</span></span>
  * <span data-ttu-id="b34bd-122">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="b34bd-122">POCO queue messages</span></span>
  * <span data-ttu-id="b34bd-123">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="b34bd-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="b34bd-124">Attributo della coda di tipi hello funziona con</span><span class="sxs-lookup"><span data-stu-id="b34bd-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="b34bd-125">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="b34bd-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="b34bd-126">Come tooread e scrittura BLOB durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="b34bd-127">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-127">String queue messages</span></span>
  * <span data-ttu-id="b34bd-128">Messaggi di coda POCO</span><span class="sxs-lookup"><span data-stu-id="b34bd-128">POCO queue messages</span></span>
  * <span data-ttu-id="b34bd-129">Attributo di Blob hello tipi funziona con</span><span class="sxs-lookup"><span data-stu-id="b34bd-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="b34bd-130">Come messaggi non elaborabili toohandle</span><span class="sxs-lookup"><span data-stu-id="b34bd-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="b34bd-131">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b34bd-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="b34bd-132">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b34bd-132">Manual poison message handling</span></span>
* [<span data-ttu-id="b34bd-133">Come le opzioni di configurazione tooset</span><span class="sxs-lookup"><span data-stu-id="b34bd-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="b34bd-134">Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="b34bd-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="b34bd-135">Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="b34bd-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="b34bd-136">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="b34bd-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="b34bd-137">Come una funzione tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="b34bd-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="b34bd-138">Modalità di registrazione toowrite</span><span class="sxs-lookup"><span data-stu-id="b34bd-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="b34bd-139">Modalità errori toohandle e configurare i timeout</span><span class="sxs-lookup"><span data-stu-id="b34bd-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="b34bd-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b34bd-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="b34bd-141"><a id="trigger"></a>Come tootrigger una funzione quando viene ricevuto un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="b34bd-142">chiama una funzione che hello WebJobs SDK toowrite quando viene ricevuto un messaggio nella coda, utilizzare hello `QueueTrigger` attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="b34bd-143">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello di hello coda toopoll.</span><span class="sxs-lookup"><span data-stu-id="b34bd-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="b34bd-144">È anche possibile [impostare dinamicamente il nome di coda hello](#config).</span><span class="sxs-lookup"><span data-stu-id="b34bd-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="b34bd-145">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-145">String queue messages</span></span>
<span data-ttu-id="b34bd-146">Nell'esempio seguente di hello, hello coda contiene una stringa di messaggio, pertanto `QueueTrigger` tooa applicato parametro di stringa denominato `logMessage` che comprende il contenuto di hello del messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="b34bd-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="b34bd-147">funzione Hello [scrive un toohello messaggio log Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="b34bd-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="b34bd-148">Oltre a `string`, il parametro hello può essere una matrice di byte, un `CloudQueueMessage` oggetto o un POCO definiti.</span><span class="sxs-lookup"><span data-stu-id="b34bd-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="b34bd-149">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="b34bd-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="b34bd-150">Nell'esempio seguente di hello, messaggio della coda contiene JSON per un `BlobInformation` oggetto che include un `BlobName` proprietà.</span><span class="sxs-lookup"><span data-stu-id="b34bd-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="b34bd-151">Hello SDK deserializza automaticamente oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="b34bd-152">Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="b34bd-153">Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.</span><span class="sxs-lookup"><span data-stu-id="b34bd-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="b34bd-154">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="b34bd-154">Async functions</span></span>
<span data-ttu-id="b34bd-155">Hello seguente funzione async [scrive un toohello log Dashboard](#logs).</span><span class="sxs-lookup"><span data-stu-id="b34bd-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="b34bd-156">Le funzioni asincrone potrebbero richiedere un [token di annullamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), come illustrato nell'esempio che consente di copiare un blob seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="b34bd-157">(Per una spiegazione di hello `queueTrigger` segnaposto, vedere hello [BLOB](#blobs) sezione.)</span><span class="sxs-lookup"><span data-stu-id="b34bd-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="b34bd-158"><a id="qtattributetypes"></a>Attributo di tipi hello QueueTrigger funziona con</span><span class="sxs-lookup"><span data-stu-id="b34bd-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="b34bd-159">È possibile utilizzare `QueueTrigger` con hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="b34bd-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="b34bd-160">Tipo POCO serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="b34bd-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="b34bd-161"><a id="polling"></a> Algoritmo di polling</span><span class="sxs-lookup"><span data-stu-id="b34bd-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="b34bd-162">Hello SDK implementa un effetto di hello esponenziale Backoff algoritmo casuali tooreduce di inattività della coda del polling sui costi delle transazioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="b34bd-163">Quando viene trovato un messaggio, hello SDK attende due secondi e ne controlla la presenza di un altro messaggio. Quando viene trovato alcun messaggio rimane in attesa circa quattro secondi prima di riprovare.</span><span class="sxs-lookup"><span data-stu-id="b34bd-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="b34bd-164">Dopo i tentativi non riusciti successivi tooget un messaggio nella coda, il tempo di attesa hello continua tooincrease finché raggiunge il tempo di attesa massimo hello, il minuto tooone valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b34bd-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="b34bd-165">[Hello tempo di attesa massimo è configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="b34bd-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="b34bd-166"><a id="instances"></a> Più istanze</span><span class="sxs-lookup"><span data-stu-id="b34bd-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="b34bd-167">Se l'app web viene eseguito su più istanze, viene eseguito un processo Web continuo in ogni computer e ogni computer tenterà di attesa per i trigger e funzioni toorun.</span><span class="sxs-lookup"><span data-stu-id="b34bd-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="b34bd-168">Hello trigger coda WebJobs SDK impedisce automaticamente una funzione di un messaggio nella coda di elaborazione più volte. le funzioni non hanno toobe scritto toobe idempotente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="b34bd-169">Tuttavia, se si desidera tooensure solo un'istanza di una funzione viene eseguita anche quando sono presenti più istanze dell'app web di hello host, è possibile utilizzare hello `Singleton` attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="b34bd-170"><a id="parallel"></a> Esecuzione parallela</span><span class="sxs-lookup"><span data-stu-id="b34bd-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="b34bd-171">Se si dispongono di più funzioni in attesa in code diverse, hello SDK verrà chiamarli in parallelo quando vengono ricevuti i messaggi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="b34bd-172">Hello stesso vale quando vengono ricevuti più messaggi per una singola coda.</span><span class="sxs-lookup"><span data-stu-id="b34bd-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="b34bd-173">Per impostazione predefinita, hello SDK riceve un batch di messaggi in coda 16 alla volta ed esegue funzione hello elaborarli in parallelo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="b34bd-174">[dimensioni del batch Hello sono configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="b34bd-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="b34bd-175">Quando il numero di hello elaborato Ottiene verso il basso toohalf della dimensione di batch di hello, hello SDK riceve un altro batch e inizia l'elaborazione di tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="b34bd-176">Numero massimo di hello simultanee messaggi vengano elaborati per ogni funzione pertanto è dimensioni di batch di una volta e mezza hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="b34bd-177">Questo limite si applica separatamente tooeach funzione che ha un `QueueTrigger` attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="b34bd-178">Se non si desidera l'esecuzione parallela per i messaggi ricevuti su una coda, è possibile impostare too1 dimensioni di batch hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="b34bd-179">Vedere anche **Maggiore controllo sull'elaborazione delle code** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="b34bd-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="b34bd-180"><a id="queuemetadata"></a>Ottenere i metadati della coda o del messaggio in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="b34bd-181">È possibile ottenere hello seguenti proprietà di messaggio mediante l'aggiunta di firma del metodo toohello parametri:</span><span class="sxs-lookup"><span data-stu-id="b34bd-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="b34bd-182">`DateTimeOffset` expirationTime</span><span class="sxs-lookup"><span data-stu-id="b34bd-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="b34bd-183">`DateTimeOffset` insertionTime</span><span class="sxs-lookup"><span data-stu-id="b34bd-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="b34bd-184">`DateTimeOffset` nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="b34bd-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="b34bd-185">`string` queueTrigger (contiene il testo del messaggio)</span><span class="sxs-lookup"><span data-stu-id="b34bd-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="b34bd-186">`string` id</span><span class="sxs-lookup"><span data-stu-id="b34bd-186">`string` id</span></span>
* <span data-ttu-id="b34bd-187">`string` popReceipt</span><span class="sxs-lookup"><span data-stu-id="b34bd-187">`string` popReceipt</span></span>
* <span data-ttu-id="b34bd-188">`int` dequeueCount</span><span class="sxs-lookup"><span data-stu-id="b34bd-188">`int` dequeueCount</span></span>

<span data-ttu-id="b34bd-189">Se si desidera toowork direttamente con hello API di archiviazione di Azure, è inoltre possibile aggiungere un `CloudStorageAccount` parametro.</span><span class="sxs-lookup"><span data-stu-id="b34bd-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="b34bd-190">Hello nell'esempio seguente vengono tutti il registro applicazioni di metadati tooan INFO.</span><span class="sxs-lookup"><span data-stu-id="b34bd-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="b34bd-191">Nell'esempio hello logMessage sia queueTrigger contenuto hello di messaggio della coda hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="b34bd-192">Di seguito è riportato un log di esempio scritto dal codice di esempio hello:</span><span class="sxs-lookup"><span data-stu-id="b34bd-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="b34bd-193"><a id="graceful"></a>Arresto normale</span><span class="sxs-lookup"><span data-stu-id="b34bd-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="b34bd-194">Una funzione che viene eseguito in un processo Web continuo può accettare un `CancellationToken` parametro che consente di hello toonotify hello funzione del sistema operativo quando hello processo Web sta toobe terminato.</span><span class="sxs-lookup"><span data-stu-id="b34bd-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="b34bd-195">È possibile utilizzare questo toomake di notifica che la funzione hello non causare l'interruzione imprevista in modo che i dati rimane in uno stato incoerente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="b34bd-196">Hello seguente esempio viene illustrato come toocheck imminente chiusura processo Web in una funzione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="b34bd-197">**Nota:** hello Dashboard potrebbe non visualizzare correttamente hello stato e l'output di funzioni che è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="b34bd-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="b34bd-198">Per altre informazioni, vedere l'articolo sull' [arresto normale dei processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="b34bd-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="b34bd-199"><a id="createqueue"></a>Come toocreate una coda dei messaggi durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="b34bd-200">una funzione che crea un nuovo messaggio, utilizzare hello toowrite `Queue` attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="b34bd-201">Ad esempio `QueueTrigger`, si passa il nome della coda hello sotto forma di stringa oppure è possibile [impostare dinamicamente il nome di coda hello](#config).</span><span class="sxs-lookup"><span data-stu-id="b34bd-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="b34bd-202">Messaggi stringa in coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-202">String queue messages</span></span>
<span data-ttu-id="b34bd-203">Hello non asincrona nell'esempio di codice seguente crea un nuovo messaggio nella coda di hello denominato "outputqueue" con stesso contenuto sotto forma di messaggio della coda di hello ricevuto nella coda di hello denominata "inputqueue" hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="b34bd-204">Per le funzioni asincrone, usare `IAsyncCollector<T>` come illustrato più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="b34bd-205">Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="b34bd-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="b34bd-206">tipo di un messaggio nella coda che contiene un POCO anziché una stringa, passata hello POCO toocreate come un toohello di parametro di output `Queue` costruttore di attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="b34bd-207">Hello SDK serializza automaticamente tooJSON oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="b34bd-208">Viene sempre creato un messaggio nella coda, anche se l'oggetto hello è null.</span><span class="sxs-lookup"><span data-stu-id="b34bd-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="b34bd-209">Creare più messaggi o in funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="b34bd-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="b34bd-210">toocreate più messaggi, rendere il tipo di parametro hello per coda di output di hello `ICollector<T>` o `IAsyncCollector<T>`, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="b34bd-211">Ogni messaggio della coda viene creato immediatamente quando hello `Add` metodo viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="b34bd-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="b34bd-212">Tipi di attributo coda hello funziona con</span><span class="sxs-lookup"><span data-stu-id="b34bd-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="b34bd-213">È possibile utilizzare hello `Queue` attributo hello seguenti tipi di parametro:</span><span class="sxs-lookup"><span data-stu-id="b34bd-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="b34bd-214">`out string`(Crea messaggio della coda se il valore del parametro è diverso da null quando la funzione hello termina)</span><span class="sxs-lookup"><span data-stu-id="b34bd-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="b34bd-215">`out byte[]` (funziona come `string`)</span><span class="sxs-lookup"><span data-stu-id="b34bd-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="b34bd-216">`out CloudQueueMessage` (funziona come `string`)</span><span class="sxs-lookup"><span data-stu-id="b34bd-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="b34bd-217">`out POCO`(un tipo serializzabile, crea un messaggio con un oggetto null, se il parametro hello è null quando la funzione hello termina)</span><span class="sxs-lookup"><span data-stu-id="b34bd-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="b34bd-218">`CloudQueue`(per la creazione di messaggi manualmente utilizzando direttamente hello API di archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="b34bd-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="b34bd-219"><a id="ibinder"></a>Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="b34bd-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="b34bd-220">Se è necessario toodo alcune funzionano nella funzione prima di utilizzare un attributo WebJobs SDK, ad esempio `Queue`, `Blob`, o `Table`, è possibile utilizzare hello `IBinder` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b34bd-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="b34bd-221">Hello di esempio seguente accetta un messaggio della coda di input e crea un nuovo messaggio con stesso contenuto in una coda di output di hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="b34bd-222">nome della coda output Hello viene impostata dal codice nel corpo di hello della funzione hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="b34bd-223">Hello `IBinder` interfaccia può essere utilizzata anche con hello `Table` e `Blob` gli attributi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="b34bd-224"><a id="blobs"></a>Come tooread e scrittura BLOB e tabelle durante l'elaborazione di un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="b34bd-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="b34bd-225">Hello `Blob` e `Table` gli attributi consentono di tooread e scrivere i BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="b34bd-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="b34bd-226">esempi di Hello in questa sezione si applicano tooblobs.</span><span class="sxs-lookup"><span data-stu-id="b34bd-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="b34bd-227">Per esempi di codice che mostrano come tootrigger elabora quando BLOB vengono creati o aggiornati, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e per esempi di codice che leggono e scrivono le tabelle, vedere [come toouse tabelle di Azure archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b34bd-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="b34bd-228">Messaggi di coda stringa che attivano operazioni BLOB</span><span class="sxs-lookup"><span data-stu-id="b34bd-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="b34bd-229">Per un messaggio nella coda che contiene una stringa, `queueTrigger` è un segnaposto che è possibile utilizzare in hello `Blob` dell'attributo `blobPath` parametro hello il contenuto del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="b34bd-230">Hello seguente utilizza `Stream` oggetti BLOB tooread e di scrittura.</span><span class="sxs-lookup"><span data-stu-id="b34bd-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="b34bd-231">messaggio della coda di Hello è il nome di hello di un blob nel contenitore textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="b34bd-232">Una copia di blob hello con "-new" nome toohello accodato viene creato in hello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="b34bd-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="b34bd-233">Hello `Blob` attributo costruttore accetta un `blobPath` parametro che specifica il nome di blob e contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="b34bd-234">Per ulteriori informazioni su questo segnaposto, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="b34bd-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="b34bd-235">Quando attributo hello decora un `Stream` dell'oggetto, un altro parametro di costruttore specifica hello `FileAccess` modalità come lettura, scrittura o lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="b34bd-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="b34bd-236">Hello esempio seguente viene utilizzato un `CloudBlockBlob` oggetto toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="b34bd-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="b34bd-237">messaggio della coda di Hello è il nome di hello del blob hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="b34bd-238"><a id="pocoblobs"></a> Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="b34bd-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="b34bd-239">Per POCO archiviato in formato JSON in messaggio hello in coda, è possibile utilizzare i segnaposto di nome di proprietà dell'oggetto hello in hello `Queue` dell'attributo `blobPath` parametro.</span><span class="sxs-lookup"><span data-stu-id="b34bd-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="b34bd-240">È anche possibile usare [nomi di proprietà dei metadati di coda](#queuemetadata) come segnaposto.</span><span class="sxs-lookup"><span data-stu-id="b34bd-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="b34bd-241">Hello esempio copia un blob tooa nuovo blob con un'estensione diversa.</span><span class="sxs-lookup"><span data-stu-id="b34bd-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="b34bd-242">messaggio della coda di Hello è un `BlobInformation` oggetto che include `BlobName` e `BlobNameWithoutExtension` proprietà.</span><span class="sxs-lookup"><span data-stu-id="b34bd-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="b34bd-243">i nomi delle proprietà Hello vengono utilizzati come segnaposto nel percorso blob hello per hello `Blob` attributi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="b34bd-244">Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="b34bd-245">Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.</span><span class="sxs-lookup"><span data-stu-id="b34bd-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="b34bd-246">Se è necessario toodo alcuni nella funzione prima di associare un oggetto tooan blob, è possibile utilizzare l'attributo di hello nel corpo di hello della funzione hello, [come illustrato in precedenza per l'attributo coda hello](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="b34bd-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="b34bd-247"><a id="blobattributetypes"></a>Tipi di dati hello Blob di attributo con</span><span class="sxs-lookup"><span data-stu-id="b34bd-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="b34bd-248">Hello `Blob` attributo può essere utilizzato con hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="b34bd-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="b34bd-249">`Stream`(lettura o scrittura, specificato utilizzando il parametro di costruttore FileAccess hello)</span><span class="sxs-lookup"><span data-stu-id="b34bd-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="b34bd-250">`string` (lettura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-250">`string` (read)</span></span>
* <span data-ttu-id="b34bd-251">`out string`(scrittura; crea un blob solo se il parametro di stringa hello è non null quando viene restituita la funzione hello)</span><span class="sxs-lookup"><span data-stu-id="b34bd-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="b34bd-252">POCO (lettura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-252">POCO (read)</span></span>
* <span data-ttu-id="b34bd-253">out POCO (scrivere; sempre creato un blob, come oggetto null se il parametro POCO è null quando viene restituita la funzione hello)</span><span class="sxs-lookup"><span data-stu-id="b34bd-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="b34bd-254">`CloudBlobStream` (scrittura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="b34bd-255">`ICloudBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="b34bd-256">`CloudBlockBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="b34bd-257">`CloudPageBlob` (lettura o scrittura)</span><span class="sxs-lookup"><span data-stu-id="b34bd-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="b34bd-258"><a id="poison"></a>Come messaggi non elaborabili toohandle</span><span class="sxs-lookup"><span data-stu-id="b34bd-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="b34bd-259">Messaggi il cui contenuto provoca un toofail funzione sono denominati *messaggi non elaborabili*.</span><span class="sxs-lookup"><span data-stu-id="b34bd-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="b34bd-260">Quando la funzione hello non riesce, il messaggio di coda hello non viene eliminato e infine viene prelevato nuovamente, causando hello ciclo toobe ripetuto.</span><span class="sxs-lookup"><span data-stu-id="b34bd-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="b34bd-261">Hello SDK automaticamente in grado di interrompere il ciclo di hello dopo un numero limitato di iterazioni o è possibile farlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="b34bd-262">Gestione automatica dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b34bd-262">Automatic poison message handling</span></span>
<span data-ttu-id="b34bd-263">Hello SDK chiama una funzione di too5 volte tooprocess un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="b34bd-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="b34bd-264">Se non riesce try quinto hello, messaggio hello è la coda non elaborabile spostato tooa.</span><span class="sxs-lookup"><span data-stu-id="b34bd-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="b34bd-265">[Hello il numero massimo di tentativi è configurabile](#config).</span><span class="sxs-lookup"><span data-stu-id="b34bd-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="b34bd-266">coda non elaborabile Hello è denominata *{originalqueuename}*-messaggi non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="b34bd-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="b34bd-267">È possibile scrivere messaggi tooprocess un funzione dalla coda non elaborabile hello registrarle o inviando una notifica che è necessario un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="b34bd-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="b34bd-268">In seguito hello esempio hello `CopyBlob` function ha esito negativo quando un messaggio nella coda contiene il nome di hello di un blob che non esiste.</span><span class="sxs-lookup"><span data-stu-id="b34bd-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="b34bd-269">In questo caso, il messaggio hello viene spostato dalla hello copyblobqueue toohello copyblobqueue poison coda.</span><span class="sxs-lookup"><span data-stu-id="b34bd-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="b34bd-270">Hello `ProcessPoisonMessage` quindi registri hello messaggi non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="b34bd-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

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

<span data-ttu-id="b34bd-271">Hello figura seguente Mostra output di console da queste funzioni durante l'elaborazione di un messaggio non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="b34bd-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Output di console per la gestione dei messaggi non elaborabili](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="b34bd-273">Gestione manuale dei messaggi non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b34bd-273">Manual poison message handling</span></span>
<span data-ttu-id="b34bd-274">È possibile ottenere un numero di volte in cui è stato selezionato un messaggio per l'elaborazione di hello aggiungendo un `int` parametro denominato `dequeueCount` tooyour funzione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="b34bd-275">È possibile quindi controllo hello numero nel codice della funzione di rimozione dalla coda ed eseguire la propria gestione di messaggio non elaborabile quando il numero di hello supera una soglia, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <span data-ttu-id="b34bd-276"><a id="config"></a>Come le opzioni di configurazione tooset</span><span class="sxs-lookup"><span data-stu-id="b34bd-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="b34bd-277">È possibile utilizzare hello `JobHostConfiguration` hello tooset tipo le opzioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="b34bd-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="b34bd-278">Impostare le stringhe di connessione SDK hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="b34bd-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="b34bd-279">Configurare le impostazioni di `QueueTrigger` , ad esempio il conteggio rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="b34bd-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="b34bd-280">Ottenere i nomi delle code dalla configurazione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="b34bd-281"><a id="setconnstr"></a>Impostare le stringhe di connessione SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="b34bd-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="b34bd-282">L'impostazione di stringhe di connessione SDK hello nel codice consente si toouse i propri nomi di stringa di connessione nel file di configurazione o le variabili di ambiente, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <span data-ttu-id="b34bd-283"><a id="configqueue"></a>Configurare le impostazioni di QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="b34bd-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="b34bd-284">È possibile configurare hello seguendo le impostazioni che si applicano toohello l'elaborazione del messaggio della coda:</span><span class="sxs-lookup"><span data-stu-id="b34bd-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="b34bd-285">numero massimo di messaggi in coda che vengono prelevati contemporaneamente toobe eseguite in parallelo Hello (valore predefinito è 16).</span><span class="sxs-lookup"><span data-stu-id="b34bd-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="b34bd-286">Hello numero massimo di tentativi prima che un messaggio nella coda venga inviato coda non elaborabile tooa (valore predefinito è 5).</span><span class="sxs-lookup"><span data-stu-id="b34bd-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="b34bd-287">tempo di attesa massimo Hello prima polling nuovamente quando una coda è vuota (valore predefinito è 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="b34bd-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="b34bd-288">Hello seguente esempio viene illustrato come tooconfigure queste impostazioni:</span><span class="sxs-lookup"><span data-stu-id="b34bd-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="b34bd-289"><a id="setnamesincode"></a>Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="b34bd-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="b34bd-290">Talvolta si desidera toospecify un nome di coda, un nome di blob o contenitore o una tabella di nome in codice anziché a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="b34bd-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="b34bd-291">Ad esempio, è consigliabile toospecify hello nome della coda `QueueTrigger` in una variabile di ambiente o i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="b34bd-292">È possibile farlo tramite il passaggio di un `NameResolver` oggetto toohello `JobHostConfiguration` tipo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="b34bd-293">Si includono segnaposto speciale racchiusi tra segni di percentuale (%) nei parametri di costruttore di attributo WebJobs SDK e `NameResolver` codice specifica toobe valori effettivi hello utilizzato al posto di questi segnaposto.</span><span class="sxs-lookup"><span data-stu-id="b34bd-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="b34bd-294">Ad esempio, si supponga che si desidera toouse una coda denominata logqueuetest nell'ambiente di test hello e uno denominato logqueueprod nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="b34bd-295">Anziché un nome di coda a livello di codice, si desidera nome hello toospecify di una voce in hello `appSettings` raccolta aventi il nome di coda effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="b34bd-296">Se hello `appSettings` chiave logqueue, la funzione potrebbe essere analogo al seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="b34bd-297">Il `NameResolver` classe quindi è stato possibile ottenere il nome della coda hello da `appSettings` come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="b34bd-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="b34bd-298">Si passa hello `NameResolver` classe toohello `JobHost` come mostrato nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="b34bd-299">**Nota:** coda, tabella e i nomi di blob vengono risolti ogni volta che viene chiamata una funzione, ma i nomi dei contenitori blob vengono risolti solo quando viene avviata un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="b34bd-300">È possibile modificare il nome di contenitore blob mentre è in esecuzione il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="b34bd-301"><a id="manual"></a>Come una funzione tootrigger manualmente</span><span class="sxs-lookup"><span data-stu-id="b34bd-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="b34bd-302">una funzione tootrigger manualmente, utilizzare hello `Call` o `CallAsync` metodo hello `JobHost` oggetto e hello `NoAutomaticTrigger` attributo funzione hello, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

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

## <span data-ttu-id="b34bd-303"><a id="logs"></a>Modalità di registrazione toowrite</span><span class="sxs-lookup"><span data-stu-id="b34bd-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="b34bd-304">Hello Dashboard Mostra i registri in due posizioni: la pagina hello per processo Web hello e hello per una chiamata a un particolare processo Web.</span><span class="sxs-lookup"><span data-stu-id="b34bd-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Log nella pagina del processo Web](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Log nella pagina di una chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="b34bd-307">Output dei metodi di Console che si chiama una funzione o hello `Main()` metodo verrà visualizzato nella pagina Dashboard hello per hello processo Web, non nella pagina hello per una chiamata di metodo specifico.</span><span class="sxs-lookup"><span data-stu-id="b34bd-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="b34bd-308">Verrà visualizzato l'output dall'oggetto TextWriter hello che si ottiene da un parametro nella firma del metodo nella pagina Dashboard hello per una chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="b34bd-309">Output della console non può essere chiamata al metodo particolare tooa collegato perché hello Console è a thread singolo, mentre molte funzioni di processo potrebbero essere in esecuzione hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="b34bd-310">Per tale motivo hello SDK fornisce a ogni chiamata di funzione con il proprio oggetto writer di log univoco.</span><span class="sxs-lookup"><span data-stu-id="b34bd-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="b34bd-311">toowrite [registri di traccia delle applicazioni](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilizzare `Console.Out` (Crea registri contrassegnati come INFO) e `Console.Error` (Crea log contrassegnato come errore).</span><span class="sxs-lookup"><span data-stu-id="b34bd-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="b34bd-312">In alternativa, è toouse [traccia o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), che fornisce Verbose, avviso, e i livelli di tooInfo aggiunta e di errore critico.</span><span class="sxs-lookup"><span data-stu-id="b34bd-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="b34bd-313">Registri di traccia delle applicazioni vengono visualizzati nel file di log di hello web app, le tabelle di Azure, o oggetti BLOB di Azure a seconda di come si configura l'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="b34bd-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="b34bd-314">Come nel caso di tutti gli output di Console, i registri applicazione 100 più recente di hello vengono inoltre visualizzati nella pagina Dashboard hello hello processo Web, la pagina di hello non per una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="b34bd-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="b34bd-315">Output della console viene visualizzato in hello Dashboard solo se il programma hello è in esecuzione in un processo Web di Azure, non se il programma hello viene eseguito localmente o in altri ambienti di rete.</span><span class="sxs-lookup"><span data-stu-id="b34bd-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="b34bd-316">Disabilitare la registrazione dei dashboard per scenari con velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="b34bd-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="b34bd-317">Per impostazione predefinita, hello SDK scrive i log toostorage e questa attività potrebbe influire negativamente sulle prestazioni quando si elaborano numerosi messaggi.</span><span class="sxs-lookup"><span data-stu-id="b34bd-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="b34bd-318">toodisable registrazione, impostare hello dashboard connessione stringa toonull come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b34bd-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="b34bd-319">Hello esempio seguente vengono illustrati vari modi toowrite log:</span><span class="sxs-lookup"><span data-stu-id="b34bd-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="b34bd-320">Nel Dashboard di processi Web SDK hello, hello output di hello `TextWriter` dell'oggetto viene visualizzato quando si passa toohello pagina per una particolare chiamata di funzione e fare clic su **attiva/disattiva Output**:</span><span class="sxs-lookup"><span data-stu-id="b34bd-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Fare clic sul collegamento della chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Log nella pagina di una chiamata di funzione](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="b34bd-323">Nel Dashboard di processi Web SDK hello, righe hello 100 più recente della Console l'output Mostra backup quando accede pagina toohello per hello processo Web (non per la chiamata di funzione hello) e fare clic su **attiva/disattiva Output**.</span><span class="sxs-lookup"><span data-stu-id="b34bd-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Fare clic su Toggle Output](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="b34bd-325">In un processo Web continuo, log applicazioni visualizzati nella/dati processi/continua/*{webjobname}*/job_log.txt nel file system di hello web app.</span><span class="sxs-lookup"><span data-stu-id="b34bd-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="b34bd-326">In un'applicazione hello blob di Azure registri simile al seguente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, errore, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="b34bd-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="b34bd-327">In un hello tabella Azure `Console.Out` e `Console.Error` registri è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b34bd-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Log delle informazioni nella tabella](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Log degli errori nella tabella](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="b34bd-330">Se si desidera tooplug un logger personalizzato, vedere [in questo esempio](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b34bd-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="b34bd-331"><a id="errors"></a>Modalità errori toohandle e configurare i timeout</span><span class="sxs-lookup"><span data-stu-id="b34bd-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="b34bd-332">Hello WebJobs SDK include anche un [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attributo che è possibile utilizzare toocause toobe una funzione annullata se non viene completato entro un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="b34bd-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="b34bd-333">E se si desidera tooraise un avviso quando verificati troppi errori si verificano all'interno di un periodo di tempo specificato, è possibile utilizzare hello `ErrorTrigger` attributo.</span><span class="sxs-lookup"><span data-stu-id="b34bd-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="b34bd-334">Ecco un [esempio ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="b34bd-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="b34bd-335">Anche in modo dinamico, è possibile disabilitare e abilitare le funzioni toocontrol se possono essere attivate, utilizzando un'opzione di configurazione che potrebbe essere un'impostazione di app o un nome di variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="b34bd-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="b34bd-336">Per esempio di codice, vedere hello `Disable` attributo [repository di esempi di hello WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="b34bd-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="b34bd-337"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b34bd-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="b34bd-338">Questa guida è fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di code di Azure.</span><span class="sxs-lookup"><span data-stu-id="b34bd-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="b34bd-339">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="b34bd-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
