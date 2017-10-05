---
title: Creare un'API senza server mediante Funzioni di Azure | Documentazione Microsoft
description: 'Procedura: creare un''API senza server mediante Funzioni di Azure'
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="9c18f-103">Creare un'API senza server mediante Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9c18f-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="9c18f-104">In questa esercitazione si apprenderà come Funzioni di Azure consente di creare API altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="9c18f-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="9c18f-105">Funzioni di Azure include una raccolta di trigger HTTP e binding integrati che semplificano la creazione di un endpoint in una varietà di linguaggi, inclusi Node.JS, C# e altri.</span><span class="sxs-lookup"><span data-stu-id="9c18f-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="9c18f-106">In questa esercitazione si personalizzerà un trigger HTTP per gestire azioni specifiche nella progettazione dell'API.</span><span class="sxs-lookup"><span data-stu-id="9c18f-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="9c18f-107">Ci si preparerà inoltre a far crescere l'API integrandola con i proxy di Funzioni di Azure e a configurare API fittizie.</span><span class="sxs-lookup"><span data-stu-id="9c18f-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="9c18f-108">Tutto ciò avviene nell'ambiente di calcolo senza server di Funzioni di Azure, pertanto non è necessario preoccuparsi della scalabilità delle risorse ma è possibile concentrarsi semplicemente sulla logica di API.</span><span class="sxs-lookup"><span data-stu-id="9c18f-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c18f-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c18f-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="9c18f-110">La funzione risultante sarà utilizzata per il resto dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9c18f-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="9c18f-111">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="9c18f-111">Sign in to Azure</span></span>

<span data-ttu-id="9c18f-112">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c18f-112">Open the Azure portal.</span></span> <span data-ttu-id="9c18f-113">Accedere a tale scopo all'indirizzo [https://portal.azure.com](https://portal.azure.com) con il proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="9c18f-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="9c18f-114">Personalizzare la funzione HTTP</span><span class="sxs-lookup"><span data-stu-id="9c18f-114">Customize your HTTP function</span></span>

<span data-ttu-id="9c18f-115">Per impostazione predefinita, la funzione attivata da HTTP è configurata per accettare qualsiasi metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c18f-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="9c18f-116">È inoltre disponibile un URL predefinito nel formato `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="9c18f-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="9c18f-117">Se è stata seguita la guida introduttiva, `<funcname>` probabilmente ha un aspetto simile a "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="9c18f-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="9c18f-118">In questa sezione si modificherà la funzione in modo che risponda solo alle richieste GET indirizzate verso la route `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="9c18f-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="9c18f-119">Accedere alla funzione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c18f-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="9c18f-120">Selezionare **Integra** nel pannello di navigazione a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9c18f-120">Select **Integrate** in the left navigation.</span></span>

