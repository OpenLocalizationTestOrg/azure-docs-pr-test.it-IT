---
title: associazioni di archiviazione della coda funzioni aaaAzure | Documenti Microsoft
description: Comprendere come toouse di archiviazione di Azure attiva e le associazioni in funzioni di Azure.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Associazione dell'archiviazione code di Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene descritto come associazioni di archiviazione Azure coda tooconfigure e codice nelle funzioni di Azure. Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure. Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Trigger per l'archiviazione code
trigger di archiviazione di Azure coda Hello consente si toomonitor di archiviazione di Accodamento di nuovi messaggi e reagire toothem. 

Definire un trigger di coda utilizzando hello **integrazione** scheda nel portale le funzioni hello. portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione. Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.

È possibile specificare impostazioni aggiuntive un [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ottimizzare i trigger di archiviazione della coda. Ad esempio, è possibile modificare l'intervallo di polling della coda hello in host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Uso di un trigger della coda
Nelle funzioni di Node.js, accedere utilizzando dati di hello coda `context.bindings.<name>`.


Nelle funzioni .NET, accedere payload coda hello utilizzando un parametro di metodo, ad esempio `CloudQueueMessage paramName`. In questo caso, `paramName` hello valore specificato in hello [configurazione trigger](#trigger). messaggio della coda può essere deserializzato tooany di hello seguenti tipi:

* Oggetto POCO. Utilizzare se il payload di coda hello è un oggetto JSON. il runtime di funzioni Hello deserializza payload hello in oggetto POCO hello. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Metadati del trigger della coda
trigger coda Hello fornisce diverse proprietà di metadati. Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice. i valori Hello hanno hello stessa semantica [ `CloudQueueMessage` ].

* **QueueTrigger**: payload della coda, se si tratta di una stringa valida
* **DequeueCount**: digitare `int`. Hello numero di volte in cui che il messaggio è stato rimosso dalla coda.
* **ExpirationTime**: digitare `DateTimeOffset?`. tempo di Hello la scadenza di tale messaggio hello.
* **Id**: digitare `string`. ID del messaggio in coda.
* **InsertionTime**: digitare `DateTimeOffset?`. tempo di Hello toohello coda è stato aggiunto il messaggio hello.
* **NextVisibleTime** - Tipo `DateTimeOffset?`. tempo di Hello tale messaggio sarà successivamente visibile.
* **PopReceipt**: digitare `string`. ricezione del messaggio Hello.

Vedere come toouse hello i metadati della coda in [esempio Trigger](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di avere seguito function.json hello che definisce un trigger di coda:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Vedere l'esempio specifico del linguaggio di hello che recupera e registra i metadati della coda.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Esempio di trigger in C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Esempio di trigger in Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Gestione di messaggi della coda non elaborabili
Quando una funzione di attivazione coda ha esito negativo, le funzioni di Azure Ritenta la funzione di toofive volte per un messaggio nella coda specificata, inclusi hello innanzitutto provare. Se tutti e cinque i tentativi hanno esito negativo, il runtime di funzioni hello aggiunge una tooa coda di archiviazione denominata  *&lt;originalqueuename >-non elaborabile*. È possibile scrivere messaggi tooprocess un funzione dalla coda non elaborabile hello registrarle o inviando una notifica che è necessario un intervento manuale. 

i messaggi non elaborabili toohandle controllare manualmente, hello `dequeueCount` di messaggio della coda hello (vedere [i metadati della coda trigger](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Associazione di output dell'archiviazione code
Hello l'archiviazione delle code di Azure output associazione consente toowrite messaggi tooa coda. 

Definire una coda di associazione di output utilizzando hello **integrazione** scheda nel portale le funzioni hello. portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione. Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Uso dell'associazione di output della coda
Nelle funzioni di Node.js, accedere coda di output di hello utilizzando `context.bindings.<name>`.

Nelle funzioni .NET, è possibile creare tooany dei seguenti tipi di hello. Quando è un parametro di tipo `T`, `T` deve essere uno dei tipi di output di hello è supportato, ad esempio `string` o un POCO.

* `out T`, serializzato come JSON
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

È inoltre possibile utilizzare il tipo restituito del metodo di hello come hello associazione di output.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Esempio di output in coda
esempio Hello *function.json* definisce un trigger HTTP e una coda di associazione di output:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Vedere l'esempio specifico del linguaggio hello che restituisce un messaggio nella coda con payload HTTP in ingresso hello.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Esempio di output della coda in C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

toosend più messaggi, utilizzare un `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Esempio di output della coda in Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

In alternativa, toosend più messaggi,

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Passaggi successivi

Per un esempio di una funzione che utilizza i trigger di archiviazione della coda e le associazioni, vedere [un tooan funzione Azure connesso il servizio di Azure creare](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
