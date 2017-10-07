---
title: associazioni di funzioni Cosmos DB aaaAzure | Documenti Microsoft
description: Comprendere come associazioni Azure Cosmos DB toouse nelle funzioni di Azure.
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="e5dd6-104">Binding di Azure Cosmos DB in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e5dd6-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e5dd6-105">Questo articolo viene illustrato come associazioni di Azure Cosmos DB tooconfigure e codice nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="e5dd6-106">Funzioni di Azure supporta le associazioni di input e output per Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="e5dd6-107">Per ulteriori informazioni su Cosmos DB, vedere [introduzione tooCosmos DB](../documentdb/documentdb-introduction.md) e [compilare un'applicazione console Cosmos DB](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="e5dd6-108">Binding di input dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-108">DocumentDB API input binding</span></span>
<span data-ttu-id="e5dd6-109">associazione di input API DocumentDB Hello recupera un documento DB Cosmos e passa toohello denominato parametro di input della funzione hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="e5dd6-110">documento Hello che ID può essere determinato in base hello trigger che richiama la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="e5dd6-111">associazione di input API DocumentDB Hello è hello seguenti proprietà in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="e5dd6-112">`name`: Nome identificatore nel codice di funzione per il documento hello</span><span class="sxs-lookup"><span data-stu-id="e5dd6-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="e5dd6-113">`type`: deve essere impostato troppo "documentdb"</span><span class="sxs-lookup"><span data-stu-id="e5dd6-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="e5dd6-114">`databaseName`: database hello contenente il documento hello</span><span class="sxs-lookup"><span data-stu-id="e5dd6-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="e5dd6-115">`collectionName`: raccolta hello contenente il documento hello</span><span class="sxs-lookup"><span data-stu-id="e5dd6-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="e5dd6-116">`id`: Id di hello documento tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="e5dd6-117">Questa proprietà supporta i parametri di binding. vedere [associare le proprietà di input toocustom in un'espressione di associazione](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) nell'articolo hello [trigger funzioni di Azure e i concetti di associazioni](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="e5dd6-118">`sqlQuery`: una query SQL di Cosmos DB utilizzata per il recupero di più documenti.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="e5dd6-119">query Hello supporta le associazioni di runtime.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="e5dd6-120">Ad esempio: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="e5dd6-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="e5dd6-121">`connection`: nome hello dell'impostazione di app di hello contenente la stringa di connessione Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e5dd6-122">`direction`: deve essere impostato troppo`"in"`.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="e5dd6-123">proprietà Hello `id` e `sqlQuery` non possono essere specificati.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="e5dd6-124">Se non si specifica `id` né `sqlQuery` è impostata, hello intero insieme viene recuperato.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="e5dd6-125">Usare un binding di input dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="e5dd6-126">In c# e funzioni F # quando si esce dalla funzione hello correttamente, tutte le modifiche apportate toohello documento di input tramite parametri di input denominati vengono rese automaticamente persistenti.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="e5dd6-127">Nelle funzioni di JavaScript gli aggiornamenti non vengono eseguiti automaticamente al termine della funzione.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="e5dd6-128">Utilizzare invece `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` toomake aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="e5dd6-129">Vedere hello [esempio JavaScript](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="e5dd6-130">Esempio di input per il singolo documento</span><span class="sxs-lookup"><span data-stu-id="e5dd6-130">Input sample for single document</span></span>
<span data-ttu-id="e5dd6-131">Si supponga di avere seguito hello API DocumentDB input associazione in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e5dd6-132">Vedere l'esempio specifico del linguaggio hello che utilizza il valore di testo del documento l'associazione di input tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="e5dd6-133">C#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="e5dd6-134">F#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="e5dd6-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5dd6-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="e5dd6-136">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="e5dd6-137">Esempio di input in F#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="e5dd6-138">Questo esempio è necessario un `project.json` file che specifica hello `FSharp.Interop.Dynamic` e `Dynamitey` le dipendenze di NuGet:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e5dd6-139">tooadd un `project.json` file, vedere [gestione dei pacchetti di F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="e5dd6-140">Esempio di input in JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5dd6-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="e5dd6-141">Esempio di input con più documenti</span><span class="sxs-lookup"><span data-stu-id="e5dd6-141">Input sample with multiple documents</span></span>

<span data-ttu-id="e5dd6-142">Si supponga che si desiderano tooretrieve più documenti specificati da una query SQL, utilizzando i parametri di query una coda trigger toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="e5dd6-143">In questo esempio, i trigger di coda hello fornisce un parametro `departmentId`. Un messaggio nella coda di `{ "departmentId" : "Finance" }` restituisce tutti i record per il reparto di contabilità hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="e5dd6-144">Utilizzare la seguente hello in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="e5dd6-145">Esempio di input con più documenti in C#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="e5dd6-146">Esempio di input con più documenti in JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5dd6-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="e5dd6-147"><a id="docdboutput"></a>Binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="e5dd6-148">l'associazione consente di scrivere un nuovo database di Azure Cosmos DB tooan documento di output Hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="e5dd6-149">Ha hello seguenti proprietà in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="e5dd6-150">`name`: Identificatore utilizzato nel codice di funzione per il nuovo documento hello</span><span class="sxs-lookup"><span data-stu-id="e5dd6-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="e5dd6-151">`type`: deve essere impostato troppo`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="e5dd6-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="e5dd6-152">`databaseName`: database hello contenente hello raccolta in cui verrà creato il nuovo documento di hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="e5dd6-153">`collectionName`: hello raccolta in cui verrà creato il nuovo documento di hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="e5dd6-154">`createIfNotExists`: Un valore booleano tooindicate se verrà creato l'insieme di hello se non esiste.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="e5dd6-155">valore predefinito di Hello è *false*.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-155">hello default is *false*.</span></span> <span data-ttu-id="e5dd6-156">Hello motivo relativo a questa nuova le raccolte vengono create con velocità effettiva riservata con prezzi implicazioni.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="e5dd6-157">Per ulteriori informazioni, visitare hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="e5dd6-158">`connection`: nome hello dell'impostazione di app di hello contenente la stringa di connessione Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="e5dd6-159">`direction`: deve essere impostato troppo`"out"`</span><span class="sxs-lookup"><span data-stu-id="e5dd6-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="e5dd6-160">Usare un binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="e5dd6-161">In questa sezione viene illustrato come toouse l'API DocumentDB output associazione nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="e5dd6-162">Quando si scrive il parametro di output toohello nella funzione, per impostazione predefinita, che viene generato un nuovo documento nel database, con un GUID generato automaticamente come hello documento ID.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="e5dd6-163">È possibile specificare l'ID documento hello del documento di output specificando hello `id` proprietà JSON in hello parametro di output.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="e5dd6-164">Quando si specifica l'ID di hello di un documento esistente, si ottiene sovrascritto dal nuovo documento di output hello.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="e5dd6-165">toooutput più documenti, è anche possibile associare troppo`ICollector<T>` o `IAsyncCollector<T>` dove `T` è uno dei tipi di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="e5dd6-166">Esempio di binding di output dell'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e5dd6-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="e5dd6-167">Si supponga di avere seguito hello API DocumentDB output associazione in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="e5dd6-168">E si dispone di un'associazione di input di coda per una coda che riceve JSON in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e5dd6-169">E si desidera toocreate DB Cosmos documenti nel seguente formato per ogni record hello:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="e5dd6-170">Vedere l'esempio specifico del linguaggio hello che utilizza il database tooyour di documenti tooadd di associazione di output.</span><span class="sxs-lookup"><span data-stu-id="e5dd6-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="e5dd6-171">C#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e5dd6-172">F#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e5dd6-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5dd6-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e5dd6-174">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="e5dd6-175">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="e5dd6-175">Output sample in F#</span></span> #

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

<span data-ttu-id="e5dd6-176">Questo esempio è necessario un `project.json` file che specifica hello `FSharp.Interop.Dynamic` e `Dynamitey` le dipendenze di NuGet:</span><span class="sxs-lookup"><span data-stu-id="e5dd6-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="e5dd6-177">tooadd un `project.json` file, vedere [gestione dei pacchetti di F #](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="e5dd6-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="e5dd6-178">Esempio di output in JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5dd6-178">Output sample in JavaScript</span></span>

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
