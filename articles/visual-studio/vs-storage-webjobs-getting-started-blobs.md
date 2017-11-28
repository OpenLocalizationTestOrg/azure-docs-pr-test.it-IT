---
title: aaaGet generali di archiviazione blob e Visual Studio (progetti processi Web) di servizi connessi | Documenti Microsoft
description: "La modalità di avvio utilizzo dell'archiviazione Blob in un progetto processo Web dopo la connessione di archiviazione di Azure con Visual Studio tooan tooget servizi connessi."
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
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="9deb7-103">Introduzione all'archiviazione BLOB di Azure e ai servizi relativi a Visual Studio (progetti WebJob)</span><span class="sxs-lookup"><span data-stu-id="9deb7-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="9deb7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9deb7-104">Overview</span></span>
<span data-ttu-id="9deb7-105">Questo articolo fornisce c# degli esempi di codice che mostrano come tootrigger un processo quando un blob di Azure viene creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="9deb7-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="9deb7-106">esempi di codice Hello utilizzano hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versione 1. x.</span><span class="sxs-lookup"><span data-stu-id="9deb7-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="9deb7-107">Quando si aggiunge un progetto di processo Web tooa account di archiviazione usando Visual Studio hello **aggiungere servizi connessi** finestra di dialogo, è installato il pacchetto NuGet di archiviazione di Azure appropriato di hello e riferimenti .NET appropriati hello sono toohello aggiunto progetto e stringhe di connessione per l'account di archiviazione hello vengono aggiornate nel file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="9deb7-108">Come tootrigger una funzione quando un blob viene creato o aggiornato</span><span class="sxs-lookup"><span data-stu-id="9deb7-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="9deb7-109">Questa sezione viene illustrato come hello toouse **BlobTrigger** attributo.</span><span class="sxs-lookup"><span data-stu-id="9deb7-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="9deb7-110">**Nota:** hello WebJobs SDK toowatch file log di analisi per i BLOB nuovo o modificato.</span><span class="sxs-lookup"><span data-stu-id="9deb7-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="9deb7-111">Questo processo è intrinsecamente lento; una funzione potrebbe non viene generata finché diversi minuti o più dopo aver creato il blob hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="9deb7-112">Se l'applicazione deve BLOB tooprocess immediatamente, hello consigliato metodo è un messaggio nella coda toocreate quando si crea il blob hello e utilizza hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attributo anziché hello **BlobTrigger** attributo nella funzione hello che elabora i blob hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="9deb7-113">Singolo segnaposto per il nome di BLOB con estensione</span><span class="sxs-lookup"><span data-stu-id="9deb7-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="9deb7-114">Hello nell'esempio di codice seguente consente di copiare BLOB di testo che vengono visualizzati in hello *input* contenitore toohello *output* contenitore:</span><span class="sxs-lookup"><span data-stu-id="9deb7-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="9deb7-115">costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di contenitore hello e un segnaposto per il nome di blob hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="9deb7-116">In questo esempio, se un blob denominato *Blob1.txt* viene creato in hello *input* contenitore, la funzione hello crea un blob denominato *Blob1.txt* in hello *output*  contenitore.</span><span class="sxs-lookup"><span data-stu-id="9deb7-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="9deb7-117">È possibile specificare un modello di nome con segnaposto per nome blob hello, come illustrato nel seguente esempio di codice hello:</span><span class="sxs-lookup"><span data-stu-id="9deb7-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="9deb7-118">Questo codice copia solo BLOB con nomi che iniziano con "original-".</span><span class="sxs-lookup"><span data-stu-id="9deb7-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="9deb7-119">Ad esempio, *originale Blob1.txt* in hello *input* contenitore viene copiato troppo*copia Blob1.txt* in hello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="9deb7-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="9deb7-120">Se è necessario un modello di nome toospecify per i nomi di blob con parentesi graffe nel nome di hello, raddoppiare le parentesi graffe di hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="9deb7-121">Ad esempio, se si desidera BLOB toofind in hello *immagini* contenitore i cui nomi simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9deb7-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="9deb7-122">usare questa soluzione per il modello:</span><span class="sxs-lookup"><span data-stu-id="9deb7-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="9deb7-123">Nell'esempio hello hello *nome* il valore di segnaposto *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="9deb7-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="9deb7-124">Segnaposto di nome ed estensione di BLOB separati</span><span class="sxs-lookup"><span data-stu-id="9deb7-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="9deb7-125">Hello seguenti modifiche di esempio di codice hello estensione di file come copia di blob che vengono visualizzati in hello *input* contenitore toohello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="9deb7-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="9deb7-126">codice Hello Registra estensione hello di hello *input* blob e imposta l'estensione hello di hello *output* blob troppo*. txt*.</span><span class="sxs-lookup"><span data-stu-id="9deb7-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="9deb7-127">Tipi che è possibile associare tooblobs</span><span class="sxs-lookup"><span data-stu-id="9deb7-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="9deb7-128">È possibile utilizzare hello **BlobTrigger** attributo hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="9deb7-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="9deb7-129">**string**</span><span class="sxs-lookup"><span data-stu-id="9deb7-129">**string**</span></span>
* <span data-ttu-id="9deb7-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="9deb7-130">**TextReader**</span></span>
* <span data-ttu-id="9deb7-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="9deb7-131">**Stream**</span></span>
* <span data-ttu-id="9deb7-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="9deb7-132">**ICloudBlob**</span></span>
* <span data-ttu-id="9deb7-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="9deb7-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="9deb7-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="9deb7-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="9deb7-135">Altri tipi deserializzati da [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="9deb7-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="9deb7-136">Se si desidera toowork direttamente con hello account di archiviazione di Azure, è inoltre possibile aggiungere un **CloudStorageAccount** firma del metodo toohello parametro.</span><span class="sxs-lookup"><span data-stu-id="9deb7-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="9deb7-137">Recupero di contenuto di testo blob dall'associazione toostring</span><span class="sxs-lookup"><span data-stu-id="9deb7-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="9deb7-138">Se si prevede che il BLOB di testo, **BlobTrigger** può essere applicato tooa **stringa** parametro.</span><span class="sxs-lookup"><span data-stu-id="9deb7-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="9deb7-139">esempio di codice seguente Hello associa un tooa blob testo **stringa** parametro denominato **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="9deb7-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="9deb7-140">funzione Hello utilizza tale contenuto hello toowrite dei parametri di hello blob toohello dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="9deb7-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="9deb7-141">Ottenere contenuto di BLOB serializzato tramite ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="9deb7-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="9deb7-142">Hello nell'esempio di codice seguente viene utilizzata una classe che implementa **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind toohello un blob di attributo **WebImage** tipo.</span><span class="sxs-lookup"><span data-stu-id="9deb7-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="9deb7-143">Hello **WebImage** codice di associazione è disponibile in un **WebImageBinder** classe che deriva da **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="9deb7-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="9deb7-144">Come non elaborabili toohandle BLOB</span><span class="sxs-lookup"><span data-stu-id="9deb7-144">How toohandle poison blobs</span></span>
<span data-ttu-id="9deb7-145">Quando un **BlobTrigger** funzione ha esito negativo, hello SDK chiama nuovamente, in caso di errore hello è stato causato da un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="9deb7-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="9deb7-146">Se l'errore hello è causato da contenuto hello del blob hello, funzione hello ha esito negativo di ogni volta che tenta di blob hello tooprocess.</span><span class="sxs-lookup"><span data-stu-id="9deb7-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="9deb7-147">Per impostazione predefinita, hello SDK chiama una funzione i tempi di too5 per un blob specificato.</span><span class="sxs-lookup"><span data-stu-id="9deb7-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="9deb7-148">Se non riesce try quinto hello, hello SDK aggiunge una coda di messaggi tooa denominata *non elaborabili processi Web-blobtrigger*.</span><span class="sxs-lookup"><span data-stu-id="9deb7-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="9deb7-149">Hello il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="9deb7-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="9deb7-150">Hello stesso [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) impostazione viene utilizzata per la gestione di messaggi non elaborabili blob e la gestione dei messaggi di coda non elaborabile.</span><span class="sxs-lookup"><span data-stu-id="9deb7-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="9deb7-151">messaggio della coda Hello per i BLOB non elaborabile è un oggetto JSON contenente hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="9deb7-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="9deb7-152">FunctionId (in formato hello *{nome del processo Web}*. Funzioni. *{Nome della funzione}*, ad esempio: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="9deb7-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="9deb7-153">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="9deb7-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="9deb7-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="9deb7-154">ContainerName</span></span>
* <span data-ttu-id="9deb7-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="9deb7-155">BlobName</span></span>
* <span data-ttu-id="9deb7-156">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="9deb7-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="9deb7-157">In seguito hello esempio di codice, hello **CopyBlob** funzione dispone di codice che causa toofail ogni volta che viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="9deb7-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="9deb7-158">Dopo aver hello SDK chiama per il numero massimo di hello di tentativi, viene creato un messaggio nella coda di messaggi non elaborabili blob hello e che il messaggio viene elaborato da hello **LogPoisonBlob** (funzione).</span><span class="sxs-lookup"><span data-stu-id="9deb7-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="9deb7-159">Hello SDK deserializza automaticamente messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="9deb7-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="9deb7-160">Ecco hello **PoisonBlobMessage** classe:</span><span class="sxs-lookup"><span data-stu-id="9deb7-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="9deb7-161">Algoritmo di polling di BLOB</span><span class="sxs-lookup"><span data-stu-id="9deb7-161">Blob polling algorithm</span></span>
<span data-ttu-id="9deb7-162">Hello WebJobs SDK analizza tutti i contenitori specificati da **BlobTrigger** attributi all'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9deb7-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="9deb7-163">In un account di archiviazione di grandi dimensioni l'analisi può richiedere tempo, pertanto l'individuazione di nuovi BLOB e l'esecuzione delle funzioni **BlobTrigger** potrebbero non essere immediate.</span><span class="sxs-lookup"><span data-stu-id="9deb7-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="9deb7-164">toodetect BLOB nuove o modificate dopo l'avvio dell'applicazione, hello che SDK legge periodicamente dall'archiviazione blob hello Registra.</span><span class="sxs-lookup"><span data-stu-id="9deb7-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="9deb7-165">Hello blob vengono memorizzati nel buffer e registri solo ottengano scritta fisicamente ogni 10 minuti oppure in tal caso, pertanto potrebbero esserci un ritardo significativo dopo un blob viene creato o aggiornato prima hello corrispondente **BlobTrigger** funzione viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="9deb7-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="9deb7-166">Si verifica un'eccezione per i BLOB creati tramite hello **Blob** attributo.</span><span class="sxs-lookup"><span data-stu-id="9deb7-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="9deb7-167">Quando hello WebJobs SDK crea un nuovo blob, passa immediatamente nuovo blob hello corrispondenza tooany **BlobTrigger** funzioni.</span><span class="sxs-lookup"><span data-stu-id="9deb7-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="9deb7-168">Pertanto se si dispone di una catena di blob input e output, hello SDK possa elaborarli in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="9deb7-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="9deb7-169">Se invece si desidera una bassa latenza per l'esecuzione delle funzioni di elaborazione dei BLOB creati o aggiornati in altri modi, è consigliabile usare **QueueTrigger** anziché **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="9deb7-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="9deb7-170">Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="9deb7-170">Blob receipts</span></span>
<span data-ttu-id="9deb7-171">Hello WebJobs SDK garantisce che nessun **BlobTrigger** funzione viene chiamato più volte per hello stesso nuovo o aggiornato i blob.</span><span class="sxs-lookup"><span data-stu-id="9deb7-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="9deb7-172">Ciò avviene tramite la gestione di *blob conferme di recapito* in ordine toodetermine se è stata elaborata una versione di blob specificato.</span><span class="sxs-lookup"><span data-stu-id="9deb7-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="9deb7-173">BLOB conferme di recapito vengono archiviati in un contenitore denominato *ospita-processi Web di azure* nell'account di archiviazione Azure hello specificato dalla stringa di connessione AzureWebJobsStorage hello.</span><span class="sxs-lookup"><span data-stu-id="9deb7-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="9deb7-174">Un carico di blob è hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="9deb7-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="9deb7-175">funzione che è stato chiamato per blob hello Hello ("*{nome del processo Web}*. Funzioni. *{Nome della funzione}*", ad esempio:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="9deb7-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="9deb7-176">nome del contenitore Hello</span><span class="sxs-lookup"><span data-stu-id="9deb7-176">hello container name</span></span>
* <span data-ttu-id="9deb7-177">tipo di blob Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="9deb7-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="9deb7-178">nome del blob Hello</span><span class="sxs-lookup"><span data-stu-id="9deb7-178">hello blob name</span></span>
* <span data-ttu-id="9deb7-179">Hello ETag (un identificatore di versione del blob, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="9deb7-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="9deb7-180">Se si desidera tooforce rielaborazione di un blob, è possibile eliminare manualmente conferma di blob hello per tale blob da hello *ospita-processi Web di azure* contenitore.</span><span class="sxs-lookup"><span data-stu-id="9deb7-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="9deb7-181">Argomenti correlati cui all'articolo code hello</span><span class="sxs-lookup"><span data-stu-id="9deb7-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="9deb7-182">Per informazioni su come l'elaborazione di blob toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non tooblob specifico, l'elaborazione, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9deb7-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="9deb7-183">Argomenti trattati in tale articolo includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9deb7-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="9deb7-184">Funzioni asincrone</span><span class="sxs-lookup"><span data-stu-id="9deb7-184">Async functions</span></span>
* <span data-ttu-id="9deb7-185">Più istanze</span><span class="sxs-lookup"><span data-stu-id="9deb7-185">Multiple instances</span></span>
* <span data-ttu-id="9deb7-186">Arresto normale</span><span class="sxs-lookup"><span data-stu-id="9deb7-186">Graceful shutdown</span></span>
* <span data-ttu-id="9deb7-187">Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione</span><span class="sxs-lookup"><span data-stu-id="9deb7-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="9deb7-188">Impostare le stringhe di connessione SDK hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="9deb7-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="9deb7-189">Impostare i valori per i parametri del costruttore WebJobs SDK nel codice</span><span class="sxs-lookup"><span data-stu-id="9deb7-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="9deb7-190">Configurare **MaxDequeueCount** per la gestione dei blob non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="9deb7-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="9deb7-191">Attivare manualmente una funzione</span><span class="sxs-lookup"><span data-stu-id="9deb7-191">Trigger a function manually</span></span>
* <span data-ttu-id="9deb7-192">Scrivere i log</span><span class="sxs-lookup"><span data-stu-id="9deb7-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="9deb7-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9deb7-193">Next steps</span></span>
<span data-ttu-id="9deb7-194">Questo articolo sono presenti esempi di codice che mostrano come toohandle scenari comuni per l'utilizzo con Azure BLOB.</span><span class="sxs-lookup"><span data-stu-id="9deb7-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="9deb7-195">Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse della documentazione di processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="9deb7-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

