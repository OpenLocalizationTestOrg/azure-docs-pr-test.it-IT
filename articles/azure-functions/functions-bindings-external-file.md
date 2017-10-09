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
# <a name="azure-functions-external-file-bindings-preview"></a>Associazioni di file esterni in Funzioni di Azure (Anteprima)
Questo articolo illustra come file toomanipulate da SaaS diversi provider (ad esempio, OneDrive, Dropbox) all'interno della funzione che utilizzano associazioni predefinite. Funzioni di Azure supporta il trigger e le associazioni di output per i file esterni.

Questa associazione consente di creare connessioni API tooSaaS provider oppure Usa connessioni API esistenti dal gruppo di risorse dell'applicazione (funzione).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Connessioni di file supportate

|Connettore|Trigger|Input|Output|
|:-----|:---:|:---:|:---:|
|[Box](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive for Business](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> È possibile usare le connessioni ai file esterni anche in [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Associazione di trigger di file esterni

i trigger di file esterno Azure Hello consente di monitorare una cartella remota ed eseguire il codice di funzione, quando vengono rilevate modifiche.

i trigger di file esterno Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json

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

### <a name="name-patterns"></a>Modelli di nome
È possibile specificare un modello di nome file in hello `path` proprietà. cartella Hello a cui fa riferimento deve essere presente nel provider SaaS hello.
Esempi:

```json
"path": "input/original-{name}",
```

Questo percorso potrebbe trovare un file denominato *originale File1.txt* in hello *input* cartella e il valore di hello di hello `name` variabile nel codice della funzione sarebbe `File1.txt`.

Un altro esempio:

```json
"path": "input/{filename}.{fileextension}",
```

Questo percorso potrebbe anche trovare un file denominato *originale File1.txt*e il valore di hello di hello `filename` e `fileextension` variabili nel codice della funzione sarebbe *originale File1* e  *txt*.

È possibile limitare il tipo di file hello del file con un valore fisso per l'estensione del file hello. ad esempio:

```json
"path": "samples/{name}.png",
```

In questo caso, solo *PNG* file hello *esempi* funzione hello trigger di cartella.

Le parentesi graffe sono caratteri speciali nei modelli di nome. i nomi di file toospecify con doppie parentesi graffe in nome hello hello parentesi graffe.
ad esempio:

```json
"path": "images/{{20140101}}-{name}",
```

Questo percorso potrebbe trovare un file denominato *{20140101}-soundfile.mp3* in hello *immagini* cartella e hello `name` valore variabile nel codice della funzione hello sarebbe *soundfile.mp3*.

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

### <a name="handling-poison-files"></a>Gestione di file non elaborabili
Quando una funzione di attivazione di file esterno ha esito negativo, tale funzione too5 ore di funzioni di Azure tentativi per impostazione predefinita (inclusi provare prima a hello) per un determinato file.
Se non tutti i tentativi di 5, le funzioni aggiunge una coda di archiviazione tooa messaggio denominata *non elaborabili processi Web-apihubtrigger*. messaggio della coda Hello per i file di messaggi non elaborabili è un oggetto JSON contenente hello le proprietà seguenti:

* FunctionId (in formato hello  *&lt;nome della funzione app >*. Funzioni.  *&lt;nome funzione >*)
* FileType
* FolderName
* FileName
* ETag (identificatore di versione del file, ad esempio: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso dei trigger
In c# le funzioni, è associare i dati di file di input toohello tramite un parametro denominato nella firma di funzione, come `<T> <name>`.
In cui `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è specificato nel nome di hello il [attivare JSON](#trigger). Nelle funzioni di Node.js, si accede a dati di file di input hello tramite `context.bindings.<name>`.

file Hello può essere deserializzato in uno dei seguenti tipi di hello:

* Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.
  Se si dichiara un tipo di input personalizzato (ad esempio `FooType`), le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.
* Stringa: utile per i dati del file di testo.

In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e hello funzioni runtime tenta di deserializzare mediante quel tipo di dati del file hello:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di avere seguito function.json hello, che definisce un trigger di file esterno:

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

Vedere l'esempio specifico del linguaggio hello che registra il contenuto di hello di ogni file che viene aggiunta una cartella monitorata toohello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Uso dei trigger in C# #

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

### <a name="trigger-usage-in-nodejs"></a>Uso dei trigger in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Associazione di input di file esterni
associazione di input di file esterno Azure Hello consente toouse un file da una cartella in una funzione esterna.

funzione di file esterno tooa input Hello utilizza hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Si noti hello segue:

* `path`deve contenere il nome di cartella hello e nome del file hello. Ad esempio, se dispone di un [trigger coda](functions-bindings-storage-queue.md) nella funzione, è possibile utilizzare `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file hello `samples-workitems` cartella con un nome che corrisponde al nome file hello specificato nel messaggio hello del trigger.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso dell'input
In c# le funzioni, è associare i dati di file di input toohello tramite un parametro denominato nella firma di funzione, come `<T> <name>`.
In cui `T` è che si desidera toodeserialize hello dati del tipo di dati hello e `paramName` è specificato nel nome di hello il [associazione di input](#input). Nelle funzioni di Node.js, si accede a dati di file di input hello tramite `context.bindings.<name>`.

file Hello può essere deserializzato in uno dei seguenti tipi di hello:

* Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati dei file serializzati con JSON.
  Se si dichiara un tipo di input personalizzato (ad esempio `InputType`), le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.
* Stringa: utile per i dati del file di testo.

In c# le funzioni, è anche possibile associare tooany dei seguenti tipi di hello e hello funzioni runtime tenta di deserializzare mediante quel tipo di dati del file hello:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Associazione di output di file esterni
associazione consente cartella esterna toowrite file tooan nella funzione di output Hello Azure file esterno.

file esterni di Hello di output per una funzione utilizza i seguenti oggetti JSON in hello hello `bindings` matrice function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Si noti hello segue:

* `path`deve contenere il nome di cartella hello e toowrite di nome file hello per. Ad esempio, se dispone di un [trigger coda](functions-bindings-storage-queue.md) nella funzione, è possibile utilizzare `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file hello `samples-workitems` cartella con un nome che corrisponde al nome file hello specificato nel messaggio hello del trigger.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso dell'output
In c# le funzioni, associare il file di output toohello utilizzando hello denominato `out` parametro nella firma di funzione, ad esempio `out <T> <name>`, dove `T` è che si desidera tooserialize hello dati del tipo di dati hello e `paramName` è hello nome specificato nella [associazione di output](#output). Nelle funzioni di Node.js, si accedere ai file di output di hello utilizzando `context.bindings.<name>`.

È possibile scrivere il file di output toohello utilizzando uno dei seguenti tipi di hello:

* Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx), utile per la serializzazione con JSON.
  Se si dichiara un tipo di output personalizzato (ad esempio `out OutputType paramName`), le funzioni di Azure tenta tooserialize oggetto in JSON. Se il parametro di output di hello è null quando si esce dalla funzione hello, hello funzioni runtime crea un file come un oggetto null.
* Stringa: `out string paramName`utile per i dati del file di testo. Hello funzioni runtime crea un file solo se il parametro della stringa non null quando si esce dalla funzione hello.

In c# le funzioni può inoltre restituire tooany di hello seguenti tipi:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Esempio di input e output
Si supponga di avere seguito function.json hello, che definisce un [trigger coda di archiviazione](functions-bindings-storage-queue.md), un file esterno di input e output di un file esterno:

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

Vedere l'esempio specifico del linguaggio hello che copia i file di output toohello hello file di input.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Utilizzo in C# #

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

### <a name="usage-in-nodejs"></a>Uso in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
