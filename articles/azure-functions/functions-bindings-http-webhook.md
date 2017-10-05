---
title: Associazioni HTTP e webhook in Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare trigger e associazioni HTTP e webhookin Funzioni di Azure.
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
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="7bd8d-104">Associazioni HTTP e webhook in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="7bd8d-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="7bd8d-105">Questo articolo illustra come configurare e usare trigger e associazioni HTTP in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="7bd8d-106">In questo modo è possibile usare Funzioni di Azure per compilare API senza server e rispondere ai webhook.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="7bd8d-107">Funzioni di Azure fornisce le associazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="7bd8d-108">Un [trigger HTTP](#httptrigger) consente di richiamare una funzione con una richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="7bd8d-109">e può essere personalizzato per rispondere ai [webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="7bd8d-110">Un'[associazione di output HTTP](#output) consente di rispondere alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="7bd8d-111">Trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-111">HTTP trigger</span></span>
<span data-ttu-id="7bd8d-112">Il trigger HTTP eseguirà la funzione in risposta a una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="7bd8d-113">È possibile personalizzarlo per rispondere a un particolare URL o set di metodi HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="7bd8d-114">Un trigger HTTP può essere configurato anche per rispondere ai webhook.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="7bd8d-115">Se si usa il portale di Funzioni, è anche possibile iniziare subito a usare un modello predefinito.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="7bd8d-116">Selezionare **Nuova funzione** e scegliere "API e webhook" dal menu a discesa **Scenario**.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="7bd8d-117">Selezionare uno dei modelli e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="7bd8d-118">Per impostazione predefinita, un trigger HTTP risponderà alla richiesta con un codice di stato HTTP 200 OK e un corpo vuoto.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="7bd8d-119">Per modificare la risposta, configurare un'[associazione di output HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="7bd8d-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="7bd8d-120">Configurazione di un trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="7bd8d-121">Un trigger HTTP viene definito includendo un oggetto JSON simile al seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="7bd8d-122">L'associazione supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="7bd8d-123">**name**: obbligatoria. Nome della variabile usato nel codice della funzione per la richiesta o il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="7bd8d-124">Vedere [Uso di un trigger HTTP dal codice](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="7bd8d-125">**type**: obbligatoria. Deve essere impostata su "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="7bd8d-126">**direction**: obbligatoria. Deve essere impostata su "in".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="7bd8d-127">_authLevel_: determina le eventuali chiavi che devono essere presenti nella richiesta per richiamare la funzione.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="7bd8d-128">Vedere [Uso delle chiavi](#keys) più avanti.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="7bd8d-129">Il valore può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="7bd8d-130">_anonymous_: nessuna chiave API obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="7bd8d-131">_function_: è obbligatoria una chiave API specifica della funzione.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="7bd8d-132">Questo è il valore predefinito se non ne viene specificato nessuno.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="7bd8d-133">_admin_: la chiave master è obbligatoria.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="7bd8d-134">**methods**: matrice dei metodi HTTP a cui la funzione risponderà.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="7bd8d-135">Se non viene specificata, la funzione risponderà a tutti i metodi HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="7bd8d-136">Vedere [Personalizzazione dell'endpoint HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="7bd8d-137">**route**: definisce il modello di route, controllando a quali URL delle richieste la funzione risponderà.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="7bd8d-138">Il valore predefinito, se non ne viene specificato nessuno, è `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="7bd8d-139">Vedere [Personalizzazione dell'endpoint HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="7bd8d-140">**webHookType**: configura il trigger HTTP perché funga da ricevitore webhook per il provider specificato.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="7bd8d-141">Se viene scelto questo valore, la proprietà _methods_ non deve essere impostata.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="7bd8d-142">Vedere [Risposta ai webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="7bd8d-143">Il valore può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="7bd8d-144">_genericJson_: endpoint di webhook per utilizzo generico senza logica per un provider specifico.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="7bd8d-145">_github_: la funzione risponderà ai webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="7bd8d-146">Se viene scelto questo valore, la proprietà _authLevel_ non deve essere impostata.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="7bd8d-147">_slack_: la funzione risponderà ai webhook Slack.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="7bd8d-148">Se viene scelto questo valore, la proprietà _authLevel_ non deve essere impostata.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="7bd8d-149">Uso di un trigger HTTP dal codice</span><span class="sxs-lookup"><span data-stu-id="7bd8d-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="7bd8d-150">Per le funzioni C# e F#, è possibile dichiarare `HttpRequestMessage` o un tipo personalizzato come tipo dell'input del trigger.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="7bd8d-151">Se si sceglie `HttpRequestMessage`, si otterrà l'accesso completo all'oggetto richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="7bd8d-152">Per un tipo personalizzato (ad esempio, POCO), Funzioni cercherà di analizzare il corpo della richiesta come JSON per popolare le proprietà dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="7bd8d-153">Per le funzioni Node.js, il runtime di Funzioni fornisce il corpo della richiesta invece dell'oggetto richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="7bd8d-154">Vedere [Esempi di trigger HTTP](#httptriggersample) per gli utilizzi di esempio.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="7bd8d-155">Associazione di output della risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-155">HTTP response output binding</span></span>
<span data-ttu-id="7bd8d-156">Usare l'associazione di output HTTP per rispondere al mittente della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="7bd8d-157">Questa associazione richiede un trigger HTTP e consente di personalizzare la risposta associata alla richiesta del trigger.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="7bd8d-158">Se non viene specificata un'associazione di output HTTP, un trigger HTTP restituirà HTTP 200 OK con un corpo vuoto.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="7bd8d-159">Configurazione di un'associazione di output HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="7bd8d-160">L'associazione di output HTTP viene definita includendo un oggetto JSON simile al seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="7bd8d-161">L'associazione contiene le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="7bd8d-162">**name**: obbligatoria. Nome della variabile usato nel codice della funzione per la risposta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="7bd8d-163">Vedere [Uso di un'associazione di output HTTP dal codice](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="7bd8d-164">**type**: obbligatoria. Deve essere impostata su "http".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="7bd8d-165">**direction**: obbligatoria. Deve essere impostata su "out".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="7bd8d-166">Uso di un'associazione di output HTTP dal codice</span><span class="sxs-lookup"><span data-stu-id="7bd8d-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="7bd8d-167">È possibile usare il parametro di output (ad esempio, "res") per rispondere al chiamante HTTP o webhook.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="7bd8d-168">In alternativa, è possibile usare il modello standard `Request.CreateResponse()` (C#) o `context.res` (Node.JS) per restituire la risposta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="7bd8d-169">Per esempi di come usare il secondo metodo, vedere [Esempi di trigger HTTP](#httptriggersample) ed [Esempi di trigger webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="7bd8d-170">Risposta ai webhook</span><span class="sxs-lookup"><span data-stu-id="7bd8d-170">Responding to webhooks</span></span>
<span data-ttu-id="7bd8d-171">Un trigger HTTP con la proprietà _webHookType_ verrà configurato per rispondere ai [webhook](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="7bd8d-172">La configurazione di base usa l'impostazione "genericJson",</span><span class="sxs-lookup"><span data-stu-id="7bd8d-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="7bd8d-173">che limita le richieste solo a quelle che usano HTTP POST e con il tipo di contenuto `application/json`.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="7bd8d-174">Il trigger può anche essere personalizzato per un provider di webhook specifico (ad esempio, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="7bd8d-175">Se viene specificato un provider, il runtime di Funzioni può eseguire automaticamente la logica di convalida del provider.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="7bd8d-176">Configurazione di GitHub come provider di webhook</span><span class="sxs-lookup"><span data-stu-id="7bd8d-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="7bd8d-177">Per rispondere ai webhook GitHub, creare prima di tutto la funzione con un trigger HTTP e impostare la proprietà _webHookType_ su "github".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="7bd8d-178">Copiare quindi l'[URL](#url) e la [chiave API](#keys) nella pagina **Add webhook** (Aggiungi webhook) del repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="7bd8d-179">Per altre informazioni, vedere la documentazione [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) (Creazione di webhook) di GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="7bd8d-180">Configurazione di Slack come provider di webhook</span><span class="sxs-lookup"><span data-stu-id="7bd8d-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="7bd8d-181">Il webhook Slack genera automaticamente un token invece di consentire di specificarlo, quindi è necessario configurare una chiave specifica della funzione con il token da Slack.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="7bd8d-182">Vedere [Uso delle chiavi](#keys).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="7bd8d-183">Personalizzazione dell'endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="7bd8d-184">Per impostazione predefinita, quando si crea una funzione per un trigger HTTP o un webhook, la funzione può essere indirizzata con una route nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="7bd8d-185">È possibile personalizzare questa route tramite la proprietà `route` facoltativa nell'associazione di input del trigger HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="7bd8d-186">Ad esempio, il file *function.json* seguente definisce una proprietà `route` per un trigger HTTP:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="7bd8d-187">Con questa configurazione, la funzione può ora essere indirizzata con la route seguente invece che con quella originale.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="7bd8d-188">In questo modo il codice della funzione può supportare due parametri nell'indirizzo: "category" e "id".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="7bd8d-189">I parametri sono compatibili con qualsiasi [vincolo di route dell'API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="7bd8d-190">Il codice di funzione C# seguente usa entrambi i parametri.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="7bd8d-191">Di seguito è mostrato il codice di funzione Node.js per usare gli stessi parametri di route.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="7bd8d-192">Per impostazione predefinita, tutte le route di funzione sono precedute da *api*.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="7bd8d-193">È inoltre possibile personalizzare o rimuovere il prefisso con la proprietà `http.routePrefix` nel file *host.json*.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="7bd8d-194">Nell'esempio seguente viene rimosso il prefisso della route *api* usando una stringa vuota per il prefisso nel file *host.json*.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="7bd8d-195">Per informazioni dettagliate su come aggiornare il file *host.json* per la funzione, vedere [Come aggiornare i file nelle app per le funzioni](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="7bd8d-196">Per informazioni su altre proprietà che è possibile configurare nel file *host.json*, vedere il [riferimento su host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="7bd8d-197">Uso delle chiavi</span><span class="sxs-lookup"><span data-stu-id="7bd8d-197">Working with keys</span></span>
<span data-ttu-id="7bd8d-198">Gli elementi HttpTrigger possono sfruttare le chiavi per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="7bd8d-199">Un elemento HttpTrigger standard può usarle come chiave API, imponendo la presenza della chiave nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="7bd8d-200">I webhook possono usare le chiavi per autorizzare le richieste in svariati modi, a seconda di ciò che il provider supporta.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="7bd8d-201">Le chiavi vengono archiviate come parte dell'app per le funzioni in Azure e crittografate inattive.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="7bd8d-202">Per visualizzare le chiavi, crearne di nuove o aggiornare le chiavi con nuovi valori, passare a una delle funzioni nel portale e selezionare "Gestisci".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="7bd8d-203">Esistono due tipi di chiavi:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-203">There are two types of keys:</span></span>
- <span data-ttu-id="7bd8d-204">**Chiavi host**: queste chiavi vengono condivise da tutte le funzioni nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="7bd8d-205">Quando vengono usate come chiave API, consentono l'accesso a tutte le funzioni nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="7bd8d-206">**Chiavi di funzione**: queste chiavi si applicano solo alle funzioni specifiche sotto le quali vengono definite.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="7bd8d-207">Quando vengono usate come chiave API, consentono l'accesso solo a tale funzione.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="7bd8d-208">Ogni chiave viene denominata per riferimento ed esiste una chiave predefinita (denominata "default") a livello di funzione e di host.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="7bd8d-209">La **chiave master** è una chiave host predefinita denominata "_master" che viene definita per ogni app per le funzioni e non può essere revocata.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="7bd8d-210">Fornisce l'accesso amministrativo alle API di runtime.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="7bd8d-211">Per usare `"authLevel": "admin"` nel file JSON di associazione, nella richiesta dovrà essere presentata questa chiave. Qualsiasi altra chiave restituirà un errore di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd8d-212">Date le autorizzazioni elevate concesse dalla chiave master, è consigliabile non condividere questa chiave con terze parti o distribuirla in applicazioni client native.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="7bd8d-213">Prestare attenzione quando si sceglie il livello di autorizzazione di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="7bd8d-214">Autorizzazione della chiave API</span><span class="sxs-lookup"><span data-stu-id="7bd8d-214">API key authorization</span></span>
<span data-ttu-id="7bd8d-215">Per impostazione predefinita, un elemento HttpTrigger richiede una chiave API nella richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="7bd8d-216">La richiesta HTTP in genere è quindi simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="7bd8d-217">La chiave può essere inclusa in una variabile della stringa di query denominata `code`, come sopra, oppure in un'intestazione HTTP `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="7bd8d-218">Il valore della chiave può essere una chiave di funzione definita per la funzione o una chiave host.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="7bd8d-219">È possibile scegliere di consentire le richieste senza chiavi o specificare che deve essere usata la chiave master modificando la proprietà `authLevel` nel file JSON dell'associazione. Vedere [Trigger HTTP](#httptrigger).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="7bd8d-220">Chiavi e webhook</span><span class="sxs-lookup"><span data-stu-id="7bd8d-220">Keys and webhooks</span></span>
<span data-ttu-id="7bd8d-221">L'autorizzazione webhook viene gestita dal componente ricevitore dei webhook, che fa parte di HttpTrigger, e il meccanismo varia in base al tipo di webhook.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="7bd8d-222">Ogni meccanismo tuttavia si basa su una chiave.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="7bd8d-223">Per impostazione predefinita, verrà usata la chiave di funzione denominata "default".</span><span class="sxs-lookup"><span data-stu-id="7bd8d-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="7bd8d-224">Per usare un'altra chiave, sarà necessario configurare il provider di webhook per inviare il nome della chiave con la richiesta in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="7bd8d-225">**Stringa di query**: il provider passa il nome della chiave nel parametro della stringa di query `clientid` (ad esempio, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="7bd8d-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="7bd8d-226">**Intestazione della richiesta**: il provider passa il nome della chiave nell'intestazione `x-functions-clientid`.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="7bd8d-227">Le chiavi di funzione hanno la precedenza sulle chiavi host.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="7bd8d-228">Se due chiavi sono definite con lo stesso nome, verrà usata la chiave di funzione.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="7bd8d-229">Esempi di trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="7bd8d-229">HTTP trigger samples</span></span>
<span data-ttu-id="7bd8d-230">Si supponga che il trigger HTTP seguente sia presente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="7bd8d-231">Vedere l'esempio specifico del linguaggio, che cerca un parametro `name` nella stringa di query o nel corpo della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="7bd8d-232">C#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="7bd8d-233">F#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="7bd8d-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7bd8d-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="7bd8d-235">Esempio di trigger HTTP in C#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-235">HTTP trigger sample in C#</span></span> #
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

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="7bd8d-236">È anche possibile eseguire l'associazione a un POCO invece di `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="7bd8d-237">POCO sarà idratato dal corpo della richiesta e analizzato come JSON.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="7bd8d-238">Analogamente, un tipo può essere passato all'associazione dell'output di risposta HTTP e verrà restituito come corpo della risposta, con un codice di stato 200.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="7bd8d-239">Esempio di trigger HTTP in F#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="7bd8d-240">È necessario un file `project.json` che usa NuGet per fare riferimento agli assembly `FSharp.Interop.Dynamic` e `Dynamitey` come segue:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="7bd8d-241">Verrà usato NuGet per recuperare le dipendenze e verrà creato un riferimento alle dipendenze nello script.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="7bd8d-242">Esempio di trigger HTTP in Node.JS</span><span class="sxs-lookup"><span data-stu-id="7bd8d-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="7bd8d-243">Esempi di webhook</span><span class="sxs-lookup"><span data-stu-id="7bd8d-243">Webhook samples</span></span>
<span data-ttu-id="7bd8d-244">Si supponga che il trigger webhook seguente sia presente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="7bd8d-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="7bd8d-245">Vedere l'esempio specifico del linguaggio che registra i commenti del problema GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bd8d-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="7bd8d-246">C#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="7bd8d-247">F#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="7bd8d-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="7bd8d-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="7bd8d-249">Esempio di webhook in C#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="7bd8d-250">Esempio di webhook in F#</span><span class="sxs-lookup"><span data-stu-id="7bd8d-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="7bd8d-251">Esempio di webhook in Node.JS</span><span class="sxs-lookup"><span data-stu-id="7bd8d-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="7bd8d-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bd8d-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

