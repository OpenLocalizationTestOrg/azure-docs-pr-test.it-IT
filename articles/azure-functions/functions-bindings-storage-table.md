---
title: Associazioni della tabella di archiviazione di Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare le associazioni di Archiviazione di Azure in Funzioni di Azure.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="6eee9-104">Associazioni della tabella di archiviazione di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="6eee9-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="6eee9-105">Questo articolo illustra come configurare e scrivere il codice delle associazioni delle tabelle di Archiviazione di Azure in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="6eee9-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="6eee9-106">Funzioni di Azure supporta le associazioni di input e output per le tabelle di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6eee9-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="6eee9-107">L'associazione delle tabelle di archiviazione supporta gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="6eee9-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="6eee9-108">**Leggere una singola riga in una funzione C# o Node.js**: impostare `partitionKey` e `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="6eee9-109">Le proprietà `filter` e `take` non vengono usate in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="6eee9-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="6eee9-110">**Leggere più righe in una funzione C#**: il runtime di Funzioni specifica un oggetto `IQueryable<T>` associato alla tabella.</span><span class="sxs-lookup"><span data-stu-id="6eee9-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="6eee9-111">Il tipo `T` deve derivare da `TableEntity` o implementare `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="6eee9-112">Le proprietà `partitionKey`, `rowKey`, `filter` e `take` non vengono usate in questo scenario. È possibile usare l'oggetto `IQueryable` per qualsiasi operazione di filtro necessaria.</span><span class="sxs-lookup"><span data-stu-id="6eee9-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="6eee9-113">**Leggere più righe in una funzione Node**: impostare le proprietà `filter` e `take`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="6eee9-114">Non impostare `partitionKey` o `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="6eee9-115">**Scrivere una o più righe in una funzione C#**: il runtime di Funzioni specifica un oggetto `ICollector<T>` o `IAsyncCollector<T>` associato alla tabella, dove `T` indica lo schema delle entità da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="6eee9-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="6eee9-116">In genere, ma non necessariamente, il tipo `T` deriva da `TableEntity` o implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="6eee9-117">Le proprietà `partitionKey`, `rowKey`, `filter` e `take` non vengono usate in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="6eee9-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="6eee9-118">Associazione di input della tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6eee9-118">Storage table input binding</span></span>
<span data-ttu-id="6eee9-119">L'associazione di input nella tabella di archiviazione di Azure consente di usare una tabella di archiviazione nella funzione.</span><span class="sxs-lookup"><span data-stu-id="6eee9-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="6eee9-120">L'input della tabella di archiviazione in una funzione usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="6eee9-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="6eee9-121">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6eee9-121">Note the following:</span></span> 

* <span data-ttu-id="6eee9-122">Usare `partitionKey` e `rowKey` insieme per leggere una singola entità.</span><span class="sxs-lookup"><span data-stu-id="6eee9-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="6eee9-123">Queste proprietà sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="6eee9-123">These properties are optional.</span></span> 
* <span data-ttu-id="6eee9-124">`connection` deve contenere il nome di un'impostazione app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6eee9-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="6eee9-125">Nel portale di Azure l'editor standard disponibile nella scheda **Integra** configura automaticamente questa impostazione app quando si crea un account di archiviazione o si seleziona un account già esistente.</span><span class="sxs-lookup"><span data-stu-id="6eee9-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="6eee9-126">È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="6eee9-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="6eee9-127">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="6eee9-127">Input usage</span></span>
<span data-ttu-id="6eee9-128">Nelle funzioni C# l'associazione all'entità, o alle entità, della tabella di input viene eseguita usando un parametro denominato nella firma funzione, ad esempio `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="6eee9-129">`T` è il tipo di dati in cui si vogliono deserializzare i dati e `paramName` è il nome specificato nell'[associazione di input](#input).</span><span class="sxs-lookup"><span data-stu-id="6eee9-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="6eee9-130">Nelle funzioni Node.js si accede all'entità (o alle entità) della tabella di input usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6eee9-131">I dati di input possono essere deserializzati in funzioni Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="6eee9-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="6eee9-132">Gli oggetti deserializzati hanno le proprietà `RowKey` e `PartitionKey`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="6eee9-133">Nelle funzioni C# è anche possibile eseguire l'associazione a uno dei seguenti tipi e il runtime di Funzioni tenterà di deserializzare i dati della tabella usando quel tipo:</span><span class="sxs-lookup"><span data-stu-id="6eee9-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="6eee9-134">Qualsiasi tipo che implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="6eee9-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="6eee9-135">Esempio di input</span><span class="sxs-lookup"><span data-stu-id="6eee9-135">Input sample</span></span>
<span data-ttu-id="6eee9-136">Si supponga di avere il seguente function.json che usa un trigger della coda per leggere una singola riga della tabella.</span><span class="sxs-lookup"><span data-stu-id="6eee9-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="6eee9-137">Il JSON specifica `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="6eee9-138">`"rowKey": "{queueTrigger}"` indica che la chiave di riga proviene dalla stringa di messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="6eee9-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6eee9-139">Vedere l'esempio specifico del linguaggio che legge una singola entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="6eee9-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="6eee9-140">C#</span><span class="sxs-lookup"><span data-stu-id="6eee9-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="6eee9-141">F#</span><span class="sxs-lookup"><span data-stu-id="6eee9-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="6eee9-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="6eee9-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="6eee9-143">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="6eee9-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="6eee9-144">Esempio di input in F#</span><span class="sxs-lookup"><span data-stu-id="6eee9-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="6eee9-145">Esempio di input in Node.js</span><span class="sxs-lookup"><span data-stu-id="6eee9-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="6eee9-146">Associazione di output della tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6eee9-146">Storage table output binding</span></span>
<span data-ttu-id="6eee9-147">L'associazione di output della tabella di Archiviazione di Azure consente di scrivere entità in una tabella di archiviazione della funzione.</span><span class="sxs-lookup"><span data-stu-id="6eee9-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="6eee9-148">L'output della tabella di archiviazione per una funzione usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="6eee9-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="6eee9-149">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="6eee9-149">Note the following:</span></span> 

