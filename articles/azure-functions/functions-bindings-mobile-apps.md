---
title: associazioni di App per dispositivi mobili funzioni aaaAzure | Documenti Microsoft
description: Comprendere come le associazioni di App mobili di Azure toouse nelle funzioni di Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Associazioni di app per dispositivi mobili in Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come tooconfigure e codice [App mobili di Azure](../app-service-mobile/app-service-mobile-value-prop.md) associazioni nelle funzioni di Azure. Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili.

Hello App per dispositivi mobili di input e output associazioni consentono di [leggere e scrivere nelle tabelle toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in app per dispositivi mobili.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Associazione di input di App per dispositivi mobili
associazione di input di App per dispositivi mobili Hello carica un record da un endpoint di tabella per dispositivi mobili e lo passa la funzione. In c# e F # funzioni, qualsiasi record di toohello le modifiche apportate vengono inviati automaticamente toohello indietro tabella quando si esce dalla funzione hello correttamente.

App per dispositivi mobili Hello input tooa funzione Usa hello seguente oggetto JSON nella hello `bindings` matrice function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Si noti hello segue:

* `id`può essere statico o può essere basato su trigger hello che richiama la funzione hello. Ad esempio, se si utilizza un [trigger coda]() per la funzione, quindi `"id": "{queueTrigger}"` utilizza hello il valore di stringa di messaggio della coda hello come hello tooretrieve ID record.
* `connection`deve contenere il nome di hello di un'impostazione di app nell'app (funzione), che a sua volta contiene hello URL dell'app per dispositivi mobili. funzione Hello utilizza questa operazioni REST di URL tooconstruct hello necessario su app mobile. Si [creare un'impostazione dell'app nell'app funzione]() che contiene l'URL dell'app mobile (che è simile `http://<appname>.azurewebsites.net`), quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà l'associazione di input. 
* È necessario toospecify `apiKey` se si [implementare una chiave API nel back-end dell'app mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementare una chiave API nel back-end dell'app mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, si [creare un'impostazione dell'app nell'app funzione]() che contiene la chiave API hello, quindi aggiungere hello `apiKey` proprietà l'associazione di input con il nome di hello dell'impostazione di app hello. 
  
  > [!IMPORTANT]
  > Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili. Deve solo essere distribuiti i client di lato tooservice in modo sicuro, come le funzioni di Azure. 
  > 
  > [!NOTE]
  > Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente. In questo modo viene garantita la protezione delle informazioni riservate.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso dell'input
In questa sezione viene illustrato come toouse App Mobile di input di associazione nel codice di funzione. 

Quando il record di hello con hello specificato ID di tabella e il record è disponibile, viene passato a hello denominato [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametro (o, in Node.js, viene passato a hello `context.bindings.<name>` oggetto). Quando i record di hello non viene trovato, il parametro hello è `null`. 

Nelle funzioni di c# e F #, tutte le modifiche apportate ai record di input toohello (parametro di input) viene inviato automaticamente toohello back-tabella di App per dispositivi mobili quando si esce dalla funzione hello correttamente. Nelle funzioni di Node.js, utilizzare `context.bindings.<name>` tooaccess hello record di input. In Node.js, inoltre, non è possibile modificare i record.

<a name="inputsample"></a>

## <a name="input-sample"></a>Esempio di input
Si supponga di avere seguito function.json hello, che consente di recuperare un record della tabella con id messaggio di attivazione coda hello hello App per dispositivi mobili:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Vedere l'esempio specifico del linguaggio hello che utilizza i record di input hello dall'associazione hello. esempi di c# e F # Hello inoltre modifichino record di hello `text` proprietà.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Esempio di input in C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Esempio di input in Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Associazione di output di App per dispositivi mobili
Utilizzare hello App per dispositivi mobili output associazione toowrite un nuovo endpoint di tabella tooa record App per dispositivi mobili.  

App per dispositivi mobili di output per una funzione utilizza hello seguente oggetto JSON nella hello Hello `bindings` matrice function.json:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Si noti hello segue:

* `connection`deve contenere il nome di hello di un'impostazione di app nell'app (funzione), che a sua volta contiene hello URL dell'app per dispositivi mobili. funzione Hello utilizza questa operazioni REST di URL tooconstruct hello necessario su app mobile. Si [creare un'impostazione dell'app nell'app funzione]() che contiene l'URL dell'app mobile (che è simile `http://<appname>.azurewebsites.net`), quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà l'associazione di input. 
* È necessario toospecify `apiKey` se si [implementare una chiave API nel back-end dell'app mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementare una chiave API nel back-end dell'app mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, si [creare un'impostazione dell'app nell'app funzione]() che contiene la chiave API hello, quindi aggiungere hello `apiKey` proprietà l'associazione di input con il nome di hello dell'impostazione di app hello. 
  
  > [!IMPORTANT]
  > Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili. Deve solo essere distribuiti i client di lato tooservice in modo sicuro, come le funzioni di Azure. 
  > 
  > [!NOTE]
  > Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente. In questo modo viene garantita la protezione delle informazioni riservate.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso dell'output
In questa sezione viene illustrato come toouse App Mobile di output di associazione nel codice di funzione. 

In c# le funzioni, usare un parametro di output con nome di tipo `out object` hello tooaccess record di output. Nelle funzioni di Node.js, utilizzare `context.bindings.<name>` hello tooaccess record di output.

<a name="outputsample"></a>

## <a name="output-sample"></a>Esempio di output
Si supponga di avere seguito function.json hello, che definisce un trigger di coda e un output di App per dispositivi mobili:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Vedere l'esempio specifico del linguaggio hello che crea un record nell'endpoint di tabella hello App per dispositivi mobili con contenuto hello di messaggio della coda hello.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Esempio di output in C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Esempio di output in Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

