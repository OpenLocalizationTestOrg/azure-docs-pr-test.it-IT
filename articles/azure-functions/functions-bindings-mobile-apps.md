---
title: Associazioni di app per dispositivi mobili in Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare le associazioni di app per dispositivi mobili in Funzioni di Azure
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
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="b929e-104">Associazioni di app per dispositivi mobili in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b929e-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b929e-105">Questo articolo illustra come configurare e scrivere il codice delle [associazioni di App per dispositivi mobili di Azure](../app-service-mobile/app-service-mobile-value-prop.md) in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b929e-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="b929e-106">Funzioni di Azure supporta le associazioni di input e output per App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="b929e-107">Le associazioni di input e output per App per dispositivi mobili consentono di [leggere e scrivere tabelle di dati](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) nella propria app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="b929e-108">Associazione di input di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b929e-108">Mobile Apps input binding</span></span>
<span data-ttu-id="b929e-109">L'associazione di input di App per dispositivi mobili carica un record da un endpoint tabella per dispositivi mobili e lo passa alla propria funzione.</span><span class="sxs-lookup"><span data-stu-id="b929e-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="b929e-110">Nelle funzioni C# e F# eventuali modifiche apportate al record vengono automaticamente inviate alla tabella se la funzione termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="b929e-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="b929e-111">L'input di App per dispositivi mobili in una funzione usa l'oggetto JSON seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="b929e-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="b929e-112">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b929e-112">Note the following:</span></span>

