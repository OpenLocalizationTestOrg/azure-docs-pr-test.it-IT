---
title: Aggiungere il caching per migliorare le prestazioni in Gestione API di Azure | Microsoft Docs
description: Informazioni su come migliorare la latenza, il consumo della larghezza di banda e il carico del servizio Web per le chiamate del servizio Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="2eb35-103">Aggiungere il caching per migliorare le prestazioni in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="2eb35-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="2eb35-104">Le operazioni in Gestione API possono essere configurate per la memorizzazione nella cache della risposta.</span><span class="sxs-lookup"><span data-stu-id="2eb35-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="2eb35-105">La memorizzazione nella cache della risposta può ridurre significativamente la latenza delle API, il consumo di larghezza di banda e il carico del servizio Web per i dati che non vengono modificati di frequente.</span><span class="sxs-lookup"><span data-stu-id="2eb35-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="2eb35-106">Questa Guida illustra come aggiungere la memorizzazione delle risposte nella cache per l'API e configurare i criteri per le operazioni API Echo di esempio.</span><span class="sxs-lookup"><span data-stu-id="2eb35-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="2eb35-107">Per verificare il funzionamento della memorizzazione della cache, è possibile chiamare l'operazione dal portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2eb35-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="2eb35-108">Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="2eb35-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2eb35-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2eb35-109">Prerequisites</span></span>
<span data-ttu-id="2eb35-110">Prima di eseguire i passaggi di questa guida, è necessario avere un'istanza del servizio Gestione API con un'API e un prodotto configurati.</span><span class="sxs-lookup"><span data-stu-id="2eb35-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="2eb35-111">Se non è stata creata un'istanza del servizio Gestione API, vedere [Creare un'istanza di Gestione API][Create an API Management service instance] nell'esercitazione [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2eb35-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="2eb35-112"><a name="configure-caching"> </a>Configurare un'operazione per la memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="2eb35-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="2eb35-113">In questo passaggio vengono riviste le impostazioni di caching dell'operazione **GET su risorsa (memorizzata nella cache)** dell'API Echo di esempio.</span><span class="sxs-lookup"><span data-stu-id="2eb35-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="2eb35-114">Ogni istanza del servizio Gestione API è preconfigurata con un'API Echo utilizzabile per sperimentare e ottenere altre informazioni su Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2eb35-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="2eb35-115">Per altre informazioni, vedere [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2eb35-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="2eb35-116">Per iniziare, fare clic sul **portale di pubblicazione** nel Portale di Azure relativo al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2eb35-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="2eb35-117">Verrà visualizzato il portale di pubblicazione di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2eb35-117">This takes you to the API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="2eb35-119">Scegliere **API** dal menu **Gestione API** a sinistra, quindi fare clic su **Echo API** (API Echo).</span><span class="sxs-lookup"><span data-stu-id="2eb35-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![API Echo][api-management-echo-api]

<span data-ttu-id="2eb35-121">Fare clic sulla scheda **Operazioni**, quindi sull'operazione **GET Resource (cached)** (GET su risorsa - memorizzata nella cache) nell'elenco **Operazioni**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Operazioni dell'API Echo][api-management-echo-api-operations]

<span data-ttu-id="2eb35-123">Fare clic sulla scheda **Caching** per visualizzare le impostazioni di caching per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="2eb35-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Scheda Memorizzazione nella cache][api-management-caching-tab]

<span data-ttu-id="2eb35-125">Per abilitare il caching per un'operazione, selezionare la casella di controllo **Abilita** .</span><span class="sxs-lookup"><span data-stu-id="2eb35-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="2eb35-126">In questo esempio, il caching è abilitato.</span><span class="sxs-lookup"><span data-stu-id="2eb35-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="2eb35-127">La risposta di ogni operazione è associata a una chiave in base ai valori dei campi **Variabile in base a parametri stringa query** e **Vary by headers** (Variabile in base a intestazioni).</span><span class="sxs-lookup"><span data-stu-id="2eb35-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="2eb35-128">Per memorizzare nella cache più risposte in base ai parametri delle stringhe di query o alle intestazioni, è possibile configurarle in questi due campi.</span><span class="sxs-lookup"><span data-stu-id="2eb35-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="2eb35-129">**durata** specifica l'intervallo di scadenza delle risposte memorizzate nella cache.</span><span class="sxs-lookup"><span data-stu-id="2eb35-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="2eb35-130">In questo esempio l'intervallo è di **3600** secondi, equivalente a un'ora.</span><span class="sxs-lookup"><span data-stu-id="2eb35-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="2eb35-131">Nella configurazione di esempio del caching la prima richiesta all'operazione **GET su risorsa (memorizzata nella cache)** restituisce una risposta dal servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="2eb35-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="2eb35-132">Questa risposta viene memorizzata nella cache, associata a una chiave mediante le intestazioni e i parametri delle stringhe di query specificati.</span><span class="sxs-lookup"><span data-stu-id="2eb35-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="2eb35-133">Le chiamate successive all'operazione, con i parametri corrispondenti, riceveranno la risposta memorizzata nella cache finché non scade l'intervallo di durata della cache.</span><span class="sxs-lookup"><span data-stu-id="2eb35-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="2eb35-134"><a name="caching-policies"> </a>Rivedere i criteri di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="2eb35-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="2eb35-135">In questo passaggio vengono riviste le impostazioni di caching dell'operazione **GET su risorsa** (memorizzata nella cache) dell'API Echo di esempio.</span><span class="sxs-lookup"><span data-stu-id="2eb35-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="2eb35-136">Quando le impostazioni di memorizzazione nella cache vengono configurate per un'operazione nella scheda **Memorizzazione nella cache** , vengono aggiunti i criteri di memorizzazione nella cache per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="2eb35-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="2eb35-137">Questi criteri possono essere visualizzati e modificati nell'editor dei criteri.</span><span class="sxs-lookup"><span data-stu-id="2eb35-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="2eb35-138">Fare clic su **Criteri** dal menu **Gestione API** a sinistra, quindi selezionare **Echo API / GET Resource (cached)** (API Echo/GET su risorsa - memorizzata nella cache) dall'elenco a discesa **Operazione**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Operazione nell'ambito dei criteri][api-management-operation-dropdown]

