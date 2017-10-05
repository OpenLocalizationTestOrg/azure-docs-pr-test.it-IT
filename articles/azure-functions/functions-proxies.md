---
title: Usare i proxy in Funzioni di Azure | Documentazione Microsoft
description: Informazioni generali sull'uso dei proxy in Funzioni di Azure
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
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="d36b0-103">Usare i proxy di Funzioni di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="d36b0-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="d36b0-104">I prozy di Funzioni di Azure sono attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="d36b0-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="d36b0-105">Sono gratuite in anteprima, ma si applicano le tariffe standard per le funzioni quando vengono eseguiti i proxy.</span><span class="sxs-lookup"><span data-stu-id="d36b0-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="d36b0-106">Per altre informazioni, vedere [Prezzi di Funzioni](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="d36b0-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="d36b0-107">Questo articolo illustra come configurare e usare i proxy in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d36b0-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="d36b0-108">Questa funzionalità consente di specificare gli endpoint nell'app per le funzioni implementati da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="d36b0-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="d36b0-109">È possibile usare questi proxy per suddividere un'API di grandi dimensioni in più app per le funzioni (come in un'architettura di microservizio), pur continuando a presentare una singola superficie API per i client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="d36b0-110"><a name="enable"></a>Abilitare i proxy di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d36b0-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="d36b0-111">I proxy non sono abilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d36b0-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="d36b0-112">È possibile creare i proxy quando la funzionalità è disabilitata, ma non è possibile eseguirli.</span><span class="sxs-lookup"><span data-stu-id="d36b0-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="d36b0-113">Per abilitare i proxy, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d36b0-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="d36b0-114">Aprire il [Portale di Azure] e passare all'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="d36b0-115">Selezionare **Impostazioni dell'app per le funzioni**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="d36b0-116">Impostare **Abilita Proxy di Funzioni di Azure (anteprima)** su **On**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="d36b0-117">È inoltre possibile ritornare qui per aggiornare il runtime del proxy man mano che le nuove funzioni diventano disponibili.</span><span class="sxs-lookup"><span data-stu-id="d36b0-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="d36b0-118"><a name="create"></a>Creare un proxy</span><span class="sxs-lookup"><span data-stu-id="d36b0-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="d36b0-119">In questa sezione viene descritto come creare un proxy nel portale Funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="d36b0-120">Aprire il [Portale di Azure] e passare all'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="d36b0-121">Nel riquadro sinistro selezionare **Nuovo proxy**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="d36b0-122">Dare un nome al proxy.</span><span class="sxs-lookup"><span data-stu-id="d36b0-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="d36b0-123">Configurare l'endpoint esposto in questa app per le funzioni, specificando il **Modello di route** e i **Metodi HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="d36b0-124">Questi parametri si comportano in base alle regole dei [trigger HTTP].</span><span class="sxs-lookup"><span data-stu-id="d36b0-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="d36b0-125">Impostare l'**URL di back-end** su un altro endpoint.</span><span class="sxs-lookup"><span data-stu-id="d36b0-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="d36b0-126">Questo endpoint potrebbe essere una funzione in un'altra app per le funzioni oppure di qualsiasi altra API.</span><span class="sxs-lookup"><span data-stu-id="d36b0-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="d36b0-127">Il valore non deve essere statico e può fare riferimento alle [impostazioni dell'applicazione] e ai [parametri della richiesta del client originale].</span><span class="sxs-lookup"><span data-stu-id="d36b0-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="d36b0-128">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-128">Click **Create**.</span></span>

<span data-ttu-id="d36b0-129">Il proxy è ora presente come un nuovo endpoint sull'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="d36b0-130">Dalla prospettiva del client, è equivalente a un HttpTrigger nelle Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d36b0-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="d36b0-131">È possibile provare il nuovo proxy copiando l'URL del proxy ed eseguendo un test con il proprio client HTTP preferito.</span><span class="sxs-lookup"><span data-stu-id="d36b0-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="d36b0-132"><a name="modify-requests-responses"></a>Modificare richieste e risposte</span><span class="sxs-lookup"><span data-stu-id="d36b0-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="d36b0-133">I proxy di Funzioni di Azure consentono di modificare le richieste al back-end e le risposte dal back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="d36b0-134">Queste trasformazioni possono usare le variabili come definito in [Usare le variabili].</span><span class="sxs-lookup"><span data-stu-id="d36b0-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="d36b0-135"><a name="modify-backend-request"></a>Modificare la richiesta al back-end</span><span class="sxs-lookup"><span data-stu-id="d36b0-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="d36b0-136">Per impostazione predefinita, la richiesta al back-end viene inizializzata come una copia della richiesta originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="d36b0-137">Oltre a impostare l'URL di back-end, è possibile apportare modifiche ai parametri del metodo HTTP, delle intestazioni e della stringa di query.</span><span class="sxs-lookup"><span data-stu-id="d36b0-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="d36b0-138">I valori modificati possono fare riferimento alle [impostazioni dell'applicazione] e ai [parametri della richiesta del client originale].</span><span class="sxs-lookup"><span data-stu-id="d36b0-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="d36b0-139">Attualmente non esiste un'esperienza del portale per la modifica delle richieste al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="d36b0-140">Per informazioni su come applicare questa funzionalità da proxies.json, vedere [Definire un oggetto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="d36b0-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="d36b0-141"><a name="modify-response"></a>Modificare la risposta</span><span class="sxs-lookup"><span data-stu-id="d36b0-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="d36b0-142">Per impostazione predefinita, la risposta del client viene inizializzata come una copia della risposta back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="d36b0-143">È possibile apportare modifiche al codice di stato, al motivo, alle intestazioni e al corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="d36b0-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="d36b0-144">I valori modificati possono fare riferimento alle [impostazioni dell'applicazione], ai [parametri della richiesta del client originale] e ai [paramenti della risposta back-end].</span><span class="sxs-lookup"><span data-stu-id="d36b0-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="d36b0-145">Attualmente non esiste un'esperienza del portale per la modifica delle risposte del back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="d36b0-146">Per informazioni su come applicare questa funzionalità da proxies.json, vedere [Definire un oggetto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="d36b0-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="d36b0-147"><a name="using-variables"></a>Usare le variabili</span><span class="sxs-lookup"><span data-stu-id="d36b0-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="d36b0-148">La configurazione di un proxy non deve essere statica.</span><span class="sxs-lookup"><span data-stu-id="d36b0-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="d36b0-149">È possibile condizionarla per fare in modo che usi le variabili della richiesta originale, la risposta back-end o le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d36b0-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="d36b0-150"><a name="request-parameters"></a>Parametri di riferimento della richiesta</span><span class="sxs-lookup"><span data-stu-id="d36b0-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="d36b0-151">I parametri della richiesta possono essere usati come input per la proprietà URL di back-end o come parte della modifica di richieste e risposte.</span><span class="sxs-lookup"><span data-stu-id="d36b0-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="d36b0-152">Alcuni parametri possono essere associati dal modello di route specificato nella configurazione del proxy di base, mentre altri derivano dalle proprietà della richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d36b0-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="d36b0-153">Parametri del modello di route</span><span class="sxs-lookup"><span data-stu-id="d36b0-153">Route template parameters</span></span>
<span data-ttu-id="d36b0-154">È possibile fare riferimento ai parametri usati nel modello di route in base al nome.</span><span class="sxs-lookup"><span data-stu-id="d36b0-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="d36b0-155">I nomi dei parametri sono racchiusi tra parentesi graffe ({}).</span><span class="sxs-lookup"><span data-stu-id="d36b0-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="d36b0-156">Ad esempio, se un proxy ha un modello di route come `/pets/{petId}`, l'URL di back-end può includere il valore `{petId}`, come in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="d36b0-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="d36b0-157">Se il modello di route termina con un carattere jolly, ad esempio `/api/{*restOfPath}`, il valore `{restOfPath}` è una rappresentazione di stringa dei segmenti del percorso rimanente della richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d36b0-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="d36b0-158">Parametri aggiuntivi della richiesta</span><span class="sxs-lookup"><span data-stu-id="d36b0-158">Additional request parameters</span></span>
<span data-ttu-id="d36b0-159">Oltre ai parametri del modello di route, i valori seguenti possono essere usati nei valori di configurazione:</span><span class="sxs-lookup"><span data-stu-id="d36b0-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="d36b0-160">**{request.method}**: il metodo HTTP usato nella richiesta originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="d36b0-161">**{request.headers.\<HeaderName\>}**: un'intestazione che può essere letta dalla richiesta originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="d36b0-162">Sostituire *\<HeaderName\>* con il nome dell'intestazione che si desidera leggere.</span><span class="sxs-lookup"><span data-stu-id="d36b0-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="d36b0-163">Se l'intestazione non è inclusa nella richiesta, il valore sarà una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="d36b0-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="d36b0-164">**{request.querystring.\<ParameterName\>}**: un parametro di stringa di query che può essere letto dalla richiesta originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="d36b0-165">Sostituire *\<ParameterName\>* con il nome del parametro che si desidera leggere.</span><span class="sxs-lookup"><span data-stu-id="d36b0-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="d36b0-166">Se il parametro non è incluso nella richiesta, il valore sarà una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="d36b0-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="d36b0-167"><a name="response-parameters"></a>Parametri di riferimento della risposta dal back-end</span><span class="sxs-lookup"><span data-stu-id="d36b0-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="d36b0-168">I parametri di risposta possono essere usati come parte della modifica della risposta al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="d36b0-169">I valori seguenti possono essere usati nei valori di configurazione:</span><span class="sxs-lookup"><span data-stu-id="d36b0-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="d36b0-170">**{backend.response.statusCode}**: il codice di stato HTTP restituito nella risposta dal back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="d36b0-171">**{backend.response.statusReason}**: la frase per il motivo HTTP restituita nella risposta dal back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="d36b0-172">**{backend.response.headers.\<HeaderName\>}**: un'intestazione che può essere letta dalla risposta dal back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="d36b0-173">Sostituire *\<HeaderName\>* con il nome dell'intestazione che si desidera leggere.</span><span class="sxs-lookup"><span data-stu-id="d36b0-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="d36b0-174">Se l'intestazione non è inclusa nella richiesta, il valore sarà una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="d36b0-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="d36b0-175"><a name="use-appsettings"></a>Impostazioni di riferimento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d36b0-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="d36b0-176">È anche possibile fare riferimento alle [impostazioni dell'applicazione definite per l'app per le funzioni](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) racchiudendo il nome dell'impostazione tra i segni di percentuale (%).</span><span class="sxs-lookup"><span data-stu-id="d36b0-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="d36b0-177">Ad esempio, per l'URL di back-end di *https://%ORDER_PROCESSING_HOST%/api/orders*, "%ORDER_PROCESSING_HOST%" verrà sostituito con il valore dell'impostazione ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="d36b0-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="d36b0-178">Usare le impostazioni dell'applicazione per gli host di back-end quando si dispone di più distribuzioni o ambienti di test.</span><span class="sxs-lookup"><span data-stu-id="d36b0-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="d36b0-179">In questo modo, è possibile assicurarsi di comunicare sempre con il back-end corretto per quell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d36b0-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="d36b0-180">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="d36b0-180">Advanced configuration</span></span>

<span data-ttu-id="d36b0-181">I proxy configurati vengono archiviati in un file proxies.json, situato nella radice di una directory dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="d36b0-182">È possibile modificare manualmente questo file e distribuirlo come parte dell'app quando si usa uno dei [metodi di distribuzione](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) supportati da Funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="d36b0-183">La funzione deve essere [abilitata](#enable) per poter elaborare il file.</span><span class="sxs-lookup"><span data-stu-id="d36b0-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="d36b0-184">Se non è stato configurato uno dei metodi di distribuzione, è anche possibile usare il file proxies.json nel portale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="d36b0-185">Passare all'app per le funzioni e selezionare **Funzionalità della piattaforma** ed **Editor del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="d36b0-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="d36b0-186">Questo consentirà di visualizzare la struttura dell'intero file dell'app per le funzioni e di apportare modifiche.</span><span class="sxs-lookup"><span data-stu-id="d36b0-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="d36b0-187">Il file proxies.JSON è definito da un oggetto proxy, composto da proxy denominati e dalle relative definizioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="d36b0-188">È facoltativamente possibile fare riferimento a uno [schema JSON](http://json.schemastore.org/proxies) per il completamento del codice se l'editor lo supporta.</span><span class="sxs-lookup"><span data-stu-id="d36b0-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="d36b0-189">Un esempio di file apparirà come segue:</span><span class="sxs-lookup"><span data-stu-id="d36b0-189">An example file might look like the following:</span></span>

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

<span data-ttu-id="d36b0-190">Ogni proxy ha un nome descrittivo, come *proxy1* nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="d36b0-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="d36b0-191">L'oggetto di definizione del proxy corrispondente viene definito dalle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d36b0-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="d36b0-192">**matchCondition**: obbligatorio, un oggetto che definisce le richieste che attivano l'esecuzione di questo proxy.</span><span class="sxs-lookup"><span data-stu-id="d36b0-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="d36b0-193">Contiene due proprietà condivise con i [trigger HTTP]:</span><span class="sxs-lookup"><span data-stu-id="d36b0-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="d36b0-194">_methods_: una matrice di metodi HTTP a cui il proxy risponde.</span><span class="sxs-lookup"><span data-stu-id="d36b0-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="d36b0-195">Se non viene specificata, il proxy risponderà a tutti i metodi HTTP nel route.</span><span class="sxs-lookup"><span data-stu-id="d36b0-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="d36b0-196">_route_: obbligatorio, definisce il modello di route, controllando a quali URL delle richieste il proxy risponde.</span><span class="sxs-lookup"><span data-stu-id="d36b0-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="d36b0-197">A differenza dei trigger HTTP, non vi è alcun valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="d36b0-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="d36b0-198">**backendUri**: l'URL della risorsa di back-end a cui la richiesta deve essere trasmessa tramite proxy.</span><span class="sxs-lookup"><span data-stu-id="d36b0-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="d36b0-199">Questo valore può fare riferimento alle impostazioni dell'applicazione e ai parametri della richiesta del client originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="d36b0-200">Se questa proprietà non è inclusa, Funzioni di Azure risponde con un HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d36b0-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="d36b0-201">**requestOverrides**: un oggetto che definisce le trasformazioni alla richiesta al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="d36b0-202">Vedere [Definire un oggetto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="d36b0-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="d36b0-203">**responseOverrides**: un oggetto che definisce le trasformazioni alla risposta del client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="d36b0-204">Vedere [Definire un oggetto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="d36b0-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="d36b0-205">I proxy di Funzioni di Azure della proprietà di route non rispettano la proprietà routePrefix della configurazione di host di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="d36b0-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="d36b0-206">Se si desidera includere un prefisso, ad esempio /api, deve essere incluso nella proprietà di route.</span><span class="sxs-lookup"><span data-stu-id="d36b0-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="d36b0-207"><a name="requestOverrides"></a>Definire un oggetto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="d36b0-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="d36b0-208">L'oggetto requestOverrides definisce le modifiche apportate alla richiesta quando viene chiamata la risorsa back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="d36b0-209">L'oggetto viene definito dalle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d36b0-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="d36b0-210">**backend.request.method**: il metodo HTTP usato per chiamare il back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="d36b0-211">**backend.request.querystring.\<ParameterName\>**: un parametro di stringa di query che può essere impostato per la chiamata al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="d36b0-212">Sostituire *\<ParameterName\>* con il nome del parametro che si desidera impostare.</span><span class="sxs-lookup"><span data-stu-id="d36b0-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="d36b0-213">Se viene generata una stringa vuota, il parametro non viene incluso nella richiesta al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="d36b0-214">**backend.request.headers.\<HeaderName\>**: un'intestazione che può essere impostata per la chiamata al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="d36b0-215">Sostituire *\<HeaderName\>* con il nome dell'intestazione che si desidera impostare.</span><span class="sxs-lookup"><span data-stu-id="d36b0-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="d36b0-216">Se viene fornita una stringa vuota, il parametro non viene incluso nella richiesta al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="d36b0-217">I valori possono fare riferimento alle impostazioni dell'applicazione e ai parametri della richiesta del client originale.</span><span class="sxs-lookup"><span data-stu-id="d36b0-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="d36b0-218">Un esempio di configurazione apparirà come segue:</span><span class="sxs-lookup"><span data-stu-id="d36b0-218">An example configuration might look like the following:</span></span>

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

### <span data-ttu-id="d36b0-219"><a name="responseOverrides"></a>Definire un oggetto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="d36b0-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="d36b0-220">L'oggetto responseOverrides definisce le modifiche apportate alla risposta passata al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="d36b0-221">L'oggetto viene definito dalle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d36b0-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="d36b0-222">**response.statusCode**: il codice di stato HTTP da restituire al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="d36b0-223">**response.statusReason**: la frase del motivo HTTP da restituire al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="d36b0-224">**response.body**: la rappresentazione di stringa del corpo da restituire al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="d36b0-225">**response.headers.\<HeaderName\>**: un'intestazione che può essere impostata per la risposta al client.</span><span class="sxs-lookup"><span data-stu-id="d36b0-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="d36b0-226">Sostituire *\<HeaderName\>* con il nome dell'intestazione che si desidera impostare.</span><span class="sxs-lookup"><span data-stu-id="d36b0-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="d36b0-227">Se viene fornita una stringa vuota, l'intestazione non viene inclusa nella richiesta al back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="d36b0-228">I valori possono fare riferimento alle impostazioni dell'applicazione, ai parametri della richiesta del client originale e ai paramenti della risposta back-end.</span><span class="sxs-lookup"><span data-stu-id="d36b0-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="d36b0-229">Un esempio di configurazione apparirà come segue:</span><span class="sxs-lookup"><span data-stu-id="d36b0-229">An example configuration might look like the following:</span></span>

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
> <span data-ttu-id="d36b0-230">In questo esempio, il corpo viene impostato direttamente, pertanto non p necessaria lacuna proprietà `backendUri`.</span><span class="sxs-lookup"><span data-stu-id="d36b0-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="d36b0-231">L'esempio illustra come usare i proxy di Funzioni di Azure per le API di simulazione.</span><span class="sxs-lookup"><span data-stu-id="d36b0-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="d36b0-232">[Portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d36b0-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="d36b0-233">[trigger HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="d36b0-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="d36b0-234">[Definire un oggetto requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="d36b0-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="d36b0-235">[Definire un oggetto responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="d36b0-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="d36b0-236">[impostazioni dell'applicazione]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="d36b0-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="d36b0-237">[Usare le variabili]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="d36b0-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="d36b0-238">[parametri della richiesta del client originale]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="d36b0-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="d36b0-239">[paramenti della risposta back-end]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="d36b0-239">[parameters from the back-end response]: #response-parameters</span></span>
