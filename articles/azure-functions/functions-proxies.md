---
title: aaaWork di proxy nelle funzioni di Azure | Documenti Microsoft
description: Panoramica di come toouse proxy funzioni di Azure
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="cac5d-103">Usare i proxy di Funzioni di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="cac5d-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="cac5d-104">I prozy di Funzioni di Azure sono attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="cac5d-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="cac5d-105">È disponibile mentre è in anteprima, ma le funzioni standard fatturazione valido tooproxy esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="cac5d-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="cac5d-106">Per altre informazioni, vedere [Prezzi di Funzioni](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="cac5d-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="cac5d-107">Questo articolo viene illustrato come tooconfigure e come utilizzare il proxy di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="cac5d-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="cac5d-108">Questa funzionalità consente di specificare gli endpoint nell'app per le funzioni implementati da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="cac5d-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="cac5d-109">È possibile usare questi proxy toobreak un'API di grandi dimensioni, in più applicazioni di funzione (ad esempio un'architettura microservizio), pur continuando a presentare una singola superficie dell'API per i client.</span><span class="sxs-lookup"><span data-stu-id="cac5d-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="cac5d-110"><a name="enable"></a>Abilitare i proxy di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="cac5d-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="cac5d-111">I proxy non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cac5d-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="cac5d-112">È possibile creare proxy mentre hello funzionalità è disabilitata, ma non verranno eseguite.</span><span class="sxs-lookup"><span data-stu-id="cac5d-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="cac5d-113">proxy tooenable, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cac5d-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="cac5d-114">Aprire hello [portale di Azure], quindi andare tooyour funzione app.</span><span class="sxs-lookup"><span data-stu-id="cac5d-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="cac5d-115">Selezionare **Impostazioni dell'app per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="cac5d-116">Opzione **abilitare i proxy di funzioni di Azure (anteprima)** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="cac5d-117">È inoltre possibile restituire qui tooupdate hello proxy runtime come diventare disponibili delle nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cac5d-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="cac5d-118"><a name="create"></a>Creare un proxy</span><span class="sxs-lookup"><span data-stu-id="cac5d-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="cac5d-119">In questa sezione viene illustrato come toocreate un proxy in hello portale funzioni.</span><span class="sxs-lookup"><span data-stu-id="cac5d-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="cac5d-120">Aprire hello [portale di Azure], quindi andare tooyour funzione app.</span><span class="sxs-lookup"><span data-stu-id="cac5d-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="cac5d-121">Nel riquadro sinistro hello selezionare **nuovo proxy**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="cac5d-122">Dare un nome al proxy.</span><span class="sxs-lookup"><span data-stu-id="cac5d-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="cac5d-123">Configurare l'endpoint di hello che viene esposto in questa app di funzione specificando hello **modello di route** e **metodi HTTP**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="cac5d-124">Questi parametri si comportano in base regole toohello per [trigger HTTP].</span><span class="sxs-lookup"><span data-stu-id="cac5d-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="cac5d-125">Set hello **URL back-end** tooanother endpoint.</span><span class="sxs-lookup"><span data-stu-id="cac5d-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="cac5d-126">Questo endpoint potrebbe essere una funzione in un'altra app per le funzioni oppure di qualsiasi altra API.</span><span class="sxs-lookup"><span data-stu-id="cac5d-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="cac5d-127">Hello valore non è necessario toobe statica e può fare riferimento [le impostazioni dell'applicazione] e [i parametri dalla richiesta client originale hello].</span><span class="sxs-lookup"><span data-stu-id="cac5d-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="cac5d-128">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-128">Click **Create**.</span></span>