* <span data-ttu-id="b929e-113">`id` può essere statico oppure può essere basato sul trigger che richiama la funzione.</span><span class="sxs-lookup"><span data-stu-id="b929e-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="b929e-114">Se ad esempio si usa un [trigger della coda]() per la propria funzione, `"id": "{queueTrigger}"` userà il valore di stringa del messaggio della coda come ID del record da recuperare.</span><span class="sxs-lookup"><span data-stu-id="b929e-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="b929e-115">`connection` deve contenere il nome di un'impostazione dell'app per le funzioni, in cui è contenuto l'URL dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="b929e-116">La funzione usa questo URL per creare le operazioni REST da eseguire sull'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="b929e-117">A questo scopo, è necessario [creare un'impostazione nell'app per le funzioni]() che contenga l'URL dell'app per dispositivi mobili (simile a `http://<appname>.azurewebsites.net`) e quindi specificare il nome dell'impostazione dell'app nella proprietà `connection` dell'associazione di input.</span><span class="sxs-lookup"><span data-stu-id="b929e-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b929e-118">È necessario specificare `apiKey` se si [implementa una chiave API nel back-end dell'app per dispositivi mobili Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) o se si [implementa una chiave API nel back-end dell'app per dispositivi mobili .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b929e-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b929e-119">A questo scopo, è necessario [creare un'impostazione nell'app per le funzioni]() che contenga la chiave API e quindi aggiungere la proprietà `apiKey` nell'associazione di input con il nome dell'impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b929e-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b929e-120">Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b929e-121">Può essere distribuita in modo sicuro solo ai client sul lato servizio, come Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b929e-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b929e-122">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="b929e-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b929e-123">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="b929e-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="b929e-124">Uso dell'input</span><span class="sxs-lookup"><span data-stu-id="b929e-124">Input usage</span></span>
<span data-ttu-id="b929e-125">In questa sezione viene illustrato come usare l'associazione di input di App per dispositivi mobili nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="b929e-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="b929e-126">Se il record corrispondente alla tabella e all'ID di record specificati viene trovato, il record viene passato al parametro denominato [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) (in Node.js viene passato all'oggetto `context.bindings.<name>`).</span><span class="sxs-lookup"><span data-stu-id="b929e-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="b929e-127">Se il record non viene trovato, il parametro è `null`.</span><span class="sxs-lookup"><span data-stu-id="b929e-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="b929e-128">Nelle funzioni C# e F# eventuali modifiche apportate al record di input (parametro di input) vengono automaticamente inviate alla tabella di App per dispositivi mobili quando la funzione termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="b929e-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="b929e-129">Nelle funzioni Node.js si accede al record di input usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b929e-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="b929e-130">In Node.js, inoltre, non è possibile modificare i record.</span><span class="sxs-lookup"><span data-stu-id="b929e-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="b929e-131">Esempio di input</span><span class="sxs-lookup"><span data-stu-id="b929e-131">Input sample</span></span>
<span data-ttu-id="b929e-132">Si supponga di avere il seguente function.json, che recupera un record della tabella di App per dispositivi mobili tramite l'ID del messaggio di attivazione della coda:</span><span class="sxs-lookup"><span data-stu-id="b929e-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="b929e-133">Vedere l'esempio specifico del linguaggio che usa il record di input dall'associazione.</span><span class="sxs-lookup"><span data-stu-id="b929e-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="b929e-134">Gli esempi in C# e F# modificano anche la proprietà `text` del record.</span><span class="sxs-lookup"><span data-stu-id="b929e-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="b929e-135">C#</span><span class="sxs-lookup"><span data-stu-id="b929e-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="b929e-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="b929e-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="b929e-137">Esempio di input in C#</span><span class="sxs-lookup"><span data-stu-id="b929e-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="b929e-138">Esempio di input in Node.js</span><span class="sxs-lookup"><span data-stu-id="b929e-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="b929e-139">Associazione di output di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="b929e-139">Mobile Apps output binding</span></span>
<span data-ttu-id="b929e-140">L'associazione di output di App per dispositivi mobili consente di scrivere un nuovo record in un endpoint tabella di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="b929e-141">L'output di App per dispositivi mobili per una funzione usa l'oggetto JSON seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="b929e-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="b929e-142">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b929e-142">Note the following:</span></span>

* <span data-ttu-id="b929e-143">`connection` deve contenere il nome di un'impostazione dell'app per le funzioni, in cui è contenuto l'URL dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="b929e-144">La funzione usa questo URL per creare le operazioni REST da eseguire sull'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="b929e-145">A questo scopo, è necessario [creare un'impostazione nell'app per le funzioni]() che contenga l'URL dell'app per dispositivi mobili (simile a `http://<appname>.azurewebsites.net`) e quindi specificare il nome dell'impostazione dell'app nella proprietà `connection` dell'associazione di input.</span><span class="sxs-lookup"><span data-stu-id="b929e-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b929e-146">È necessario specificare `apiKey` se si [implementa una chiave API nel back-end dell'app per dispositivi mobili Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) o se si [implementa una chiave API nel back-end dell'app per dispositivi mobili .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b929e-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b929e-147">A questo scopo, è necessario [creare un'impostazione nell'app per le funzioni]() che contenga la chiave API e quindi aggiungere la proprietà `apiKey` nell'associazione di input con il nome dell'impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b929e-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b929e-148">Questa chiave API non deve essere condivisa con i client dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b929e-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b929e-149">Può essere distribuita in modo sicuro solo ai client sul lato servizio, come Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b929e-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b929e-150">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="b929e-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b929e-151">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="b929e-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="b929e-152">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="b929e-152">Output usage</span></span>
<span data-ttu-id="b929e-153">In questa sezione viene illustrato come usare l'associazione di output di App per dispositivi mobili nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="b929e-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="b929e-154">Nelle funzioni C# è necessario usare un parametro di output denominato di tipo `out object` per accedere al record di output.</span><span class="sxs-lookup"><span data-stu-id="b929e-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="b929e-155">Nelle funzioni Node.js si accede al record di output usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b929e-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b929e-156">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="b929e-156">Output sample</span></span>
<span data-ttu-id="b929e-157">Si supponga di avere il seguente function.json, che definisce un trigger della coda e un output di App per dispositivi mobili:</span><span class="sxs-lookup"><span data-stu-id="b929e-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="b929e-158">Vedere l'esempio specifico del linguaggio che crea un record nell'endpoint tabella di App per dispositivi mobili con il contenuto del messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="b929e-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="b929e-159">C#</span><span class="sxs-lookup"><span data-stu-id="b929e-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b929e-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="b929e-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b929e-161">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="b929e-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="b929e-162">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="b929e-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b929e-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b929e-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

