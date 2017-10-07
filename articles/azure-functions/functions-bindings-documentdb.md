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
# <a name="azure-functions-cosmos-db-bindings"></a>Binding di Azure Cosmos DB in Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come associazioni di Azure Cosmos DB tooconfigure e codice nelle funzioni di Azure. Funzioni di Azure supporta le associazioni di input e output per Cosmos DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Per ulteriori informazioni su Cosmos DB, vedere [introduzione tooCosmos DB](../documentdb/documentdb-introduction.md) e [compilare un'applicazione console Cosmos DB](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>Binding di input dell'API DocumentDB
associazione di input API DocumentDB Hello recupera un documento DB Cosmos e passa toohello denominato parametro di input della funzione hello. documento Hello che ID può essere determinato in base hello trigger che richiama la funzione hello. 

associazione di input API DocumentDB Hello è hello seguenti proprietà in *function.json*:

- `name`: Nome identificatore nel codice di funzione per il documento hello
- `type`: deve essere impostato troppo "documentdb"
- `databaseName`: database hello contenente il documento hello
- `collectionName`: raccolta hello contenente il documento hello
- `id`: Id di hello documento tooretrieve hello. Questa proprietà supporta i parametri di binding. vedere [associare le proprietà di input toocustom in un'espressione di associazione](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) nell'articolo hello [trigger funzioni di Azure e i concetti di associazioni](functions-triggers-bindings.md).
- `sqlQuery`: una query SQL di Cosmos DB utilizzata per il recupero di più documenti. query Hello supporta le associazioni di runtime. Ad esempio: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: nome hello dell'impostazione di app di hello contenente la stringa di connessione Cosmos DB
- `direction`: deve essere impostato troppo`"in"`.

proprietà Hello `id` e `sqlQuery` non possono essere specificati. Se non si specifica `id` né `sqlQuery` è impostata, hello intero insieme viene recuperato.

## <a name="using-a-documentdb-api-input-binding"></a>Usare un binding di input dell'API DocumentDB

* In c# e funzioni F # quando si esce dalla funzione hello correttamente, tutte le modifiche apportate toohello documento di input tramite parametri di input denominati vengono rese automaticamente persistenti. 
* Nelle funzioni di JavaScript gli aggiornamenti non vengono eseguiti automaticamente al termine della funzione. Utilizzare invece `context.bindings.<documentName>In` e `context.bindings.<documentName>Out` toomake aggiornamenti. Vedere hello [esempio JavaScript](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Esempio di input per il singolo documento
Si supponga di avere seguito hello API DocumentDB input associazione in hello `bindings` matrice function.json:

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

Vedere l'esempio specifico del linguaggio hello che utilizza il valore di testo del documento l'associazione di input tooupdate hello.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Esempio di input in C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Esempio di input in F# #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Questo esempio è necessario un `project.json` file che specifica hello `FSharp.Interop.Dynamic` e `Dynamitey` le dipendenze di NuGet:

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

tooadd un `project.json` file, vedere [gestione dei pacchetti di F #](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Esempio di input in JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Esempio di input con più documenti

Si supponga che si desiderano tooretrieve più documenti specificati da una query SQL, utilizzando i parametri di query una coda trigger toocustomize hello. 

In questo esempio, i trigger di coda hello fornisce un parametro `departmentId`. Un messaggio nella coda di `{ "departmentId" : "Finance" }` restituisce tutti i record per il reparto di contabilità hello. Utilizzare la seguente hello in *function.json*:

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

### <a name="input-sample-with-multiple-documents-in-c"></a>Esempio di input con più documenti in C#

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Esempio di input con più documenti in JavaScript

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

## <a id="docdboutput"></a>Binding di output dell'API DocumentDB
l'associazione consente di scrivere un nuovo database di Azure Cosmos DB tooan documento di output Hello API DocumentDB. Ha hello seguenti proprietà in *function.json*:

- `name`: Identificatore utilizzato nel codice di funzione per il nuovo documento hello
- `type`: deve essere impostato troppo`"documentdb"`
- `databaseName`: database hello contenente hello raccolta in cui verrà creato il nuovo documento di hello.
- `collectionName`: hello raccolta in cui verrà creato il nuovo documento di hello.
- `createIfNotExists`: Un valore booleano tooindicate se verrà creato l'insieme di hello se non esiste. valore predefinito di Hello è *false*. Hello motivo relativo a questa nuova le raccolte vengono create con velocità effettiva riservata con prezzi implicazioni. Per ulteriori informazioni, visitare hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: nome hello dell'impostazione di app di hello contenente la stringa di connessione Cosmos DB
- `direction`: deve essere impostato troppo`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Usare un binding di output dell'API DocumentDB
In questa sezione viene illustrato come toouse l'API DocumentDB output associazione nel codice di funzione.

Quando si scrive il parametro di output toohello nella funzione, per impostazione predefinita, che viene generato un nuovo documento nel database, con un GUID generato automaticamente come hello documento ID. È possibile specificare l'ID documento hello del documento di output specificando hello `id` proprietà JSON in hello parametro di output. 

>[!Note]  
>Quando si specifica l'ID di hello di un documento esistente, si ottiene sovrascritto dal nuovo documento di output hello. 

toooutput più documenti, è anche possibile associare troppo`ICollector<T>` o `IAsyncCollector<T>` dove `T` è uno dei tipi di hello è supportato.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>Esempio di binding di output dell'API DocumentDB
Si supponga di avere seguito hello API DocumentDB output associazione in hello `bindings` matrice function.json:

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

E si dispone di un'associazione di input di coda per una coda che riceve JSON in hello seguente formato:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

E si desidera toocreate DB Cosmos documenti nel seguente formato per ogni record hello:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Vedere l'esempio specifico del linguaggio hello che utilizza il database tooyour di documenti tooadd di associazione di output.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Esempio di output in C# #

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

### <a name="output-sample-in-f"></a>Esempio di output in F# #

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

Questo esempio è necessario un `project.json` file che specifica hello `FSharp.Interop.Dynamic` e `Dynamitey` le dipendenze di NuGet:

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

tooadd un `project.json` file, vedere [gestione dei pacchetti di F #](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Esempio di output in JavaScript

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
