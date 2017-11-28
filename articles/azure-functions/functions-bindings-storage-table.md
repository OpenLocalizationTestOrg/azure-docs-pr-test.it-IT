---
title: associazioni di tabella di archiviazione funzioni aaaAzure | Documenti Microsoft
description: Comprendere come le associazioni di archiviazione di Azure toouse nelle funzioni di Azure.
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
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="fdce4-104">Associazioni della tabella di archiviazione di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="fdce4-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fdce4-105">Questo articolo spiega come codice di archiviazione di Azure e tooconfigure tabella associazioni nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdce4-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="fdce4-106">Funzioni di Azure supporta le associazioni di input e output per le tabelle di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdce4-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="fdce4-107">associazione di Hello archiviazione tabella supporta hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="fdce4-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="fdce4-108">**Leggere una singola riga in una funzione C# o Node.js**: impostare `partitionKey` e `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="fdce4-109">Hello `filter` e `take` proprietà non vengono utilizzate in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="fdce4-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="fdce4-110">**Lettura di più righe in una funzione c#** -hello funzioni runtime fornisce un `IQueryable<T>` oggetto associato toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="fdce4-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="fdce4-111">Il tipo `T` deve derivare da `TableEntity` o implementare `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="fdce4-112">Hello `partitionKey`, `rowKey`, `filter`, e `take` proprietà non vengono utilizzate in questo scenario, è possibile utilizzare hello `IQueryable` oggetto toodo eventuali filtri necessari.</span><span class="sxs-lookup"><span data-stu-id="fdce4-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="fdce4-113">**Lettura di più righe in una funzione di nodo** - hello impostare `filter` e `take` proprietà.</span><span class="sxs-lookup"><span data-stu-id="fdce4-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="fdce4-114">Non impostare `partitionKey` o `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="fdce4-115">**Scrivere una o più righe in una funzione c#** -hello funzioni runtime fornisce un `ICollector<T>` o `IAsyncCollector<T>` tabella toohello associato, in cui `T` specifica dello schema hello di entità hello desiderato tooadd.</span><span class="sxs-lookup"><span data-stu-id="fdce4-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="fdce4-116">In genere, ma non necessariamente, il tipo `T` deriva da `TableEntity` o implementa `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="fdce4-117">Hello `partitionKey`, `rowKey`, `filter`, e `take` proprietà non vengono utilizzate in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="fdce4-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="fdce4-118">Associazione di input della tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="fdce4-118">Storage table input binding</span></span>
<span data-ttu-id="fdce4-119">Hello associazione di input nella tabella di archiviazione di Azure consente toouse nella funzione di una tabella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fdce4-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="fdce4-120">funzione di archiviazione tabella tooa input Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="fdce4-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="fdce4-121">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="fdce4-121">Note hello following:</span></span> 

* <span data-ttu-id="fdce4-122">Utilizzare `partitionKey` e `rowKey` tooread insieme una singola entità.</span><span class="sxs-lookup"><span data-stu-id="fdce4-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="fdce4-123">Queste proprietà sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="fdce4-123">These properties are optional.</span></span> 
* <span data-ttu-id="fdce4-124">`connection`deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fdce4-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fdce4-125">Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per utente quando si crea uno spazio di archiviazione dell'account o si seleziona uno esistente.</span><span class="sxs-lookup"><span data-stu-id="fdce4-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="fdce4-126">È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="fdce4-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="fdce4-127">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="fdce4-127">Input usage</span></span>
<span data-ttu-id="fdce4-128">In c# le funzioni, associare toohello input tabella (o più entità) tramite un parametro denominato nella firma di funzione, come `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="fdce4-129">Dove `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è il nome di hello è specificato in hello [associazione di input](#input).</span><span class="sxs-lookup"><span data-stu-id="fdce4-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="fdce4-130">Nelle funzioni di Node.js, accedere hello input tabella entità o entità mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="fdce4-131">dati di input Hello possono essere deserializzati in funzioni di Node.js o c#.</span><span class="sxs-lookup"><span data-stu-id="fdce4-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="fdce4-132">oggetti Hello deserializzato `RowKey` e `PartitionKey` proprietà.</span><span class="sxs-lookup"><span data-stu-id="fdce4-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="fdce4-133">In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e di funzioni hello runtime tenterà deserializzare troppo mediante quel tipo di dati della tabella hello:</span><span class="sxs-lookup"><span data-stu-id="fdce4-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="fdce4-134">Qualsiasi tipo che implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="fdce4-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="fdce4-135">Esempio di input</span><span class="sxs-lookup"><span data-stu-id="fdce4-135">Input sample</span></span>
<span data-ttu-id="fdce4-136">Si supponga di che aver hello function.json, che utilizza un tooread trigger coda una riga nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="fdce4-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="fdce4-137">Specifica Hello JSON `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="fdce4-138">`"rowKey": "{queueTrigger}"`indica che la chiave di riga hello proviene dalla stringa di messaggio hello coda.</span><span class="sxs-lookup"><span data-stu-id="fdce4-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="fdce4-139">Vedere l'esempio specifico del linguaggio hello che legge una tabella singola entità.</span><span class="sxs-lookup"><span data-stu-id="fdce4-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="fdce4-140">C#</span><span class="sxs-lookup"><span data-stu-id="fdce4-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="fdce4-141">F#</span><span class="sxs-lookup"><span data-stu-id="fdce4-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="fdce4-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="fdce4-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="fdce4-143">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="fdce4-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="fdce4-144">Esempio di input in F#</span><span class="sxs-lookup"><span data-stu-id="fdce4-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="fdce4-145">Esempio di input in Node.js</span><span class="sxs-lookup"><span data-stu-id="fdce4-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="fdce4-146">Associazione di output della tabella di archiviazione</span><span class="sxs-lookup"><span data-stu-id="fdce4-146">Storage table output binding</span></span>
<span data-ttu-id="fdce4-147">associazione consente di tabella di archiviazione tooa entità toowrite nella funzione di output Hello tabella di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdce4-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="fdce4-148">Hello output di tabella di archiviazione per una funzione utilizza i seguenti oggetti JSON in hello hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="fdce4-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="fdce4-149">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="fdce4-149">Note hello following:</span></span> 

