---
title: aaaCreate un'API senza server utilizzando le funzioni di Azure | Documenti Microsoft
description: Come toocreate un'API senza server utilizzando le funzioni di Azure
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="4ef4b-103">Creare un'API senza server mediante Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4ef4b-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="4ef4b-104">In questa esercitazione verrà illustrato come le funzioni di Azure consente toobuild API altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="4ef4b-105">Funzioni di Azure include una raccolta incorporata HTTP e le associazioni che rendono facilmente tooauthor un endpoint in una vasta gamma di linguaggi, tra cui Node.JS, c# e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="4ef4b-106">In questa esercitazione si personalizzerà un azioni specifiche di HTTP trigger toohandle nella progettazione delle API.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="4ef4b-107">Ci si preparerà inoltre a far crescere l'API integrandola con i proxy di Funzioni di Azure e a configurare API fittizie.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="4ef4b-108">Tutto ciò avviene su hello funzioni senza ambiente di calcolo, in modo non si dispone di tooworry sulla scalabilità delle risorse: è possibile concentrarsi solo alla logica di API.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ef4b-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ef4b-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="4ef4b-110">funzione risultante Hello da utilizzare per il resto di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="4ef4b-111">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="4ef4b-111">Sign in tooAzure</span></span>

<span data-ttu-id="4ef4b-112">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-112">Open hello Azure portal.</span></span> <span data-ttu-id="4ef4b-113">toodo, accedi troppo[https://portal.azure.com](https://portal.azure.com) con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="4ef4b-114">Personalizzare la funzione HTTP</span><span class="sxs-lookup"><span data-stu-id="4ef4b-114">Customize your HTTP function</span></span>

<span data-ttu-id="4ef4b-115">Per impostazione predefinita, la funzione di attivazione HTTP è configurato tooaccept qualsiasi metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="4ef4b-116">È inoltre disponibile un URL predefinito del modulo di hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="4ef4b-117">Se si sono seguite Guide rapide hello, quindi `<funcname>` probabilmente ha un aspetto simile al seguente "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="4ef4b-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="4ef4b-118">In questa sezione, si modificherà hello funzione toorespond tooGET solo delle richieste pervenute `/api/hello` invece di routing.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="4ef4b-119">Passare la funzione tooyour in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="4ef4b-120">Selezionare **integrazione** nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-120">Select **Integrate** in hello left navigation.</span></span>

