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
# <a name="azure-functions-storage-table-bindings"></a>Associazioni della tabella di archiviazione di Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo spiega come codice di archiviazione di Azure e tooconfigure tabella associazioni nelle funzioni di Azure. Funzioni di Azure supporta le associazioni di input e output per le tabelle di Archiviazione di Azure.

associazione di Hello archiviazione tabella supporta hello seguenti scenari:

* **Leggere una singola riga in una funzione C# o Node.js**: impostare `partitionKey` e `rowKey`. Hello `filter` e `take` proprietà non vengono utilizzate in questo scenario.
* **Lettura di più righe in una funzione c#** -hello funzioni runtime fornisce un `IQueryable<T>` oggetto associato toohello tabella. Il tipo `T` deve derivare da `TableEntity` o implementare `ITableEntity`. Hello `partitionKey`, `rowKey`, `filter`, e `take` proprietà non vengono utilizzate in questo scenario, è possibile utilizzare hello `IQueryable` oggetto toodo eventuali filtri necessari. 
* **Lettura di più righe in una funzione di nodo** - hello impostare `filter` e `take` proprietà. Non impostare `partitionKey` o `rowKey`.
* **Scrivere una o più righe in una funzione c#** -hello funzioni runtime fornisce un `ICollector<T>` o `IAsyncCollector<T>` tabella toohello associato, in cui `T` specifica dello schema hello di entità hello desiderato tooadd. In genere, ma non necessariamente, il tipo `T` deriva da `TableEntity` o implementa `ITableEntity`. Hello `partitionKey`, `rowKey`, `filter`, e `take` proprietà non vengono utilizzate in questo scenario.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Associazione di input della tabella di archiviazione
Hello associazione di input nella tabella di archiviazione di Azure consente toouse nella funzione di una tabella di archiviazione. 

funzione di archiviazione tabella tooa input Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:

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

Si noti hello segue: 

* Utilizzare `partitionKey` e `rowKey` tooread insieme una singola entità. Queste proprietà sono facoltative. 
* `connection`deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione. Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per utente quando si crea uno spazio di archiviazione dell'account o si seleziona uno esistente. È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso dell'input
In c# le funzioni, associare toohello input tabella (o più entità) tramite un parametro denominato nella firma di funzione, come `<T> <name>`.
Dove `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è il nome di hello è specificato in hello [associazione di input](#input). Nelle funzioni di Node.js, accedere hello input tabella entità o entità mediante `context.bindings.<name>`.

dati di input Hello possono essere deserializzati in funzioni di Node.js o c#. oggetti Hello deserializzato `RowKey` e `PartitionKey` proprietà.

In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e di funzioni hello runtime tenterà deserializzare troppo mediante quel tipo di dati della tabella hello:

* Qualsiasi tipo che implementa `ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Esempio di input
Si supponga di che aver hello function.json, che utilizza un tooread trigger coda una riga nella tabella seguente. Specifica Hello JSON `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`indica che la chiave di riga hello proviene dalla stringa di messaggio hello coda.

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

Vedere l'esempio specifico del linguaggio hello che legge una tabella singola entità.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Esempio di input in C# #
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

### <a name="input-sample-in-f"></a>Esempio di input in F# #
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

### <a name="input-sample-in-nodejs"></a>Esempio di input in Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Associazione di output della tabella di archiviazione
associazione consente di tabella di archiviazione tooa entità toowrite nella funzione di output Hello tabella di archiviazione di Azure. 

Hello output di tabella di archiviazione per una funzione utilizza i seguenti oggetti JSON in hello hello `bindings` matrice function.json:

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

Si noti hello segue: 

* Utilizzare `partitionKey` e `rowKey` toowrite insieme una singola entità. Queste proprietà sono facoltative. È inoltre possibile specificare `PartitionKey` e `RowKey` quando si crea hello oggetti entità nel codice di funzione.
* `connection`deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione. Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per utente quando si crea uno spazio di archiviazione dell'account o si seleziona uno esistente. È anche possibile [configurare questa impostazione dell'app manualmente](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso dell'output
In c# le funzioni, associare output tabella toohello utilizzando hello denominato `out` parametro nella firma di funzione, ad esempio `out <T> <name>`, dove `T` è che si desidera tooserialize hello dati del tipo di dati hello e `paramName` è hello nome specificato in hello [associazione di output](#output). Nelle funzioni di Node.js, si accede tabella di hello output utilizzando `context.bindings.<name>`.

È possibile serializzare gli oggetti nelle funzioni Node.js o C#. In c# le funzioni, è anche possibile associare toohello seguenti tipi:

* Qualsiasi tipo che implementa `ITableEntity`
* `ICollector<T>`(toooutput più entità. vedere l'[esempio](#outcsharp)).
* `IAsyncCollector<T>` (versione asincrona di `ICollector<T>`)
* `CloudTable`(tramite hello Azure Storage SDK. vedere l'[esempio](#readmulti)).

<a name="outputsample"></a>

## <a name="output-sample"></a>Esempio di output
esempio Hello *function.json* e *run.csx* esempio viene illustrato come toowrite più entità di tabella.

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

Vedere l'esempio specifico del linguaggio hello che crea più entità di tabella.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Esempio di output in C# #
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

### <a name="output-sample-in-f"></a>Esempio di output in F# #
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

### <a name="output-sample-in-nodejs"></a>Esempio di output in Node.js
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

## <a name="sample-read-multiple-table-entities-in-c"></a>Esempio: Leggere più entità di tabella in C#  #
esempio Hello *function.json* ed esempio di codice c# legge le entità per una chiave di partizione specificato nel messaggio della coda hello.

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

codice c# di Hello aggiunge toohello un riferimento Azure Storage SDK in modo che il tipo di entità hello può derivare da `TableEntity`.

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

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

