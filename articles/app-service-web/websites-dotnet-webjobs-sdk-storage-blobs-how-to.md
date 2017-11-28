---
title: Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK
description: Informazioni su come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK. Attivare un processo quando viene visualizzato un nuovo BLOB in un contenitore e gestire i BLOB non elaborabili.
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="4bd46-104">Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="4bd46-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="4bd46-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4bd46-105">Overview</span></span>
<span data-ttu-id="4bd46-106">In questa guida vengono forniti esempi di codice C# che illustrano come attivare un processo quando viene creato o aggiornato un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd46-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="4bd46-107">Gli esempi di codice usano [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="4bd46-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="4bd46-108">Per gli esempi di codice che illustrano come creare BLOB, vedere [Come usare il servizio di archiviazione di accodamento di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4bd46-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="4bd46-109">Nella guida si presuppone che si sappia come [creare un progetto processo Web in Visual Studio con stringhe di connessione che puntano all'account di archiviazione](websites-dotnet-webjobs-sdk-get-started.md) o a [più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="4bd46-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="4bd46-110"><a id="trigger"></a> Come attivare una funzione quando viene creato o aggiornato un BLOB</span><span class="sxs-lookup"><span data-stu-id="4bd46-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="4bd46-111">Questa sezione illustra come usare l'attributo `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="4bd46-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="4bd46-112">WebJobs SDK esegue la scansione dei file di log per verificare la presenza di BLOB nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="4bd46-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="4bd46-113">Questo processo non avviene in tempo reale. Una funzione potrebbe non essere attivata per diversi minuti o più dopo la creazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="4bd46-114">I [log di archiviazione vengono creati in base al principio del "massimo sforzo"](https://msdn.microsoft.com/library/azure/hh343262.aspx). Non è garantito che tutti gli eventi vengano acquisiti.</span><span class="sxs-lookup"><span data-stu-id="4bd46-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="4bd46-115">In alcune condizioni, l'acquisizione dei log potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="4bd46-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="4bd46-116">Se le limitazioni di velocità e affidabilità dei trigger dei BLOB non sono accettabili per l'applicazione, il metodo consigliato consiste nel creare un messaggio nella coda quando si crea il BLOB e usare l'attributo [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) invece dell'attributo `BlobTrigger` nella funzione che elabora il BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="4bd46-117">Singolo segnaposto per il nome di BLOB con estensione</span><span class="sxs-lookup"><span data-stu-id="4bd46-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="4bd46-118">L'esempio di codice seguente copia i BLOB di testo del contenitore di *input* nel contenitore di *output*:</span><span class="sxs-lookup"><span data-stu-id="4bd46-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4bd46-119">Il costruttore dell'attributo usa un parametro di stringa che specifica il nome del contenitore e un segnaposto per il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="4bd46-120">In questo esempio, se viene creato un BLOB denominato *Blob1.txt* nel contenitore di *input*, la funzione crea un BLOB denominato *Blob1.txt* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="4bd46-121">È possibile specificare un modello di nome con il segnaposto del nome del BLOB, come illustrato nel seguente esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="4bd46-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4bd46-122">Questo codice copia solo BLOB con nomi che iniziano con "original-".</span><span class="sxs-lookup"><span data-stu-id="4bd46-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="4bd46-123">Ad esempio, *original-Blob1.txt* nel contenitore di *input* viene copiato in *copy-Blob1.txt* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="4bd46-124">Se è necessario specificare un modello di nome per i nomi di BLOB con parentesi graffe nel nome, raddoppiare le parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="4bd46-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="4bd46-125">Se ad esempio si desidera trovare i BLOB nel contenitore *images* con nomi simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4bd46-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="4bd46-126">usare questa soluzione per il modello:</span><span class="sxs-lookup"><span data-stu-id="4bd46-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="4bd46-127">Nell'esempio il valore del segnaposto *name* sarebbe *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="4bd46-128">Segnaposto di nome ed estensione di BLOB separati</span><span class="sxs-lookup"><span data-stu-id="4bd46-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="4bd46-129">L'esempio di codice seguente modifica l'estensione del file mentre copia i BLOB visualizzati nel contenitore di *input* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="4bd46-130">Il codice registra l'estensione del BLOB di *input* e imposta l'estensione del BLOB di *output* su *.txt*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="4bd46-131"><a id="types"></a> Tipi che possono essere associati a BLOB</span><span class="sxs-lookup"><span data-stu-id="4bd46-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="4bd46-132">È possibile usare l'attributo `BlobTrigger` per i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4bd46-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="4bd46-133">Altri tipi deserializzati da [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="4bd46-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="4bd46-134">Se si desidera usare direttamente l'account di archiviazione di Azure, è anche possibile aggiungere un parametro `CloudStorageAccount` alla firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="4bd46-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="4bd46-135">Vedere ad esempio il [codice di binding dei BLOB nel repository webjobs-sdk in GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="4bd46-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="4bd46-136"><a id="string"></a> Ottenere contenuti di BLOB di testo tramite associazione alla stringa</span><span class="sxs-lookup"><span data-stu-id="4bd46-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="4bd46-137">Se sono previsti BLOB di testo, è possibile applicare `BlobTrigger` a un parametro `string`.</span><span class="sxs-lookup"><span data-stu-id="4bd46-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="4bd46-138">L'esempio di codice seguente associa un BLOB di testo a un parametro `string` denominato `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="4bd46-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="4bd46-139">La funzione usa tale parametro per scrivere il contenuto del BLOB nel dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="4bd46-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="4bd46-140"><a id="icbsb"></a> Ottenere contenuti di BLOB serializzati tramite ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="4bd46-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="4bd46-141">L'esempio di codice seguente usa una classe che implementa `ICloudBlobStreamBinder` per consentire all'attributo `BlobTrigger` di associare un BLOB al tipo `WebImage`.</span><span class="sxs-lookup"><span data-stu-id="4bd46-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="4bd46-142">Il codice di associazione `WebImage` viene fornito in una classe `WebImageBinder` che deriva da `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="4bd46-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="4bd46-143">Ottenere il percorso BLOB per il BLOB di attivazione</span><span class="sxs-lookup"><span data-stu-id="4bd46-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="4bd46-144">Per ottenere il nome del contenitore e il nome BLOB del BLOB che ha attivato la funzione, includere un parametro stringa `blobTrigger` nella firma della funzione.</span><span class="sxs-lookup"><span data-stu-id="4bd46-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="4bd46-145"><a id="poison"></a> Come gestire i BLOB non elaborabili</span><span class="sxs-lookup"><span data-stu-id="4bd46-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="4bd46-146">Quando una funzione `BlobTrigger` ha esito negativo, l'SDK la chiama nuovamente in caso in cui il problema sia stato causato da un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="4bd46-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="4bd46-147">Se il problema è causato dal contenuto del BLOB, la funzione ha esito negativo ogni volta che tenta di elaborare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="4bd46-148">Per impostazione predefinita, l'SDK chiama una funzione fino a cinque volte per un determinato BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="4bd46-149">Se il quinto tentativo ha esito negativo, l'SDK aggiunge un messaggio a una coda denominata *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="4bd46-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="4bd46-150">Il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="4bd46-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="4bd46-151">La stessa impostazione [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) viene usata per la gestione dei BLOB non elaborabili e per la gestione dei messaggi della coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="4bd46-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="4bd46-152">Il messaggio di coda per i BLOB non elaborabili è un oggetto JSON che contiene le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="4bd46-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="4bd46-153">FunctionId (nel formato *{Nome processo Web}*.Functions.*{Nome funzione}*, ad esempio: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="4bd46-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="4bd46-154">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4bd46-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4bd46-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="4bd46-155">ContainerName</span></span>
* <span data-ttu-id="4bd46-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="4bd46-156">BlobName</span></span>
* <span data-ttu-id="4bd46-157">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4bd46-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4bd46-158">Nell'esempio di codice seguente la funzione `CopyBlob` contiene codice che ne determina l'esito negativo ogni volta che viene chiamata.</span><span class="sxs-lookup"><span data-stu-id="4bd46-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="4bd46-159">Dopo che l'SDK chiama la funzione per il numero massimo di tentativi, nella coda di BLOB non elaborabili viene creato un messaggio elaborato dalla funzione `LogPoisonBlob` .</span><span class="sxs-lookup"><span data-stu-id="4bd46-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="4bd46-160">L'SDK deserializza automaticamente il messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="4bd46-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="4bd46-161">Questa è la classe `PoisonBlobMessage` :</span><span class="sxs-lookup"><span data-stu-id="4bd46-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="4bd46-162"><a id="polling"></a> Algoritmo di polling di BLOB</span><span class="sxs-lookup"><span data-stu-id="4bd46-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="4bd46-163">WebJobs SDK analizza tutti i contenitori specificati da attributi `BlobTrigger` all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4bd46-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="4bd46-164">In un account di archiviazione di grandi dimensioni l'analisi può richiedere tempo, pertanto l'individuazione di nuovi BLOB e l'esecuzione delle funzioni `BlobTrigger` potrebbero non essere immediate.</span><span class="sxs-lookup"><span data-stu-id="4bd46-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="4bd46-165">Per rilevare BLOB nuovi o modificati dopo l'avvio dell'applicazione, l'SDK legge periodicamente i log di archiviazione dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="4bd46-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="4bd46-166">Tali log vengono inseriti nel buffer e vengono scritti fisicamente solo ogni 10 minuti circa, pertanto si può riscontrare un ritardo significativo tra la creazione o l'aggiornamento di un BLOB e l'esecuzione della funzione `BlobTrigger` corrispondente.</span><span class="sxs-lookup"><span data-stu-id="4bd46-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="4bd46-167">Si verifica un'eccezione per i BLOB creati tramite l'attributo `Blob` .</span><span class="sxs-lookup"><span data-stu-id="4bd46-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="4bd46-168">Quando WebJobs SDK crea un nuovo BLOB, lo passa immediatamente a tutte le funzioni `BlobTrigger` corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="4bd46-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="4bd46-169">Se pertanto si dispone di una catena di input e output di BLOB, l'SDK può elaborarli in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="4bd46-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="4bd46-170">Se invece si desidera una bassa latenza per l'esecuzione delle funzioni di elaborazione dei BLOB creati o aggiornati in altri modi, è consigliabile usare `QueueTrigger` anziché `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="4bd46-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="4bd46-171"><a id="receipts"></a> Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="4bd46-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="4bd46-172">WebJobs SDK verifica che nessuna funzione `BlobTrigger` venga chiamata più volte per lo stesso BLOB nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="4bd46-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="4bd46-173">A tale scopo, gestisce *conferme di BLOB* per determinare se una versione di BLOB specifica è stata elaborata.</span><span class="sxs-lookup"><span data-stu-id="4bd46-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="4bd46-174">Le conferme di BLOB vengono archiviate in un contenitore denominato *azure-webjobs-hosts* nell'account di archiviazione di Azure specificato dalla stringa di connessione AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="4bd46-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="4bd46-175">Una conferma di BLOB contiene le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="4bd46-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="4bd46-176">La funzione chiamata per il BLOB ("*{Nome processo Web}*.Functions.*{Nome funzione}*", ad esempio: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="4bd46-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="4bd46-177">Il nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="4bd46-177">The container name</span></span>
* <span data-ttu-id="4bd46-178">Il tipo di BLOB ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4bd46-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4bd46-179">Il nome del BLOB</span><span class="sxs-lookup"><span data-stu-id="4bd46-179">The blob name</span></span>
* <span data-ttu-id="4bd46-180">Il valore ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4bd46-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4bd46-181">Se si desidera forzare la rielaborazione di un BLOB, è possibile eliminare manualmente la conferma per tale BLOB dal contenitore *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="4bd46-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="4bd46-182"><a id="queues"></a>Argomenti correlati trattati dall'articolo sulle code</span><span class="sxs-lookup"><span data-stu-id="4bd46-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="4bd46-183">Per informazioni su come gestire l'elaborazione di BLOB attivata da un messaggio di coda o per scenari di WebJobs SDK non specifici dell'elaborazione di BLOB, vedere [Come usare il servizio di archiviazione di accodamento di Azure con WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4bd46-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="4bd46-184">Tra gli argomenti correlati trattati nell'articolo sono inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4bd46-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="4bd46-185">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="4bd46-185">Async functions</span></span>
* <span data-ttu-id="4bd46-186">Più istanze</span><span class="sxs-lookup"><span data-stu-id="4bd46-186">Multiple instances</span></span>
* <span data-ttu-id="4bd46-187">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="4bd46-187">Graceful shutdown</span></span>
* <span data-ttu-id="4bd46-188">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="4bd46-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="4bd46-189">Impostare le stringhe di connessione SDK nel codice.</span><span class="sxs-lookup"><span data-stu-id="4bd46-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="4bd46-190">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="4bd46-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4bd46-191">Configurare `MaxDequeueCount` per la gestione di BLOB non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="4bd46-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="4bd46-192">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="4bd46-192">Trigger a function manually</span></span>
* <span data-ttu-id="4bd46-193">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="4bd46-193">Write logs</span></span>

## <span data-ttu-id="4bd46-194"><a id="nextsteps"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bd46-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="4bd46-195">Questa guida ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd46-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="4bd46-196">Per altre informazioni su come usare i processi Web di Azure e su WebJobs SDK, vedere le [risorse consigliate per i processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="4bd46-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

