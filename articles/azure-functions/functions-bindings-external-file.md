---
title: Associazioni di file esterni in Funzioni di Azure (Anteprima) | Microsoft Docs
description: Utilizzo di associazioni di file esterni in Funzioni di Azure
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="6a067-103">Associazioni di file esterni in Funzioni di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="6a067-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="6a067-104">Questo articolo illustra come modificare i file da diversi provider di SaaS (ad esempio OneDrive, Dropbox) all'interno della funzione che usa binding incorporati.</span><span class="sxs-lookup"><span data-stu-id="6a067-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="6a067-105">Funzioni di Azure supporta il trigger e le associazioni di output per i file esterni.</span><span class="sxs-lookup"><span data-stu-id="6a067-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="6a067-106">Il binding crea connessioni API ai provider SaaS o usa quelle esistenti prelevandole dal gruppo di risorse dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="6a067-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="6a067-107">Connessioni di file supportate</span><span class="sxs-lookup"><span data-stu-id="6a067-107">Supported File connections</span></span>

|<span data-ttu-id="6a067-108">Connettore</span><span class="sxs-lookup"><span data-stu-id="6a067-108">Connector</span></span>|<span data-ttu-id="6a067-109">Trigger</span><span class="sxs-lookup"><span data-stu-id="6a067-109">Trigger</span></span>|<span data-ttu-id="6a067-110">Input</span><span class="sxs-lookup"><span data-stu-id="6a067-110">Input</span></span>|<span data-ttu-id="6a067-111">Output</span><span class="sxs-lookup"><span data-stu-id="6a067-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="6a067-112">Box</span><span class="sxs-lookup"><span data-stu-id="6a067-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="6a067-113">x</span><span class="sxs-lookup"><span data-stu-id="6a067-113">x</span></span>|<span data-ttu-id="6a067-114">x</span><span class="sxs-lookup"><span data-stu-id="6a067-114">x</span></span>|<span data-ttu-id="6a067-115">x</span><span class="sxs-lookup"><span data-stu-id="6a067-115">x</span></span>
|[<span data-ttu-id="6a067-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="6a067-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="6a067-117">x</span><span class="sxs-lookup"><span data-stu-id="6a067-117">x</span></span>|<span data-ttu-id="6a067-118">x</span><span class="sxs-lookup"><span data-stu-id="6a067-118">x</span></span>|<span data-ttu-id="6a067-119">x</span><span class="sxs-lookup"><span data-stu-id="6a067-119">x</span></span>
|[<span data-ttu-id="6a067-120">FTP</span><span class="sxs-lookup"><span data-stu-id="6a067-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="6a067-121">x</span><span class="sxs-lookup"><span data-stu-id="6a067-121">x</span></span>|<span data-ttu-id="6a067-122">x</span><span class="sxs-lookup"><span data-stu-id="6a067-122">x</span></span>|<span data-ttu-id="6a067-123">x</span><span class="sxs-lookup"><span data-stu-id="6a067-123">x</span></span>
|[<span data-ttu-id="6a067-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="6a067-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="6a067-125">x</span><span class="sxs-lookup"><span data-stu-id="6a067-125">x</span></span>|<span data-ttu-id="6a067-126">x</span><span class="sxs-lookup"><span data-stu-id="6a067-126">x</span></span>|<span data-ttu-id="6a067-127">x</span><span class="sxs-lookup"><span data-stu-id="6a067-127">x</span></span>
|[<span data-ttu-id="6a067-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="6a067-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="6a067-129">x</span><span class="sxs-lookup"><span data-stu-id="6a067-129">x</span></span>|<span data-ttu-id="6a067-130">x</span><span class="sxs-lookup"><span data-stu-id="6a067-130">x</span></span>|<span data-ttu-id="6a067-131">x</span><span class="sxs-lookup"><span data-stu-id="6a067-131">x</span></span>
|[<span data-ttu-id="6a067-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="6a067-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="6a067-133">x</span><span class="sxs-lookup"><span data-stu-id="6a067-133">x</span></span>|<span data-ttu-id="6a067-134">x</span><span class="sxs-lookup"><span data-stu-id="6a067-134">x</span></span>|<span data-ttu-id="6a067-135">x</span><span class="sxs-lookup"><span data-stu-id="6a067-135">x</span></span>
|[<span data-ttu-id="6a067-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="6a067-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="6a067-137">x</span><span class="sxs-lookup"><span data-stu-id="6a067-137">x</span></span>|<span data-ttu-id="6a067-138">x</span><span class="sxs-lookup"><span data-stu-id="6a067-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="6a067-139">È possibile usare le connessioni ai file esterni anche in [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="6a067-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="6a067-140">Associazione di trigger di file esterni</span><span class="sxs-lookup"><span data-stu-id="6a067-140">External File trigger binding</span></span>

<span data-ttu-id="6a067-141">Il trigger di file esterni di Azure consente di monitorare una cartella remota ed eseguire il codice della funzione qualora vengano rilevate modifiche.</span><span class="sxs-lookup"><span data-stu-id="6a067-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="6a067-142">Tale trigger usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="6a067-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="6a067-143">Modelli di nome</span><span class="sxs-lookup"><span data-stu-id="6a067-143">Name patterns</span></span>
<span data-ttu-id="6a067-144">È possibile specificare un modello di nome per il file nella proprietà `path`,</span><span class="sxs-lookup"><span data-stu-id="6a067-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="6a067-145">La cartella a cui si fa riferimento deve esistere nel provider SaaS.</span><span class="sxs-lookup"><span data-stu-id="6a067-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="6a067-146">Esempi:</span><span class="sxs-lookup"><span data-stu-id="6a067-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="6a067-147">Questo percorso individua il file denominato *original-File1.txt* nella cartella *input* e il valore della variabile `name` nel codice della funzione sarà `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="6a067-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="6a067-148">Un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="6a067-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="6a067-149">Anche questo percorso individua un file denominato *original-File1.txt* e i valori delle variabili `filename` e `fileextension` nel codice della funzione saranno *original-File1* e *txt*.</span><span class="sxs-lookup"><span data-stu-id="6a067-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="6a067-150">È possibile limitare il tipo di file dei file usando un valore fisso per l'estensione del file.</span><span class="sxs-lookup"><span data-stu-id="6a067-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="6a067-151">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a067-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="6a067-152">In questo caso, la funzione verrà attivata solo dai file *.png* nella cartella *samples*.</span><span class="sxs-lookup"><span data-stu-id="6a067-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="6a067-153">Le parentesi graffe sono caratteri speciali nei modelli di nome.</span><span class="sxs-lookup"><span data-stu-id="6a067-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="6a067-154">Per specificare nomi di file con parentesi graffe nel nome, raddoppiare le parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="6a067-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="6a067-155">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6a067-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="6a067-156">Questo percorso troverà un file denominato *{20140101}-soundfile.mp3* nella cartella *images* e il valore della variabile `name` nel codice della funzione sarà *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6a067-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="6a067-157">Gestione di file non elaborabili</span><span class="sxs-lookup"><span data-stu-id="6a067-157">Handling poison files</span></span>
<span data-ttu-id="6a067-158">Quando una funzione di trigger del file esterno ha esito negativo, per impostazione predefinita Funzioni di Azure ritenta l'esecuzione fino a 5 volte (incluso il primo tentativo) per un dato messaggio.</span><span class="sxs-lookup"><span data-stu-id="6a067-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="6a067-159">Se tutti i 5 tentativi non riescono, Funzioni di Azure aggiunge un messaggio a una coda di archiviazione denominata *webjobs-apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6a067-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="6a067-160">Il messaggio di coda per i file non elaborabili è un oggetto JSON che contiene le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="6a067-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="6a067-161">FunctionId (nel formato *&lt;nome dell'app per le funzioni>*.Functions.*&lt;nome della funzione>*)</span><span class="sxs-lookup"><span data-stu-id="6a067-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="6a067-162">FileType</span><span class="sxs-lookup"><span data-stu-id="6a067-162">FileType</span></span>
* <span data-ttu-id="6a067-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="6a067-163">FolderName</span></span>
* <span data-ttu-id="6a067-164">FileName</span><span class="sxs-lookup"><span data-stu-id="6a067-164">FileName</span></span>
* <span data-ttu-id="6a067-165">ETag (identificatore di versione del file, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6a067-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="6a067-166">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="6a067-166">Trigger usage</span></span>
<span data-ttu-id="6a067-167">Nelle funzioni C# l'associazione ai dati del file di input viene eseguita usando un parametro denominato nella firma funzione, ad esempio `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6a067-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6a067-168">`T` è il tipo di dati in cui si vogliono deserializzare i dati e `paramName` è il nome specificato nel [JSON del trigger](#trigger).</span><span class="sxs-lookup"><span data-stu-id="6a067-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="6a067-169">Nelle funzioni Node.js si accede ai dati del file di input usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6a067-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6a067-170">È possibile deserializzare il file in uno dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a067-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6a067-171">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="6a067-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6a067-172">Se si dichiara un tipo di input personalizzato, ad esempio `FooType`, Funzioni di Azure tenta di deserializzare i dati JSON nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="6a067-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6a067-173">Stringa: utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="6a067-173">String - useful for text file data.</span></span>

<span data-ttu-id="6a067-174">Nelle funzioni C# è anche possibile eseguire l'associazione a uno dei tipi seguenti e il runtime di Funzioni di Azure tenta di deserializzare i dati del file usando quel tipo:</span><span class="sxs-lookup"><span data-stu-id="6a067-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="6a067-175">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="6a067-175">Trigger sample</span></span>
<span data-ttu-id="6a067-176">Si supponga di avere il function.json seguente, che definisce un trigger di file esterno:</span><span class="sxs-lookup"><span data-stu-id="6a067-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="6a067-177">Vedere l'esempio specifico del linguaggio che registra i contenuti di ogni file aggiunto alla cartella monitorata.</span><span class="sxs-lookup"><span data-stu-id="6a067-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="6a067-178">C#</span><span class="sxs-lookup"><span data-stu-id="6a067-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="6a067-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a067-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="6a067-180">Uso dei trigger in C#</span><span class="sxs-lookup"><span data-stu-id="6a067-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="6a067-181">Uso dei trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="6a067-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="6a067-182">Associazione di input di file esterni</span><span class="sxs-lookup"><span data-stu-id="6a067-182">External File input binding</span></span>
<span data-ttu-id="6a067-183">L'associazione di input di file esterni di Azure consente di usare un file da una cartella esterna nella funzione.</span><span class="sxs-lookup"><span data-stu-id="6a067-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="6a067-184">L'input del file esterno in una funzione usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="6a067-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="6a067-185">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6a067-185">Note the following:</span></span>

* <span data-ttu-id="6a067-186">`path` deve contenere il nome della cartella e il nome del file.</span><span class="sxs-lookup"><span data-stu-id="6a067-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="6a067-187">Se, ad esempio, nella funzione è presente un [trigger della coda](functions-bindings-storage-queue.md), è possibile usare `"path": "samples-workitems/{queueTrigger}"` in modo che punti a un file nella cartella `samples-workitems` con un nome che corrisponde al nome di file specificato nel messaggio di trigger.</span><span class="sxs-lookup"><span data-stu-id="6a067-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6a067-188">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="6a067-188">Input usage</span></span>
<span data-ttu-id="6a067-189">Nelle funzioni C# l'associazione ai dati del file di input viene eseguita usando un parametro denominato nella firma funzione, ad esempio `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6a067-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6a067-190">`T` è il tipo di dati in cui si vogliono deserializzare i dati e `paramName` è il nome specificato nell'[associazione di input](#input).</span><span class="sxs-lookup"><span data-stu-id="6a067-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="6a067-191">Nelle funzioni Node.js si accede ai dati del file di input usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6a067-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6a067-192">È possibile deserializzare il file in uno dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a067-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="6a067-193">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="6a067-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="6a067-194">Se si dichiara un tipo di input personalizzato, ad esempio `InputType`, Funzioni di Azure tenta di deserializzare i dati JSON nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="6a067-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="6a067-195">Stringa: utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="6a067-195">String - useful for text file data.</span></span>

<span data-ttu-id="6a067-196">Nelle funzioni C# è anche possibile eseguire l'associazione a uno dei tipi seguenti e il runtime di Funzioni di Azure tenta di deserializzare i dati del file usando quel tipo:</span><span class="sxs-lookup"><span data-stu-id="6a067-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="6a067-197">Associazione di output di file esterni</span><span class="sxs-lookup"><span data-stu-id="6a067-197">External File output binding</span></span>
<span data-ttu-id="6a067-198">L'associazione di input di file esterni di Azure consente di usare un file da una cartella esterna nella funzione.</span><span class="sxs-lookup"><span data-stu-id="6a067-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="6a067-199">L'output del file esterno per una funzione usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="6a067-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="6a067-200">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6a067-200">Note the following:</span></span>

* <span data-ttu-id="6a067-201">`path` deve contenere il nome della cartella e il nome del file in cui scrivere.</span><span class="sxs-lookup"><span data-stu-id="6a067-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="6a067-202">Se, ad esempio, nella funzione è presente un [trigger della coda](functions-bindings-storage-queue.md), è possibile usare `"path": "samples-workitems/{queueTrigger}"` in modo che punti a un file nella cartella `samples-workitems` con un nome che corrisponde al nome di file specificato nel messaggio di trigger.</span><span class="sxs-lookup"><span data-stu-id="6a067-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6a067-203">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="6a067-203">Output usage</span></span>
<span data-ttu-id="6a067-204">Nelle funzioni C# è possibile eseguire l'associazione al file di output usando il parametro denominato `out` nella firma funzione, ad esempio `out <T> <name>`, dove `T` è il tipo di dati in cui si vuole serializzare i dati e `paramName` è il nome specificato nell'[associazione di output](#output).</span><span class="sxs-lookup"><span data-stu-id="6a067-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="6a067-205">Nelle funzioni Node.js si accede al file di output usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6a067-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6a067-206">È possibile scrivere nel file di output usando uno dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a067-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="6a067-207">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx), utile per la serializzazione con JSON.</span><span class="sxs-lookup"><span data-stu-id="6a067-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="6a067-208">Se si dichiara un tipo di output personalizzato (ad esempio `out OutputType paramName`), Funzioni di Azure tenta di serializzare l'oggetto in JSON.</span><span class="sxs-lookup"><span data-stu-id="6a067-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="6a067-209">Se il parametro di output è null quando la funzione viene chiusa, il runtime di Funzioni crea un file come un oggetto null.</span><span class="sxs-lookup"><span data-stu-id="6a067-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="6a067-210">Stringa: `out string paramName`utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="6a067-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="6a067-211">Il runtime di Funzioni crea un file solo se il parametro di stringa è diverso da null quando la funzione viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="6a067-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="6a067-212">Nelle funzioni C# è anche possibile eseguire l'output in uno dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6a067-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="6a067-213">Esempio di input e output</span><span class="sxs-lookup"><span data-stu-id="6a067-213">Input + Output sample</span></span>
<span data-ttu-id="6a067-214">Si supponga di avere il function.json seguente, che definisce un [trigger della coda di archiviazione](functions-bindings-storage-queue.md), un input del file esterno e un output del file esterno:</span><span class="sxs-lookup"><span data-stu-id="6a067-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6a067-215">Vedere l'esempio specifico del linguaggio che copia il file di input nel file di output.</span><span class="sxs-lookup"><span data-stu-id="6a067-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="6a067-216">C#</span><span class="sxs-lookup"><span data-stu-id="6a067-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="6a067-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="6a067-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="6a067-218">Utilizzo in C#</span><span class="sxs-lookup"><span data-stu-id="6a067-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="6a067-219">Uso in Node.js</span><span class="sxs-lookup"><span data-stu-id="6a067-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="6a067-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a067-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
