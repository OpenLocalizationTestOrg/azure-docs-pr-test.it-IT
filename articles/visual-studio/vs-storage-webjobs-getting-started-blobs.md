---
title: Introduzione all'archiviazione BLOB e ai Servizi connessi di Visual Studio (progetti processo Web) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione di BLOB di Azure in un progetto WebJob dopo aver eseguito la connessione a un account di archiviazione di Azure con i servizi connessi di Visual Studio.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: a50a265feff8c0aec28825eb0bc4e33585ea5a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="b7284-103">Introduzione all'archiviazione BLOB di Azure e ai servizi relativi a Visual Studio (progetti WebJob)</span><span class="sxs-lookup"><span data-stu-id="b7284-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b7284-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b7284-104">Overview</span></span>
<span data-ttu-id="b7284-105">In questo articolo vengono forniti esempi di codice C# che illustrano come attivare un processo quando viene creato o aggiornato un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7284-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="b7284-106">Gli esempi di codice usano [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versione 1.x.</span><span class="sxs-lookup"><span data-stu-id="b7284-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="b7284-107">Quando si aggiunge un account di archiviazione a un progetto WebJob tramite la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio, viene installato il pacchetto NuGet di archiviazione di Azure appropriato, i riferimenti .NET appropriati vengono aggiunti al progetto e le stringhe di connessione per l'account di archiviazione vengono aggiornate nel file App.config.</span><span class="sxs-lookup"><span data-stu-id="b7284-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="b7284-108">Come attivare una funzione quando viene creato o aggiornato un BLOB</span><span class="sxs-lookup"><span data-stu-id="b7284-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="b7284-109">Questa sezione illustra come usare l'attributo **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="b7284-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="b7284-110">**Nota:** WebJobs SDK esegue la scansione dei file di log per verificare la presenza di BLOB nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="b7284-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="b7284-111">Questo processo è particolarmente lento: una funzione potrebbe non essere attivata per diversi minuti o più dopo la creazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="b7284-112">Se l'applicazione deve elaborare BLOB immediatamente, si consiglia di creare un messaggio nella coda quando si crea il BLOB e usare l'attributo [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) anziché l'attributo **BlobTrigger** sulla funzione che elabora il BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="b7284-113">Singolo segnaposto per il nome di BLOB con estensione</span><span class="sxs-lookup"><span data-stu-id="b7284-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="b7284-114">L'esempio di codice seguente copia i BLOB di testo del contenitore di *input* nel contenitore di *output*:</span><span class="sxs-lookup"><span data-stu-id="b7284-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="b7284-115">Il costruttore dell'attributo usa un parametro di stringa che specifica il nome del contenitore e un segnaposto per il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="b7284-116">In questo esempio, se viene creato un BLOB denominato *Blob1.txt* nel contenitore di *input*, la funzione crea un BLOB denominato *Blob1.txt* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="b7284-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="b7284-117">È possibile specificare un modello di nome con il segnaposto del nome del BLOB, come illustrato nel seguente esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="b7284-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="b7284-118">Questo codice copia solo BLOB con nomi che iniziano con "original-".</span><span class="sxs-lookup"><span data-stu-id="b7284-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="b7284-119">Ad esempio, *original-Blob1.txt* nel contenitore di *input* viene copiato in *copy-Blob1.txt* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="b7284-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="b7284-120">Se è necessario specificare un modello di nome per i nomi di BLOB con parentesi graffe nel nome, raddoppiare le parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="b7284-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="b7284-121">Se ad esempio si desidera trovare i BLOB nel contenitore *images* con nomi simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b7284-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="b7284-122">usare questa soluzione per il modello:</span><span class="sxs-lookup"><span data-stu-id="b7284-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="b7284-123">Nell'esempio il valore del segnaposto *name* sarebbe *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="b7284-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="b7284-124">Segnaposto di nome ed estensione di BLOB separati</span><span class="sxs-lookup"><span data-stu-id="b7284-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="b7284-125">L'esempio di codice seguente modifica l'estensione del file mentre copia i BLOB visualizzati nel contenitore di *input* nel contenitore di *output*.</span><span class="sxs-lookup"><span data-stu-id="b7284-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="b7284-126">Il codice registra l'estensione del BLOB di *input* e imposta l'estensione del BLOB di *output* su *.txt*.</span><span class="sxs-lookup"><span data-stu-id="b7284-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="b7284-127">Tipi che possono essere associati a BLOB</span><span class="sxs-lookup"><span data-stu-id="b7284-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="b7284-128">È possibile usare l'attributo **BlobTrigger** per i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7284-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="b7284-129">**string**</span><span class="sxs-lookup"><span data-stu-id="b7284-129">**string**</span></span>
* <span data-ttu-id="b7284-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="b7284-130">**TextReader**</span></span>
* <span data-ttu-id="b7284-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="b7284-131">**Stream**</span></span>
* <span data-ttu-id="b7284-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="b7284-132">**ICloudBlob**</span></span>
* <span data-ttu-id="b7284-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="b7284-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="b7284-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="b7284-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="b7284-135">Altri tipi deserializzati da [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="b7284-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="b7284-136">Se si desidera usare direttamente l'account di archiviazione di Azure, è anche possibile aggiungere un parametro **CloudStorageAccount** alla firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="b7284-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="b7284-137">Ottenere contenuto di BLOB di testo tramite associazione alla stringa</span><span class="sxs-lookup"><span data-stu-id="b7284-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="b7284-138">Se sono previsti BLOB di testo, è possibile applicare **BlobTrigger** a un parametro **stringa**.</span><span class="sxs-lookup"><span data-stu-id="b7284-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="b7284-139">L'esempio di codice seguente associa un BLOB di testo a un parametro **stringa** denominato **IogMessage**.</span><span class="sxs-lookup"><span data-stu-id="b7284-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="b7284-140">La funzione usa tale parametro per scrivere il contenuto del BLOB nel dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="b7284-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="b7284-141">Ottenere contenuto di BLOB serializzato tramite ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="b7284-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="b7284-142">L'esempio di codice seguente usa una classe che implementa **ICloudBlobStreamBinder** per consentire all'attributo **BlobTrigger** di associare un BLOB al tipo **WebImage**.</span><span class="sxs-lookup"><span data-stu-id="b7284-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

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

<span data-ttu-id="b7284-143">Il codice di associazione **WebImage** viene fornito in una classe **WebImageBinder** che deriva da **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="b7284-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="b7284-144">Come gestire i BLOB non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b7284-144">How to handle poison blobs</span></span>
<span data-ttu-id="b7284-145">Quando una funzione **BlobTrigger** ha esito negativo, l'SDK la chiama nuovamente in caso in cui il problema sia stato causato da un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="b7284-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="b7284-146">Se il problema è causato dal contenuto del BLOB, la funzione ha esito negativo ogni volta che tenta di elaborare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="b7284-147">Per impostazione predefinita, l'SDK chiama una funzione fino a cinque volte per un determinato BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="b7284-148">Se il quinto tentativo ha esito negativo, l'SDK aggiunge un messaggio a una coda denominata *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="b7284-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="b7284-149">Il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="b7284-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="b7284-150">La stessa impostazione [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) viene usata per la gestione dei BLOB non elaborabili e per la gestione dei messaggi della coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="b7284-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="b7284-151">Il messaggio di coda per i BLOB non elaborabili è un oggetto JSON che contiene le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="b7284-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="b7284-152">FunctionId (nel formato *{Nome processo Web}*.Functions.*{Nome funzione}*, ad esempio: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="b7284-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="b7284-153">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b7284-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b7284-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="b7284-154">ContainerName</span></span>
* <span data-ttu-id="b7284-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="b7284-155">BlobName</span></span>
* <span data-ttu-id="b7284-156">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b7284-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b7284-157">Nell'esempio di codice seguente la funzione **CopyBlob** contiene codice che ne determina l'esito negativo ogni volta che viene chiamata.</span><span class="sxs-lookup"><span data-stu-id="b7284-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="b7284-158">Dopo che l'SDK chiama la funzione per il numero massimo di tentativi, nella coda di BLOB non elaborabili viene creato un messaggio elaborato dalla funzione **LogPoisonBlob** .</span><span class="sxs-lookup"><span data-stu-id="b7284-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="b7284-159">L'SDK deserializza automaticamente il messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="b7284-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="b7284-160">Ecco la classe **PoisonBlobMessage** :</span><span class="sxs-lookup"><span data-stu-id="b7284-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="b7284-161">Algoritmo di polling di BLOB</span><span class="sxs-lookup"><span data-stu-id="b7284-161">Blob polling algorithm</span></span>
<span data-ttu-id="b7284-162">WebJobs SDK analizza tutti i contenitori specificati da attributi **BlobTrigger** all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7284-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="b7284-163">In un account di archiviazione di grandi dimensioni l'analisi può richiedere tempo, pertanto l'individuazione di nuovi BLOB e l'esecuzione delle funzioni **BlobTrigger** potrebbero non essere immediate.</span><span class="sxs-lookup"><span data-stu-id="b7284-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="b7284-164">Per rilevare BLOB nuovi o modificati dopo l'avvio dell'applicazione, l'SDK legge periodicamente i log di archiviazione dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="b7284-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="b7284-165">Tali log dei BLOB vengono inseriti nel buffer e vengono scritti fisicamente solo ogni 10 minuti circa, pertanto si può riscontrare un ritardo significativo tra la creazione o l'aggiornamento di un BLOB e l'esecuzione della funzione **BlobTrigger** corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b7284-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="b7284-166">Si verifica un'eccezione per i BLOB creati tramite l'attributo **Blob** .</span><span class="sxs-lookup"><span data-stu-id="b7284-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="b7284-167">Quando WebJobs SDK crea un nuovo BLOB, lo passa immediatamente a tutte le funzioni **BlobTrigger** corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="b7284-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="b7284-168">Se pertanto si dispone di una catena di input e output di BLOB, l'SDK può elaborarli in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="b7284-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="b7284-169">Se invece si desidera una bassa latenza per l'esecuzione delle funzioni di elaborazione dei BLOB creati o aggiornati in altri modi, è consigliabile usare **QueueTrigger** anziché **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="b7284-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="b7284-170">Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="b7284-170">Blob receipts</span></span>
<span data-ttu-id="b7284-171">WebJobs SDK verifica che nessuna funzione **BlobTrigger** venga chiamata più volte per lo stesso BLOB nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="b7284-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="b7284-172">A tale scopo, gestisce *conferme di BLOB* per determinare se una versione di BLOB specifica è stata elaborata.</span><span class="sxs-lookup"><span data-stu-id="b7284-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="b7284-173">Le conferme di BLOB vengono archiviate in un contenitore denominato *azure-webjobs-hosts* nell'account di archiviazione di Azure specificato dalla stringa di connessione AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="b7284-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="b7284-174">Una conferma di BLOB contiene le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="b7284-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="b7284-175">La funzione chiamata per il BLOB ("*{Nome processo Web}*.Functions.*{Nome funzione}*", ad esempio: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="b7284-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="b7284-176">Il nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="b7284-176">The container name</span></span>
* <span data-ttu-id="b7284-177">Il tipo di BLOB ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b7284-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b7284-178">Il nome del BLOB</span><span class="sxs-lookup"><span data-stu-id="b7284-178">The blob name</span></span>
* <span data-ttu-id="b7284-179">Il valore ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b7284-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b7284-180">Se si desidera forzare la rielaborazione di un BLOB, è possibile eliminare manualmente la conferma per tale BLOB dal contenitore *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="b7284-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="b7284-181">Argomenti correlati trattati dall'articolo sulle code</span><span class="sxs-lookup"><span data-stu-id="b7284-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="b7284-182">Per informazioni su come gestire l'elaborazione di BLOB attivata da un messaggio di coda o per scenari di WebJobs SDK non specifici dell'elaborazione di BLOB, vedere [Come usare il servizio di archiviazione di accodamento di Azure con WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b7284-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="b7284-183">Tra gli argomenti correlati trattati nell'articolo sono inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7284-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="b7284-184">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="b7284-184">Async functions</span></span>
* <span data-ttu-id="b7284-185">Più istanze</span><span class="sxs-lookup"><span data-stu-id="b7284-185">Multiple instances</span></span>
* <span data-ttu-id="b7284-186">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="b7284-186">Graceful shutdown</span></span>
* <span data-ttu-id="b7284-187">Usare gli attributi di WebJobs SDK nel corpo di una funzione</span><span class="sxs-lookup"><span data-stu-id="b7284-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="b7284-188">Impostare le stringhe di connessione SDK nel codice.</span><span class="sxs-lookup"><span data-stu-id="b7284-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="b7284-189">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="b7284-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="b7284-190">Configurare **MaxDequeueCount** per la gestione dei blob non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="b7284-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="b7284-191">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="b7284-191">Trigger a function manually</span></span>
* <span data-ttu-id="b7284-192">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="b7284-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7284-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7284-193">Next steps</span></span>
<span data-ttu-id="b7284-194">Questo articolo ha fornito esempi di codice che illustrano come gestire scenari comuni per l'uso di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7284-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="b7284-195">Per altre informazioni su come usare Processi Web di Azure e WebJobs SDK, vedere le [risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="b7284-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