* <span data-ttu-id="6eee9-150">Usare `partitionKey` e `rowKey` insieme per scrivere una singola entità.</span><span class="sxs-lookup"><span data-stu-id="6eee9-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="6eee9-151">Queste proprietà sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="6eee9-151">These properties are optional.</span></span> <span data-ttu-id="6eee9-152">È possibile specificare `PartitionKey` e `RowKey` anche quando si creano gli oggetti entità nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="6eee9-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="6eee9-153">`connection` deve contenere il nome di un'impostazione app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6eee9-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="6eee9-154">Nel portale di Azure l'editor standard disponibile nella scheda **Integra** configura automaticamente questa impostazione app quando si crea un account di archiviazione o si seleziona un account già esistente.</span><span class="sxs-lookup"><span data-stu-id="6eee9-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="6eee9-155">È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="6eee9-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="6eee9-156">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="6eee9-156">Output usage</span></span>
<span data-ttu-id="6eee9-157">Nelle funzioni C# è possibile eseguire l'associazione all'output della tabella usando il parametro denominato `out` nella firma funzione, ad esempio `out <T> <name>`, dove `T` è il tipo di dati in cui si vuole serializzare i dati e `paramName` è il nome specificato nell'[associazione di output](#output).</span><span class="sxs-lookup"><span data-stu-id="6eee9-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="6eee9-158">Nelle funzioni Node.js si accede all'output della tabella usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="6eee9-159">È possibile serializzare gli oggetti nelle funzioni Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="6eee9-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="6eee9-160">Nelle funzioni C# è anche possibile definire associazioni con i seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="6eee9-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="6eee9-161">Qualsiasi tipo che implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="6eee9-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="6eee9-162">`ICollector<T>` (per restituire più entità,</span><span class="sxs-lookup"><span data-stu-id="6eee9-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="6eee9-163">vedere l'[esempio](#outcsharp)).</span><span class="sxs-lookup"><span data-stu-id="6eee9-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="6eee9-164">`IAsyncCollector<T>` (versione asincrona di `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="6eee9-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="6eee9-165">`CloudTable` (uso di Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="6eee9-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="6eee9-166">vedere l'[esempio](#readmulti)).</span><span class="sxs-lookup"><span data-stu-id="6eee9-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="6eee9-167">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="6eee9-167">Output sample</span></span>
<span data-ttu-id="6eee9-168">L'esempio di *function.json* e *run.csx* seguente illustra come scrivere più entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="6eee9-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6eee9-169">Vedere l'esempio specifico del linguaggio che crea più entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="6eee9-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="6eee9-170">C#</span><span class="sxs-lookup"><span data-stu-id="6eee9-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="6eee9-171">F#</span><span class="sxs-lookup"><span data-stu-id="6eee9-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="6eee9-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6eee9-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="6eee9-173">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="6eee9-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="6eee9-174">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="6eee9-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="6eee9-175">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="6eee9-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="6eee9-176">Esempio: Leggere più entità di tabella in C#</span><span class="sxs-lookup"><span data-stu-id="6eee9-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="6eee9-177">Il codice di esempio di *function.json* e di C# seguente legge le entità per una chiave di partizione specificata nel messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="6eee9-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="6eee9-178">Il codice C# aggiunge un riferimento ad Azure Storage SDK in modo che il tipo di entità possa derivare da `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="6eee9-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="6eee9-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6eee9-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

