---
title: Come aggiungere operazioni a un'API in Gestione API di Azure | Microsoft Docs
description: Informazioni su come aggiungere operazioni a un'API in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="e901d-103">Come aggiungere operazioni a un'API in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="e901d-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="e901d-104">Prima di poter usare un'API in Gestione API, è necessario aggiungervi le operazioni.</span><span class="sxs-lookup"><span data-stu-id="e901d-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="e901d-105">Questa guida descrive come aggiungere e configurare diversi tipi di operazioni a un'API in Gestione API.</span><span class="sxs-lookup"><span data-stu-id="e901d-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="e901d-106"><a name="add-operation"> </a>Aggiungere un'operazione</span><span class="sxs-lookup"><span data-stu-id="e901d-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="e901d-107">Le operazioni vengono aggiunte e configurate in un'API nel portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="e901d-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="e901d-108">Per accedere al portale di pubblicazione, fare clic su **Portale di pubblicazione** nel portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="e901d-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portale di pubblicazione][api-management-management-console]

> <span data-ttu-id="e901d-110">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e901d-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="e901d-111">Selezionare l'API desiderata nel portale di pubblicazione e quindi selezionare la scheda **Operazioni** .</span><span class="sxs-lookup"><span data-stu-id="e901d-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Operazioni][api-management-operations]

<span data-ttu-id="e901d-113">Fare clic su **Aggiungi operazione** per aggiungere una nuova operazione.</span><span class="sxs-lookup"><span data-stu-id="e901d-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="e901d-114">Verrà visualizzata la finestra **Nuova operazione** in cui la scheda **Firma** è visualizzata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e901d-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Aggiungi operazione][api-management-add-operation]