![Personalizzazione di una funzione HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="4ef4b-122">Utilizzare le impostazioni di trigger HTTP come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="4ef4b-123">Campo</span><span class="sxs-lookup"><span data-stu-id="4ef4b-123">Field</span></span> | <span data-ttu-id="4ef4b-124">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="4ef4b-124">Sample value</span></span> | <span data-ttu-id="4ef4b-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="4ef4b-126">Metodi HTTP consentiti</span><span class="sxs-lookup"><span data-stu-id="4ef4b-126">Allowed HTTP methods</span></span> | <span data-ttu-id="4ef4b-127">Metodi selezionati</span><span class="sxs-lookup"><span data-stu-id="4ef4b-127">Selected methods</span></span> | <span data-ttu-id="4ef4b-128">Determina quali metodi HTTP possono essere utilizzato tooinvoke questa funzione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="4ef4b-129">Metodi HTTP selezionati</span><span class="sxs-lookup"><span data-stu-id="4ef4b-129">Selected HTTP methods</span></span> | <span data-ttu-id="4ef4b-130">GET</span><span class="sxs-lookup"><span data-stu-id="4ef4b-130">GET</span></span> | <span data-ttu-id="4ef4b-131">Consente solo toobe metodi HTTP selezionato usati tooinvoke questa funzione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="4ef4b-132">Modello di route</span><span class="sxs-lookup"><span data-stu-id="4ef4b-132">Route template</span></span> | <span data-ttu-id="4ef4b-133">/hello</span><span class="sxs-lookup"><span data-stu-id="4ef4b-133">/hello</span></span> | <span data-ttu-id="4ef4b-134">Determina la route è tooinvoke utilizzata questa funzione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="4ef4b-135">Si noti che non include hello `/api` prefisso di percorso nel modello di route hello, di base come questa operazione viene gestita da un'impostazione globale.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="4ef4b-136">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-136">Click **Save**.</span></span>

<span data-ttu-id="4ef4b-137">Altre informazioni sulla personalizzazione delle funzioni HTTP sono riportate in [Binding Azure HTTP e webhook di Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="4ef4b-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="4ef4b-138">Testare l'API</span><span class="sxs-lookup"><span data-stu-id="4ef4b-138">Test your API</span></span>

<span data-ttu-id="4ef4b-139">Quindi, testarlo toosee la funzione utilizzo superficie dell'API nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="4ef4b-140">Passare pagina sviluppo toohello indietro facendo clic sul nome della funzione hello in hello riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="4ef4b-141">Fare clic su **ottenere l'URL di funzione** e copiare l'URL di hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="4ef4b-142">Si noterà che usa hello `/api/hello` indirizzare ora.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="4ef4b-143">Copiare l'URL di hello in una nuova scheda del browser o un client REST preferito.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="4ef4b-144">I browser useranno GET per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="4ef4b-145">Eseguire la funzione hello e confermare che è in corso.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="4ef4b-146">Parametro "name" di hello tooprovide potrebbe essere necessario un codice di avvio rapido query stringa toosatisfy hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="4ef4b-147">È anche possibile richiamare l'endpoint di hello con un altro tooconfirm di metodo HTTP che la funzione hello non viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="4ef4b-148">A tale scopo, è necessario un client REST, ad esempio cURL, Postman o Fiddler toouse.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="4ef4b-149">Panoramica dei proxy</span><span class="sxs-lookup"><span data-stu-id="4ef4b-149">Proxies overview</span></span>

<span data-ttu-id="4ef4b-150">Nella sezione successiva hello, verrà di superficie dell'API tramite un proxy.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="4ef4b-151">Proxy di funzioni di Azure è una funzionalità di anteprima che consente di tooforward richieste tooother risorse.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="4ef4b-152">Si definisce un endpoint HTTP nello stesso modo con trigger HTTP, ma invece di scrivere codice tooexecute quando viene chiamato tale endpoint, si fornisce un'implementazione di URL tooa remota.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="4ef4b-153">In questo modo toocompose API più origini in una singola superficie API semplice per i client tooconsume.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="4ef4b-154">Ciò è particolarmente utile se si desidera toobuild dell'API come microservizi.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="4ef4b-155">Un proxy può puntare risorsa tooany HTTP, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ef4b-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="4ef4b-156">Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4ef4b-156">Azure Functions</span></span> 
- <span data-ttu-id="4ef4b-157">App per le API in [Servizio app di Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="4ef4b-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="4ef4b-158">Contenitori docker in [Servizio App in Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="4ef4b-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="4ef4b-159">Qualsiasi altra API in hosting</span><span class="sxs-lookup"><span data-stu-id="4ef4b-159">Any other hosted API</span></span>

<span data-ttu-id="4ef4b-160">toolearn ulteriori informazioni sui proxy, vedere [utilizzo di proxy di funzioni di Azure (anteprima)].</span><span class="sxs-lookup"><span data-stu-id="4ef4b-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="4ef4b-161">Creare il primo proxy</span><span class="sxs-lookup"><span data-stu-id="4ef4b-161">Create your first proxy</span></span>

<span data-ttu-id="4ef4b-162">In questa sezione verrà creato un nuovo proxy che viene utilizzata come un front-end tooyour API complessiva.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="4ef4b-163">Impostazione di ambiente front-end hello</span><span class="sxs-lookup"><span data-stu-id="4ef4b-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="4ef4b-164">Ripetere i passaggi di hello troppo[creare un'app di funzione](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate una nuova app di funzione in cui verrà creato il proxy.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="4ef4b-165">Questa nuova applicazione verrà utilizzato come server front-end hello per API e app di funzione hello in precedenza, che si stava modificando fungerà da un back-end.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="4ef4b-166">Passare tooyour nuovo front-end funzione app nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="4ef4b-167">Selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-167">Select **Settings**.</span></span> <span data-ttu-id="4ef4b-168">Passare quindi **abilitare i proxy di funzioni di Azure (anteprima)** troppo "On".</span><span class="sxs-lookup"><span data-stu-id="4ef4b-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="4ef4b-169">Selezionare **Impostazioni piattaforma** e scegliere **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="4ef4b-170">Scorrere verso il basso troppo**impostazioni App** e creare una nuova impostazione con la chiave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="4ef4b-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="4ef4b-171">Impostare il relativo host toohello valore della funzione app back-end, ad esempio `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="4ef4b-172">Questo fa parte dell'URL hello copiato in precedenza durante il test di una funzione HTTP.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="4ef4b-173">Riferimento a questa impostazione nella configurazione hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="4ef4b-174">Le impostazioni dell'App sono consigliate per hello host configurazione tooprevent una dipendenza hardcoded di ambiente per il proxy di hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="4ef4b-175">Utilizzando le impostazioni dell'app indica che è possibile spostare la configurazione del proxy hello tra gli ambienti e verranno applicate le impostazioni specifiche dell'ambiente app hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="4ef4b-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="4ef4b-177">Creazione di un proxy in front-end hello</span><span class="sxs-lookup"><span data-stu-id="4ef4b-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="4ef4b-178">Spostarsi indietro tooyour front-end funzione app nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="4ef4b-179">Nella finestra di navigazione a sinistra di hello, fare clic su hello segno successivo '+' troppo "Proxy (anteprima)".</span><span class="sxs-lookup"><span data-stu-id="4ef4b-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Creazione di un proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="4ef4b-181">Utilizzare le impostazioni del proxy come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="4ef4b-182">Campo</span><span class="sxs-lookup"><span data-stu-id="4ef4b-182">Field</span></span> | <span data-ttu-id="4ef4b-183">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="4ef4b-183">Sample value</span></span> | <span data-ttu-id="4ef4b-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="4ef4b-185">Nome</span><span class="sxs-lookup"><span data-stu-id="4ef4b-185">Name</span></span> | <span data-ttu-id="4ef4b-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="4ef4b-186">HelloProxy</span></span> | <span data-ttu-id="4ef4b-187">Nome descrittivo utilizzato solo per la gestione</span><span class="sxs-lookup"><span data-stu-id="4ef4b-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="4ef4b-188">Modello di route</span><span class="sxs-lookup"><span data-stu-id="4ef4b-188">Route template</span></span> | <span data-ttu-id="4ef4b-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="4ef4b-189">/api/hello</span></span> | <span data-ttu-id="4ef4b-190">Determina la route è tooinvoke usato questo proxy</span><span class="sxs-lookup"><span data-stu-id="4ef4b-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="4ef4b-191">URL back-end</span><span class="sxs-lookup"><span data-stu-id="4ef4b-191">Backend URL</span></span> | <span data-ttu-id="4ef4b-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="4ef4b-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="4ef4b-193">Specifica richiesta di hello endpoint toowhich hello deve essere elaborata</span><span class="sxs-lookup"><span data-stu-id="4ef4b-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="4ef4b-194">Si noti che proxy non fornisce hello `/api` prefisso di percorso di base e questo deve essere incluso nel modello di route hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="4ef4b-195">Hello `%HELLO_HOST%` sintassi farà riferimento impostazione app hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="4ef4b-196">Hello risolto che URL punterà tooyour di funzione originale.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="4ef4b-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-197">Click **Create**.</span></span>

<span data-ttu-id="4ef4b-198">È possibile provare il nuovo proxy copiando hello URL del Proxy e testarlo nel browser hello o con il client HTTP preferito.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="4ef4b-199">Creare un'API fittizia</span><span class="sxs-lookup"><span data-stu-id="4ef4b-199">Create a mock API</span></span>

<span data-ttu-id="4ef4b-200">Successivamente, si utilizzerà un toocreate proxy un'API fittizia per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="4ef4b-201">In questo modo lo sviluppo di client tooprogress, senza la necessità di back-end hello implementata completamente.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="4ef4b-202">In un secondo momento in fase di sviluppo, è possibile creare una nuova app di funzione che supporta questa logica e reindirizzare tooit il proxy.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="4ef4b-203">toocreate questo modello API, si creerà un nuovo proxy, questa volta utilizzando hello [Editor di servizio App](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="4ef4b-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="4ef4b-204">tooget avviato, passare tooyour funzione app nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="4ef4b-205">Selezionare **Funzionalità della piattaforma** e trovare **Editor del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="4ef4b-206">Facendo clic su questa, hello Editor di servizio App verrà aperto in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="4ef4b-207">Selezionare `proxies.json` nel riquadro di spostamento sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="4ef4b-208">Si tratta di file hello che memorizza la configurazione di hello per tutti i proxy.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="4ef4b-209">Se si utilizza uno di hello [funzioni metodi di distribuzione](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), si tratta di file hello verranno mantenuti nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="4ef4b-210">toolearn informazioni su questo file, vedere [configurazione avanzata proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="4ef4b-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="4ef4b-211">Se è stato seguito fino a questo punto, il proxies.json dovrebbe essere simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ef4b-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="4ef4b-212">Ora si aggiungerà l'API fittizia.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-212">Next you'll add your mock API.</span></span> <span data-ttu-id="4ef4b-213">Sostituire il file proxies.json con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4ef4b-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="4ef4b-214">Aggiunge un nuovo proxy "GetUserByName", senza la proprietà backendUri hello.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="4ef4b-215">Invece di chiamare un'altra risorsa, viene modificata in risposta predefinita hello dal proxy utilizzando una sostituzione di risposta.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="4ef4b-216">È possibile anche usare gli override di richiesta e risposta in combinazione con un URL di back-end.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="4ef4b-217">Ciò è particolarmente utile quando l'inoltro dei dati tooa sistema legacy, in cui potrebbe essere necessario toomodify intestazioni, i parametri di query, toolearn e così via. ulteriori informazioni sulla richiesta e risposta sostituzioni, vedere [modifica richieste e risposte in proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="4ef4b-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="4ef4b-218">Per testare l'API fittizio hello chiamante `/api/users/{username}` endpoint utilizzando un browser o un client REST preferito.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="4ef4b-219">Tooreplace assicurarsi di essere _{username}_ con un valore stringa che rappresenta un nome utente.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef4b-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ef4b-220">Next steps</span></span>

<span data-ttu-id="4ef4b-221">In questa esercitazione, si è appreso come toobuild e personalizzare un'API sulle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="4ef4b-222">È stato inoltre descritto come toobring più le API, inclusi mocks, insieme come una superficie API unificata.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="4ef4b-223">È possibile utilizzare queste tecniche toobuild all'API di qualsiasi complessità, tutte durante l'esecuzione in modalità hello calcolo modello fornito dalle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef4b-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="4ef4b-224">Hello riferimenti seguenti possono essere utili quando si sviluppa ulteriormente l'API:</span><span class="sxs-lookup"><span data-stu-id="4ef4b-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="4ef4b-225">Binding HTTP e webhook di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4ef4b-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="4ef4b-226">[utilizzo di proxy di funzioni di Azure (anteprima)]</span><span class="sxs-lookup"><span data-stu-id="4ef4b-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="4ef4b-227">Documentazione di un'API di Funzioni di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4ef4b-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[utilizzo di proxy di funzioni di Azure (anteprima)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
