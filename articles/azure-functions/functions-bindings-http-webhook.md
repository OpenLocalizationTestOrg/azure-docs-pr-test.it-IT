---
title: associazioni di funzioni HTTP e webhook aaaAzure | Documenti Microsoft
description: Comprendere come toouse HTTP e webhook i trigger e le associazioni in funzioni di Azure.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: funzioni di Azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server, HTTP, API, REST
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="3a264-104">Associazioni HTTP e webhook in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="3a264-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3a264-105">Questo articolo viene illustrato come tooconfigure e funziona con HTTP attiva e le associazioni in funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a264-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="3a264-106">Queste operazioni, è possibile utilizzare funzioni di Azure toobuild senza server API e rispondere toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="3a264-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="3a264-107">Funzioni di Azure fornisce hello seguenti associazioni:</span><span class="sxs-lookup"><span data-stu-id="3a264-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="3a264-108">Un [trigger HTTP](#httptrigger) consente di richiamare una funzione con una richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="3a264-109">Può essere personalizzato toorespond troppo[webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="3a264-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="3a264-110">Un [associazione di output HTTP](#output) consente toorespond toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a264-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="3a264-111">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-111">HTTP trigger</span></span>
<span data-ttu-id="3a264-112">trigger HTTP Hello eseguirà la funzione nella richiesta HTTP tooan di risposta.</span><span class="sxs-lookup"><span data-stu-id="3a264-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="3a264-113">È possibile personalizzarlo toorespond tooa determinato URL o un set di metodi HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a264-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="3a264-114">Un trigger HTTP può anche essere toowebhooks toorespond configurato.</span><span class="sxs-lookup"><span data-stu-id="3a264-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="3a264-115">Se tramite il portale di funzioni hello, è possibile inoltre iniziare subito usando un modello predefinito.</span><span class="sxs-lookup"><span data-stu-id="3a264-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="3a264-116">Selezionare **nuova funzione** e scegliere "Webhook & API" hello **Scenario** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="3a264-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="3a264-117">Selezionare uno dei modelli di hello e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="3a264-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="3a264-118">Per impostazione predefinita, un trigger HTTP risponderà toohello richiesta con un codice di stato HTTP 200 OK e un corpo vuoto.</span><span class="sxs-lookup"><span data-stu-id="3a264-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="3a264-119">toomodify risposta hello, configurare un [associazione di output HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="3a264-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="3a264-120">Configurazione di un trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="3a264-121">Includendo un toohello simile oggetto JSON seguente in hello è definito un trigger HTTP `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3a264-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="3a264-122">associazione di Hello supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a264-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="3a264-123">**nome** : obbligatorio - nome della variabile hello utilizzati nel codice della funzione per richiesta hello o il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a264-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="3a264-124">Vedere [Uso di un trigger HTTP dal codice](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="3a264-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="3a264-125">**tipo** : obbligatorio - deve essere impostato troppo "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="3a264-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="3a264-126">**direzione** : obbligatorio - deve essere impostato troppo "in".</span><span class="sxs-lookup"><span data-stu-id="3a264-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="3a264-127">_authLevel_ : questo parametro determina quali tasti, se presente, è necessario toobe presente nella richiesta di hello nella funzione di ordine tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="3a264-128">Vedere [Uso delle chiavi](#keys) più avanti.</span><span class="sxs-lookup"><span data-stu-id="3a264-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="3a264-129">il valore di Hello può essere uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="3a264-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="3a264-130">_anonymous_: nessuna chiave API obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="3a264-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="3a264-131">_function_: è obbligatoria una chiave API specifica della funzione.</span><span class="sxs-lookup"><span data-stu-id="3a264-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="3a264-132">Questo è il valore di predefinito hello se non è specificato.</span><span class="sxs-lookup"><span data-stu-id="3a264-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="3a264-133">_amministrazione_ : hello master chiave è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="3a264-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="3a264-134">**metodi** : si tratta di una matrice di metodi HTTP hello funzione hello toowhich risponderà.</span><span class="sxs-lookup"><span data-stu-id="3a264-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="3a264-135">Se non specificato, la funzione hello risponderà metodi tooall HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a264-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="3a264-136">Vedere [personalizzazione endpoint HTTP hello](#url).</span><span class="sxs-lookup"><span data-stu-id="3a264-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="3a264-137">**route** : definisce il modello di route hello, controllo toowhich URL risponderà la funzione richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a264-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="3a264-138">Hello valore predefinito se non è specificato è `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="3a264-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="3a264-139">Vedere [personalizzazione endpoint HTTP hello](#url).</span><span class="sxs-lookup"><span data-stu-id="3a264-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="3a264-140">**webHookType** : hello HTTP trigger tooact viene quindi configurato come il ricevitore un webhook per provider specificato hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="3a264-141">Hello _metodi_ proprietà non deve essere impostata se si è scelto.</span><span class="sxs-lookup"><span data-stu-id="3a264-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="3a264-142">Vedere [toowebhooks risposta](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="3a264-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="3a264-143">il valore di Hello può essere uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="3a264-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="3a264-144">_genericJson_: endpoint di webhook per utilizzo generico senza logica per un provider specifico.</span><span class="sxs-lookup"><span data-stu-id="3a264-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="3a264-145">_github_ : funzione hello risponderà tooGitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="3a264-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="3a264-146">Hello _authLevel_ proprietà non deve essere impostata se si è scelto.</span><span class="sxs-lookup"><span data-stu-id="3a264-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="3a264-147">_il margine di flessibilità_ : funzione hello risponderà tooSlack webhook.</span><span class="sxs-lookup"><span data-stu-id="3a264-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="3a264-148">Hello _authLevel_ proprietà non deve essere impostata se si è scelto.</span><span class="sxs-lookup"><span data-stu-id="3a264-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="3a264-149">Uso di un trigger HTTP dal codice</span><span class="sxs-lookup"><span data-stu-id="3a264-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="3a264-150">Per le funzioni di c# e F #, è possibile dichiarare il tipo di hello di toobe di input il trigger è `HttpRequestMessage` o un tipo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3a264-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="3a264-151">Se si sceglie `HttpRequestMessage`, si otterrà un oggetto di richiesta di accesso completo toohello.</span><span class="sxs-lookup"><span data-stu-id="3a264-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="3a264-152">Per un tipo personalizzato (ad esempio un POCO), funzioni tenterà il corpo della richiesta hello tooparse come proprietà dell'oggetto JSON toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="3a264-153">Per le funzioni di Node.js, hello funzioni runtime fornisce il corpo della richiesta hello anziché l'oggetto richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="3a264-154">Vedere [Esempi di trigger HTTP](#httptriggersample) per gli utilizzi di esempio.</span><span class="sxs-lookup"><span data-stu-id="3a264-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="3a264-155">Associazione di output della risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-155">HTTP response output binding</span></span>
<span data-ttu-id="3a264-156">Utilizzare hello output associazione toorespond toohello HTTP richiesta mittente HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a264-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="3a264-157">Questa associazione consente risposta hello toocustomize associata alla richiesta del trigger hello e richiede un trigger HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a264-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="3a264-158">Se non viene specificata un'associazione di output HTTP, un trigger HTTP restituirà HTTP 200 OK con un corpo vuoto.</span><span class="sxs-lookup"><span data-stu-id="3a264-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="3a264-159">Configurazione di un'associazione di output HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="3a264-160">output di Hello HTTP viene definita l'associazione includendo un toohello simile oggetto JSON seguente in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3a264-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="3a264-161">associazione di Hello contiene hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="3a264-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="3a264-162">**nome** : obbligatorio - hello nome della variabile utilizzata nel codice di funzione per hello risposta.</span><span class="sxs-lookup"><span data-stu-id="3a264-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="3a264-163">Vedere [Uso di un'associazione di output HTTP dal codice](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="3a264-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="3a264-164">**tipo** : obbligatorio - deve essere impostato troppo "http".</span><span class="sxs-lookup"><span data-stu-id="3a264-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="3a264-165">**direzione** : obbligatorio - deve essere impostato troppo "out".</span><span class="sxs-lookup"><span data-stu-id="3a264-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="3a264-166">Uso di un'associazione di output HTTP dal codice</span><span class="sxs-lookup"><span data-stu-id="3a264-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="3a264-167">È possibile utilizzare hello output parametro (ad esempio, "Risoluzione") toorespond toohello http o webhook chiamante.</span><span class="sxs-lookup"><span data-stu-id="3a264-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="3a264-168">In alternativa, è possibile utilizzare lo standard `Request.CreateResponse()` (c#) o `context.res` tooreturn modello (Node.JS) nella risposta.</span><span class="sxs-lookup"><span data-stu-id="3a264-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="3a264-169">Per esempi su come toouse hello quest'ultimo metodo, vedere [esempi di trigger HTTP](#httptriggersample) e [esempi di trigger Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="3a264-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="3a264-170">Risponde toowebhooks</span><span class="sxs-lookup"><span data-stu-id="3a264-170">Responding toowebhooks</span></span>
<span data-ttu-id="3a264-171">Un trigger HTTP con hello _webHookType_ proprietà sarà configurato toorespond troppo[webhook](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="3a264-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="3a264-172">configurazione di base Hello utilizza l'impostazione "genericJson" hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="3a264-173">Questo limita richieste tooonly quelle che usano HTTP POST e con hello `application/json` tipo di contenuto.</span><span class="sxs-lookup"><span data-stu-id="3a264-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="3a264-174">Hello trigger può inoltre essere personalizzati tooa webhook specifici provider (ad esempio, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="3a264-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="3a264-175">Se viene specificato un provider, hello funzioni runtime può svolgere della logica di convalida del provider di hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3a264-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="3a264-176">Configurazione di GitHub come provider di webhook</span><span class="sxs-lookup"><span data-stu-id="3a264-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="3a264-177">toorespond tooGitHub webhook, innanzitutto creare una funzione con un Trigger di HTTP e imposta hello _webHookType_ proprietà troppo "github".</span><span class="sxs-lookup"><span data-stu-id="3a264-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="3a264-178">Copiare quindi l'[URL](#url) e la [chiave API](#keys) nella pagina **Add webhook** (Aggiungi webhook) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a264-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="3a264-179">Per altre informazioni, vedere la documentazione [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) (Creazione di webhook) di GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a264-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="3a264-180">Configurazione di Slack come provider di webhook</span><span class="sxs-lookup"><span data-stu-id="3a264-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="3a264-181">Hello Slack webhook genera un token per l'utente invece che consente di specificare, pertanto è necessario configurare una chiave specifica con token hello da Slack.</span><span class="sxs-lookup"><span data-stu-id="3a264-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="3a264-182">Vedere [Uso delle chiavi](#keys).</span><span class="sxs-lookup"><span data-stu-id="3a264-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="3a264-183">Personalizzazione di endpoint HTTP hello</span><span class="sxs-lookup"><span data-stu-id="3a264-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="3a264-184">Per impostazione predefinita quando si crea una funzione per un trigger HTTP o WebHook, la funzione hello è indirizzabile tramite una route di form hello:</span><span class="sxs-lookup"><span data-stu-id="3a264-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="3a264-185">È possibile personalizzare questa route tramite hello facoltativo `route` proprietà trigger hello HTTP l'input dell'associazione.</span><span class="sxs-lookup"><span data-stu-id="3a264-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="3a264-186">Ad esempio, hello seguente *function.json* file definisce un `route` proprietà per un trigger HTTP:</span><span class="sxs-lookup"><span data-stu-id="3a264-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="3a264-187">Con questa configurazione, la funzione hello è indirizzabile con hello successivo itinerario anziché route originale hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="3a264-188">In questo modo il codice di funzione hello toosupport due parametri indirizzo hello, "category" e "id".</span><span class="sxs-lookup"><span data-stu-id="3a264-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="3a264-189">I parametri sono compatibili con qualsiasi [vincolo di route dell'API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints).</span><span class="sxs-lookup"><span data-stu-id="3a264-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="3a264-190">Hello seguente di codice della funzione in c# si avvalgono di entrambi i parametri.</span><span class="sxs-lookup"><span data-stu-id="3a264-190">hello following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="3a264-191">Qui è Node.js funzione codice toouse hello stessi parametri di route.</span><span class="sxs-lookup"><span data-stu-id="3a264-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="3a264-192">Per impostazione predefinita, tutte le route di funzione sono precedute da *api*.</span><span class="sxs-lookup"><span data-stu-id="3a264-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="3a264-193">È anche possibile personalizzare o rimuovere il prefisso di hello utilizzando hello `http.routePrefix` proprietà il *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="3a264-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="3a264-194">esempio Hello rimuove hello *api* prefisso della route utilizzando una stringa vuota per il prefisso di hello in hello *host.json* file.</span><span class="sxs-lookup"><span data-stu-id="3a264-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="3a264-195">Per informazioni dettagliate su come hello tooupdate *host.json* file per la funzione, vedere [funzionamento di file dell'app tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="3a264-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="3a264-196">Per informazioni su altre proprietà che è possibile configurare nel file *host.json*, vedere il [riferimento su host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="3a264-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="3a264-197">Uso delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a264-197">Working with keys</span></span>
<span data-ttu-id="3a264-198">Gli elementi HttpTrigger possono sfruttare le chiavi per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3a264-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="3a264-199">Un HttpTrigger standard possibile utilizzare queste informazioni come una chiave API, che richiedono toobe chiave hello hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="3a264-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="3a264-200">Webhook è possono utilizzare chiavi tooauthorize richieste in diversi modi, a seconda di quale provider hello supporta.</span><span class="sxs-lookup"><span data-stu-id="3a264-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="3a264-201">Le chiavi vengono archiviate come parte dell'app per le funzioni in Azure e crittografate inattive.</span><span class="sxs-lookup"><span data-stu-id="3a264-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="3a264-202">tooview le chiavi, creare nuovi o toonew valori delle chiavi di raggruppamento, passare tooone delle funzioni nel portale di hello e selezionare "Gestisci".</span><span class="sxs-lookup"><span data-stu-id="3a264-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="3a264-203">Esistono due tipi di chiavi:</span><span class="sxs-lookup"><span data-stu-id="3a264-203">There are two types of keys:</span></span>
- <span data-ttu-id="3a264-204">**Host chiavi**: queste chiavi sono condivisi da tutte le funzioni all'interno di app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="3a264-205">Quando viene utilizzata come una chiave API, questi consente accesso tooany funzione all'interno di app di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="3a264-206">**Tasti funzione**: queste chiavi si applicano solo toohello funzioni specifiche in cui sono definiti.</span><span class="sxs-lookup"><span data-stu-id="3a264-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="3a264-207">Quando viene utilizzata come una chiave API, solo consente accesso toothat funzione.</span><span class="sxs-lookup"><span data-stu-id="3a264-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="3a264-208">Ogni chiave è denominato per riferimento e a livello di funzione e host hello è una chiave predefinita (denominata "default").</span><span class="sxs-lookup"><span data-stu-id="3a264-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="3a264-209">Hello **chiave master** è una chiave host predefinita denominata "_master" che è definita per ogni app di funzione e non può essere revocata.</span><span class="sxs-lookup"><span data-stu-id="3a264-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="3a264-210">Fornisce l'API di runtime toohello accesso amministrativo.</span><span class="sxs-lookup"><span data-stu-id="3a264-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="3a264-211">Utilizzando `"authLevel": "admin"` in hello associazione JSON richiederà questa chiave toobe presentato su richiesta hello; qualsiasi altro tasto comporterà un errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="3a264-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="3a264-212">Scadenza toohello elevati le autorizzazioni consentite dalla chiave master di hello, è consigliabile non condividono questa chiave con terze parti o distribuirlo nelle applicazioni client native.</span><span class="sxs-lookup"><span data-stu-id="3a264-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="3a264-213">Prestare attenzione quando si sceglie di livello di autorizzazione di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="3a264-214">Autorizzazione della chiave API</span><span class="sxs-lookup"><span data-stu-id="3a264-214">API key authorization</span></span>
<span data-ttu-id="3a264-215">Per impostazione predefinita, un HttpTrigger richiede una chiave API nella richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="3a264-216">La richiesta HTTP in genere è quindi simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3a264-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="3a264-217">chiave Hello può essere incluso in una variabile di stringa di query denominata `code`, come sopra, o può essere incluso un `x-functions-key` intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="3a264-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="3a264-218">il valore di Hello della chiave hello può essere qualsiasi tasto di funzione definiti per la funzione hello o qualsiasi chiave host.</span><span class="sxs-lookup"><span data-stu-id="3a264-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="3a264-219">È possibile scegliere le richieste di tooallow senza chiavi o specificare la chiave master di hello deve essere usata da modifica hello `authLevel` proprietà hello associazione JSON (vedere [trigger HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="3a264-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="3a264-220">Chiavi e webhook</span><span class="sxs-lookup"><span data-stu-id="3a264-220">Keys and webhooks</span></span>
<span data-ttu-id="3a264-221">Parte di hello HttpTrigger e il meccanismo di hello varia in base al tipo webhook hello Webhook l'autorizzazione viene gestita dal componente di hello webhook il ricevitore.</span><span class="sxs-lookup"><span data-stu-id="3a264-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="3a264-222">Ogni meccanismo tuttavia si basa su una chiave.</span><span class="sxs-lookup"><span data-stu-id="3a264-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="3a264-223">Per impostazione predefinita, verrà utilizzato il tasto di funzione hello denominato "default".</span><span class="sxs-lookup"><span data-stu-id="3a264-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="3a264-224">Se si desidera toouse una chiave diversa, occorre tooconfigure hello webhook toosend hello Nome chiave del provider con richiesta di hello in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="3a264-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="3a264-225">**Stringa di query**: provider hello passa nome della chiave hello hello `clientid` parametro della stringa di query (ad esempio, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="3a264-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="3a264-226">**Intestazione della richiesta**: provider hello passa nome della chiave hello hello `x-functions-clientid` intestazione.</span><span class="sxs-lookup"><span data-stu-id="3a264-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="3a264-227">Le chiavi di funzione hanno la precedenza sulle chiavi host.</span><span class="sxs-lookup"><span data-stu-id="3a264-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="3a264-228">Se due chiavi sono definite con stesso nome, hello hello funzione chiave verrà usata.</span><span class="sxs-lookup"><span data-stu-id="3a264-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="3a264-229">Esempi di trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="3a264-229">HTTP trigger samples</span></span>
<span data-ttu-id="3a264-230">Si supponga di avere seguito trigger HTTP hello hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3a264-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="3a264-231">Vedere l'esempio specifico del linguaggio hello che cerca un `name` parametro nella stringa di query hello o corpo hello della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="3a264-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="3a264-232">C#</span><span class="sxs-lookup"><span data-stu-id="3a264-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="3a264-233">F#</span><span class="sxs-lookup"><span data-stu-id="3a264-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="3a264-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3a264-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="3a264-235">Esempio di trigger HTTP in C#</span><span class="sxs-lookup"><span data-stu-id="3a264-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="3a264-236">È anche possibile associare tooa POCO anziché `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="3a264-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="3a264-237">Questo sarà possibile Alluminosilicato dal corpo hello della richiesta di hello, analizzato come JSON.</span><span class="sxs-lookup"><span data-stu-id="3a264-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="3a264-238">Analogamente, un tipo può essere passato a un output di risposta HTTP toohello associazione e verrà restituito come corpo della risposta hello, con un codice di 200 stato.</span><span class="sxs-lookup"><span data-stu-id="3a264-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="3a264-239">Esempio di trigger HTTP in F#</span><span class="sxs-lookup"><span data-stu-id="3a264-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="3a264-240">È necessario un `project.json` file che usa NuGet tooreference hello `FSharp.Interop.Dynamic` e `Dynamitey` assembly, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3a264-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="3a264-241">Si utilizzeranno toofetch NuGet le dipendenze e farà riferimento a essi nello script.</span><span class="sxs-lookup"><span data-stu-id="3a264-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="3a264-242">Esempio di trigger HTTP in Node.JS</span><span class="sxs-lookup"><span data-stu-id="3a264-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="3a264-243">Esempi di webhook</span><span class="sxs-lookup"><span data-stu-id="3a264-243">Webhook samples</span></span>
<span data-ttu-id="3a264-244">Si supponga di avere seguito trigger webhook hello hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="3a264-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="3a264-245">Vedere l'esempio specifico del linguaggio hello che registra i commenti problema GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a264-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="3a264-246">C#</span><span class="sxs-lookup"><span data-stu-id="3a264-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="3a264-247">F#</span><span class="sxs-lookup"><span data-stu-id="3a264-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="3a264-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="3a264-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="3a264-249">Esempio di webhook in C#</span><span class="sxs-lookup"><span data-stu-id="3a264-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="3a264-250">Esempio di webhook in F#</span><span class="sxs-lookup"><span data-stu-id="3a264-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="3a264-251">Esempio di webhook in Node.JS</span><span class="sxs-lookup"><span data-stu-id="3a264-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="3a264-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a264-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

