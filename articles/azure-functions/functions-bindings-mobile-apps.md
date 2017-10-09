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
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="a8dc2-104">Associazioni di app per dispositivi mobili in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="a8dc2-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a8dc2-105">Questo articolo viene illustrato come tooconfigure e codice [App mobili di Azure](../app-service-mobile/app-service-mobile-value-prop.md) associazioni nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="a8dc2-106">Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="a8dc2-107">Hello App per dispositivi mobili di input e output associazioni consentono di [leggere e scrivere nelle tabelle toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="a8dc2-108">Associazione di input di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="a8dc2-108">Mobile Apps input binding</span></span>
<span data-ttu-id="a8dc2-109">associazione di input di App per dispositivi mobili Hello carica un record da un endpoint di tabella per dispositivi mobili e lo passa la funzione.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="a8dc2-110">In c# e F # funzioni, qualsiasi record di toohello le modifiche apportate vengono inviati automaticamente toohello indietro tabella quando si esce dalla funzione hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="a8dc2-111">App per dispositivi mobili Hello input tooa funzione Usa hello seguente oggetto JSON nella hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="a8dc2-112">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-112">Note hello following:</span></span>

* <span data-ttu-id="a8dc2-113">`id`può essere statico o può essere basato su trigger hello che richiama la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="a8dc2-114">Ad esempio, se si utilizza un [trigger coda]() per la funzione, quindi `"id": "{queueTrigger}"` utilizza hello il valore di stringa di messaggio della coda hello come hello tooretrieve ID record.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="a8dc2-115">`connection`deve contenere il nome di hello di un'impostazione di app nell'app (funzione), che a sua volta contiene hello URL dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="a8dc2-116">funzione Hello utilizza questa operazioni REST di URL tooconstruct hello necessario su app mobile.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="a8dc2-117">Si [creare un'impostazione dell'app nell'app funzione]() che contiene l'URL dell'app mobile (che è simile `http://<appname>.azurewebsites.net`), quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà l'associazione di input.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="a8dc2-118">È necessario toospecify `apiKey` se si [implementare una chiave API nel back-end dell'app mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementare una chiave API nel back-end dell'app mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="a8dc2-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="a8dc2-119">toodo, si [creare un'impostazione dell'app nell'app funzione]() che contiene la chiave API hello, quindi aggiungere hello `apiKey` proprietà l'associazione di input con il nome di hello dell'impostazione di app hello.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="a8dc2-120">Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="a8dc2-121">Deve solo essere distribuiti i client di lato tooservice in modo sicuro, come le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="a8dc2-122">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="a8dc2-123">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="a8dc2-124">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="a8dc2-124">Input usage</span></span>
<span data-ttu-id="a8dc2-125">In questa sezione viene illustrato come toouse App Mobile di input di associazione nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="a8dc2-126">Quando il record di hello con hello specificato ID di tabella e il record è disponibile, viene passato a hello denominato [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parametro (o, in Node.js, viene passato a hello `context.bindings.<name>` oggetto).</span><span class="sxs-lookup"><span data-stu-id="a8dc2-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="a8dc2-127">Quando i record di hello non viene trovato, il parametro hello è `null`.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="a8dc2-128">Nelle funzioni di c# e F #, tutte le modifiche apportate ai record di input toohello (parametro di input) viene inviato automaticamente toohello back-tabella di App per dispositivi mobili quando si esce dalla funzione hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="a8dc2-129">Nelle funzioni di Node.js, utilizzare `context.bindings.<name>` tooaccess hello record di input.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="a8dc2-130">In Node.js, inoltre, non è possibile modificare i record.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="a8dc2-131">Esempio di input</span><span class="sxs-lookup"><span data-stu-id="a8dc2-131">Input sample</span></span>
<span data-ttu-id="a8dc2-132">Si supponga di avere seguito function.json hello, che consente di recuperare un record della tabella con id messaggio di attivazione coda hello hello App per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

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

<span data-ttu-id="a8dc2-133">Vedere l'esempio specifico del linguaggio hello che utilizza i record di input hello dall'associazione hello.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="a8dc2-134">esempi di c# e F # Hello inoltre modifichino record di hello `text` proprietà.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="a8dc2-135">C#</span><span class="sxs-lookup"><span data-stu-id="a8dc2-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="a8dc2-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8dc2-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="a8dc2-137">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="a8dc2-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="a8dc2-138">Esempio di input in Node.js</span><span class="sxs-lookup"><span data-stu-id="a8dc2-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="a8dc2-139">Associazione di output di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="a8dc2-139">Mobile Apps output binding</span></span>
<span data-ttu-id="a8dc2-140">Utilizzare hello App per dispositivi mobili output associazione toowrite un nuovo endpoint di tabella tooa record App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="a8dc2-141">App per dispositivi mobili di output per una funzione utilizza hello seguente oggetto JSON nella hello Hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="a8dc2-142">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-142">Note hello following:</span></span>

* <span data-ttu-id="a8dc2-143">`connection`deve contenere il nome di hello di un'impostazione di app nell'app (funzione), che a sua volta contiene hello URL dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="a8dc2-144">funzione Hello utilizza questa operazioni REST di URL tooconstruct hello necessario su app mobile.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="a8dc2-145">Si [creare un'impostazione dell'app nell'app funzione]() che contiene l'URL dell'app mobile (che è simile `http://<appname>.azurewebsites.net`), quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà l'associazione di input.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="a8dc2-146">È necessario toospecify `apiKey` se si [implementare una chiave API nel back-end dell'app mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementare una chiave API nel back-end dell'app mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="a8dc2-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="a8dc2-147">toodo, si [creare un'impostazione dell'app nell'app funzione]() che contiene la chiave API hello, quindi aggiungere hello `apiKey` proprietà l'associazione di input con il nome di hello dell'impostazione di app hello.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="a8dc2-148">Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="a8dc2-149">Deve solo essere distribuiti i client di lato tooservice in modo sicuro, come le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="a8dc2-150">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="a8dc2-151">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="a8dc2-152">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="a8dc2-152">Output usage</span></span>
<span data-ttu-id="a8dc2-153">In questa sezione viene illustrato come toouse App Mobile di output di associazione nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="a8dc2-154">In c# le funzioni, usare un parametro di output con nome di tipo `out object` hello tooaccess record di output.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="a8dc2-155">Nelle funzioni di Node.js, utilizzare `context.bindings.<name>` hello tooaccess record di output.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="a8dc2-156">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="a8dc2-156">Output sample</span></span>
<span data-ttu-id="a8dc2-157">Si supponga di avere seguito function.json hello, che definisce un trigger di coda e un output di App per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="a8dc2-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="a8dc2-158">Vedere l'esempio specifico del linguaggio hello che crea un record nell'endpoint di tabella hello App per dispositivi mobili con contenuto hello di messaggio della coda hello.</span><span class="sxs-lookup"><span data-stu-id="a8dc2-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="a8dc2-159">C#</span><span class="sxs-lookup"><span data-stu-id="a8dc2-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="a8dc2-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8dc2-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="a8dc2-161">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="a8dc2-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="a8dc2-162">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="a8dc2-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="a8dc2-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8dc2-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