* <span data-ttu-id="fdce4-150">Utilizzare `partitionKey` e `rowKey` toowrite insieme una singola entità.</span><span class="sxs-lookup"><span data-stu-id="fdce4-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="fdce4-151">Queste proprietà sono facoltative.</span><span class="sxs-lookup"><span data-stu-id="fdce4-151">These properties are optional.</span></span> <span data-ttu-id="fdce4-152">È inoltre possibile specificare `PartitionKey` e `RowKey` quando si crea hello oggetti entità nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="fdce4-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="fdce4-153">`connection`deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fdce4-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fdce4-154">Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per utente quando si crea uno spazio di archiviazione dell'account o si seleziona uno esistente.</span><span class="sxs-lookup"><span data-stu-id="fdce4-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="fdce4-155">È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="fdce4-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="fdce4-156">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="fdce4-156">Output usage</span></span>
<span data-ttu-id="fdce4-157">In c# le funzioni, associare output tabella toohello utilizzando hello denominato `out` parametro nella firma di funzione, ad esempio `out <T> <name>`, dove `T` è che si desidera tooserialize hello dati del tipo di dati hello e `paramName` è hello nome specificato in hello [associazione di output](#output).</span><span class="sxs-lookup"><span data-stu-id="fdce4-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="fdce4-158">Nelle funzioni di Node.js, si accede tabella di hello output utilizzando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="fdce4-159">È possibile serializzare gli oggetti nelle funzioni Node.js o C#.</span><span class="sxs-lookup"><span data-stu-id="fdce4-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="fdce4-160">In c# le funzioni, è anche possibile associare toohello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="fdce4-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="fdce4-161">Qualsiasi tipo che implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="fdce4-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="fdce4-162">`ICollector<T>`(toooutput più entità.</span><span class="sxs-lookup"><span data-stu-id="fdce4-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="fdce4-163">vedere l'[esempio](#outcsharp)).</span><span class="sxs-lookup"><span data-stu-id="fdce4-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="fdce4-164">`IAsyncCollector<T>` (versione asincrona di `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="fdce4-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="fdce4-165">`CloudTable`(tramite hello Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="fdce4-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="fdce4-166">vedere l'[esempio](#readmulti)).</span><span class="sxs-lookup"><span data-stu-id="fdce4-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="fdce4-167">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="fdce4-167">Output sample</span></span>
<span data-ttu-id="fdce4-168">esempio Hello *function.json* e *run.csx* esempio viene illustrato come toowrite più entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="fdce4-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="fdce4-169">Vedere l'esempio specifico del linguaggio hello che crea più entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="fdce4-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="fdce4-170">C#</span><span class="sxs-lookup"><span data-stu-id="fdce4-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="fdce4-171">F#</span><span class="sxs-lookup"><span data-stu-id="fdce4-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="fdce4-172">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fdce4-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="fdce4-173">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="fdce4-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="fdce4-174">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="fdce4-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="fdce4-175">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="fdce4-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="fdce4-176">Esempio: Leggere più entità di tabella in C#</span><span class="sxs-lookup"><span data-stu-id="fdce4-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="fdce4-177">esempio Hello *function.json* ed esempio di codice c# legge le entità per una chiave di partizione specificato nel messaggio della coda hello.</span><span class="sxs-lookup"><span data-stu-id="fdce4-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="fdce4-178">codice c# di Hello aggiunge toohello un riferimento Azure Storage SDK in modo che il tipo di entità hello può derivare da `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="fdce4-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fdce4-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdce4-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

