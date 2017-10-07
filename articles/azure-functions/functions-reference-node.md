---
title: riferimenti per sviluppatori aaaJavaScript per le funzioni di Azure | Documenti Microsoft
description: Comprendere il funzionamento toodevelop utilizzando JavaScript.
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="71b12-104">Guida per gli sviluppatori JavaScript di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="71b12-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71b12-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="71b12-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="71b12-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="71b12-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="71b12-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="71b12-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="71b12-108">Hello JavaScript esperienza per le funzioni di Azure rende facile tooexport una funzione, che viene passata come un `context` oggetto per la comunicazione con il runtime hello e per la ricezione e invio di dati tramite i binding.</span><span class="sxs-lookup"><span data-stu-id="71b12-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="71b12-109">Questo articolo si presuppone che sia già stata letta hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="71b12-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="71b12-110">Esportazione di una funzione</span><span class="sxs-lookup"><span data-stu-id="71b12-110">Exporting a function</span></span>
<span data-ttu-id="71b12-111">Tutte le funzioni JavaScript necessario esportare un singolo `function` tramite `module.exports` per hello runtime toofind hello funzione ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="71b12-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="71b12-112">Questa funzione deve sempre includere un oggetto `context` .</span><span class="sxs-lookup"><span data-stu-id="71b12-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="71b12-113">Associazioni di `direction === "in"` vengono passate come argomenti della funzione, il che significa che è possibile utilizzare [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically gestire nuovi input (ad esempio, tramite `arguments.length` tooiterate su tutti gli input).</span><span class="sxs-lookup"><span data-stu-id="71b12-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="71b12-114">Questa funzionalità è utile se si ha solo un trigger e nessun input aggiuntivo, in quanto consente di accedere ai dati del trigger in modo prevedibile senza fare riferimento all'oggetto `context`.</span><span class="sxs-lookup"><span data-stu-id="71b12-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="71b12-115">gli argomenti di Hello vengono sempre passati funzione toohello in ordine di hello in cui si trovano in *function.json*, anche se non si specifica li nell'istruzione esportazioni.</span><span class="sxs-lookup"><span data-stu-id="71b12-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="71b12-116">Ad esempio, se dispone di `function(context, a, b)` e modificarlo troppo`function(context, a)`, è comunque possibile ottenere il valore di hello di `b` nel codice della funzione riferendosi troppo`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="71b12-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="71b12-117">Tutte le associazioni, indipendentemente dalla direzione, vengono inoltre passate in hello `context` (vedere lo script seguente hello) dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="71b12-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="71b12-118">Oggetto context</span><span class="sxs-lookup"><span data-stu-id="71b12-118">context object</span></span>
<span data-ttu-id="71b12-119">Hello runtime usa un `context` oggetto toopass dati tooand della propria funzione e toolet per comunicare con il runtime di hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="71b12-120">è sempre funzione tooa hello del primo parametro Hello oggetto di contesto e deve essere incluso perché contiene i metodi, ad esempio `context.done` e `context.log`, che sono necessari toouse hello runtime correttamente.</span><span class="sxs-lookup"><span data-stu-id="71b12-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="71b12-121">È possibile assegnare un nome oggetto hello qualsiasi desiderato (ad esempio, `ctx` o `c`).</span><span class="sxs-lookup"><span data-stu-id="71b12-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="71b12-122">Proprietà context.bindings</span><span class="sxs-lookup"><span data-stu-id="71b12-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="71b12-123">Restituisce un oggetto denominato che contiene tutti i dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="71b12-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="71b12-124">Ad esempio, hello seguente definizione di associazione nel *function.json* permette di accedere a hello contenuto della coda di hello da hello `context.bindings.myInput` oggetto.</span><span class="sxs-lookup"><span data-stu-id="71b12-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="71b12-125">Metodo context.done</span><span class="sxs-lookup"><span data-stu-id="71b12-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="71b12-126">Informa il runtime hello che il codice è stata completata.</span><span class="sxs-lookup"><span data-stu-id="71b12-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="71b12-127">È necessario chiamare `context.done`, o else hello runtime non sa mai che la funzione è stata completata e il timeout di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="71b12-128">Hello `context.done` metodo consente toopass eseguire sia un runtime toohello di errore definiti dall'utente e un elenco di proprietà della proprietà che sovrascrivono proprietà hello hello `context.bindings` oggetto.</span><span class="sxs-lookup"><span data-stu-id="71b12-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="71b12-129">Metodo context.log</span><span class="sxs-lookup"><span data-stu-id="71b12-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="71b12-130">Consente di toowrite toohello console i log di streaming a livello di traccia predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="71b12-131">In `context.log`, altri metodi di registrazione sono disponibili che consentono di scrivere log console toohello ad altri livelli di traccia:</span><span class="sxs-lookup"><span data-stu-id="71b12-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="71b12-132">Metodo</span><span class="sxs-lookup"><span data-stu-id="71b12-132">Method</span></span>                 | <span data-ttu-id="71b12-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71b12-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="71b12-134">**error(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="71b12-134">**error(_message_)**</span></span>   | <span data-ttu-id="71b12-135">Scrive tooerror livello di registrazione o inferiore.</span><span class="sxs-lookup"><span data-stu-id="71b12-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="71b12-136">**warn(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="71b12-136">**warn(_message_)**</span></span>    | <span data-ttu-id="71b12-137">Scrive toowarning livello di registrazione o inferiore.</span><span class="sxs-lookup"><span data-stu-id="71b12-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="71b12-138">**info(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="71b12-138">**info(_message_)**</span></span>    | <span data-ttu-id="71b12-139">Scrive tooinfo livello di registrazione o inferiore.</span><span class="sxs-lookup"><span data-stu-id="71b12-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="71b12-140">**verbose(_messaggio_)**</span><span class="sxs-lookup"><span data-stu-id="71b12-140">**verbose(_message_)**</span></span> | <span data-ttu-id="71b12-141">Scrive la registrazione a livello tooverbose.</span><span class="sxs-lookup"><span data-stu-id="71b12-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="71b12-142">Hello nell'esempio seguente vengono toohello console a livello di traccia di avviso hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="71b12-143">È possibile impostare hello soglia di livello di traccia per la registrazione nel file host.json hello o disattivarla.</span><span class="sxs-lookup"><span data-stu-id="71b12-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="71b12-144">Per ulteriori informazioni sulla modalità di registrazione toowrite toohello, vedere la sezione successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="71b12-145">Associazione del tipo di dati</span><span class="sxs-lookup"><span data-stu-id="71b12-145">Binding data type</span></span>

<span data-ttu-id="71b12-146">toodefine tipo di dati hello per un'associazione di input, utilizzare hello `dataType` proprietà nella definizione di associazioni hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="71b12-147">Ad esempio, tooread hello contenuto di una richiesta HTTP in formato binario, utilizzare il tipo di hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="71b12-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="71b12-148">Altre opzioni per `dataType` sono `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="71b12-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="71b12-149">Console toohello output di traccia scrittura</span><span class="sxs-lookup"><span data-stu-id="71b12-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="71b12-150">Nelle funzioni, utilizzare hello `context.log` console toohello di metodi toowrite traccia output.</span><span class="sxs-lookup"><span data-stu-id="71b12-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="71b12-151">A questo punto, è possibile utilizzare `console.log` toowrite toohello console.</span><span class="sxs-lookup"><span data-stu-id="71b12-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="71b12-152">Quando si chiama `context.log()`, il messaggio viene scritto toohello console a livello di traccia predefinito hello, ovvero hello _info_ livello di traccia.</span><span class="sxs-lookup"><span data-stu-id="71b12-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="71b12-153">Hello codice seguente viene scritto toohello console a livello di traccia info hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="71b12-154">Hello codice precedente è equivalente toohello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="71b12-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="71b12-155">Hello codice seguente viene scritto toohello console a livello di errore hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="71b12-156">Poiché _errore_ hello traccia di più alto livello, la traccia viene scritto output toohello a tutti i livelli di traccia, purché la registrazione è abilitata.</span><span class="sxs-lookup"><span data-stu-id="71b12-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="71b12-157">Tutti `context.log` metodi supportano hello stesso formato del parametro che è supportato da Node.js hello [util.format metodo](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="71b12-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="71b12-158">Prendere in considerazione hello seguente di codice, che scrive toohello console usando il livello di traccia predefinito hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="71b12-159">È inoltre possibile hello scrittura stesso codice in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="71b12-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="71b12-160">Configurare il livello di traccia hello per registrazione nella console</span><span class="sxs-lookup"><span data-stu-id="71b12-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="71b12-161">Funzioni consente di definire il livello di traccia hello soglia per la scrittura di console toohello, che rende facile toocontrol hello le tracce vengono scritte toohello console da funzioni.</span><span class="sxs-lookup"><span data-stu-id="71b12-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="71b12-162">soglia di hello tooset per tutte le tracce scritto toohello console, utilizzare hello `tracing.consoleLevel` proprietà nel file host.json hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="71b12-163">Questa impostazione si applica a funzioni tooall nell'app (funzione).</span><span class="sxs-lookup"><span data-stu-id="71b12-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="71b12-164">Hello esempio seguente imposta hello traccia soglia tooenable la registrazione dettagliata:</span><span class="sxs-lookup"><span data-stu-id="71b12-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="71b12-165">I valori di **consoleLevel** corrispondono toohello nomi di hello `context.log` metodi.</span><span class="sxs-lookup"><span data-stu-id="71b12-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="71b12-166">impostare traccia tutte le console toohello, registrazione toodisable **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="71b12-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="71b12-167">Per ulteriori informazioni sul file host.json hello, vedere hello [argomento di riferimento host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="71b12-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="71b12-168">Trigger e associazioni HTTP</span><span class="sxs-lookup"><span data-stu-id="71b12-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="71b12-169">E trigger webhook HTTP e output associazioni utilizzano richiesta e risposta oggetti toorepresent hello HTTP messaggistica.</span><span class="sxs-lookup"><span data-stu-id="71b12-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="71b12-170">Oggetto della richiesta</span><span class="sxs-lookup"><span data-stu-id="71b12-170">Request object</span></span>

<span data-ttu-id="71b12-171">Hello `request` oggetto ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="71b12-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="71b12-172">Proprietà</span><span class="sxs-lookup"><span data-stu-id="71b12-172">Property</span></span>      | <span data-ttu-id="71b12-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71b12-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="71b12-174">_body_</span><span class="sxs-lookup"><span data-stu-id="71b12-174">_body_</span></span>        | <span data-ttu-id="71b12-175">Oggetto che contiene hello corpo della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="71b12-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="71b12-176">_headers_</span></span>     | <span data-ttu-id="71b12-177">Oggetto che contiene le intestazioni di richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="71b12-178">_method_</span><span class="sxs-lookup"><span data-stu-id="71b12-178">_method_</span></span>      | <span data-ttu-id="71b12-179">metodo HTTP della richiesta di hello Hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="71b12-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="71b12-180">_originalUrl_</span></span> | <span data-ttu-id="71b12-181">Hello l'URL della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="71b12-182">_params_</span><span class="sxs-lookup"><span data-stu-id="71b12-182">_params_</span></span>      | <span data-ttu-id="71b12-183">Oggetto che contiene i parametri di routing della richiesta di hello hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="71b12-184">_query_</span><span class="sxs-lookup"><span data-stu-id="71b12-184">_query_</span></span>       | <span data-ttu-id="71b12-185">Oggetto che contiene i parametri di query hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="71b12-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="71b12-186">_rawBody_</span></span>     | <span data-ttu-id="71b12-187">corpo Hello del messaggio sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="71b12-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="71b12-188">Oggetto della risposta</span><span class="sxs-lookup"><span data-stu-id="71b12-188">Response object</span></span>

<span data-ttu-id="71b12-189">Hello `response` oggetto ha hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="71b12-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="71b12-190">Proprietà</span><span class="sxs-lookup"><span data-stu-id="71b12-190">Property</span></span>  | <span data-ttu-id="71b12-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="71b12-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="71b12-192">_body_</span><span class="sxs-lookup"><span data-stu-id="71b12-192">_body_</span></span>    | <span data-ttu-id="71b12-193">Oggetto che contiene hello corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="71b12-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="71b12-194">_headers_</span></span> | <span data-ttu-id="71b12-195">Oggetto che contiene le intestazioni di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="71b12-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="71b12-196">_isRaw_</span></span>   | <span data-ttu-id="71b12-197">Indica che la formattazione è ignorata per la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="71b12-198">_Stato_</span><span class="sxs-lookup"><span data-stu-id="71b12-198">_status_</span></span>  | <span data-ttu-id="71b12-199">codice di stato HTTP della risposta hello Hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="71b12-200">L'accesso a hello richiesta e risposta</span><span class="sxs-lookup"><span data-stu-id="71b12-200">Accessing hello request and response</span></span> 

<span data-ttu-id="71b12-201">Quando si lavora con i trigger HTTP, è possibile accedere a oggetti hello HTTP richiesta e risposta in uno dei tre modi:</span><span class="sxs-lookup"><span data-stu-id="71b12-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="71b12-202">Dal hello denominato input e output di associazioni.</span><span class="sxs-lookup"><span data-stu-id="71b12-202">From hello named input and output bindings.</span></span> <span data-ttu-id="71b12-203">In questo modo, i trigger HTTP hello e associazioni lavoro hello stesso come qualsiasi altra associazione.</span><span class="sxs-lookup"><span data-stu-id="71b12-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="71b12-204">Hello esempio seguente imposta hello risposta oggetto utilizzando un oggetto denominato `response` associazione:</span><span class="sxs-lookup"><span data-stu-id="71b12-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="71b12-205">Da `req` e `res` proprietà hello `context` oggetto.</span><span class="sxs-lookup"><span data-stu-id="71b12-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="71b12-206">In questo modo, è possibile utilizzare hello modello convenzionale tooaccess HTTP dati oggetto di contesto hello, invece di dover hello toouse completo `context.bindings.name` modello.</span><span class="sxs-lookup"><span data-stu-id="71b12-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="71b12-207">Hello seguente esempio viene illustrato come hello tooaccess `req` e `res` oggetti hello `context`:</span><span class="sxs-lookup"><span data-stu-id="71b12-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="71b12-208">Oppure chiamando `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="71b12-208">By calling `context.done()`.</span></span> <span data-ttu-id="71b12-209">Un tipo speciale di associazione HTTP restituisce risposta hello passato toohello `context.done()` metodo.</span><span class="sxs-lookup"><span data-stu-id="71b12-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="71b12-210">output di Hello seguente HTTP associazione definisce un `$return` parametro di output:</span><span class="sxs-lookup"><span data-stu-id="71b12-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="71b12-211">L'associazione di output è prevista è toosupply hello risposta quando si chiama `done()`, come segue:</span><span class="sxs-lookup"><span data-stu-id="71b12-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="71b12-212">Versione di Node e gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="71b12-212">Node version and Package Management</span></span>
<span data-ttu-id="71b12-213">versione del nodo Hello è attualmente bloccato `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="71b12-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="71b12-214">Si sta analizzando la possibilità di aggiungere il supporto per altre versioni e renderle configurabili.</span><span class="sxs-lookup"><span data-stu-id="71b12-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="71b12-215">Hello alla procedura seguente consente di includere i pacchetti dell'app di funzione:</span><span class="sxs-lookup"><span data-stu-id="71b12-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="71b12-216">Andare troppo`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="71b12-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="71b12-217">Fare clic su **Debug Console** > **CMD** (Console di debug > CMD).</span><span class="sxs-lookup"><span data-stu-id="71b12-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="71b12-218">Andare troppo`D:\home\site\wwwroot`, quindi trascinare il toohello file package. JSON **wwwroot** cartella nella metà superiore hello pagina hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="71b12-219">Inoltre, è possibile caricare file tooyour funzione app in altri modi.</span><span class="sxs-lookup"><span data-stu-id="71b12-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="71b12-220">Per ulteriori informazioni, vedere [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="71b12-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="71b12-221">Dopo aver caricato il file di package. JSON hello, eseguire hello `npm install` comando hello **console l'esecuzione remota Kudu**.</span><span class="sxs-lookup"><span data-stu-id="71b12-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="71b12-222">Questa azione Scarica i pacchetti hello indicati nel file package. JSON hello e riavvia hello funzione app.</span><span class="sxs-lookup"><span data-stu-id="71b12-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="71b12-223">Dopo aver hello pacchetti necessari sono installati, importarli tooyour funzione chiamando `require('packagename')`, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="71b12-224">È necessario definire un `package.json` file alla radice di hello dell'app in funzione.</span><span class="sxs-lookup"><span data-stu-id="71b12-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="71b12-225">File di definizione hello consente tutte le funzioni nella condivisione di app hello hello stessi pacchetti memorizzati nella cache, che offre prestazioni migliori hello.</span><span class="sxs-lookup"><span data-stu-id="71b12-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="71b12-226">Se si verifica un conflitto di versione, è possibile risolverlo aggiungendo un `package.json` file nella cartella hello di una funzione specifica.</span><span class="sxs-lookup"><span data-stu-id="71b12-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="71b12-227">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="71b12-227">Environment variables</span></span>
<span data-ttu-id="71b12-228">tooget una variabile di ambiente o un valore di impostazione di app, utilizzare `process.env`, come illustrato nell'esempio di codice seguente hello:</span><span class="sxs-lookup"><span data-stu-id="71b12-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="71b12-229">Considerazioni per le funzioni JavaScript</span><span class="sxs-lookup"><span data-stu-id="71b12-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="71b12-230">Quando si utilizzano le funzioni JavaScript, tenere presenti le considerazioni sulle hello hello nelle due sezioni che seguono.</span><span class="sxs-lookup"><span data-stu-id="71b12-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="71b12-231">Scegliere i piani di servizio app single core</span><span class="sxs-lookup"><span data-stu-id="71b12-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="71b12-232">Quando si crea un'app di funzione che usa hello piano di servizio App, si consiglia di selezionare un piano a core singolo anziché un piano con più core.</span><span class="sxs-lookup"><span data-stu-id="71b12-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="71b12-233">Oggi, funzioni esegue le funzioni JavaScript in modo più efficiente nelle macchine virtuali a core singolo e utilizzando macchine virtuali di dimensioni maggiori non produce hello previsto miglioramento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="71b12-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="71b12-234">Se necessario, è possibile scalare orizzontalmente manualmente aggiungendo altre istanze di macchine virtuali single core oppure abilitare la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="71b12-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="71b12-235">Per altre informazioni, vedere [Scalare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71b12-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="71b12-236">Supporto TypeScript e CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="71b12-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="71b12-237">Poiché il supporto diretto non esiste ancora per la compilazione automatica TypeScript o CoffeeScript tramite il runtime di hello, questo tipo di supporto deve toobe gestite all'esterno di hello runtime, in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="71b12-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="71b12-238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71b12-238">Next steps</span></span>
<span data-ttu-id="71b12-239">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="71b12-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="71b12-240">Procedure consigliate per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="71b12-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="71b12-241">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="71b12-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="71b12-242">Guida di riferimento per gli sviluppatori C# di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="71b12-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="71b12-243">Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#</span><span class="sxs-lookup"><span data-stu-id="71b12-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="71b12-244">Trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="71b12-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