<span data-ttu-id="2eb35-140">Visualizza i criteri per l'operazione nell'editor dei criteri.</span><span class="sxs-lookup"><span data-stu-id="2eb35-140">This displays the policies for this operation in the policy editor.</span></span>

![Editor dei criteri di Gestione API][api-management-policy-editor]

<span data-ttu-id="2eb35-142">La definizione dei criteri per questa operazione include i criteri che definiscono la configurazione della memorizzazione nella cache rivisti usando la scheda **Memorizzazione nella cache** nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="2eb35-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="2eb35-143">Le modifiche apportate ai criteri di caching nell'editor dei criteri si rifletteranno nella scheda **Caching** di un'operazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="2eb35-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="2eb35-144"><a name="test-operation"> </a>Chiamare un'operazione e testare la memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="2eb35-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="2eb35-145">Per vedere il funzionamento della memorizzazione nella cache, l'operazione viene chiamata dal portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2eb35-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="2eb35-146">Fare clic su **Developer portal** nel menu in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="2eb35-146">Click **Developer portal** in the top right menu.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="2eb35-148">Fare clic su **API** dal menu in alto e quindi scegliere **Echo API** (API Echo).</span><span class="sxs-lookup"><span data-stu-id="2eb35-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> <span data-ttu-id="2eb35-150">Se è stata configurata una sola API o se ne è visibile solo una per l'account, facendo clic sulle API vengono visualizzate le operazioni per l'API.</span><span class="sxs-lookup"><span data-stu-id="2eb35-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="2eb35-151">Selezionare l'operazione **GET Resource (cached)** (GET su risorsa - memorizzata nella cache), quindi fare clic su **Apri console**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="2eb35-153">La console consente di richiamare le operazioni direttamente dal portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2eb35-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="2eb35-155">Mantenere i valori predefiniti per **param1** e **param2**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="2eb35-156">Selezionare la chiave desiderata dall'elenco a discesa **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="2eb35-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="2eb35-157">Se l'account ha una sola sottoscrizione, sarà già selezionata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2eb35-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="2eb35-158">Immettere **sampleheader:value1** nella casella di testo **Intestazioni della richiesta**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="2eb35-159">Fare clic su **GET HTTP** e annotare le intestazioni di risposta.</span><span class="sxs-lookup"><span data-stu-id="2eb35-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="2eb35-160">Immettere **sampleheader:value2** nella casella di testo **Intestazioni della richiesta** e quindi fare clic su **GET HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="2eb35-161">Il valore di **sampleheader** nella risposta è ancora **value1**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="2eb35-162">Provare altri valori diversi e notare che viene restituita la risposta memorizzata nella cache della prima chiamata.</span><span class="sxs-lookup"><span data-stu-id="2eb35-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="2eb35-163">Immettere **25** nel campo **param2**, quindi fare clic su **GET HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="2eb35-164">Il valore di **sampleheader** nella risposta ora è **value2**.</span><span class="sxs-lookup"><span data-stu-id="2eb35-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="2eb35-165">I risultati dell'operazione vengono associati a una chiave in base alla stringa di query, quindi non viene restituita la risposta memorizzata nella cache precedente.</span><span class="sxs-lookup"><span data-stu-id="2eb35-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="2eb35-166"><a name="next-steps"> </a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2eb35-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2eb35-167">Per altre informazioni sui criteri di caching, vedere [Caching policies][Caching policies] (Criteri di caching) nell'argomento [API Management policy reference][API Management policy reference] (Riferimento ai criteri di Gestione API).</span><span class="sxs-lookup"><span data-stu-id="2eb35-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="2eb35-168">Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="2eb35-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
