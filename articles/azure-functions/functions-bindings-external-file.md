---
title: associazioni di File esterno funzioni aaaAzure (anteprima) | Documenti Microsoft
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
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="3c8a9-103">Associazioni di file esterni in Funzioni di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="3c8a9-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="3c8a9-104">Questo articolo illustra come file toomanipulate da SaaS diversi provider (ad esempio, OneDrive, Dropbox) all'interno della funzione che utilizzano associazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="3c8a9-105">Funzioni di Azure supporta il trigger e le associazioni di output per i file esterni.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="3c8a9-106">Questa associazione consente di creare connessioni API tooSaaS provider oppure Usa connessioni API esistenti dal gruppo di risorse dell'applicazione (funzione).</span><span class="sxs-lookup"><span data-stu-id="3c8a9-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="3c8a9-107">Connessioni di file supportate</span><span class="sxs-lookup"><span data-stu-id="3c8a9-107">Supported File connections</span></span>

|<span data-ttu-id="3c8a9-108">Connettore</span><span class="sxs-lookup"><span data-stu-id="3c8a9-108">Connector</span></span>|<span data-ttu-id="3c8a9-109">Trigger</span><span class="sxs-lookup"><span data-stu-id="3c8a9-109">Trigger</span></span>|<span data-ttu-id="3c8a9-110">Input</span><span class="sxs-lookup"><span data-stu-id="3c8a9-110">Input</span></span>|<span data-ttu-id="3c8a9-111">Output</span><span class="sxs-lookup"><span data-stu-id="3c8a9-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="3c8a9-112">Box</span><span class="sxs-lookup"><span data-stu-id="3c8a9-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="3c8a9-113">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-113">x</span></span>|<span data-ttu-id="3c8a9-114">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-114">x</span></span>|<span data-ttu-id="3c8a9-115">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-115">x</span></span>
|[<span data-ttu-id="3c8a9-116">Dropbox</span><span class="sxs-lookup"><span data-stu-id="3c8a9-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="3c8a9-117">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-117">x</span></span>|<span data-ttu-id="3c8a9-118">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-118">x</span></span>|<span data-ttu-id="3c8a9-119">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-119">x</span></span>
|[<span data-ttu-id="3c8a9-120">FTP</span><span class="sxs-lookup"><span data-stu-id="3c8a9-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="3c8a9-121">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-121">x</span></span>|<span data-ttu-id="3c8a9-122">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-122">x</span></span>|<span data-ttu-id="3c8a9-123">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-123">x</span></span>
|[<span data-ttu-id="3c8a9-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="3c8a9-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="3c8a9-125">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-125">x</span></span>|<span data-ttu-id="3c8a9-126">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-126">x</span></span>|<span data-ttu-id="3c8a9-127">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-127">x</span></span>
|[<span data-ttu-id="3c8a9-128">OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="3c8a9-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="3c8a9-129">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-129">x</span></span>|<span data-ttu-id="3c8a9-130">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-130">x</span></span>|<span data-ttu-id="3c8a9-131">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-131">x</span></span>
|[<span data-ttu-id="3c8a9-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="3c8a9-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="3c8a9-133">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-133">x</span></span>|<span data-ttu-id="3c8a9-134">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-134">x</span></span>|<span data-ttu-id="3c8a9-135">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-135">x</span></span>
|[<span data-ttu-id="3c8a9-136">Google Drive</span><span class="sxs-lookup"><span data-stu-id="3c8a9-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="3c8a9-137">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-137">x</span></span>|<span data-ttu-id="3c8a9-138">x</span><span class="sxs-lookup"><span data-stu-id="3c8a9-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="3c8a9-139">È possibile usare le connessioni ai file esterni anche in [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="3c8a9-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="3c8a9-140">Associazione di trigger di file esterni</span><span class="sxs-lookup"><span data-stu-id="3c8a9-140">External File trigger binding</span></span>

<span data-ttu-id="3c8a9-141">i trigger di file esterno Azure Hello consente di monitorare una cartella remota ed eseguire il codice di funzione, quando vengono rilevate modifiche.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="3c8a9-142">i trigger di file esterno Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json</span><span class="sxs-lookup"><span data-stu-id="3c8a9-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="3c8a9-143">Modelli di nome</span><span class="sxs-lookup"><span data-stu-id="3c8a9-143">Name patterns</span></span>
<span data-ttu-id="3c8a9-144">È possibile specificare un modello di nome file in hello `path` proprietà.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="3c8a9-145">cartella Hello a cui fa riferimento deve essere presente nel provider SaaS hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="3c8a9-146">Esempi:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="3c8a9-147">Questo percorso potrebbe trovare un file denominato *originale File1.txt* in hello *input* cartella e il valore di hello di hello `name` variabile nel codice della funzione sarebbe `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="3c8a9-148">Un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="3c8a9-149">Questo percorso potrebbe anche trovare un file denominato *originale File1.txt*e il valore di hello di hello `filename` e `fileextension` variabili nel codice della funzione sarebbe *originale File1* e  *txt*.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="3c8a9-150">È possibile limitare il tipo di file hello del file con un valore fisso per l'estensione del file hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="3c8a9-151">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="3c8a9-152">In questo caso, solo *PNG* file hello *esempi* funzione hello trigger di cartella.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="3c8a9-153">Le parentesi graffe sono caratteri speciali nei modelli di nome.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="3c8a9-154">i nomi di file toospecify con doppie parentesi graffe in nome hello hello parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="3c8a9-155">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="3c8a9-156">Questo percorso potrebbe trovare un file denominato *{20140101}-soundfile.mp3* in hello *immagini* cartella e hello `name` valore variabile nel codice della funzione hello sarebbe *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="3c8a9-157">Gestione di file non elaborabili</span><span class="sxs-lookup"><span data-stu-id="3c8a9-157">Handling poison files</span></span>
<span data-ttu-id="3c8a9-158">Quando una funzione di attivazione di file esterno ha esito negativo, tale funzione too5 ore di funzioni di Azure tentativi per impostazione predefinita (inclusi provare prima a hello) per un determinato file.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="3c8a9-159">Se non tutti i tentativi di 5, le funzioni aggiunge una coda di archiviazione tooa messaggio denominata *non elaborabili processi Web-apihubtrigger*.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="3c8a9-160">messaggio della coda Hello per i file di messaggi non elaborabili è un oggetto JSON contenente hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="3c8a9-161">FunctionId (in formato hello  *&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*)</span><span class="sxs-lookup"><span data-stu-id="3c8a9-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="3c8a9-162">FileType</span><span class="sxs-lookup"><span data-stu-id="3c8a9-162">FileType</span></span>
* <span data-ttu-id="3c8a9-163">FolderName</span><span class="sxs-lookup"><span data-stu-id="3c8a9-163">FolderName</span></span>
* <span data-ttu-id="3c8a9-164">FileName</span><span class="sxs-lookup"><span data-stu-id="3c8a9-164">FileName</span></span>
* <span data-ttu-id="3c8a9-165">ETag (identificatore di versione del file, ad esempio: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="3c8a9-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="3c8a9-166">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="3c8a9-166">Trigger usage</span></span>
<span data-ttu-id="3c8a9-167">In c# le funzioni, è associare i dati di file di input toohello tramite un parametro denominato nella firma di funzione, come `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="3c8a9-168">In cui `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è specificato nel nome di hello il [attivare JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="3c8a9-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="3c8a9-169">Nelle funzioni di Node.js, si accede a dati di file di input hello tramite `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="3c8a9-170">file Hello può essere deserializzato in uno dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="3c8a9-171">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="3c8a9-172">Se si dichiara un tipo di input personalizzato (ad esempio `FooType`), le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="3c8a9-173">Stringa: utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-173">String - useful for text file data.</span></span>

<span data-ttu-id="3c8a9-174">In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e hello funzioni runtime tenta di deserializzare mediante quel tipo di dati del file hello:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="3c8a9-175">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="3c8a9-175">Trigger sample</span></span>
<span data-ttu-id="3c8a9-176">Si supponga di avere seguito function.json hello, che definisce un trigger di file esterno:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="3c8a9-177">Vedere l'esempio specifico del linguaggio hello che registra il contenuto di hello di ogni file che viene aggiunta una cartella monitorata toohello.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="3c8a9-178">C#</span><span class="sxs-lookup"><span data-stu-id="3c8a9-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="3c8a9-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c8a9-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="3c8a9-180">Uso dei trigger in C#</span><span class="sxs-lookup"><span data-stu-id="3c8a9-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="3c8a9-181">Uso dei trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="3c8a9-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="3c8a9-182">Associazione di input di file esterni</span><span class="sxs-lookup"><span data-stu-id="3c8a9-182">External File input binding</span></span>
<span data-ttu-id="3c8a9-183">associazione di input di file esterno Azure Hello consente toouse un file da una cartella in una funzione esterna.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="3c8a9-184">funzione di file esterno tooa input Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="3c8a9-185">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-185">Note hello following:</span></span>

* <span data-ttu-id="3c8a9-186">`path`deve contenere il nome di cartella hello e nome del file hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="3c8a9-187">Ad esempio, se dispone di un [trigger coda](functions-bindings-storage-queue.md) nella funzione, è possibile utilizzare `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file hello `samples-workitems` cartella con un nome che corrisponde al nome file hello specificato nel messaggio hello del trigger.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="3c8a9-188">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="3c8a9-188">Input usage</span></span>
<span data-ttu-id="3c8a9-189">In c# le funzioni, è associare i dati di file di input toohello tramite un parametro denominato nella firma di funzione, come `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="3c8a9-190">In cui `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è specificato nel nome di hello il [associazione di input](#input).</span><span class="sxs-lookup"><span data-stu-id="3c8a9-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="3c8a9-191">Nelle funzioni di Node.js, si accede a dati di file di input hello tramite `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="3c8a9-192">file Hello può essere deserializzato in uno dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="3c8a9-193">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="3c8a9-194">Se si dichiara un tipo di input personalizzato (ad esempio `InputType`), le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="3c8a9-195">Stringa: utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-195">String - useful for text file data.</span></span>

<span data-ttu-id="3c8a9-196">In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e hello funzioni runtime tenta di deserializzare mediante quel tipo di dati del file hello:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="3c8a9-197">Associazione di output di file esterni</span><span class="sxs-lookup"><span data-stu-id="3c8a9-197">External File output binding</span></span>
<span data-ttu-id="3c8a9-198">associazione consente cartella esterna toowrite file tooan nella funzione di output Hello Azure file esterno.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="3c8a9-199">file esterni di Hello di output per una funzione utilizza i seguenti oggetti JSON in hello hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="3c8a9-200">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-200">Note hello following:</span></span>

* <span data-ttu-id="3c8a9-201">`path`deve contenere il nome di cartella hello e toowrite di nome file hello per.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="3c8a9-202">Ad esempio, se dispone di un [trigger coda](functions-bindings-storage-queue.md) nella funzione, è possibile utilizzare `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file hello `samples-workitems` cartella con un nome che corrisponde al nome file hello specificato nel messaggio hello del trigger.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="3c8a9-203">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="3c8a9-203">Output usage</span></span>
<span data-ttu-id="3c8a9-204">In c# le funzioni, associare il file di output toohello utilizzando hello denominato `out` parametro nella firma di funzione, ad esempio `out <T> <name>`, dove `T` è che si desidera tooserialize hello dati del tipo di dati hello e `paramName` è hello nome specificato nella [associazione di output](#output).</span><span class="sxs-lookup"><span data-stu-id="3c8a9-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="3c8a9-205">Nelle funzioni di Node.js, si accedere ai file di output di hello utilizzando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="3c8a9-206">È possibile scrivere il file di output toohello utilizzando uno dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="3c8a9-207">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx), utile per la serializzazione con JSON.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="3c8a9-208">Se si dichiara un tipo di output personalizzato (ad esempio `out OutputType paramName`), le funzioni di Azure tenta tooserialize oggetto in JSON.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="3c8a9-209">Se il parametro di output di hello è null quando si esce dalla funzione hello, hello funzioni runtime crea un file come un oggetto null.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="3c8a9-210">Stringa: `out string paramName`utile per i dati del file di testo.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="3c8a9-211">Hello funzioni runtime crea un file solo se il parametro della stringa non null quando si esce dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="3c8a9-212">In c# le funzioni può inoltre restituire tooany di hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="3c8a9-213">Esempio di input e output</span><span class="sxs-lookup"><span data-stu-id="3c8a9-213">Input + Output sample</span></span>
<span data-ttu-id="3c8a9-214">Si supponga di avere seguito function.json hello, che definisce un [trigger coda di archiviazione](functions-bindings-storage-queue.md), un file esterno di input e output di un file esterno:</span><span class="sxs-lookup"><span data-stu-id="3c8a9-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="3c8a9-215">Vedere l'esempio specifico del linguaggio hello che copia i file di output toohello hello file di input.</span><span class="sxs-lookup"><span data-stu-id="3c8a9-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="3c8a9-216">C#</span><span class="sxs-lookup"><span data-stu-id="3c8a9-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="3c8a9-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c8a9-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="3c8a9-218">Utilizzo in C#</span><span class="sxs-lookup"><span data-stu-id="3c8a9-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="3c8a9-219">Uso in Node.js</span><span class="sxs-lookup"><span data-stu-id="3c8a9-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="3c8a9-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c8a9-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
