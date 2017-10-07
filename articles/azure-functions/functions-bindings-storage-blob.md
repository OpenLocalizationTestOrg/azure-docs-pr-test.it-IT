---
title: associazioni di funzioni di archiviazione Blob aaaAzure | Documenti Microsoft
description: Comprendere come toouse di archiviazione di Azure attiva e le associazioni in funzioni di Azure.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="940ca-104">Binding dell'archiviazione BLOB di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="940ca-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="940ca-105">Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di archiviazione Blob di Azure in funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="940ca-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="940ca-106">Funzioni di Azure supporta i trigger e le associazioni di input e di output per l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="940ca-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="940ca-107">Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="940ca-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="940ca-108">Non sono supportati [account di archiviazione solo BLOB](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="940ca-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="940ca-109">I trigger e le associazioni di archiviazione BLOB richiedono un account di archiviazione generico.</span><span class="sxs-lookup"><span data-stu-id="940ca-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="940ca-110">Trigger e associazioni do archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="940ca-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="940ca-111">Utilizzo di trigger di archiviazione Blob di Azure hello, il codice della funzione viene chiamato quando viene rilevato un blob nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="940ca-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="940ca-112">contenuto del blob Hello viene forniti come input toohello funzione.</span><span class="sxs-lookup"><span data-stu-id="940ca-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="940ca-113">Definire un trigger di archiviazione blob utilizzando hello **integrazione** scheda nel portale le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="940ca-114">portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:</span><span class="sxs-lookup"><span data-stu-id="940ca-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="940ca-115">BLOB di input e output associazioni vengono definite utilizzando `blob` come tipo di associazione hello:</span><span class="sxs-lookup"><span data-stu-id="940ca-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="940ca-116">Hello `path` proprietà supporta l'associazione di espressioni e parametri di filtro.</span><span class="sxs-lookup"><span data-stu-id="940ca-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="940ca-117">Vedere [Modelli di nome](#pattern).</span><span class="sxs-lookup"><span data-stu-id="940ca-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="940ca-118">Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="940ca-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="940ca-119">Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="940ca-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="940ca-120">Quando si utilizza un trigger di blob in un piano di utilizzo, in può essere presente di ritardo di 10 minuti tooa l'elaborazione di nuovi BLOB dopo che un'app di funzione è diventato inattiva.</span><span class="sxs-lookup"><span data-stu-id="940ca-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="940ca-121">Dopo l'applicazione di funzione hello è in esecuzione, i BLOB vengono elaborati immediatamente.</span><span class="sxs-lookup"><span data-stu-id="940ca-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="940ca-122">tooavoid iniziale di questo ritardo, considerare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="940ca-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="940ca-123">Usare un piano di servizio app con l'opzione Always On abilitata.</span><span class="sxs-lookup"><span data-stu-id="940ca-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="940ca-124">Utilizzare un altro blob di hello tootrigger meccanismo di elaborazione, ad esempio un messaggio nella coda che contiene il nome di blob hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="940ca-125">Per un esempio, vedere il [Queue trigger with blob input binding](#input-sample) (Trigger della coda con associazione di input del BLOB).</span><span class="sxs-lookup"><span data-stu-id="940ca-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="940ca-126">Modelli di nome</span><span class="sxs-lookup"><span data-stu-id="940ca-126">Name patterns</span></span>
<span data-ttu-id="940ca-127">È possibile specificare un modello di nome di blob in hello `path` proprietà, che può essere un'espressione di filtro o di associazione.</span><span class="sxs-lookup"><span data-stu-id="940ca-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="940ca-128">Vedere [Modelli ed espressioni di associazione](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="940ca-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="940ca-129">Tooblobs toofilter che iniziano con una stringa hello "originale", ad esempio, utilizzare hello seguente definizione.</span><span class="sxs-lookup"><span data-stu-id="940ca-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="940ca-130">Questo percorso consente di individuare un blob denominato *originale Blob1.txt* in hello *input* contenitore e il valore di hello di hello `name` variabile nel codice della funzione è `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="940ca-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="940ca-131">estensione e il nome di file blob toohello toobind separatamente, usare due modelli.</span><span class="sxs-lookup"><span data-stu-id="940ca-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="940ca-132">Questo percorso consente anche di trovare un blob denominato *originale Blob1.txt*e il valore di hello di hello `blobname` e `blobextension` variabili nel codice della funzione vengono *originale Blob1* e *txt*.</span><span class="sxs-lookup"><span data-stu-id="940ca-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="940ca-133">È possibile limitare il tipo di file hello del BLOB utilizzando un valore fisso per l'estensione del file hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="940ca-134">Ad esempio, tootrigger solo per i file con estensione png, utilizzare hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="940ca-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="940ca-135">Le parentesi graffe sono caratteri speciali nei modelli di nome.</span><span class="sxs-lookup"><span data-stu-id="940ca-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="940ca-136">i nomi di blob toospecify con parentesi graffe nel nome di hello, fare in modo che le parentesi graffe hello utilizzando due parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="940ca-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="940ca-137">esempio Hello trova un blob denominato *{20140101}-soundfile.mp3* in hello *immagini* contenitore e hello `name` valore della variabile nel codice della funzione hello è  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="940ca-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="940ca-138">Metadati del trigger</span><span class="sxs-lookup"><span data-stu-id="940ca-138">Trigger metadata</span></span>

<span data-ttu-id="940ca-139">i trigger di blob Hello fornisce diverse proprietà di metadati.</span><span class="sxs-lookup"><span data-stu-id="940ca-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="940ca-140">Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice.</span><span class="sxs-lookup"><span data-stu-id="940ca-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="940ca-141">Questi valori hanno hello stessa semantica [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="940ca-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="940ca-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="940ca-142">**BlobTrigger**.</span></span> <span data-ttu-id="940ca-143">Digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="940ca-143">Type `string`.</span></span> <span data-ttu-id="940ca-144">percorso blob attivazione Hello</span><span class="sxs-lookup"><span data-stu-id="940ca-144">hello triggering blob path</span></span>
- <span data-ttu-id="940ca-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="940ca-145">**Uri**.</span></span> <span data-ttu-id="940ca-146">Digitare `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="940ca-146">Type `System.Uri`.</span></span> <span data-ttu-id="940ca-147">URI del blob Hello posizione primaria hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="940ca-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="940ca-148">**Properties**.</span></span> <span data-ttu-id="940ca-149">Digitare `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="940ca-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="940ca-150">salve le proprietà di sistema del blob.</span><span class="sxs-lookup"><span data-stu-id="940ca-150">hello blob's system properties.</span></span>
- <span data-ttu-id="940ca-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="940ca-151">**Metadata**.</span></span> <span data-ttu-id="940ca-152">Digitare `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="940ca-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="940ca-153">Hello metadati definiti dall'utente per il blob hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="940ca-154">Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="940ca-154">Blob receipts</span></span>
<span data-ttu-id="940ca-155">Funzioni di Azure Hello runtime garantisce che nessuna funzione trigger blob viene chiamata più volte per hello nello stesso blob nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="940ca-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="940ca-156">toodetermine se è stata elaborata una versione di blob specificato, viene mantenuta *blob conferme di recapito*.</span><span class="sxs-lookup"><span data-stu-id="940ca-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="940ca-157">Blob di Azure archivi funzioni conferme di recapito in un contenitore denominato *ospita-processi Web di azure* nell'account di archiviazione di Azure per l'app di funzione hello (definito dall'impostazione di app hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="940ca-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="940ca-158">Un carico di blob è hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="940ca-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="940ca-159">Hello attivato funzione ("*&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*", ad esempio:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="940ca-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="940ca-160">nome del contenitore Hello</span><span class="sxs-lookup"><span data-stu-id="940ca-160">hello container name</span></span>
* <span data-ttu-id="940ca-161">tipo di blob Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="940ca-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="940ca-162">nome del blob Hello</span><span class="sxs-lookup"><span data-stu-id="940ca-162">hello blob name</span></span>
* <span data-ttu-id="940ca-163">Hello ETag (un identificatore di versione del blob, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="940ca-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="940ca-164">conferma di blob hello per tale blob tooforce rielaborazione di un blob, eliminare hello *ospita-processi Web di azure* contenitore manualmente.</span><span class="sxs-lookup"><span data-stu-id="940ca-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="940ca-165">Gestione di BLOB non elaborabili</span><span class="sxs-lookup"><span data-stu-id="940ca-165">Handling poison blobs</span></span>
<span data-ttu-id="940ca-166">Se una funzione di trigger del BLOB ha esito negativo per un determinato BLOB, per impostazione predefinita Funzioni di Azure ritenta l'esecuzione fino a 5 volte.</span><span class="sxs-lookup"><span data-stu-id="940ca-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="940ca-167">Se non tutti i tentativi di 5, le funzioni di Azure consente di aggiungere una coda di archiviazione tooa messaggio denominata *non elaborabili processi Web-blobtrigger*.</span><span class="sxs-lookup"><span data-stu-id="940ca-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="940ca-168">messaggio della coda Hello per i BLOB non elaborabile è un oggetto JSON contenente hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="940ca-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="940ca-169">FunctionId (in formato hello  *&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*)</span><span class="sxs-lookup"><span data-stu-id="940ca-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="940ca-170">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="940ca-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="940ca-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="940ca-171">ContainerName</span></span>
* <span data-ttu-id="940ca-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="940ca-172">BlobName</span></span>
* <span data-ttu-id="940ca-173">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="940ca-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="940ca-174">Polling dei BLOB per contenitori di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="940ca-174">Blob polling for large containers</span></span>
<span data-ttu-id="940ca-175">Se il contenitore di blob hello monitorato contiene più di 10.000 BLOB, hello toowatch funzioni runtime analisi log file per i BLOB nuovo o modificato.</span><span class="sxs-lookup"><span data-stu-id="940ca-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="940ca-176">Questo processo non avviene in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="940ca-176">This process is not real time.</span></span> <span data-ttu-id="940ca-177">Una funzione potrebbe non viene generata finché diversi minuti o più dopo aver creato il blob hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="940ca-178">Per di più [i log di archiviazione vengono creati in base al principio del "massimo sforzo"](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="940ca-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="940ca-179">Non è garantito che tutti gli eventi vengano acquisiti.</span><span class="sxs-lookup"><span data-stu-id="940ca-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="940ca-180">In alcune condizioni, l'acquisizione dei log può non riuscire.</span><span class="sxs-lookup"><span data-stu-id="940ca-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="940ca-181">Se è necessaria un'elaborazione di blob più veloce o più affidabile, è consigliabile creare un [messaggio della coda](../storage/queues/storage-dotnet-how-to-use-queues.md) quando si crea il blob hello.</span><span class="sxs-lookup"><span data-stu-id="940ca-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="940ca-182">Quindi, usare un [trigger coda](functions-bindings-storage-queue.md) invece di un blob di hello tooprocess trigger blob.</span><span class="sxs-lookup"><span data-stu-id="940ca-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="940ca-183">Uso di un trigger di BLOB e dell'associazione di input</span><span class="sxs-lookup"><span data-stu-id="940ca-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="940ca-184">Nelle funzioni .NET, accedere ai dati di blob hello utilizzando un parametro di metodo, ad esempio `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="940ca-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="940ca-185">In questo caso, `paramName` hello valore specificato in hello [configurazione trigger](#trigger).</span><span class="sxs-lookup"><span data-stu-id="940ca-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="940ca-186">Nelle funzioni di Node.js, hello accesso input di dati blob utilizzando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="940ca-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="940ca-187">In .NET, è possibile associare tooany dei tipi di hello in hello in basso.</span><span class="sxs-lookup"><span data-stu-id="940ca-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="940ca-188">Se usati come associazione di input, alcuni di questi tipi richiedono una direzione di associazione `inout` in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="940ca-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="940ca-189">Questa direzione non è supportata dall'editor standard hello, pertanto è necessario utilizzare hello editor avanzato.</span><span class="sxs-lookup"><span data-stu-id="940ca-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="940ca-190">`ICloudBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="940ca-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="940ca-191">`CloudBlockBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="940ca-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="940ca-192">`CloudPageBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="940ca-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="940ca-193">`CloudAppendBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="940ca-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="940ca-194">Se si prevede che il BLOB di testo, è anche possibile associare .NET tooa `string` tipo.</span><span class="sxs-lookup"><span data-stu-id="940ca-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="940ca-195">È consigliato solo se dimensioni blob hello sono ridotto, in quanto hello intero contenuto del blob viene caricati in memoria.</span><span class="sxs-lookup"><span data-stu-id="940ca-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="940ca-196">In genere, è preferibile toouse un `Stream` o `CloudBlockBlob` tipo.</span><span class="sxs-lookup"><span data-stu-id="940ca-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="940ca-197">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="940ca-197">Trigger sample</span></span>
<span data-ttu-id="940ca-198">Si supponga di che avere hello function.json che definisce un trigger di archiviazione blob di seguito:</span><span class="sxs-lookup"><span data-stu-id="940ca-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="940ca-199">Vedere l'esempio specifico del linguaggio hello che registra il contenuto di hello di ogni blob che viene aggiunto toohello monitorato contenitore.</span><span class="sxs-lookup"><span data-stu-id="940ca-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="940ca-200">C#</span><span class="sxs-lookup"><span data-stu-id="940ca-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="940ca-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="940ca-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="940ca-202">Esempi di trigger BLOB in C#</span><span class="sxs-lookup"><span data-stu-id="940ca-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="940ca-203">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="940ca-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="940ca-204">Uso dell'associazione di output nel BLOB</span><span class="sxs-lookup"><span data-stu-id="940ca-204">Using a blob output binding</span></span>

<span data-ttu-id="940ca-205">Nelle funzioni .NET, è necessario utilizzare un `out string` parametro la firma della funzione o utilizzare uno dei tipi di hello in hello seguente elenco.</span><span class="sxs-lookup"><span data-stu-id="940ca-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="940ca-206">Nelle funzioni di Node.js, accedere hello output blob utilizzando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="940ca-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="940ca-207">Nelle funzioni .NET è possibile output tooany di hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="940ca-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="940ca-208">Trigger di coda con esempio di input e output del BLOB</span><span class="sxs-lookup"><span data-stu-id="940ca-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="940ca-209">Si supponga di avere seguito function.json hello, che definisce un [trigger di archiviazione delle code](functions-bindings-storage-queue.md), un'archiviazione blob di input e output di un'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="940ca-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="940ca-210">Utilizzo di hello preavviso di hello `queueTrigger` proprietà dei metadati.</span><span class="sxs-lookup"><span data-stu-id="940ca-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="940ca-211">hello BLOB di input e output `path` proprietà:</span><span class="sxs-lookup"><span data-stu-id="940ca-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="940ca-212">Vedere l'esempio specifico del linguaggio hello che copia hello blob di input toohello output blob.</span><span class="sxs-lookup"><span data-stu-id="940ca-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="940ca-213">C#</span><span class="sxs-lookup"><span data-stu-id="940ca-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="940ca-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="940ca-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="940ca-215">Esempio di associazione del BLOB in C#</span><span class="sxs-lookup"><span data-stu-id="940ca-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="940ca-216">Esempio di associazione del BLOB in Node.js</span><span class="sxs-lookup"><span data-stu-id="940ca-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="940ca-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="940ca-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

