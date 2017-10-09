---
title: aaaHow toouse archiviazione blob di Azure con hello WebJobs SDK
description: Informazioni su come toouse Azure blob storage con hello WebJobs SDK. Attivare un processo quando viene visualizzato un nuovo BLOB in un contenitore e gestire i BLOB non elaborabili.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="0f366-104">La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="0f366-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="0f366-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0f366-105">Overview</span></span>
<span data-ttu-id="0f366-106">Questa guida fornisce c# degli esempi di codice che mostrano come tootrigger un processo quando un blob di Azure viene creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="0f366-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="0f366-107">utilizzo di esempi di codice Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.</span><span class="sxs-lookup"><span data-stu-id="0f366-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="0f366-108">Per esempi di codice che mostrano come toocreate BLOB, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="0f366-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="0f366-109">Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o troppo[più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="0f366-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="0f366-110"><a id="trigger"></a>Come tootrigger una funzione quando un blob viene creato o aggiornato</span><span class="sxs-lookup"><span data-stu-id="0f366-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="0f366-111">Questa sezione viene illustrato come hello toouse `BlobTrigger` attributo.</span><span class="sxs-lookup"><span data-stu-id="0f366-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f366-112">Hello WebJobs SDK toowatch file log di analisi per i BLOB nuovo o modificato.</span><span class="sxs-lookup"><span data-stu-id="0f366-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="0f366-113">Questo processo non è in tempo reale; una funzione potrebbe non viene generata finché diversi minuti o più dopo aver creato il blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f366-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="0f366-114">I [log di archiviazione vengono creati in base al principio del "massimo sforzo"](https://msdn.microsoft.com/library/azure/hh343262.aspx). Non è garantito che tutti gli eventi vengano acquisiti.</span><span class="sxs-lookup"><span data-stu-id="0f366-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="0f366-115">In alcune condizioni, l'acquisizione dei log potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="0f366-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="0f366-116">Se i limiti di velocità e affidabilità hello dei trigger di blob non sono accettabili per l'applicazione, hello consigliato metodo è un messaggio nella coda toocreate quando si crea il blob hello e utilizza hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attributo invece di Hello `BlobTrigger` attributo nella funzione hello che elabora i blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f366-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="0f366-117">Singolo segnaposto per il nome di BLOB con estensione</span><span class="sxs-lookup"><span data-stu-id="0f366-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="0f366-118">Hello nell'esempio di codice seguente consente di copiare BLOB di testo che vengono visualizzati in hello *input* contenitore toohello *output* contenitore:</span><span class="sxs-lookup"><span data-stu-id="0f366-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="0f366-119">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di contenitore hello e un segnaposto per il nome di blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f366-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="0f366-120">In questo esempio, se un blob denominato *Blob1.txt* viene creato in hello *input* contenitore, la funzione hello crea un blob denominato *Blob1.txt* in hello *output*  contenitore.</span><span class="sxs-lookup"><span data-stu-id="0f366-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="0f366-121">È possibile specificare un modello di nome con segnaposto per nome blob hello, come illustrato nel seguente esempio di codice hello:</span><span class="sxs-lookup"><span data-stu-id="0f366-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="0f366-122">Questo codice copia solo BLOB con nomi che iniziano con "original-".</span><span class="sxs-lookup"><span data-stu-id="0f366-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="0f366-123">Ad esempio, *originale Blob1.txt* in hello *input* contenitore viene copiato troppo*copia Blob1.txt* in hello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="0f366-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="0f366-124">Se è necessario un modello di nome toospecify per i nomi di blob con parentesi graffe nel nome di hello, raddoppiare le parentesi graffe di hello.</span><span class="sxs-lookup"><span data-stu-id="0f366-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="0f366-125">Ad esempio, se si desidera BLOB toofind in hello *immagini* contenitore i cui nomi simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0f366-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="0f366-126">usare questa soluzione per il modello:</span><span class="sxs-lookup"><span data-stu-id="0f366-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="0f366-127">Nell'esempio hello hello *nome* il valore di segnaposto *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="0f366-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="0f366-128">Segnaposto di nome ed estensione di BLOB separati</span><span class="sxs-lookup"><span data-stu-id="0f366-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="0f366-129">Hello seguenti modifiche di esempio di codice hello estensione di file come copia di blob che vengono visualizzati in hello *input* contenitore toohello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="0f366-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="0f366-130">codice Hello Registra estensione hello di hello *input* blob e imposta l'estensione hello di hello *output* blob troppo*. txt*.</span><span class="sxs-lookup"><span data-stu-id="0f366-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="0f366-131"><a id="types"></a>Tipi che è possibile associare tooblobs</span><span class="sxs-lookup"><span data-stu-id="0f366-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="0f366-132">È possibile utilizzare hello `BlobTrigger` attributo hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="0f366-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="0f366-133">Altri tipi deserializzati da [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="0f366-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="0f366-134">Se si desidera toowork direttamente con hello account di archiviazione di Azure, è inoltre possibile aggiungere un `CloudStorageAccount` firma del metodo toohello parametro.</span><span class="sxs-lookup"><span data-stu-id="0f366-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="0f366-135">Per esempi, vedere hello [blob codice di associazione nel repository di azure-sdk-processi Web hello in GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="0f366-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="0f366-136"><a id="string"></a>Recupero di contenuto di testo blob dall'associazione toostring</span><span class="sxs-lookup"><span data-stu-id="0f366-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="0f366-137">Se si prevede che il BLOB di testo, `BlobTrigger` può essere applicato tooa `string` parametro.</span><span class="sxs-lookup"><span data-stu-id="0f366-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="0f366-138">esempio di codice seguente Hello associa un tooa blob testo `string` parametro denominato `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="0f366-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="0f366-139">funzione Hello utilizza tale contenuto hello toowrite dei parametri di hello blob toohello dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="0f366-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="0f366-140"><a id="icbsb"></a> Ottenere contenuti di BLOB serializzati tramite ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="0f366-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="0f366-141">Hello nell'esempio di codice seguente viene utilizzata una classe che implementa `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind toohello un blob di attributo `WebImage` tipo.</span><span class="sxs-lookup"><span data-stu-id="0f366-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="0f366-142">Hello `WebImage` codice di associazione è disponibile in un `WebImageBinder` classe che deriva da `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="0f366-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="0f366-143">Recupero di percorso blob hello per hello attivazione blob</span><span class="sxs-lookup"><span data-stu-id="0f366-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="0f366-144">nome del contenitore tooget hello e nome del blob del blob hello che ha attivato la funzione hello, includere un `blobTrigger` parametro nella firma della funzione hello di stringa.</span><span class="sxs-lookup"><span data-stu-id="0f366-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="0f366-145"><a id="poison"></a>Come non elaborabili toohandle BLOB</span><span class="sxs-lookup"><span data-stu-id="0f366-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="0f366-146">Quando un `BlobTrigger` funzione ha esito negativo, hello SDK chiama nuovamente, in caso di errore hello è stato causato da un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="0f366-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="0f366-147">Se l'errore hello è causato da contenuto hello del blob hello, funzione hello ha esito negativo di ogni volta che tenta di blob hello tooprocess.</span><span class="sxs-lookup"><span data-stu-id="0f366-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="0f366-148">Per impostazione predefinita, hello SDK chiama una funzione i tempi di too5 per un blob specificato.</span><span class="sxs-lookup"><span data-stu-id="0f366-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="0f366-149">Se non riesce try quinto hello, hello SDK aggiunge una coda di messaggi tooa denominata *non elaborabili processi Web-blobtrigger*.</span><span class="sxs-lookup"><span data-stu-id="0f366-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="0f366-150">Hello il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="0f366-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="0f366-151">Hello stesso [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) impostazione viene utilizzata per la gestione di messaggi non elaborabili blob e la gestione dei messaggi di coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="0f366-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="0f366-152">messaggio della coda Hello per i BLOB non elaborabile è un oggetto JSON contenente hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f366-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="0f366-153">FunctionId (in formato hello *{nome del processo Web}*. Funzioni. *{Nome della funzione}*, ad esempio: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="0f366-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="0f366-154">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="0f366-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="0f366-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="0f366-155">ContainerName</span></span>
* <span data-ttu-id="0f366-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="0f366-156">BlobName</span></span>
* <span data-ttu-id="0f366-157">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="0f366-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="0f366-158">In seguito hello esempio di codice, hello `CopyBlob` funzione dispone di codice che causa toofail ogni volta che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="0f366-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="0f366-159">Dopo aver hello SDK chiama per il numero massimo di hello di tentativi, viene creato un messaggio nella coda di messaggi non elaborabili blob hello e che il messaggio viene elaborato da hello `LogPoisonBlob` (funzione).</span><span class="sxs-lookup"><span data-stu-id="0f366-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="0f366-160">Hello SDK deserializza automaticamente messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="0f366-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="0f366-161">Ecco hello `PoisonBlobMessage` classe:</span><span class="sxs-lookup"><span data-stu-id="0f366-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="0f366-162"><a id="polling"></a> Algoritmo di polling di BLOB</span><span class="sxs-lookup"><span data-stu-id="0f366-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="0f366-163">Hello WebJobs SDK analizza tutti i contenitori specificati da `BlobTrigger` attributi all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0f366-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="0f366-164">In un account di archiviazione di grandi dimensioni l'analisi può richiedere tempo, pertanto l'individuazione di nuovi BLOB e l'esecuzione delle funzioni `BlobTrigger` potrebbero non essere immediate.</span><span class="sxs-lookup"><span data-stu-id="0f366-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="0f366-165">toodetect BLOB nuove o modificate dopo l'avvio dell'applicazione, hello che SDK legge periodicamente dall'archiviazione blob hello Registra.</span><span class="sxs-lookup"><span data-stu-id="0f366-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="0f366-166">Hello blob vengono memorizzati nel buffer e registri solo ottengano scritta fisicamente ogni 10 minuti oppure in tal caso, pertanto potrebbero esserci un ritardo significativo dopo un blob viene creato o aggiornato prima hello corrispondente `BlobTrigger` funzione viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="0f366-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="0f366-167">Si verifica un'eccezione per i BLOB creati tramite hello `Blob` attributo.</span><span class="sxs-lookup"><span data-stu-id="0f366-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="0f366-168">Quando hello WebJobs SDK crea un nuovo blob, passa immediatamente nuovo blob hello tooany corrispondenza `BlobTrigger` funzioni.</span><span class="sxs-lookup"><span data-stu-id="0f366-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="0f366-169">Pertanto se si dispone di una catena di blob input e output, hello SDK possa elaborarli in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="0f366-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="0f366-170">Se invece si desidera una bassa latenza per l'esecuzione delle funzioni di elaborazione dei BLOB creati o aggiornati in altri modi, è consigliabile usare `QueueTrigger` anziché `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="0f366-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="0f366-171"><a id="receipts"></a> Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="0f366-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="0f366-172">Hello WebJobs SDK garantisce che nessun `BlobTrigger` funzione viene chiamato più volte per hello stesso nuovo o aggiornato i blob.</span><span class="sxs-lookup"><span data-stu-id="0f366-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="0f366-173">Ciò avviene tramite la gestione di *blob conferme di recapito* in ordine toodetermine se è stata elaborata una versione di blob specificato.</span><span class="sxs-lookup"><span data-stu-id="0f366-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="0f366-174">BLOB conferme di recapito vengono archiviati in un contenitore denominato *ospita-processi Web di azure* nell'account di archiviazione Azure hello specificato dalla stringa di connessione AzureWebJobsStorage hello.</span><span class="sxs-lookup"><span data-stu-id="0f366-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="0f366-175">Un carico di blob è hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="0f366-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="0f366-176">funzione che è stato chiamato per blob hello Hello ("*{nome del processo Web}*. Funzioni. *{Nome della funzione}*", ad esempio:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="0f366-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="0f366-177">nome del contenitore Hello</span><span class="sxs-lookup"><span data-stu-id="0f366-177">hello container name</span></span>
* <span data-ttu-id="0f366-178">tipo di blob Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="0f366-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="0f366-179">nome del blob Hello</span><span class="sxs-lookup"><span data-stu-id="0f366-179">hello blob name</span></span>
* <span data-ttu-id="0f366-180">Hello ETag (un identificatore di versione del blob, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="0f366-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="0f366-181">Se si desidera tooforce rielaborazione di un blob, è possibile eliminare manualmente conferma di blob hello per tale blob da hello *ospita-processi Web di azure* contenitore.</span><span class="sxs-lookup"><span data-stu-id="0f366-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="0f366-182"><a id="queues"></a>Argomenti correlati cui all'articolo code hello</span><span class="sxs-lookup"><span data-stu-id="0f366-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="0f366-183">Per informazioni su come l'elaborazione di blob toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non tooblob specifico, l'elaborazione, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="0f366-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="0f366-184">Argomenti trattati in tale articolo includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f366-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="0f366-185">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="0f366-185">Async functions</span></span>
* <span data-ttu-id="0f366-186">Più istanze</span><span class="sxs-lookup"><span data-stu-id="0f366-186">Multiple instances</span></span>
* <span data-ttu-id="0f366-187">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="0f366-187">Graceful shutdown</span></span>
* <span data-ttu-id="0f366-188">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="0f366-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="0f366-189">Impostare le stringhe di connessione SDK hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="0f366-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="0f366-190">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="0f366-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="0f366-191">Configurare `MaxDequeueCount` per la gestione di BLOB non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="0f366-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="0f366-192">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="0f366-192">Trigger a function manually</span></span>
* <span data-ttu-id="0f366-193">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="0f366-193">Write logs</span></span>

## <span data-ttu-id="0f366-194"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f366-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="0f366-195">Questa guida fornisce esempi di codice che mostrano come toohandle scenari comuni per l'utilizzo con Azure BLOB.</span><span class="sxs-lookup"><span data-stu-id="0f366-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="0f366-196">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="0f366-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

