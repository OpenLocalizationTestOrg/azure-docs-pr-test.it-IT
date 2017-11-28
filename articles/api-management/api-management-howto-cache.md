---
title: la memorizzazione nella cache le prestazioni di tooimprove in Gestione API di Azure aaaAdd | Documenti Microsoft
description: Informazioni su come caricare il servizio web, il consumo di larghezza di banda e latenza hello tooimprove per le chiamate al servizio Gestione API.
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
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="01bf0-103">Aggiungere la memorizzazione nella cache delle prestazioni tooimprove in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="01bf0-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="01bf0-104">Le operazioni in Gestione API possono essere configurate per la memorizzazione nella cache della risposta.</span><span class="sxs-lookup"><span data-stu-id="01bf0-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="01bf0-105">La memorizzazione nella cache della risposta può ridurre significativamente la latenza delle API, il consumo di larghezza di banda e il carico del servizio Web per i dati che non vengono modificati di frequente.</span><span class="sxs-lookup"><span data-stu-id="01bf0-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="01bf0-106">Questa guida illustra come risposta tooadd la memorizzazione nella cache per l'API e configurare i criteri per le operazioni dell'API di Echo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="01bf0-107">È quindi possibile chiamare l'operazione di hello dalla hello memorizzazione nella cache tooverify portale per sviluppatori in azione.</span><span class="sxs-lookup"><span data-stu-id="01bf0-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="01bf0-108">Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="01bf0-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="01bf0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="01bf0-109">Prerequisites</span></span>
<span data-ttu-id="01bf0-110">Prima di hello seguente passaggi in questa Guida, è necessario disporre di un'istanza del servizio Gestione API con un'API e un prodotto configurato.</span><span class="sxs-lookup"><span data-stu-id="01bf0-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="01bf0-111">Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="01bf0-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="01bf0-112"><a name="configure-caching"></a>Configurare un'operazione per la memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="01bf0-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="01bf0-113">In questo passaggio si esamineranno hello la memorizzazione nella cache le impostazioni di hello **ottenere risorse (cache)** operazione dell'esempio hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="01bf0-114">Ogni istanza del servizio Gestione API preconfigurato con un'API Echo che possono essere tooexperiment utilizzati con e acquisire informazioni su gestione API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="01bf0-115">Per altre informazioni, vedere [Introduzione a Gestione API di Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="01bf0-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="01bf0-116">tooget avviato, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="01bf0-117">Consente di procedere toohello portale di pubblicazione di gestione API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-117">This takes you toohello API Management publisher portal.</span></span>

![Portale di pubblicazione][api-management-management-console]

<span data-ttu-id="01bf0-119">Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![API Echo][api-management-echo-api]

<span data-ttu-id="01bf0-121">Fare clic su hello **operazioni** scheda e quindi fare clic su hello **ottenere risorse (cache)** operazione hello **operazioni** elenco.</span><span class="sxs-lookup"><span data-stu-id="01bf0-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Operazioni dell'API Echo][api-management-echo-api-operations]

<span data-ttu-id="01bf0-123">Fare clic su hello **la memorizzazione nella cache** hello tooview scheda Impostazioni per l'operazione di memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="01bf0-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Scheda Memorizzazione nella cache][api-management-caching-tab]

<span data-ttu-id="01bf0-125">tooenable la memorizzazione nella cache per un'operazione, seleziona hello **abilitare** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="01bf0-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="01bf0-126">In questo esempio, il caching è abilitato.</span><span class="sxs-lookup"><span data-stu-id="01bf0-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="01bf0-127">Ogni risposta di operazione con chiave, in base ai valori hello hello **possono variare dai parametri di stringa di query** e **possono variare dalle intestazioni** campi.</span><span class="sxs-lookup"><span data-stu-id="01bf0-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="01bf0-128">Se si desidera toocache più risposte in base a parametri di stringa di query o le intestazioni, è possibile configurare loro questi due campi.</span><span class="sxs-lookup"><span data-stu-id="01bf0-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="01bf0-129">**Durata** specifica l'intervallo di scadenza hello delle risposte hello memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="01bf0-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="01bf0-130">In questo esempio, è l'intervallo hello **3600** secondi, ovvero ora tooone equivalente.</span><span class="sxs-lookup"><span data-stu-id="01bf0-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="01bf0-131">Utilizza la memorizzazione nella cache di configurazione in questo esempio hello, hello prima richiesta toohello **ottenere risorse (cache)** operazione restituisce una risposta dal servizio back-end hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="01bf0-132">Questa risposta nella cache, con chiave fornita da hello specificato parametri di stringa di query e le intestazioni.</span><span class="sxs-lookup"><span data-stu-id="01bf0-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="01bf0-133">Le chiamate successive operazione toohello, con i corrispondenti parametri, sarà necessario hello memorizzati nella cache di risposta restituito, fino a quando l'intervallo di durata della cache di hello è scaduto.</span><span class="sxs-lookup"><span data-stu-id="01bf0-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="01bf0-134"><a name="caching-policies"></a>Hello rivedere i criteri di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="01bf0-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="01bf0-135">In questo passaggio è esaminare la memorizzazione nella cache le impostazioni per hello hello **ottenere risorse (cache)** operazione dell'esempio hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="01bf0-136">Quando le impostazioni della cache sono configurate per un'operazione su hello **la memorizzazione nella cache** scheda, la memorizzazione nella cache vengono aggiunti i criteri per l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="01bf0-137">Questi criteri possono essere visualizzati e modificati nell'editor Criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="01bf0-138">Fare clic su **criteri** da hello **gestione API** menu hello a sinistra e quindi seleziona **API Echo / ottenere una risorsa (cache)** da hello **operazione**elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="01bf0-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Operazione nell'ambito dei criteri][api-management-operation-dropdown]

