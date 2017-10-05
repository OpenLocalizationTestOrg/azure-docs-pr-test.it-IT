---
title: Binding di Azure Cosmos DB in Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare i binding di Azure Cosmos DB in Funzioni di Azure.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="be20c-104">Binding di Azure Cosmos DB in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="be20c-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="be20c-105">Questo articolo illustra come configurare e scrivere il codice di associazioni di Azure Cosmos DB in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="be20c-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="be20c-106">Funzioni di Azure supporta le associazioni di input e output per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="be20c-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="be20c-107">Per altre informazioni su Cosmos DB, vedere [Introduzione a Cosmos DB](../documentdb/documentdb-introduction.md) e [Compilare un'applicazione console Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be20c-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="be20c-108">Binding di input dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="be20c-108">DocumentDB API input binding</span></span>
<span data-ttu-id="be20c-109">Il binding di input di DocumentDB recupera un documento di DocumentDB e lo passa al parametro di input denominato della funzione.</span><span class="sxs-lookup"><span data-stu-id="be20c-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="be20c-110">L'ID documento può essere determinato in base al trigger che richiama la funzione.</span><span class="sxs-lookup"><span data-stu-id="be20c-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="be20c-111">Il binding di input di DocumentDB presenta le seguenti proprietà *function.json*:</span><span class="sxs-lookup"><span data-stu-id="be20c-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="be20c-112">`name`: nome dell'identificatore usato nel codice della funzione per il documento</span><span class="sxs-lookup"><span data-stu-id="be20c-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="be20c-113">`type`: deve essere impostato su "documentdb"</span><span class="sxs-lookup"><span data-stu-id="be20c-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="be20c-114">`databaseName`: database che contiene il documento</span><span class="sxs-lookup"><span data-stu-id="be20c-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="be20c-115">`collectionName`: raccolta che contiene il documento</span><span class="sxs-lookup"><span data-stu-id="be20c-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="be20c-116">`id` : ID del documento da recuperare.</span><span class="sxs-lookup"><span data-stu-id="be20c-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="be20c-117">Questa proprietà supporta i parametri di associazione. Vedere [Associare le proprietà di input personalizzate in un'espressione di associazione](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) nell'articolo [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="be20c-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="be20c-118">`sqlQuery`: una query SQL di Cosmos DB utilizzata per il recupero di più documenti.</span><span class="sxs-lookup"><span data-stu-id="be20c-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="be20c-119">La query supporta le associazioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="be20c-119">The query supports runtime bindings.</span></span> <span data-ttu-id="be20c-120">Ad esempio: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="be20c-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="be20c-121">`connection`: il nome dell'impostazione dell'app contenente la stringa di connessione di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="be20c-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="be20c-122">`direction`: deve essere impostato su `"in"`.</span><span class="sxs-lookup"><span data-stu-id="be20c-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="be20c-123">Le proprietà `id` e `sqlQuery` non possono essere entrambe specificate.</span><span class="sxs-lookup"><span data-stu-id="be20c-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="be20c-124">Se non si specifica `id` né `sqlQuery`, viene recuperata l'intera raccolta.</span><span class="sxs-lookup"><span data-stu-id="be20c-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="be20c-125">Usare un binding di input dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="be20c-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="be20c-126">Nelle funzioni C# e F#, quando la funzione termina correttamente, le modifiche apportate al documento di input tramite i parametri di input denominati vengono rese automaticamente persistenti.</span><span class="sxs-lookup"><span data-stu-id="be20c-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="be20c-127">Nelle funzioni di JavaScript gli aggiornamenti non vengono eseguiti automaticamente al termine della funzione.</span><span class="sxs-lookup"><span data-stu-id="be20c-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="be20c-128">Per eseguire gli aggiornamenti usare invece `context.bindings.<documentName>In` e `context.bindings.<documentName>Out`.</span><span class="sxs-lookup"><span data-stu-id="be20c-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="be20c-129">Vedere l'[esempio di JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="be20c-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="be20c-130">Esempio di input per il singolo documento</span><span class="sxs-lookup"><span data-stu-id="be20c-130">Input sample for single document</span></span>
<span data-ttu-id="be20c-131">Si supponga di avere il seguente binding di input dell'API DocumentDB nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="be20c-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="be20c-132">Vedere l'esempio specifico del linguaggio che usa questa associazione di input per aggiornare il valore di testo del documento.</span><span class="sxs-lookup"><span data-stu-id="be20c-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="be20c-133">C#</span><span class="sxs-lookup"><span data-stu-id="be20c-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="be20c-134">F#</span><span class="sxs-lookup"><span data-stu-id="be20c-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="be20c-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="be20c-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="be20c-136">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="be20c-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="be20c-137">Esempio di input in F#</span><span class="sxs-lookup"><span data-stu-id="be20c-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="be20c-138">Per questo esempio è necessario un file `project.json` che specifichi le dipendenze NuGet `FSharp.Interop.Dynamic` e `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="be20c-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="be20c-139">Per aggiungere un file `project.json`, vedere l'argomento relativo alla [gestione dei pacchetti F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="be20c-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="be20c-140">Esempio di input in JavaScript</span><span class="sxs-lookup"><span data-stu-id="be20c-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="be20c-141">Esempio di input con più documenti</span><span class="sxs-lookup"><span data-stu-id="be20c-141">Input sample with multiple documents</span></span>

<span data-ttu-id="be20c-142">Si supponga che si desideri recuperare più documenti specificati da una query SQL, mediante un trigger di coda per personalizzare i parametri di query.</span><span class="sxs-lookup"><span data-stu-id="be20c-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="be20c-143">In questo esempio, il trigger di coda offre un parametro `departmentId`. Un messaggio di coda `{ "departmentId" : "Finance" }` restituirà tutti i record per il reparto finanziario.</span><span class="sxs-lookup"><span data-stu-id="be20c-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="be20c-144">Usare il codice seguente in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="be20c-144">Use the following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="be20c-145">Esempio di input con più documenti in C#</span><span class="sxs-lookup"><span data-stu-id="be20c-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="be20c-146">Esempio di input con più documenti in JavaScript</span><span class="sxs-lookup"><span data-stu-id="be20c-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="be20c-147"><a id="docdboutput"></a>Binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="be20c-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="be20c-148">Il binding di output dell'API DocumentDB consente di scrivere un nuovo documento in un database di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="be20c-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="be20c-149">In *function.json* ha le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="be20c-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="be20c-150">`name`: nome dell'identificatore usato nel codice della funzione per il nuovo documento</span><span class="sxs-lookup"><span data-stu-id="be20c-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="be20c-151">`type`: deve essere impostato su `"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="be20c-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="be20c-152">`databaseName` : database contenente la raccolta in cui verrà creato il nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="be20c-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="be20c-153">`collectionName` : raccolta in cui verrà creato il nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="be20c-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="be20c-154">`createIfNotExists`: valore booleano che indica se la raccolta viene creata quando non esiste.</span><span class="sxs-lookup"><span data-stu-id="be20c-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="be20c-155">Il valore predefinito è *false*.</span><span class="sxs-lookup"><span data-stu-id="be20c-155">The default is *false*.</span></span> <span data-ttu-id="be20c-156">Il motivo è che le nuove raccolte vengono create con una velocità effettiva riservata, che ha implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="be20c-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="be20c-157">Per altre informazioni, visitare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="be20c-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="be20c-158">`connection`: il nome dell'impostazione dell'app contenente la stringa di connessione di Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="be20c-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="be20c-159">`direction`: deve essere impostato su `"out"`</span><span class="sxs-lookup"><span data-stu-id="be20c-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="be20c-160">Usare un binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="be20c-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="be20c-161">Questa sezione illustra come usare il binding di output dell'API DocumentDB nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="be20c-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="be20c-162">Quando si scrive per il parametro di output nella funzione, per impostazione predefinita viene generato un nuovo documento nel database con un GUID generato automaticamente come ID documento.</span><span class="sxs-lookup"><span data-stu-id="be20c-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="be20c-163">È possibile specificare l'ID documento del documento di output specificando la proprietà JSON `id` nel parametro di output.</span><span class="sxs-lookup"><span data-stu-id="be20c-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="be20c-164">Quando si specifica l'ID di un documento esistente, questo viene sovrascritto dal nuovo documento di output.</span><span class="sxs-lookup"><span data-stu-id="be20c-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="be20c-165">Per visualizzare più documenti, è anche possibile definire l'associazione a `ICollector<T>` o `IAsyncCollector<T>` dove `T` è uno dei tipi supportati.</span><span class="sxs-lookup"><span data-stu-id="be20c-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="be20c-166">Esempio di binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="be20c-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="be20c-167">Si supponga di avere la seguente associazione di output dell'API DocumentDB nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="be20c-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="be20c-168">Ed è disponibile un'associazione di input di coda per una coda che riceve JSON nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="be20c-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="be20c-169">Si vuole creare documenti di Cosmos DB nel formato seguente per ogni record:</span><span class="sxs-lookup"><span data-stu-id="be20c-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="be20c-170">Vedere l'esempio specifico del linguaggio che usa questa associazione di output per aggiungere i documenti al database.</span><span class="sxs-lookup"><span data-stu-id="be20c-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="be20c-171">C#</span><span class="sxs-lookup"><span data-stu-id="be20c-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="be20c-172">F#</span><span class="sxs-lookup"><span data-stu-id="be20c-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="be20c-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="be20c-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="be20c-174">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="be20c-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="be20c-175">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="be20c-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="be20c-176">Per questo esempio è necessario un file `project.json` che specifichi le dipendenze NuGet `FSharp.Interop.Dynamic` e `Dynamitey`:</span><span class="sxs-lookup"><span data-stu-id="be20c-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="be20c-177">Per aggiungere un file `project.json`, vedere l'argomento relativo alla [gestione dei pacchetti F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="be20c-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="be20c-178">Esempio di output in JavaScript</span><span class="sxs-lookup"><span data-stu-id="be20c-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