<span data-ttu-id="cac5d-129">Il proxy è ora presente come un nuovo endpoint sull'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="cac5d-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="cac5d-130">Dalla prospettiva del client, è equivalente tooan HttpTrigger nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="cac5d-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="cac5d-131">È possibile provare il nuovo proxy copiando hello URL del Proxy e di eseguire il test con il client HTTP preferito.</span><span class="sxs-lookup"><span data-stu-id="cac5d-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="cac5d-132"><a name="modify-requests-responses"></a>Modificare richieste e risposte</span><span class="sxs-lookup"><span data-stu-id="cac5d-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="cac5d-133">Con il proxy di funzioni di Azure, è possibile modificare le risposte tooand richieste dal back-end hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="cac5d-134">Queste trasformazioni possono usare le variabili come definito in [Usare le variabili].</span><span class="sxs-lookup"><span data-stu-id="cac5d-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="cac5d-135"><a name="modify-backend-request"></a>Modificare una richiesta di back-end hello</span><span class="sxs-lookup"><span data-stu-id="cac5d-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="cac5d-136">Per impostazione predefinita, la richiesta di back-end hello viene inizializzata come una copia della richiesta originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="cac5d-137">Inoltre toosetting hello back-end URL, è possibile apportare metodo HTTP toohello di modifiche, le intestazioni e parametri di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="cac5d-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="cac5d-138">Hello valori modificati possono fare riferimento [le impostazioni dell'applicazione] e [i parametri dalla richiesta client originale hello].</span><span class="sxs-lookup"><span data-stu-id="cac5d-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="cac5d-139">Attualmente non esiste un'esperienza del portale per la modifica delle richieste al back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="cac5d-140">toolearn tooapply vedere questa funzionalità, proxies.json [definire un oggetto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="cac5d-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="cac5d-141"><a name="modify-response"></a>Modificare la risposta hello</span><span class="sxs-lookup"><span data-stu-id="cac5d-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="cac5d-142">Per impostazione predefinita, risposta client hello viene inizializzato come una copia della risposta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="cac5d-143">È possibile rendere il codice di stato della risposta di modifiche toohello, frase del motivo, le intestazioni e corpo.</span><span class="sxs-lookup"><span data-stu-id="cac5d-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="cac5d-144">Hello valori modificati possono fare riferimento [le impostazioni dell'applicazione], [i parametri dalla richiesta client originale hello], e [parametri dalla risposta back-end hello].</span><span class="sxs-lookup"><span data-stu-id="cac5d-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="cac5d-145">Attualmente non esiste un'esperienza del portale per la modifica delle risposte del back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="cac5d-146">toolearn tooapply vedere questa funzionalità, proxies.json [definire un oggetto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="cac5d-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="cac5d-147"><a name="using-variables"></a>Usare le variabili</span><span class="sxs-lookup"><span data-stu-id="cac5d-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="cac5d-148">configurazione di Hello per un proxy non è necessario toobe statico.</span><span class="sxs-lookup"><span data-stu-id="cac5d-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="cac5d-149">È possibile, condizione variabili toouse dalla richiesta originale hello, risposta back-end hello o le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cac5d-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="cac5d-150"><a name="request-parameters"></a>Parametri di riferimento della richiesta</span><span class="sxs-lookup"><span data-stu-id="cac5d-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="cac5d-151">È possibile utilizzare i parametri della richiesta come input proprietà URL di back-end toohello o come parte della modifica delle richieste e risposte.</span><span class="sxs-lookup"><span data-stu-id="cac5d-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="cac5d-152">È possibile associare alcuni parametri di modello di route hello specificato nella configurazione del proxy base hello e ad altri utenti possono provenire dalle proprietà della richiesta in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="cac5d-153">Parametri del modello di route</span><span class="sxs-lookup"><span data-stu-id="cac5d-153">Route template parameters</span></span>
<span data-ttu-id="cac5d-154">I parametri vengono utilizzati nel modello di route hello sono toobe disponibili a cui fa riferimento in base al nome.</span><span class="sxs-lookup"><span data-stu-id="cac5d-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="cac5d-155">i nomi di parametro Hello sono racchiusi tra parentesi graffe ({}).</span><span class="sxs-lookup"><span data-stu-id="cac5d-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="cac5d-156">Ad esempio, se un proxy ha un modello di route, ad esempio `/pets/{petId}`, hello back-end URL può includere il valore di hello di `{petId}`, come in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="cac5d-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="cac5d-157">Se il modello di route hello termina in un carattere jolly, ad esempio `/api/{*restOfPath}`, hello valore `{restOfPath}` è una rappresentazione di stringa di hello rimanenti segmenti di percorso hello richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="cac5d-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="cac5d-158">Parametri aggiuntivi della richiesta</span><span class="sxs-lookup"><span data-stu-id="cac5d-158">Additional request parameters</span></span>
<span data-ttu-id="cac5d-159">Inoltre toohello indirizzare i parametri del modello, hello seguente i valori può essere utilizzato nei valori di configurazione:</span><span class="sxs-lookup"><span data-stu-id="cac5d-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="cac5d-160">**{Request}** : hello metodo HTTP utilizzato nella richiesta originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="cac5d-161">**{Request. Headers. \<HeaderName\>}**: un'intestazione che può essere letto dalla richiesta originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="cac5d-162">Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooread.</span><span class="sxs-lookup"><span data-stu-id="cac5d-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="cac5d-163">Se l'intestazione hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="cac5d-164">**{QueryString. \<ParameterName\>}**: un parametro di stringa di query che può essere letti dalla richiesta originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="cac5d-165">Sostituire  *\<ParameterName\>*  con nome hello del parametro hello che si desidera tooread.</span><span class="sxs-lookup"><span data-stu-id="cac5d-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="cac5d-166">Se il parametro hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="cac5d-167"><a name="response-parameters"></a>Parametri di riferimento della risposta dal back-end</span><span class="sxs-lookup"><span data-stu-id="cac5d-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="cac5d-168">Parametri di risposta è utilizzabile come parte del client di hello risposta toohello di modifica.</span><span class="sxs-lookup"><span data-stu-id="cac5d-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="cac5d-169">i valori di configurazione, è possibile utilizzare Hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="cac5d-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="cac5d-170">**{backend.response.statusCode}** : hello codice di stato HTTP restituito nella risposta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="cac5d-171">**{backend.response.statusReason}** : frase del motivo hello HTTP restituito nella risposta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="cac5d-172">**{backend.response.headers. \<HeaderName\>}**: un'intestazione che può essere letto dalla risposta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="cac5d-173">Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione hello da tooread.</span><span class="sxs-lookup"><span data-stu-id="cac5d-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="cac5d-174">Se l'intestazione hello non è incluso nella richiesta di hello, il valore di hello sarà una stringa vuota hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="cac5d-175"><a name="use-appsettings"></a>Impostazioni di riferimento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cac5d-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="cac5d-176">È anche possibile fare riferimento [le impostazioni dell'applicazione definite per app di funzione hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) racchiudendo il nome dell'impostazione hello con segni di percentuale (%)).</span><span class="sxs-lookup"><span data-stu-id="cac5d-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="cac5d-177">Ad esempio, un URL di back-end di *https://%ORDER_PROCESSING_HOST%/api/orders* avrebbe "ORDER_PROCESSING_HOST %" sostituito con il valore di hello dell'impostazione ORDER_PROCESSING_HOST hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="cac5d-178">Usare le impostazioni dell'applicazione per gli host di back-end quando si dispone di più distribuzioni o ambienti di test.</span><span class="sxs-lookup"><span data-stu-id="cac5d-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="cac5d-179">In questo modo, è possibile assicurarsi che si parla sempre toohello nuovo finale per tale ambiente.</span><span class="sxs-lookup"><span data-stu-id="cac5d-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="cac5d-180">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="cac5d-180">Advanced configuration</span></span>

<span data-ttu-id="cac5d-181">proxy Hello configurate vengono archiviati in un file proxies.json, che si trova nella radice di hello di una directory di app di funzione.</span><span class="sxs-lookup"><span data-stu-id="cac5d-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="cac5d-182">È possibile manualmente modificare questo file e distribuirlo come parte dell'applicazione quando si usa uno di hello [metodi di distribuzione](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) che supporta le funzioni.</span><span class="sxs-lookup"><span data-stu-id="cac5d-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="cac5d-183">funzionalità di Hello deve essere [abilitato](#enable) per hello toobe di file elaborati.</span><span class="sxs-lookup"><span data-stu-id="cac5d-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="cac5d-184">Se non impostati uno dei metodi di distribuzione hello, è anche possibile lavorare con file proxies.json hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="cac5d-185">Passare tooyour funzione app, selezionare **funzionalità della piattaforma**, quindi selezionare **Editor di servizio App**.</span><span class="sxs-lookup"><span data-stu-id="cac5d-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="cac5d-186">In questo modo, è possibile visualizzare hello file intera struttura dell'app in funzione e quindi apportare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="cac5d-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="cac5d-187">Il file proxies.JSON è definito da un oggetto proxy, composto da proxy denominati e dalle relative definizioni.</span><span class="sxs-lookup"><span data-stu-id="cac5d-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="cac5d-188">È facoltativamente possibile fare riferimento a uno [schema JSON](http://json.schemastore.org/proxies) per il completamento del codice se l'editor lo supporta.</span><span class="sxs-lookup"><span data-stu-id="cac5d-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="cac5d-189">Un esempio di file potrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="cac5d-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="cac5d-190">Ogni proxy ha un nome descrittivo, ad esempio *proxy1* in hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="cac5d-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="cac5d-191">oggetto di definizione proxy corrispondente Hello è definito da hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cac5d-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="cac5d-192">**matchCondition**: obbligatorio--un oggetto che definisce le richieste di hello che attivano l'esecuzione di hello del proxy.</span><span class="sxs-lookup"><span data-stu-id="cac5d-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="cac5d-193">Contiene due proprietà condivise con i [trigger HTTP]:</span><span class="sxs-lookup"><span data-stu-id="cac5d-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="cac5d-194">_metodi_: una matrice di metodi HTTP hello hello proxy risponde a.</span><span class="sxs-lookup"><span data-stu-id="cac5d-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="cac5d-195">Se non è specificato, il proxy di hello risponde metodi HTTP tooall nella route hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="cac5d-196">_route_: obbligatorio - definisce il modello di route hello, il controllo cui URL di richiesta del proxy risponde.</span><span class="sxs-lookup"><span data-stu-id="cac5d-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="cac5d-197">A differenza dei trigger HTTP, non vi è alcun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="cac5d-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="cac5d-198">**backendUri**: hello URL della richiesta di hello risorse back-end toowhich hello devono essere elaborate.</span><span class="sxs-lookup"><span data-stu-id="cac5d-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="cac5d-199">Questo valore può fare riferimento le impostazioni dell'applicazione e i parametri di richiesta client originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="cac5d-200">Se questa proprietà non è inclusa, Funzioni di Azure risponde con un HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="cac5d-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="cac5d-201">**requestOverrides**: un oggetto che definisce una richiesta di trasformazioni toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="cac5d-202">Vedere [definire un oggetto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="cac5d-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="cac5d-203">**responseOverrides**: un oggetto che definisce le trasformazioni toohello client risposta.</span><span class="sxs-lookup"><span data-stu-id="cac5d-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="cac5d-204">Vedere [definire un oggetto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="cac5d-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="cac5d-205">proprietà route Hello Azure funzioni proxy non rispetta proprietà routePrefix hello di configurazione dell'host funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="cac5d-206">Se si desidera un prefisso, ad esempio /api tooinclude, deve essere incluso nella proprietà route hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="cac5d-207"><a name="requestOverrides"></a>Definire un oggetto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="cac5d-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="cac5d-208">l'oggetto requestOverrides Hello definisce le modifiche apportate toohello richiesta quando viene chiamata risorse back-end hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="cac5d-209">oggetto Hello è definito da hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cac5d-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="cac5d-210">**backend.Request.Method**: hello metodo HTTP utilizzato toocall hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="cac5d-211">**backend.Request.QueryString. \<ParameterName\>**: un parametro di stringa di query che è possibile impostare per hello chiamata toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="cac5d-212">Sostituire  *\<ParameterName\>*  con nome hello del parametro hello che si desidera tooset.</span><span class="sxs-lookup"><span data-stu-id="cac5d-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="cac5d-213">Se viene fornita una stringa vuota hello, parametro hello non è incluso nella richiesta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="cac5d-214">**backend.Request.Headers. \<HeaderName\>**: un'intestazione che può essere impostata per hello chiamata toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="cac5d-215">Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooset.</span><span class="sxs-lookup"><span data-stu-id="cac5d-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="cac5d-216">Se si specifica una stringa vuota hello, intestazione hello non è incluso nella richiesta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="cac5d-217">I valori possono fare riferimento le impostazioni dell'applicazione e i parametri di richiesta client originale hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="cac5d-218">Una configurazione di esempio potrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="cac5d-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="cac5d-219"><a name="responseOverrides"></a>Definire un oggetto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="cac5d-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="cac5d-220">l'oggetto requestOverrides Hello definisce le modifiche apportate risposta toohello che ha superato i client toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="cac5d-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="cac5d-221">oggetto Hello è definito da hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cac5d-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="cac5d-222">**response.statusCode**: toobe codice di stato HTTP hello restituito toohello client.</span><span class="sxs-lookup"><span data-stu-id="cac5d-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="cac5d-223">**response.statusReason**: hello HTTP motivo frase toobe restituito toohello client.</span><span class="sxs-lookup"><span data-stu-id="cac5d-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="cac5d-224">**Response.Body**: rappresentazione di stringa hello di hello corpo toobe restituito toohello client.</span><span class="sxs-lookup"><span data-stu-id="cac5d-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="cac5d-225">**Response.Headers. \<HeaderName\>**: un'intestazione che può essere impostata per il client di toohello risposta hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="cac5d-226">Sostituire  *\<HeaderName\>*  con nome hello dell'intestazione di hello che si desidera tooset.</span><span class="sxs-lookup"><span data-stu-id="cac5d-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="cac5d-227">Se si specifica una stringa vuota hello, intestazione hello non è incluso nella risposta hello.</span><span class="sxs-lookup"><span data-stu-id="cac5d-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="cac5d-228">I valori è possono fare riferimento le impostazioni dell'applicazione, i parametri dalla richiesta client originale hello e parametri dalla risposta di hello back-end.</span><span class="sxs-lookup"><span data-stu-id="cac5d-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="cac5d-229">Una configurazione di esempio potrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="cac5d-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="cac5d-230">In questo esempio, il corpo di hello viene impostato direttamente, pertanto non `backendUri` proprietà necessaria.</span><span class="sxs-lookup"><span data-stu-id="cac5d-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="cac5d-231">esempio Hello viene illustrato come è possibile utilizzare il proxy di funzioni di Azure per tali API.</span><span class="sxs-lookup"><span data-stu-id="cac5d-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portale di Azure]: https://portal.azure.com
[trigger HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definire un oggetto requestOverrides]: #requestOverrides
[definire un oggetto responseOverrides]: #responseOverrides
[le impostazioni dell'applicazione]: #use-appsettings
[Usare le variabili]: #using-variables
[i parametri dalla richiesta client originale hello]: #request-parameters
[parametri dalla risposta back-end hello]: #response-parameters