<span data-ttu-id="e901d-116">Specificare il **verbo HTTP** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e901d-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![Metodo HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="e901d-118">Definire il modello di URL digitando un frammento dell'URL composto da uno o più segmenti di percorso dell'URL e zero o più parametri di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="e901d-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="e901d-119">Il modello di URL, aggiunto all'URL di base dell'API, identifica una singola operazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="e901d-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="e901d-120">Può contenere una o più parti variabili denominate identificate da parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="e901d-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="e901d-121">Queste parti variabili sono denominate parametri di modello e ad esse vengono assegnati in modo dinamico i valori estratti dall'URL della richiesta quando la richiesta viene elaborata dalla piattaforma di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="e901d-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="e901d-122">Il modello di URL può includere caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="e901d-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="e901d-123">Specificando ad esempio `/*`, tutte le richieste per il metodo HTTP verranno inoltrate al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="e901d-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![Modello di URL][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="e901d-125">Se si vuole, è possibile specificare il **Modello di URL di riscrittura**.</span><span class="sxs-lookup"><span data-stu-id="e901d-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="e901d-126">Questo consente di usare il modello di URL standard per elaborare le richieste in ingresso nel front-end, chiamando il back-end tramite un URL convertito in base al modello di riscrittura.</span><span class="sxs-lookup"><span data-stu-id="e901d-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="e901d-127">Nel modello di riscrittura è necessario usare i parametri di modello dell'URL di modello.</span><span class="sxs-lookup"><span data-stu-id="e901d-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="e901d-128">L'esempio seguente mostra il modo in cui il tipo di contenuto codificato come segmento del percorso nel servizio Web dell'esempio precedente può essere specificato come parametro di query nell'API pubblicata tramite la piattaforma di Gestione API usando i modelli di URL.</span><span class="sxs-lookup"><span data-stu-id="e901d-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![Riscrittura modello di URL][api-management-url-template-rewrite]

<span data-ttu-id="e901d-130">I chiamanti delle operazioni useranno il formato `/customers?customerid=ALFKI` che verrà mappato a `/Customers('ALFKI')` quando viene richiamato il servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="e901d-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="e901d-131">In **Nome visualizzato** e **Descrizione** viene fornita una descrizione dell'operazione e vengono usati per fornire la documentazione necessaria agli sviluppatori che usano questa API nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="e901d-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Description][api-management-description]

<span data-ttu-id="e901d-133">È possibile specificare la descrizione dell'operazione come testo normale o HTML nella casella di testo **Descrizione** .</span><span class="sxs-lookup"><span data-stu-id="e901d-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="e901d-134"><a name="operation-caching"> </a>Memorizzazione nella cache di un'operazione</span><span class="sxs-lookup"><span data-stu-id="e901d-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="e901d-135">La memorizzazione nella cache della risposta riduce la latenza percepita dai consumer dell'API, riduce l'utilizzo della larghezza di banda e diminuisce il carico nel servizio Web HTTP che implementa l'API.</span><span class="sxs-lookup"><span data-stu-id="e901d-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="e901d-136">Per abilitare la memorizzazione nella cache per l'operazione in modo facile e veloce, selezionare la scheda **Memorizzazione nella cache** e selezionare la casella di controllo **Abilita**.</span><span class="sxs-lookup"><span data-stu-id="e901d-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Memorizzazione nella cache][api-management-caching-tab]

<span data-ttu-id="e901d-138">**Durata** viene specificato il periodo di tempo durante il quale la risposta dell'operazione rimane nella cache.</span><span class="sxs-lookup"><span data-stu-id="e901d-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="e901d-139">Il valore predefinito è 3.600 secondi o un'ora.</span><span class="sxs-lookup"><span data-stu-id="e901d-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="e901d-140">Le chiavi della cache vengono usate per differenziare le risposte in modo che ogni risposta corrispondente a una chiave della cache ottenga il proprio valore memorizzato nella cache separato.</span><span class="sxs-lookup"><span data-stu-id="e901d-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="e901d-141">Facoltativamente, è possibile immettere parametri di stringa di query specifici e/o intestazioni HTTP da usare nei valori delle chiavi della cache di calcolo rispettivamente nelle caselle di testo **Varia in base ai parametri di stringa di query** e **Varia in base alle intestazioni**.</span><span class="sxs-lookup"><span data-stu-id="e901d-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="e901d-142">Se non viene specificato alcun valore, per la generazione della chiave della cache vengono usati i valori dell'URL di richiesta completo e l'intestazione HTTP seguenti: **Accept** e **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="e901d-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="e901d-143">Per altre informazioni sulla memorizzazione nella cache e sui relativi criteri, vedere [Come memorizzare nella cache i risultati dell'operazione in Gestione API di Azure][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="e901d-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="e901d-144"><a name="request-parameters"> </a>Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="e901d-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="e901d-145">È possibile gestire i parametri dell'operazione nella scheda Parametri.</span><span class="sxs-lookup"><span data-stu-id="e901d-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="e901d-146">I parametri specificati in **Modello di URL** nella scheda **Firma** vengono aggiunti automaticamente e possono essere cambiati solo modificando il modello di URL.</span><span class="sxs-lookup"><span data-stu-id="e901d-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="e901d-147">È possibile immettere i parametri aggiuntivi manualmente.</span><span class="sxs-lookup"><span data-stu-id="e901d-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="e901d-148">Per aggiungere un parametro di query, fare clic su **Aggiungi parametro di query** e immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e901d-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="e901d-149">**Nome** : nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="e901d-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="e901d-150">**Descrizione** : breve descrizione del parametro (facoltativa).</span><span class="sxs-lookup"><span data-stu-id="e901d-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="e901d-151">**Tipo** : tipo del parametro, selezionato nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e901d-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="e901d-152">**Valori** : valori che possono essere assegnati al parametro.</span><span class="sxs-lookup"><span data-stu-id="e901d-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="e901d-153">Uno dei valori può essere contrassegnato come predefinito (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="e901d-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="e901d-154">**Obbligatorio** : selezionare questa casella di controllo per rendere il parametro obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="e901d-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Parametri della richiesta][api-management-request-parameters]

## <span data-ttu-id="e901d-156"><a name="request-body"> </a>Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="e901d-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="e901d-157">Se l'operazione consente (ad esempio, PUT, POST) e richiede un corpo, è possibile fornirne un esempio in tutti i formati di rappresentazione supportati, ad esempio JSON e XML.</span><span class="sxs-lookup"><span data-stu-id="e901d-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="e901d-158">Il corpo della richiesta è usato solo ai fini della documentazione e non viene convalidato.</span><span class="sxs-lookup"><span data-stu-id="e901d-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="e901d-159">Per immettere un corpo della richiesta, passare alla scheda **Corpo** .</span><span class="sxs-lookup"><span data-stu-id="e901d-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="e901d-160">Fare clic su **Aggiungi rappresentazione**, iniziare a digitare il nome del tipo di contenuto desiderato (ad esempio, applicazione/json), selezionarlo nell'elenco a discesa e incollare nella casella di testo l'esempio di corpo della richiesta nel formato selezionato.</span><span class="sxs-lookup"><span data-stu-id="e901d-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Corpo della richiesta][api-management-request-body]

<span data-ttu-id="e901d-162">Oltre alle rappresentazioni, è possibile specificare una descrizione di testo facoltativa nella casella di testo **Descrizione** .</span><span class="sxs-lookup"><span data-stu-id="e901d-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="e901d-163"><a name="responses"> </a>Risposte</span><span class="sxs-lookup"><span data-stu-id="e901d-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="e901d-164">È consigliabile fornire esempi di risposte per tutti i codici di stato restituiti dall'operazione.</span><span class="sxs-lookup"><span data-stu-id="e901d-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="e901d-165">Per ogni codice di stato può esistere più di un esempio di corpo della risposta, ovvero uno per ogni tipo di contenuto supportato.</span><span class="sxs-lookup"><span data-stu-id="e901d-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="e901d-166">Per aggiungere una risposta, fare clic su **Aggiungi** e iniziare a digitare il codice di stato desiderato.</span><span class="sxs-lookup"><span data-stu-id="e901d-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="e901d-167">In questo esempio il codice di stato è **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e901d-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="e901d-168">Quando il codice viene visualizzato nell'elenco a discesa, selezionarlo in modo che il codice della risposta venga creato e aggiunto all'operazione.</span><span class="sxs-lookup"><span data-stu-id="e901d-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Codice della risposta][api-management-response-code]

<span data-ttu-id="e901d-170">Fare clic su **Aggiungi rappresentazione**, iniziare a digitare il nome del tipo di contenuto desiderato (ad esempio, applicazione/json) e selezionarlo nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="e901d-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Tipo di contenuto del corpo][api-management-response-body-content-type]

<span data-ttu-id="e901d-172">Incollare nella casella di testo l'esempio del corpo della risposta nel formato selezionato.</span><span class="sxs-lookup"><span data-stu-id="e901d-172">Paste the response body example in the selected format into the text box.</span></span> 

![Corpo della risposta][api-management-response-body]

<span data-ttu-id="e901d-174">Se necessario, aggiungere una descrizione facoltativa nella casella di testo **Descrizione** .</span><span class="sxs-lookup"><span data-stu-id="e901d-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="e901d-175">Dopo avere configurato l'operazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e901d-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="e901d-176"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e901d-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="e901d-177">Una volta aggiunte le operazioni a un'API, nel passaggio successivo l'API verrà associata a un prodotto e verrà pubblicata in modo che gli sviluppatori possano chiamare le relative operazioni.</span><span class="sxs-lookup"><span data-stu-id="e901d-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="e901d-178">[Come creare e pubblicare un prodotto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="e901d-178">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
