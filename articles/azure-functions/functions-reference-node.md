---
title: Guida di riferimento per gli sviluppatori JavaScript di Funzioni di Azure | Microsoft Docs
description: Informazioni su come sviluppare funzioni con JavaScript.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="d85ff-104">Guida per gli sviluppatori JavaScript di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d85ff-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d85ff-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="d85ff-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="d85ff-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="d85ff-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="d85ff-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d85ff-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="d85ff-108">L'esperienza JavaScript per Funzioni di Azure semplifica l'esportazione di una funzione, che viene passata come oggetto `context` per la comunicazione con il runtime e per la ricezione e l'invio di dati tramite associazioni.</span><span class="sxs-lookup"><span data-stu-id="d85ff-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="d85ff-109">Questo articolo presuppone che l'utente abbia già letto [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d85ff-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="d85ff-110">Esportazione di una funzione</span><span class="sxs-lookup"><span data-stu-id="d85ff-110">Exporting a function</span></span>
<span data-ttu-id="d85ff-111">Tutte le funzioni JavaScript devono esportare una singola `function` tramite `module.exports` per consentire al runtime di trovare la funzione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="d85ff-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="d85ff-112">Questa funzione deve sempre includere un oggetto `context` .</span><span class="sxs-lookup"><span data-stu-id="d85ff-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="d85ff-113">Le associazioni di `direction === "in"` vengono passate come argomenti della funzione, pertanto è possibile usare [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) per gestire in modo dinamico nuovi input, ad esempio usando `arguments.length` per l'iterazione di tutti gli input.</span><span class="sxs-lookup"><span data-stu-id="d85ff-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="d85ff-114">Questa funzionalità è utile se si ha solo un trigger e nessun input aggiuntivo, in quanto consente di accedere ai dati del trigger in modo prevedibile senza fare riferimento all'oggetto `context`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="d85ff-115">Gli argomenti vengono sempre passati insieme alla funzione nell'ordine in cui sono indicati nel file *function.json*, anche se non vengono specificati nell'istruzione exports.</span><span class="sxs-lookup"><span data-stu-id="d85ff-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="d85ff-116">Se ad esempio si ha `function(context, a, b)` e viene modificato in `function(context, a)`, è comunque possibile ottenere il valore di `b` nel codice della funzione facendo riferimento a `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="d85ff-117">Anche tutte le associazioni, indipendentemente dalla direzione, vengono passate sull'oggetto `context` (vedere lo script seguente).</span><span class="sxs-lookup"><span data-stu-id="d85ff-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="d85ff-118">Oggetto context</span><span class="sxs-lookup"><span data-stu-id="d85ff-118">context object</span></span>
<span data-ttu-id="d85ff-119">Il runtime usa un oggetto `context` per passare dati dalla e alla funzione e consentire la comunicazione con il runtime.</span><span class="sxs-lookup"><span data-stu-id="d85ff-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="d85ff-120">L'oggetto context è sempre il primo parametro di una funzione e deve essere incluso, in quanto contiene i metodi necessari per usare correttamente il runtime, ad esempio `context.done` e `context.log`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="d85ff-121">È possibile assegnare all'oggetto un nome qualsiasi, ad esempio `ctx` o `c`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="d85ff-122">Proprietà context.bindings</span><span class="sxs-lookup"><span data-stu-id="d85ff-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="d85ff-123">Restituisce un oggetto denominato che contiene tutti i dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="d85ff-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="d85ff-124">Data la seguente definizione di associazione in *function.json*, è ad esempio possibile accedere al contenuto della coda tramite l'oggetto `context.bindings.myInput`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="d85ff-125">Metodo context.done</span><span class="sxs-lookup"><span data-stu-id="d85ff-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="d85ff-126">Comunica al runtime che l'esecuzione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="d85ff-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="d85ff-127">La chiamata a `context.done` è necessaria. In caso contrario, il runtime non saprà mai che la funzione è stata completata e l'esecuzione raggiungerà il timeout.</span><span class="sxs-lookup"><span data-stu-id="d85ff-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="d85ff-128">Il metodo `context.done` consente di passare di nuovo al runtime sia un errore definito dall'utente sia un contenitore delle proprietà con proprietà che sovrascriveranno quelle presenti nell'oggetto `context.bindings`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="d85ff-129">Metodo context.log</span><span class="sxs-lookup"><span data-stu-id="d85ff-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="d85ff-130">Consente di scrivere nei log della console in streaming a livello di traccia predefinito.</span><span class="sxs-lookup"><span data-stu-id="d85ff-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="d85ff-131">In `context.log` sono disponibili altri metodi di registrazione che consentono di scrivere nel log della console ad altri livelli di traccia:</span><span class="sxs-lookup"><span data-stu-id="d85ff-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="d85ff-132">Metodo</span><span class="sxs-lookup"><span data-stu-id="d85ff-132">Method</span></span>                 | <span data-ttu-id="d85ff-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d85ff-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="d85ff-134">**error(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="d85ff-134">**error(_message_)**</span></span>   | <span data-ttu-id="d85ff-135">Scrive nella registrazione a livello di errore o inferiore.</span><span class="sxs-lookup"><span data-stu-id="d85ff-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="d85ff-136">**warn(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="d85ff-136">**warn(_message_)**</span></span>    | <span data-ttu-id="d85ff-137">Scrive nella registrazione a livello di avviso o inferiore.</span><span class="sxs-lookup"><span data-stu-id="d85ff-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="d85ff-138">**info(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="d85ff-138">**info(_message_)**</span></span>    | <span data-ttu-id="d85ff-139">Scrive nella registrazione a livello di informazioni o inferiore.</span><span class="sxs-lookup"><span data-stu-id="d85ff-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="d85ff-140">**verbose(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="d85ff-140">**verbose(_message_)**</span></span> | <span data-ttu-id="d85ff-141">Scrive nella registrazione a livello dettagliato.</span><span class="sxs-lookup"><span data-stu-id="d85ff-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="d85ff-142">L'esempio seguente scrive nella console a livello di traccia di avviso:</span><span class="sxs-lookup"><span data-stu-id="d85ff-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="d85ff-143">È possibile impostare la soglia del livello di traccia per la registrazione nel file host.json o disattivarla.</span><span class="sxs-lookup"><span data-stu-id="d85ff-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="d85ff-144">Per altre informazioni su come scrivere nei log, vedere la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d85ff-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="d85ff-145">Associazione del tipo di dati</span><span class="sxs-lookup"><span data-stu-id="d85ff-145">Binding data type</span></span>

<span data-ttu-id="d85ff-146">Per definire il tipo di dati per un'associazione di input, usare la proprietà `dataType` nella definizione dell'associazione.</span><span class="sxs-lookup"><span data-stu-id="d85ff-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="d85ff-147">Ad esempio, per leggere il contenuto di una richiesta HTTP in formato binario, usare il tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="d85ff-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="d85ff-148">Altre opzioni per `dataType` sono `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="d85ff-149">Scrittura dell'output di traccia nella console</span><span class="sxs-lookup"><span data-stu-id="d85ff-149">Writing trace output to the console</span></span> 

<span data-ttu-id="d85ff-150">In Funzioni usare i metodi `context.log` per scrivere l'output di traccia nella console.</span><span class="sxs-lookup"><span data-stu-id="d85ff-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="d85ff-151">A questo punto, non è possibile usare `console.log` per scrivere nella console.</span><span class="sxs-lookup"><span data-stu-id="d85ff-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="d85ff-152">Quando si chiama `context.log()`, il messaggio viene scritto nella console a livello di traccia predefinito, ovvero il livello di traccia _info_.</span><span class="sxs-lookup"><span data-stu-id="d85ff-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="d85ff-153">Il codice seguente scrive nella console a livello di traccia informazioni:</span><span class="sxs-lookup"><span data-stu-id="d85ff-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="d85ff-154">Il codice precedente equivale al seguente:</span><span class="sxs-lookup"><span data-stu-id="d85ff-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="d85ff-155">Il codice seguente scrive nella console a livello di errore:</span><span class="sxs-lookup"><span data-stu-id="d85ff-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="d85ff-156">Poiché _error_ è il livello di traccia più alto, questa traccia viene scritta nell'output a tutti i livelli di traccia, fintantoché la registrazione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="d85ff-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="d85ff-157">Tutti i metodi `context.log` supportano lo stesso formato di parametri supportato dal metodo Node.js [ util.format](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="d85ff-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="d85ff-158">Si consideri il codice seguente, che scrive nella console usando il livello di traccia predefinito:</span><span class="sxs-lookup"><span data-stu-id="d85ff-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="d85ff-159">È possibile scrivere lo stesso codice anche nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="d85ff-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="d85ff-160">Configurare il livello di traccia per la registrazione della console</span><span class="sxs-lookup"><span data-stu-id="d85ff-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="d85ff-161">Funzioni consente di definire la soglia del livello di traccia per la scrittura nella console; questo consente di controllare più facilmente il modo in cui le tracce vengono scritte nella console dalle funzioni.</span><span class="sxs-lookup"><span data-stu-id="d85ff-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="d85ff-162">Per impostare la soglia per tutte le tracce scritte nella console, usare la proprietà `tracing.consoleLevel` nel file host.json.</span><span class="sxs-lookup"><span data-stu-id="d85ff-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="d85ff-163">Questa impostazione si applica a tutte le funzioni dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d85ff-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="d85ff-164">L'esempio seguente imposta la soglia di traccia per abilitare la registrazione dettagliata:</span><span class="sxs-lookup"><span data-stu-id="d85ff-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="d85ff-165">I valori di **consoleLevel** corrispondono ai nomi dei metodi `context.log`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="d85ff-166">Per disabilitare tutta la registrazione traccia nella console, impostare **consoleLevel** su _off_.</span><span class="sxs-lookup"><span data-stu-id="d85ff-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="d85ff-167">Per altre informazioni sul file host.json, vedere l'[argomento di riferimento host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="d85ff-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="d85ff-168">Trigger e associazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="d85ff-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="d85ff-169">I trigger e i webhook HTTP e le associazioni di output HTTP usano oggetti di richiesta e risposta per rappresentare la messaggistica HTTP.</span><span class="sxs-lookup"><span data-stu-id="d85ff-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="d85ff-170">Oggetto della richiesta</span><span class="sxs-lookup"><span data-stu-id="d85ff-170">Request object</span></span>

<span data-ttu-id="d85ff-171">Di seguito sono elencate le proprietà dell'oggetto `request`:</span><span class="sxs-lookup"><span data-stu-id="d85ff-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="d85ff-172">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d85ff-172">Property</span></span>      | <span data-ttu-id="d85ff-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d85ff-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="d85ff-174">_body_</span><span class="sxs-lookup"><span data-stu-id="d85ff-174">_body_</span></span>        | <span data-ttu-id="d85ff-175">Oggetto che contiene il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="d85ff-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="d85ff-176">_headers_</span></span>     | <span data-ttu-id="d85ff-177">Oggetto che contiene le intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="d85ff-178">_method_</span><span class="sxs-lookup"><span data-stu-id="d85ff-178">_method_</span></span>      | <span data-ttu-id="d85ff-179">Metodo HTTP della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="d85ff-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="d85ff-180">_originalUrl_</span></span> | <span data-ttu-id="d85ff-181">URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="d85ff-182">_params_</span><span class="sxs-lookup"><span data-stu-id="d85ff-182">_params_</span></span>      | <span data-ttu-id="d85ff-183">Oggetto che contiene i parametri di routing della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="d85ff-184">_query_</span><span class="sxs-lookup"><span data-stu-id="d85ff-184">_query_</span></span>       | <span data-ttu-id="d85ff-185">Oggetto che contiene i parametri di query della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="d85ff-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="d85ff-186">_rawBody_</span></span>     | <span data-ttu-id="d85ff-187">Il corpo del messaggio sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="d85ff-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="d85ff-188">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="d85ff-188">Response object</span></span>

<span data-ttu-id="d85ff-189">Di seguito sono elencate le proprietà dell'oggetto `response`:</span><span class="sxs-lookup"><span data-stu-id="d85ff-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="d85ff-190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d85ff-190">Property</span></span>  | <span data-ttu-id="d85ff-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d85ff-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="d85ff-192">_body_</span><span class="sxs-lookup"><span data-stu-id="d85ff-192">_body_</span></span>    | <span data-ttu-id="d85ff-193">Oggetto che contiene il corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="d85ff-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="d85ff-194">_headers_</span></span> | <span data-ttu-id="d85ff-195">Oggetto che contiene le intestazioni della risposta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="d85ff-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="d85ff-196">_isRaw_</span></span>   | <span data-ttu-id="d85ff-197">Indica che la formattazione viene ignorata per la risposta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="d85ff-198">_Stato_</span><span class="sxs-lookup"><span data-stu-id="d85ff-198">_status_</span></span>  | <span data-ttu-id="d85ff-199">Codice di stato HTTP della risposta.</span><span class="sxs-lookup"><span data-stu-id="d85ff-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="d85ff-200">Accesso a richiesta e risposta</span><span class="sxs-lookup"><span data-stu-id="d85ff-200">Accessing the request and response</span></span> 

<span data-ttu-id="d85ff-201">Quando si lavora con i trigger HTTP, è possibile accedere agli oggetti richiesta e risposta HTTP in uno qualsiasi dei tre modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d85ff-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="d85ff-202">Dalle associazioni di input e di output denominate.</span><span class="sxs-lookup"><span data-stu-id="d85ff-202">From the named input and output bindings.</span></span> <span data-ttu-id="d85ff-203">In questo modo, il trigger e le associazioni HTTP funzionano come qualsiasi altra associazione.</span><span class="sxs-lookup"><span data-stu-id="d85ff-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="d85ff-204">L'esempio seguente imposta l'oggetto risposta usando un'associazione `response` denominata.</span><span class="sxs-lookup"><span data-stu-id="d85ff-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="d85ff-205">Dalle proprietà `req` e `res` sull'oggetto `context`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="d85ff-206">In questo modo per accedere ai dati HTTP dall'oggetto di contesto è possibile usare il modello convenzionale anziché il modello `context.bindings.name` completo.</span><span class="sxs-lookup"><span data-stu-id="d85ff-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="d85ff-207">L'esempio seguente illustra come accedere agli oggetti `req` e `res` nell'oggetto `context`:</span><span class="sxs-lookup"><span data-stu-id="d85ff-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="d85ff-208">Oppure chiamando `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-208">By calling `context.done()`.</span></span> <span data-ttu-id="d85ff-209">Un tipo speciale di associazione HTTP restituisce la risposta che viene passata al metodo `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="d85ff-210">L'associazione di output HTTP seguente definisce un parametro di output `$return`:</span><span class="sxs-lookup"><span data-stu-id="d85ff-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="d85ff-211">Questa associazione di output prevede che l'utente dia la risposta quando chiama `done()`, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d85ff-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="d85ff-212">Versione di Node e gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d85ff-212">Node version and Package Management</span></span>
<span data-ttu-id="d85ff-213">La versione di Node è attualmente bloccata alla `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="d85ff-214">Si sta analizzando la possibilità di aggiungere il supporto per altre versioni e renderle configurabili.</span><span class="sxs-lookup"><span data-stu-id="d85ff-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="d85ff-215">I passaggi seguenti consentono di includere i pacchetti nell'app per le funzioni:</span><span class="sxs-lookup"><span data-stu-id="d85ff-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="d85ff-216">Passare a `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d85ff-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="d85ff-217">Fare clic su **Debug Console** > **CMD** (Console di debug > CMD).</span><span class="sxs-lookup"><span data-stu-id="d85ff-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="d85ff-218">Passare a `D:\home\site\wwwroot`, quindi trascinare il file package.json nella cartella **wwwroot** nella metà superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="d85ff-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="d85ff-219">È possibile caricare i file nell'app per le funzioni anche in altri modi.</span><span class="sxs-lookup"><span data-stu-id="d85ff-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="d85ff-220">Per altre informazioni, vedere [Come aggiornare i file delle app per le funzioni](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="d85ff-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="d85ff-221">Dopo aver caricato il file package.json, eseguire il comando `npm install` nella  **console di esecuzione remota Kudu**.</span><span class="sxs-lookup"><span data-stu-id="d85ff-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="d85ff-222">Questa azione scarica i pacchetti indicati nel file package.json e riavvia l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d85ff-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="d85ff-223">Una volta che i pacchetti necessari sono installati, è possibile importarli nella funzione chiamando il metodo `require('packagename')`, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d85ff-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="d85ff-224">È necessario definire un file `package.json` nella directory principale dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d85ff-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="d85ff-225">La definizione del file consente a tutte le funzioni dell'app di condividere gli stessi pacchetti memorizzati nella cache garantendo prestazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="d85ff-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="d85ff-226">In caso di conflitto di versione, è possibile risolverlo aggiungendo un file `package.json` nella cartella di una funzione specifica.</span><span class="sxs-lookup"><span data-stu-id="d85ff-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="d85ff-227">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="d85ff-227">Environment variables</span></span>
<span data-ttu-id="d85ff-228">Per ottenere una variabile di ambiente o un valore di impostazione dell'app, usare `process.env`come illustrato nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d85ff-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="d85ff-229">Considerazioni per le funzioni JavaScript</span><span class="sxs-lookup"><span data-stu-id="d85ff-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="d85ff-230">Quando si usano le funzioni JavaScript, tenere presente le considerazioni nelle due sezioni che seguono.</span><span class="sxs-lookup"><span data-stu-id="d85ff-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="d85ff-231">Scegliere i piani di servizio app single core</span><span class="sxs-lookup"><span data-stu-id="d85ff-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="d85ff-232">Quando si crea un'app per le funzioni che usa il piano di servizio app, è consigliabile selezionare un piano single core anziché uno con più core.</span><span class="sxs-lookup"><span data-stu-id="d85ff-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="d85ff-233">Oggi Funzioni esegue funzioni JavaScript in modo più efficiente in macchine virtuali single core e l'uso di macchine virtuali di dimensioni maggiori non produce i miglioramenti delle prestazioni previsti.</span><span class="sxs-lookup"><span data-stu-id="d85ff-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="d85ff-234">Se necessario, è possibile scalare orizzontalmente manualmente aggiungendo altre istanze di macchine virtuali single core oppure abilitare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="d85ff-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="d85ff-235">Per altre informazioni, vedere [Scalare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d85ff-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="d85ff-236">Supporto TypeScript e CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="d85ff-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="d85ff-237">Dal momento che non è ancora disponibile il supporto diretto per la compilazione automatica di TypeScript o CoffeeScript tramite il runtime, il supporto deve essere gestito all'esterno del runtime al momento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d85ff-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d85ff-238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d85ff-238">Next steps</span></span>
<span data-ttu-id="d85ff-239">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d85ff-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="d85ff-240">Procedure consigliate per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d85ff-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="d85ff-241">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d85ff-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="d85ff-242">Guida di riferimento per gli sviluppatori C# di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d85ff-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="d85ff-243">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="d85ff-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="d85ff-244">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d85ff-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