![Personalizzazione di una funzione HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="9c18f-122">Usare le impostazioni di trigger HTTP come specificato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="9c18f-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="9c18f-123">Campo</span><span class="sxs-lookup"><span data-stu-id="9c18f-123">Field</span></span> | <span data-ttu-id="9c18f-124">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="9c18f-124">Sample value</span></span> | <span data-ttu-id="9c18f-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c18f-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="9c18f-126">Metodi HTTP consentiti</span><span class="sxs-lookup"><span data-stu-id="9c18f-126">Allowed HTTP methods</span></span> | <span data-ttu-id="9c18f-127">Metodi selezionati</span><span class="sxs-lookup"><span data-stu-id="9c18f-127">Selected methods</span></span> | <span data-ttu-id="9c18f-128">Determina quali metodi HTTP possono essere usati per chiamare questa funzione</span><span class="sxs-lookup"><span data-stu-id="9c18f-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="9c18f-129">Metodi HTTP selezionati</span><span class="sxs-lookup"><span data-stu-id="9c18f-129">Selected HTTP methods</span></span> | <span data-ttu-id="9c18f-130">GET</span><span class="sxs-lookup"><span data-stu-id="9c18f-130">GET</span></span> | <span data-ttu-id="9c18f-131">Consente di usare solo i metodi HTTP selezionati per chiamare questa funzione</span><span class="sxs-lookup"><span data-stu-id="9c18f-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="9c18f-132">Modello di route</span><span class="sxs-lookup"><span data-stu-id="9c18f-132">Route template</span></span> | <span data-ttu-id="9c18f-133">/hello</span><span class="sxs-lookup"><span data-stu-id="9c18f-133">/hello</span></span> | <span data-ttu-id="9c18f-134">Determina quale route viene usata per chiamare questa funzione</span><span class="sxs-lookup"><span data-stu-id="9c18f-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="9c18f-135">Si noti che non è stato incluso il prefisso del percorso base `/api` nel modello di route e l'operazione viene gestita da un'impostazione globale.</span><span class="sxs-lookup"><span data-stu-id="9c18f-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="9c18f-136">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-136">Click **Save**.</span></span>

<span data-ttu-id="9c18f-137">Altre informazioni sulla personalizzazione delle funzioni HTTP sono riportate in [Binding Azure HTTP e webhook di Funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="9c18f-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="9c18f-138">Testare l'API</span><span class="sxs-lookup"><span data-stu-id="9c18f-138">Test your API</span></span>

<span data-ttu-id="9c18f-139">Testare quindi la funzione per verificarne il funzionamento con la nuova superficie dell'API.</span><span class="sxs-lookup"><span data-stu-id="9c18f-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="9c18f-140">Passare alla pagina di sviluppo facendo clic sul nome della funzione nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9c18f-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="9c18f-141">Fare clic su **Recupera URL della funzione** e copiare l'URL.</span><span class="sxs-lookup"><span data-stu-id="9c18f-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="9c18f-142">Si dovrebbe vedere che a questo punto usa la route `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="9c18f-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="9c18f-143">Copiare l'URL in una nuova scheda del browser o nel client REST preferito.</span><span class="sxs-lookup"><span data-stu-id="9c18f-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="9c18f-144">I browser useranno GET per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9c18f-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="9c18f-145">Eseguire la funzione e verificare che operi correttamente.</span><span class="sxs-lookup"><span data-stu-id="9c18f-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="9c18f-146">Potrebbe essere necessario fornire il parametro "name" come stringa di query per soddisfare il codice di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="9c18f-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="9c18f-147">È anche possibile chiamare l'endpoint con un altro metodo HTTP per confermare che non viene eseguita la funzione.</span><span class="sxs-lookup"><span data-stu-id="9c18f-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="9c18f-148">A tale scopo è necessario usare un client REST, ad esempio cURL, Postman o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="9c18f-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="9c18f-149">Panoramica dei proxy</span><span class="sxs-lookup"><span data-stu-id="9c18f-149">Proxies overview</span></span>

<span data-ttu-id="9c18f-150">Nella sezione successiva si esporrà l'API tramite un proxy.</span><span class="sxs-lookup"><span data-stu-id="9c18f-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="9c18f-151">I proxy di Funzioni di Azure sono una funzionalità di anteprima che consente di inoltrare le richieste ad altre risorse.</span><span class="sxs-lookup"><span data-stu-id="9c18f-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="9c18f-152">Si definisce un endpoint HTTP come con il trigger HTTP, ma anziché scrivere codice da eseguire quando viene chiamato tale endpoint si fornisce un URL a un'implementazione remota.</span><span class="sxs-lookup"><span data-stu-id="9c18f-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="9c18f-153">Ciò consente di comporre più origini di API in una singola superficie API facile da consumare per i client.</span><span class="sxs-lookup"><span data-stu-id="9c18f-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="9c18f-154">Questo è particolarmente utile se si desidera compilare le API come microservizi.</span><span class="sxs-lookup"><span data-stu-id="9c18f-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="9c18f-155">Un proxy può puntare a qualsiasi risorsa HTTP, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9c18f-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="9c18f-156">Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9c18f-156">Azure Functions</span></span> 
- <span data-ttu-id="9c18f-157">App per le API in [Servizio app di Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="9c18f-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="9c18f-158">Contenitori docker in [Servizio App in Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="9c18f-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="9c18f-159">Qualsiasi altra API in hosting</span><span class="sxs-lookup"><span data-stu-id="9c18f-159">Any other hosted API</span></span>

<span data-ttu-id="9c18f-160">Per altre informazioni sui proxy, vedere [Uso di proxy in Funzioni di Azure (anteprima)].</span><span class="sxs-lookup"><span data-stu-id="9c18f-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="9c18f-161">Creare il primo proxy</span><span class="sxs-lookup"><span data-stu-id="9c18f-161">Create your first proxy</span></span>

<span data-ttu-id="9c18f-162">In questa sezione si creerà un nuovo proxy che funge da front-end per l'API complessiva.</span><span class="sxs-lookup"><span data-stu-id="9c18f-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="9c18f-163">Configurazione dell'ambiente front-end</span><span class="sxs-lookup"><span data-stu-id="9c18f-163">Setting up the frontend environment</span></span>

<span data-ttu-id="9c18f-164">Ripetere i passaggi per [creare un'app per le funzioni](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app), creando una nuova app per le funzioni in cui verrà creato il proxy.</span><span class="sxs-lookup"><span data-stu-id="9c18f-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="9c18f-165">La nuova app servirà come front-end per l'API e l'app per le funzioni modificata in precedenza servirà come back-end.</span><span class="sxs-lookup"><span data-stu-id="9c18f-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="9c18f-166">Passare alla nuova app per le funzioni front-end nel portale.</span><span class="sxs-lookup"><span data-stu-id="9c18f-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="9c18f-167">Selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-167">Select **Settings**.</span></span> <span data-ttu-id="9c18f-168">Quindi attivare **Abilita Proxy di Funzioni di Azure (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="9c18f-169">Selezionare **Impostazioni piattaforma** e scegliere **Impostazioni applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="9c18f-170">Scorrere verso il basso fino a **Impostazioni app** e creare una nuova impostazione con chiave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="9c18f-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="9c18f-171">Impostare il suo valore all'host dell'app per le funzioni di back-end, ad esempio `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9c18f-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="9c18f-172">Fa parte dell'URL copiato in precedenza durante il test della funzione HTTP.</span><span class="sxs-lookup"><span data-stu-id="9c18f-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="9c18f-173">Si farà riferimento a questa impostazione nella configurazione in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9c18f-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="9c18f-174">Le impostazioni di app sono consigliate perché la configurazione dell'host eviti una dipendenza di ambiente hard-coded per il proxy.</span><span class="sxs-lookup"><span data-stu-id="9c18f-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="9c18f-175">Usare le impostazioni dell'app significa che è possibile spostare la configurazione del proxy tra ambienti e saranno applicate le impostazioni dell'app specifiche dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9c18f-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="9c18f-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="9c18f-177">Creazione di un proxy nel front-end</span><span class="sxs-lookup"><span data-stu-id="9c18f-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="9c18f-178">Passare all'app per le funzioni front-end nel portale.</span><span class="sxs-lookup"><span data-stu-id="9c18f-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="9c18f-179">Nel riquadro di spostamento sinistro fare clic sul segno "+" accanto a "Proxy (anteprima)".</span><span class="sxs-lookup"><span data-stu-id="9c18f-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![Creazione di un proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="9c18f-181">Usare le impostazioni specificate nella tabella.</span><span class="sxs-lookup"><span data-stu-id="9c18f-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="9c18f-182">Campo</span><span class="sxs-lookup"><span data-stu-id="9c18f-182">Field</span></span> | <span data-ttu-id="9c18f-183">Valore di esempio</span><span class="sxs-lookup"><span data-stu-id="9c18f-183">Sample value</span></span> | <span data-ttu-id="9c18f-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c18f-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="9c18f-185">Nome</span><span class="sxs-lookup"><span data-stu-id="9c18f-185">Name</span></span> | <span data-ttu-id="9c18f-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="9c18f-186">HelloProxy</span></span> | <span data-ttu-id="9c18f-187">Nome descrittivo utilizzato solo per la gestione</span><span class="sxs-lookup"><span data-stu-id="9c18f-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="9c18f-188">Modello di route</span><span class="sxs-lookup"><span data-stu-id="9c18f-188">Route template</span></span> | <span data-ttu-id="9c18f-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="9c18f-189">/api/hello</span></span> | <span data-ttu-id="9c18f-190">Determina quale route viene usata per chiamare questo proxy</span><span class="sxs-lookup"><span data-stu-id="9c18f-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="9c18f-191">URL back-end</span><span class="sxs-lookup"><span data-stu-id="9c18f-191">Backend URL</span></span> | <span data-ttu-id="9c18f-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="9c18f-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="9c18f-193">Specifica l'endpoint a cui la richiesta deve essere trasmessa tramite proxy</span><span class="sxs-lookup"><span data-stu-id="9c18f-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="9c18f-194">Si noti che Proxy non fornisce il prefisso del percorso di base `/api` e questo deve essere incluso nel modello di route.</span><span class="sxs-lookup"><span data-stu-id="9c18f-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="9c18f-195">La sintassi `%HELLO_HOST%` fa riferimento all'impostazione di app creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c18f-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="9c18f-196">L'URL risolto punterà alla funzione originale.</span><span class="sxs-lookup"><span data-stu-id="9c18f-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="9c18f-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-197">Click **Create**.</span></span>

<span data-ttu-id="9c18f-198">È possibile provare il nuovo proxy copiando l'URL del proxy e testandolo nel browser o con il proprio client HTTP preferito.</span><span class="sxs-lookup"><span data-stu-id="9c18f-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="9c18f-199">Creare un'API fittizia</span><span class="sxs-lookup"><span data-stu-id="9c18f-199">Create a mock API</span></span>

<span data-ttu-id="9c18f-200">Quindi si userà un proxy per creare un'API fittizia per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9c18f-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="9c18f-201">Questo consente allo sviluppo client di procedere, senza bisogno della completa implementazione del back-end.</span><span class="sxs-lookup"><span data-stu-id="9c18f-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="9c18f-202">In un secondo momento della fase di sviluppo è possibile creare una nuova app per le funzioni che supporta questa logica e reindirizzare il proxy a essa.</span><span class="sxs-lookup"><span data-stu-id="9c18f-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="9c18f-203">Per creare questa API fittizia, si creerà un nuovo proxy, questa volta usando l'[Editor del servizio app](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="9c18f-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="9c18f-204">Per iniziare passare all'app per le funzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="9c18f-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="9c18f-205">Selezionare **Funzionalità della piattaforma** e trovare **Editor del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="9c18f-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="9c18f-206">Facendo clic su questa opzione si apre l'Editor del servizio app in una nuova scheda.</span><span class="sxs-lookup"><span data-stu-id="9c18f-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="9c18f-207">Selezionare `proxies.json` nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9c18f-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="9c18f-208">Si tratta del file che memorizza la configurazione per tutti i proxy.</span><span class="sxs-lookup"><span data-stu-id="9c18f-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="9c18f-209">Se si usa uno dei [metodi di distribuzione delle funzioni](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), questo è il file che si manterrà nel controllo sorgente.</span><span class="sxs-lookup"><span data-stu-id="9c18f-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="9c18f-210">Per altre informazioni su questo file, vedere [Configurazione avanzata](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="9c18f-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="9c18f-211">Se la procedura è stata completata fino a questo punto, il file proxies.json dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9c18f-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="9c18f-212">Ora si aggiungerà l'API fittizia.</span><span class="sxs-lookup"><span data-stu-id="9c18f-212">Next you'll add your mock API.</span></span> <span data-ttu-id="9c18f-213">Sostituire il file proxies.json con il seguente:</span><span class="sxs-lookup"><span data-stu-id="9c18f-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="9c18f-214">In questo modo viene aggiunto un nuovo proxy, "GetUserByName", senza la proprietà backendUri.</span><span class="sxs-lookup"><span data-stu-id="9c18f-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="9c18f-215">Invece di chiamare un'altra risorsa, viene modificata la risposta predefinita di Proxy usando un override della risposta.</span><span class="sxs-lookup"><span data-stu-id="9c18f-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="9c18f-216">È possibile anche usare gli override di richiesta e risposta in combinazione con un URL di back-end.</span><span class="sxs-lookup"><span data-stu-id="9c18f-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="9c18f-217">Ciò è particolarmente utile quando si esegue l'inoltro tramite proxy dei dati di un sistema legacy, in cui potrebbe essere necessario modificare le intestazioni, eseguire una query dei parametri e così via. Per altre informazioni sugli override di richiesta e risposta, vedere [Modifica delle richieste e delle risposte](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="9c18f-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="9c18f-218">Testare l'API fittizia chiamando l'endpoint `/api/users/{username}` mediante un browser o il client REST preferito.</span><span class="sxs-lookup"><span data-stu-id="9c18f-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="9c18f-219">Assicurarsi di sostituire _{username}_ con un valore stringa che rappresenta un nome utente.</span><span class="sxs-lookup"><span data-stu-id="9c18f-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c18f-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c18f-220">Next steps</span></span>

<span data-ttu-id="9c18f-221">In questa esercitazione è stato illustrato come creare e personalizzare un'API in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c18f-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="9c18f-222">È stato inoltre illustrato come mettere insieme più API, incluse quelle fittizie, in una sola superficie API unificata.</span><span class="sxs-lookup"><span data-stu-id="9c18f-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="9c18f-223">È possibile usare queste tecniche per creare API di qualsiasi complessità, il tutto durante l'esecuzione del modello di calcolo senza server fornito da Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c18f-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="9c18f-224">I riferimenti seguenti possono essere utili quando si sviluppa ulteriormente l'API:</span><span class="sxs-lookup"><span data-stu-id="9c18f-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="9c18f-225">Binding HTTP e webhook di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9c18f-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="9c18f-226">[Uso di proxy in Funzioni di Azure (anteprima)]</span><span class="sxs-lookup"><span data-stu-id="9c18f-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="9c18f-227">Documentazione di un'API di Funzioni di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9c18f-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Uso di proxy in Funzioni di Azure (anteprima)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