<span data-ttu-id="01bf0-140">Consente di visualizzare i criteri per questa operazione hello editor Criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Editor dei criteri di Gestione API][api-management-policy-editor]

<span data-ttu-id="01bf0-142">definizione dei criteri Hello per questa operazione include hello criteri che definiscono una configurazione di cache di hello e che sono stati controllati tramite hello **la memorizzazione nella cache** scheda nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

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
> <span data-ttu-id="01bf0-143">Toohello le modifiche apportate nell'editor Criteri di hello i criteri di memorizzazione nella cache verrà riflesse nella hello **la memorizzazione nella cache** scheda di un'operazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="01bf0-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="01bf0-144"><a name="test-operation"></a>Chiamare un'operazione e verificare la memorizzazione nella cache di hello</span><span class="sxs-lookup"><span data-stu-id="01bf0-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="01bf0-145">hello toosee la memorizzazione nella cache in azione, è possibile chiamare operazione hello dal portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="01bf0-146">Fare clic su **portale per sviluppatori** nel menu in alto destra hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-146">Click **Developer portal** in hello top right menu.</span></span>

![Portale per sviluppatori][api-management-developer-portal-menu]

<span data-ttu-id="01bf0-148">Fare clic su **API** in hello menu superiore e quindi selezionare **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> <span data-ttu-id="01bf0-150">Se si dispone di un solo API configurata o account tooyour visibile, quindi fare clic su API consente di passare direttamente toohello operazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="01bf0-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="01bf0-151">Seleziona hello **ottenere risorse (cache)** operazione e quindi fare clic su **aprire la Console di**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="01bf0-153">console Hello consente operazioni di tooinvoke direttamente dal portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="01bf0-155">Mantenere i valori predefiniti di hello per **param1** e **param2**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="01bf0-156">Selezionare hello chiave desiderato da hello **chiave di sottoscrizione** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="01bf0-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="01bf0-157">Se l'account ha una sola sottoscrizione, sarà già selezionata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="01bf0-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="01bf0-158">Immettere **sampleheader:value1** in hello **le intestazioni di richiesta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="01bf0-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="01bf0-159">Fare clic su **HTTP Get** e prendere nota di hello intestazioni di risposta.</span><span class="sxs-lookup"><span data-stu-id="01bf0-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="01bf0-160">Immettere **sampleheader:value2** in hello **le intestazioni di richiesta** casella di testo e quindi fare clic su **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="01bf0-161">Si noti il valore di hello di **sampleheader** è ancora **value1** in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="01bf0-162">Provare alcuni valori diversi e viene restituito si noti che la risposta memorizzata nella cache dalla prima chiamata hello hello.</span><span class="sxs-lookup"><span data-stu-id="01bf0-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="01bf0-163">Immettere **25** in hello **param2** campo e quindi fare clic su **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="01bf0-164">Si noti il valore di hello di **sampleheader** in hello risposta è ora **value2**.</span><span class="sxs-lookup"><span data-stu-id="01bf0-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="01bf0-165">Poiché i risultati dell'operazione hello vengono codificati dalla stringa di query, risposta memorizzata nella cache di hello precedente non è stato restituito.</span><span class="sxs-lookup"><span data-stu-id="01bf0-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="01bf0-166"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01bf0-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="01bf0-167">Per ulteriori informazioni sulla memorizzazione nella cache i criteri, vedere [criteri di memorizzazione nella cache] [ Caching policies] in hello [riferimento ai criteri di gestione API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="01bf0-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="01bf0-168">Per informazioni sul caching degli elementi in base alla chiave usando espressioni di criteri, vedere [Caching personalizzato in Gestione API di Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="01bf0-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
