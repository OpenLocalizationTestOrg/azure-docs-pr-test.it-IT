---
title: Associazioni dell'archiviazione BLOB di Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare trigger e associazioni di Archiviazione di Azure in Funzioni di Azure.
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
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="f36ec-104">Binding dell'archiviazione BLOB di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f36ec-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f36ec-105">Questo articolo illustra come configurare e operare con le associazioni dell'archiviazione BLOB in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="f36ec-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="f36ec-106">Funzioni di Azure supporta trigger, associazioni di input e di output per l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="f36ec-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="f36ec-107">Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="f36ec-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="f36ec-108">Non sono supportati [account di archiviazione solo BLOB](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="f36ec-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="f36ec-109">I trigger e le associazioni di archiviazione BLOB richiedono un account di archiviazione generico.</span><span class="sxs-lookup"><span data-stu-id="f36ec-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="f36ec-110">Trigger e associazioni do archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="f36ec-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="f36ec-111">Con l'uso del trigger di archiviazione BLOB di Azure, il codice della funzione viene chiamato quando viene rilevato un BLOB nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="f36ec-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="f36ec-112">I contenuti del BLOB vengono dati come input alla funzione.</span><span class="sxs-lookup"><span data-stu-id="f36ec-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="f36ec-113">Definire un'archiviazione BLOB usando la scheda **Integrazione** nel portale Funzioni.</span><span class="sxs-lookup"><span data-stu-id="f36ec-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="f36ec-114">Il portale crea la definizione seguente nella sezione **associazioni** di *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f36ec-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="f36ec-115">Le associazioni di input e output BLOB vengono definite usando `blob` come tipo di associazione:</span><span class="sxs-lookup"><span data-stu-id="f36ec-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="f36ec-116">La proprietà `path` supporta le espressioni di associazione e parametri di filtro.</span><span class="sxs-lookup"><span data-stu-id="f36ec-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="f36ec-117">Vedere [Modelli di nome](#pattern).</span><span class="sxs-lookup"><span data-stu-id="f36ec-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="f36ec-118">La proprietà `connection` deve contenere il nome di un'impostazione app che contiene una stringa di connessione alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f36ec-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="f36ec-119">Nel portale di Azure l'editor standard disponibile nella scheda **Integrazione** configura questa impostazione app quando si sceglie un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f36ec-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f36ec-120">Quando si usa un trigger di tipo BLOB in un piano a consumo, è possibile che si verifichi un ritardo di un massimo di 10 minuti per l'elaborazione di nuovi BLOB in caso di inattività di un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f36ec-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="f36ec-121">Quando l'app per le funzioni è in esecuzione, i BLOB vengono elaborati immediatamente.</span><span class="sxs-lookup"><span data-stu-id="f36ec-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="f36ec-122">Per evitare questo ritardo iniziale, prendere in considerazione una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f36ec-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="f36ec-123">Usare un piano di servizio app con l'opzione Always On abilitata.</span><span class="sxs-lookup"><span data-stu-id="f36ec-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="f36ec-124">Usare un altro meccanismo per attivare l'elaborazione dei BLOB, ad esempio un messaggio della coda che contiene il nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="f36ec-125">Per un esempio, vedere il [Queue trigger with blob input binding](#input-sample) (Trigger della coda con associazione di input del BLOB).</span><span class="sxs-lookup"><span data-stu-id="f36ec-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="f36ec-126">Modelli di nome</span><span class="sxs-lookup"><span data-stu-id="f36ec-126">Name patterns</span></span>
<span data-ttu-id="f36ec-127">È possibile specificare un modello di nome del BLOB nella proprietà `path`, che può essere un'espressione di filtro o di associazione.</span><span class="sxs-lookup"><span data-stu-id="f36ec-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="f36ec-128">Vedere [Modelli ed espressioni di associazione](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="f36ec-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="f36ec-129">Ad esempio, per filtrare i BLOB che iniziano con la stringa "original", usare la definizione seguente.</span><span class="sxs-lookup"><span data-stu-id="f36ec-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="f36ec-130">Questo percorso troverà un BLOB denominato *original-Blob1.txt* nel contenitore *input* e il valore della variabile `name` nel codice della funzione sarà `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="f36ec-131">Per associare il nome del file BLOB e l'estensione separatamente, usare due modelli.</span><span class="sxs-lookup"><span data-stu-id="f36ec-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="f36ec-132">Anche questo percorso troverà un BLOB denominato *original-Blob1.txt* e i valori delle variabili `blobname` e `blobextension` nel codice della funzione saranno *original-Blob1* e *txt*.</span><span class="sxs-lookup"><span data-stu-id="f36ec-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="f36ec-133">È possibile limitare il tipo di file dei BLOB usando un valore fisso per l'estensione del file.</span><span class="sxs-lookup"><span data-stu-id="f36ec-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="f36ec-134">Ad esempio, per attivare solo i file con estensione PNG, usare il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="f36ec-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="f36ec-135">Le parentesi graffe sono caratteri speciali nei modelli di nome.</span><span class="sxs-lookup"><span data-stu-id="f36ec-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="f36ec-136">Per specificare i nomi di BLOB con parentesi graffe nel nome, raddoppiare le parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="f36ec-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="f36ec-137">L'esempio seguente troverà un BLOB denominato *{20140101}-soundfile.mp3* nel contenitore *images* e il valore della variabile `name` nel codice della funzione sarà *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="f36ec-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="f36ec-138">Metadati del trigger</span><span class="sxs-lookup"><span data-stu-id="f36ec-138">Trigger metadata</span></span>

<span data-ttu-id="f36ec-139">Il trigger del BLOB contiene diverse proprietà di metadati.</span><span class="sxs-lookup"><span data-stu-id="f36ec-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="f36ec-140">Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice.</span><span class="sxs-lookup"><span data-stu-id="f36ec-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="f36ec-141">Questi valori hanno la stessa semantica di [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="f36ec-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="f36ec-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="f36ec-142">**BlobTrigger**.</span></span> <span data-ttu-id="f36ec-143">Digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-143">Type `string`.</span></span> <span data-ttu-id="f36ec-144">Il percorso del BLOB trigger</span><span class="sxs-lookup"><span data-stu-id="f36ec-144">The triggering blob path</span></span>
- <span data-ttu-id="f36ec-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="f36ec-145">**Uri**.</span></span> <span data-ttu-id="f36ec-146">Digitare `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-146">Type `System.Uri`.</span></span> <span data-ttu-id="f36ec-147">L'URI del BLOB per la posizione primaria.</span><span class="sxs-lookup"><span data-stu-id="f36ec-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="f36ec-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="f36ec-148">**Properties**.</span></span> <span data-ttu-id="f36ec-149">Digitare `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="f36ec-150">Le proprietà di sistema del BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-150">The blob's system properties.</span></span>
- <span data-ttu-id="f36ec-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="f36ec-151">**Metadata**.</span></span> <span data-ttu-id="f36ec-152">Digitare `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="f36ec-153">I metadati definiti dall'utente per il BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="f36ec-154">Conferme di BLOB</span><span class="sxs-lookup"><span data-stu-id="f36ec-154">Blob receipts</span></span>
<span data-ttu-id="f36ec-155">Il runtime di Funzioni di Azure verifica che nessuna funzione trigger di BLOB venga chiamata più volte per lo stesso BLOB nuovo o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="f36ec-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="f36ec-156">Gestisce *conferme di BLOB* per determinare se una versione di BLOB specifica è stata elaborata.</span><span class="sxs-lookup"><span data-stu-id="f36ec-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="f36ec-157">Funzioni di Azure archivia le conferme di BLOB in un contenitore denominato *azure-webjobs-hosts* nell'account di archiviazione di Azure per l'app per le funzioni, specificato dall'impostazione app `AzureWebJobsStorage`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="f36ec-158">Una conferma di BLOB contiene le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="f36ec-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="f36ec-159">La funzione attivata, ovvero "*&lt;nome dell'app per le funzioni>*.Functions.*&lt;nome della funzione>*", ad esempio: "MyFunctionApp.Functions.CopyBlob"</span><span class="sxs-lookup"><span data-stu-id="f36ec-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="f36ec-160">Il nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="f36ec-160">The container name</span></span>
* <span data-ttu-id="f36ec-161">Il tipo di BLOB ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="f36ec-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f36ec-162">Il nome del BLOB</span><span class="sxs-lookup"><span data-stu-id="f36ec-162">The blob name</span></span>
* <span data-ttu-id="f36ec-163">Il valore ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="f36ec-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="f36ec-164">Per forzare la rielaborazione di un BLOB è possibile eliminare manualmente la conferma del BLOB dal contenitore *azure-webjobs-hosts*.</span><span class="sxs-lookup"><span data-stu-id="f36ec-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="f36ec-165">Gestione di BLOB non elaborabili</span><span class="sxs-lookup"><span data-stu-id="f36ec-165">Handling poison blobs</span></span>
<span data-ttu-id="f36ec-166">Se una funzione di trigger del BLOB ha esito negativo per un determinato BLOB, per impostazione predefinita Funzioni di Azure ritenta l'esecuzione fino a 5 volte.</span><span class="sxs-lookup"><span data-stu-id="f36ec-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="f36ec-167">Se tutti i 5 tentativi non riescono, Funzioni di Azure aggiunge un messaggio a una coda di archiviazione denominata *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="f36ec-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="f36ec-168">Il messaggio di coda per i BLOB non elaborabili è un oggetto JSON che contiene le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="f36ec-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="f36ec-169">FunctionId (nel formato *&lt;nome dell'app per le funzioni>*.Functions.*&lt;nome della funzione>*)</span><span class="sxs-lookup"><span data-stu-id="f36ec-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="f36ec-170">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="f36ec-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f36ec-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="f36ec-171">ContainerName</span></span>
* <span data-ttu-id="f36ec-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="f36ec-172">BlobName</span></span>
* <span data-ttu-id="f36ec-173">ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="f36ec-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="f36ec-174">Polling dei BLOB per contenitori di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="f36ec-174">Blob polling for large containers</span></span>
<span data-ttu-id="f36ec-175">Se il contenitore BLOB monitorato contiene più di 10.000 BLOB, il runtime di Funzioni analizza i file di log per cercare i BLOB nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="f36ec-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="f36ec-176">Questo processo non avviene in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f36ec-176">This process is not real time.</span></span> <span data-ttu-id="f36ec-177">È possibile quindi che una funzione non venga attivata per diversi minuti o più dopo la creazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="f36ec-178">Per di più [i log di archiviazione vengono creati in base al principio del "massimo sforzo"](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="f36ec-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="f36ec-179">Non è garantito che tutti gli eventi vengano acquisiti.</span><span class="sxs-lookup"><span data-stu-id="f36ec-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="f36ec-180">In alcune condizioni, l'acquisizione dei log può non riuscire.</span><span class="sxs-lookup"><span data-stu-id="f36ec-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="f36ec-181">Se è necessaria un'elaborazione dei BLOB più veloce o affidabile, valutare la possibilità di creare un [messaggio della coda](../storage/queues/storage-dotnet-how-to-use-queues.md) quando si crea il BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="f36ec-182">Usare quindi un [trigger di coda](functions-bindings-storage-queue.md) invece di un trigger di BLOB per elaborare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="f36ec-183">Uso di un trigger di BLOB e dell'associazione di input</span><span class="sxs-lookup"><span data-stu-id="f36ec-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="f36ec-184">Nelle funzioni .NET è possibile accedere ai dati del BLOB con un parametro del metodo, ad esempio `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="f36ec-185">In questo caso, `paramName` è il valore specificato nella [configurazione del trigger](#trigger).</span><span class="sxs-lookup"><span data-stu-id="f36ec-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="f36ec-186">Nelle funzioni Node.js si accede a dati del BLOB di input usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f36ec-187">In .NET è possibile eseguire l'associazione a uno tipo qualsiasi nell'elenco riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f36ec-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="f36ec-188">Se usati come associazione di input, alcuni di questi tipi richiedono una direzione di associazione `inout` in *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f36ec-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="f36ec-189">Questa direzione non è supportata dall'editor standard, pertanto è necessario usare l'editor avanzato.</span><span class="sxs-lookup"><span data-stu-id="f36ec-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="f36ec-190">`ICloudBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="f36ec-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f36ec-191">`CloudBlockBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="f36ec-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f36ec-192">`CloudPageBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="f36ec-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f36ec-193">`CloudAppendBlob`, è necessaria la direzione di associazione "inout"</span><span class="sxs-lookup"><span data-stu-id="f36ec-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="f36ec-194">Se sono previsti BLOB di testo, è anche possibile eseguire l'associazione a un tipo `string` .NET.</span><span class="sxs-lookup"><span data-stu-id="f36ec-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="f36ec-195">È consigliabile solo se le dimensioni del BLOB sono ridotte, in quanto l'intero contenuto del BLOB viene caricato in memoria.</span><span class="sxs-lookup"><span data-stu-id="f36ec-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="f36ec-196">In genere, è preferibile usare un tipo `Stream` o `CloudBlockBlob`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="f36ec-197">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="f36ec-197">Trigger sample</span></span>
<span data-ttu-id="f36ec-198">Si supponga di avere function.json seguente, che definisce un trigger di archiviazione del BLOB:</span><span class="sxs-lookup"><span data-stu-id="f36ec-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="f36ec-199">Vedere l'esempio specifico del linguaggio che registra i contenuti di ogni BLOB aggiunto al contenitore monitorato.</span><span class="sxs-lookup"><span data-stu-id="f36ec-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="f36ec-200">C#</span><span class="sxs-lookup"><span data-stu-id="f36ec-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f36ec-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="f36ec-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="f36ec-202">Esempi di trigger BLOB in C#</span><span class="sxs-lookup"><span data-stu-id="f36ec-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="f36ec-203">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="f36ec-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="f36ec-204">Uso dell'associazione di output nel BLOB</span><span class="sxs-lookup"><span data-stu-id="f36ec-204">Using a blob output binding</span></span>

<span data-ttu-id="f36ec-205">Nelle funzioni .NET, è necessario usare un parametro `out string` nella firma della funzione o uno dei tipi nell'elenco seguente.</span><span class="sxs-lookup"><span data-stu-id="f36ec-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="f36ec-206">Nelle funzioni Node.js si accede al BLOB di output usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f36ec-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f36ec-207">Nelle funzioni .NET è possibile eseguire l'output in uno dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f36ec-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="f36ec-208">Trigger di coda con esempio di input e output del BLOB</span><span class="sxs-lookup"><span data-stu-id="f36ec-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="f36ec-209">Si supponga di avere function.json seguente, che definisce un [trigger di archiviazione della coda](functions-bindings-storage-queue.md), un input di archiviazione del BLOB e un output di archiviazione del BLOB.</span><span class="sxs-lookup"><span data-stu-id="f36ec-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="f36ec-210">Si noti l'uso della proprietà dei metadati `queueTrigger`</span><span class="sxs-lookup"><span data-stu-id="f36ec-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="f36ec-211">nelle proprietà `path` di input e output del BLOB:</span><span class="sxs-lookup"><span data-stu-id="f36ec-211">in the blob input and output `path` properties:</span></span>

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

<span data-ttu-id="f36ec-212">Vedere l'esempio specifico del linguaggio che copia il BLOB di input nel BLOB di output.</span><span class="sxs-lookup"><span data-stu-id="f36ec-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="f36ec-213">C#</span><span class="sxs-lookup"><span data-stu-id="f36ec-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="f36ec-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="f36ec-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="f36ec-215">Esempio di associazione del BLOB in C#</span><span class="sxs-lookup"><span data-stu-id="f36ec-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="f36ec-216">Esempio di associazione del BLOB in Node.js</span><span class="sxs-lookup"><span data-stu-id="f36ec-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="f36ec-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f36ec-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

