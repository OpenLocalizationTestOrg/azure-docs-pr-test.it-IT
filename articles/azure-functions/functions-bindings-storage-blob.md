---
title: associazioni di funzioni di archiviazione Blob aaaAzure | Documenti Microsoft
description: Comprendere come toouse di archiviazione di Azure attiva e le associazioni in funzioni di Azure.
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
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Binding dell'archiviazione BLOB di Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di archiviazione Blob di Azure in funzioni di Azure. Funzioni di Azure supporta i trigger e le associazioni di input e di output per l'archiviazione BLOB di Azure. Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> Non sono supportati [account di archiviazione solo BLOB](../storage/common/storage-create-storage-account.md#blob-storage-accounts). I trigger e le associazioni di archiviazione BLOB richiedono un account di archiviazione generico. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Trigger e associazioni do archiviazione BLOB

Utilizzo di trigger di archiviazione Blob di Azure hello, il codice della funzione viene chiamato quando viene rilevato un blob nuovo o aggiornato. contenuto del blob Hello viene forniti come input toohello funzione.

Definire un trigger di archiviazione blob utilizzando hello **integrazione** scheda nel portale le funzioni hello. portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

BLOB di input e output associazioni vengono definite utilizzando `blob` come tipo di associazione hello:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Hello `path` proprietà supporta l'associazione di espressioni e parametri di filtro. Vedere [Modelli di nome](#pattern).
* Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione. Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.

> [!NOTE]
> Quando si utilizza un trigger di blob in un piano di utilizzo, in può essere presente di ritardo di 10 minuti tooa l'elaborazione di nuovi BLOB dopo che un'app di funzione è diventato inattiva. Dopo l'applicazione di funzione hello è in esecuzione, i BLOB vengono elaborati immediatamente. tooavoid iniziale di questo ritardo, considerare una delle seguenti opzioni hello:
> - Usare un piano di servizio app con l'opzione Always On abilitata.
> - Utilizzare un altro blob di hello tootrigger meccanismo di elaborazione, ad esempio un messaggio nella coda che contiene il nome di blob hello. Per un esempio, vedere il [Queue trigger with blob input binding](#input-sample) (Trigger della coda con associazione di input del BLOB).

<a name="pattern"></a>

### <a name="name-patterns"></a>Modelli di nome
È possibile specificare un modello di nome di blob in hello `path` proprietà, che può essere un'espressione di filtro o di associazione. Vedere [Modelli ed espressioni di associazione](functions-triggers-bindings.md#binding-expressions-and-patterns).

Tooblobs toofilter che iniziano con una stringa hello "originale", ad esempio, utilizzare hello seguente definizione. Questo percorso consente di individuare un blob denominato *originale Blob1.txt* in hello *input* contenitore e il valore di hello di hello `name` variabile nel codice della funzione è `Blob1`.

```json
"path": "input/original-{name}",
```

estensione e il nome di file blob toohello toobind separatamente, usare due modelli. Questo percorso consente anche di trovare un blob denominato *originale Blob1.txt*e il valore di hello di hello `blobname` e `blobextension` variabili nel codice della funzione vengono *originale Blob1* e *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

È possibile limitare il tipo di file hello del BLOB utilizzando un valore fisso per l'estensione del file hello. Ad esempio, tootrigger solo per i file con estensione png, utilizzare hello seguente modello:

```json
"path": "samples/{name}.png",
```

Le parentesi graffe sono caratteri speciali nei modelli di nome. i nomi di blob toospecify con parentesi graffe nel nome di hello, fare in modo che le parentesi graffe hello utilizzando due parentesi graffe. esempio Hello trova un blob denominato *{20140101}-soundfile.mp3* in hello *immagini* contenitore e hello `name` valore della variabile nel codice della funzione hello è  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Metadati del trigger

i trigger di blob Hello fornisce diverse proprietà di metadati. Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice. Questi valori hanno hello stessa semantica [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Digitare `string`. percorso blob attivazione Hello
- **Uri**. Digitare `System.Uri`. URI del blob Hello posizione primaria hello.
- **Properties**. Digitare `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. salve le proprietà di sistema del blob.
- **Metadata**. Digitare `IDictionary<string,string>`. Hello metadati definiti dall'utente per il blob hello.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Conferme di BLOB
Funzioni di Azure Hello runtime garantisce che nessuna funzione trigger blob viene chiamata più volte per hello nello stesso blob nuovo o aggiornato. toodetermine se è stata elaborata una versione di blob specificato, viene mantenuta *blob conferme di recapito*.

Blob di Azure archivi funzioni conferme di recapito in un contenitore denominato *ospita-processi Web di azure* nell'account di archiviazione di Azure per l'app di funzione hello (definito dall'impostazione di app hello `AzureWebJobsStorage`). Un carico di blob è hello le seguenti informazioni:

* Hello attivato funzione ("*&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*", ad esempio:"MyFunctionApp.Functions.CopyBlob")
* nome del contenitore Hello
* tipo di blob Hello ("BlockBlob" o "PageBlob")
* nome del blob Hello
* Hello ETag (un identificatore di versione del blob, ad esempio: "0x8D1DC6E70A277EF")

conferma di blob hello per tale blob tooforce rielaborazione di un blob, eliminare hello *ospita-processi Web di azure* contenitore manualmente.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Gestione di BLOB non elaborabili
Se una funzione di trigger del BLOB ha esito negativo per un determinato BLOB, per impostazione predefinita Funzioni di Azure ritenta l'esecuzione fino a 5 volte. 

Se non tutti i tentativi di 5, le funzioni di Azure consente di aggiungere una coda di archiviazione tooa messaggio denominata *non elaborabili processi Web-blobtrigger*. messaggio della coda Hello per i BLOB non elaborabile è un oggetto JSON contenente hello le proprietà seguenti:

* FunctionId (in formato hello  *&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*)
* BlobType ("BlockBlob" o "PageBlob")
* ContainerName
* BlobName
* ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>Polling dei BLOB per contenitori di grandi dimensioni
Se il contenitore di blob hello monitorato contiene più di 10.000 BLOB, hello toowatch funzioni runtime analisi log file per i BLOB nuovo o modificato. Questo processo non avviene in tempo reale. Una funzione potrebbe non viene generata finché diversi minuti o più dopo aver creato il blob hello. Per di più [i log di archiviazione vengono creati in base al principio del "massimo sforzo"](/rest/api/storageservices/About-Storage-Analytics-Logging). Non è garantito che tutti gli eventi vengano acquisiti. In alcune condizioni, l'acquisizione dei log può non riuscire. Se è necessaria un'elaborazione di blob più veloce o più affidabile, è consigliabile creare un [messaggio della coda](../storage/queues/storage-dotnet-how-to-use-queues.md) quando si crea il blob hello. Quindi, usare un [trigger coda](functions-bindings-storage-queue.md) invece di un blob di hello tooprocess trigger blob.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Uso di un trigger di BLOB e dell'associazione di input
Nelle funzioni .NET, accedere ai dati di blob hello utilizzando un parametro di metodo, ad esempio `Stream paramName`. In questo caso, `paramName` hello valore specificato in hello [configurazione trigger](#trigger). Nelle funzioni di Node.js, hello accesso input di dati blob utilizzando `context.bindings.<name>`.

In .NET, è possibile associare tooany dei tipi di hello in hello in basso. Se usati come associazione di input, alcuni di questi tipi richiedono una direzione di associazione `inout` in *function.json*. Questa direzione non è supportata dall'editor standard hello, pertanto è necessario utilizzare hello editor avanzato.

* `TextReader`
* `Stream`
* `ICloudBlob`, è necessaria la direzione di associazione "inout"
* `CloudBlockBlob`, è necessaria la direzione di associazione "inout"
* `CloudPageBlob`, è necessaria la direzione di associazione "inout"
* `CloudAppendBlob`, è necessaria la direzione di associazione "inout"

Se si prevede che il BLOB di testo, è anche possibile associare .NET tooa `string` tipo. È consigliato solo se dimensioni blob hello sono ridotto, in quanto hello intero contenuto del blob viene caricati in memoria. In genere, è preferibile toouse un `Stream` o `CloudBlockBlob` tipo.

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di che avere hello function.json che definisce un trigger di archiviazione blob di seguito:

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

Vedere l'esempio specifico del linguaggio hello che registra il contenuto di hello di ogni blob che viene aggiunto toohello monitorato contenitore.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Esempi di trigger BLOB in C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Esempio di trigger in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Uso dell'associazione di output nel BLOB

Nelle funzioni .NET, è necessario utilizzare un `out string` parametro la firma della funzione o utilizzare uno dei tipi di hello in hello seguente elenco. Nelle funzioni di Node.js, accedere hello output blob utilizzando `context.bindings.<name>`.

Nelle funzioni .NET è possibile output tooany di hello seguenti tipi:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Trigger di coda con esempio di input e output del BLOB
Si supponga di avere seguito function.json hello, che definisce un [trigger di archiviazione delle code](functions-bindings-storage-queue.md), un'archiviazione blob di input e output di un'archiviazione blob. Utilizzo di hello preavviso di hello `queueTrigger` proprietà dei metadati. hello BLOB di input e output `path` proprietà:

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

Vedere l'esempio specifico del linguaggio hello che copia hello blob di input toohello output blob.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Esempio di associazione del BLOB in C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Esempio di associazione del BLOB in Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

