---
title: modelli aaaProduct in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come le pagine contenuto hello toocustomize del prodotto hello nel portale per sviluppatori di hello gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="fdac3-103">Modelli di prodotto in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="fdac3-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="fdac3-104">Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti.</span><span class="sxs-lookup"><span data-stu-id="fdac3-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="fdac3-105">Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.</span><span class="sxs-lookup"><span data-stu-id="fdac3-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="fdac3-106">i modelli di Hello in questa sezione consentono di contenuto di hello toocustomize delle pagine di prodotto di hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="fdac3-107">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="fdac3-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="fdac3-108">Prodotto</span><span class="sxs-lookup"><span data-stu-id="fdac3-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="fdac3-109">Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="fdac3-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="fdac3-110">È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="fdac3-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="fdac3-111">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="fdac3-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="fdac3-112"><a name="ProductList"></a> Elenco prodotti</span><span class="sxs-lookup"><span data-stu-id="fdac3-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="fdac3-113">Hello **Product list** modello consente il corpo di hello toocustomize della pagina di elenco prodotto hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="fdac3-114">![Elenco prodotti](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="fdac3-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="fdac3-115">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="fdac3-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="fdac3-116">Controlli</span><span class="sxs-lookup"><span data-stu-id="fdac3-116">Controls</span></span>  
 <span data-ttu-id="fdac3-117">Hello `Product list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="fdac3-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="fdac3-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="fdac3-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="fdac3-119">search-control</span><span class="sxs-lookup"><span data-stu-id="fdac3-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="fdac3-120">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="fdac3-120">Data model</span></span>  
  
|<span data-ttu-id="fdac3-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fdac3-121">Property</span></span>|<span data-ttu-id="fdac3-122">Tipo</span><span class="sxs-lookup"><span data-stu-id="fdac3-122">Type</span></span>|<span data-ttu-id="fdac3-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fdac3-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="fdac3-124">Paging</span><span class="sxs-lookup"><span data-stu-id="fdac3-124">Paging</span></span>|<span data-ttu-id="fdac3-125">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="fdac3-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="fdac3-126">Hello paging le informazioni per la raccolta di prodotti hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="fdac3-127">Filtri</span><span class="sxs-lookup"><span data-stu-id="fdac3-127">Filtering</span></span>|<span data-ttu-id="fdac3-128">Entità [Filtri](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="fdac3-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="fdac3-129">Hello informazioni di filtro per i prodotti hello pagina di elenco.</span><span class="sxs-lookup"><span data-stu-id="fdac3-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="fdac3-130">Prodotti</span><span class="sxs-lookup"><span data-stu-id="fdac3-130">Products</span></span>|<span data-ttu-id="fdac3-131">Raccolta di entità [Prodotto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="fdac3-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="fdac3-132">utente corrente toohello visibile prodotti Hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="fdac3-133">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="fdac3-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="fdac3-134"><a name="Product"></a>Prodotto</span><span class="sxs-lookup"><span data-stu-id="fdac3-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="fdac3-135">Hello **prodotto** modello consente il corpo di hello toocustomize della pagina del prodotto hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="fdac3-136">![Pagina prodotto nel portale per sviluppatori](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="fdac3-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="fdac3-137">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="fdac3-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="fdac3-138">Controlli</span><span class="sxs-lookup"><span data-stu-id="fdac3-138">Controls</span></span>  
 <span data-ttu-id="fdac3-139">Hello `Product list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="fdac3-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="fdac3-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="fdac3-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="fdac3-141">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="fdac3-141">Data model</span></span>  
  
|<span data-ttu-id="fdac3-142">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fdac3-142">Property</span></span>|<span data-ttu-id="fdac3-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="fdac3-143">Type</span></span>|<span data-ttu-id="fdac3-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fdac3-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="fdac3-145">Prodotto</span><span class="sxs-lookup"><span data-stu-id="fdac3-145">Product</span></span>|[<span data-ttu-id="fdac3-146">Prodotto</span><span class="sxs-lookup"><span data-stu-id="fdac3-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="fdac3-147">prodotto specificato Hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-147">hello specified product.</span></span>|  
|<span data-ttu-id="fdac3-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="fdac3-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="fdac3-149">boolean</span><span class="sxs-lookup"><span data-stu-id="fdac3-149">boolean</span></span>|<span data-ttu-id="fdac3-150">Indica se l'utente corrente hello è prodotto toothis sottoscritti.</span><span class="sxs-lookup"><span data-stu-id="fdac3-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="fdac3-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="fdac3-151">SubscriptionState</span></span>|<span data-ttu-id="fdac3-152">number</span><span class="sxs-lookup"><span data-stu-id="fdac3-152">number</span></span>|<span data-ttu-id="fdac3-153">stato di Hello della sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-153">hello state of hello subscription.</span></span> <span data-ttu-id="fdac3-154">Gli stati possibili sono elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="fdac3-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="fdac3-155">-   `0 - suspended`: hello sottoscrizione è bloccata e il sottoscrittore hello non è possibile chiamare le API del prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="fdac3-156">-   `1 - active`: hello sottoscrizione è attiva.</span><span class="sxs-lookup"><span data-stu-id="fdac3-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="fdac3-157">-   `2 - expired`: hello ha raggiunto la data di scadenza ed è stata disattivata.</span><span class="sxs-lookup"><span data-stu-id="fdac3-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="fdac3-158">-   `3 - submitted`: la richiesta di sottoscrizione hello è stata effettuata dallo sviluppatore di hello, ma non è ancora stata approvata o rifiutata.</span><span class="sxs-lookup"><span data-stu-id="fdac3-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="fdac3-159">-   `4 - rejected`: hello sottoscrizione richiesta è stata rifiutata da un amministratore.</span><span class="sxs-lookup"><span data-stu-id="fdac3-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="fdac3-160">-   `5 - cancelled`-sottoscrizione hello è stata annullata dallo sviluppatore hello o un amministratore.</span><span class="sxs-lookup"><span data-stu-id="fdac3-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="fdac3-161">Limiti</span><span class="sxs-lookup"><span data-stu-id="fdac3-161">Limits</span></span>|<span data-ttu-id="fdac3-162">array</span><span class="sxs-lookup"><span data-stu-id="fdac3-162">array</span></span>|<span data-ttu-id="fdac3-163">Questa proprietà è deprecata e non deve essere usata.</span><span class="sxs-lookup"><span data-stu-id="fdac3-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="fdac3-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="fdac3-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="fdac3-165">boolean</span><span class="sxs-lookup"><span data-stu-id="fdac3-165">boolean</span></span>|<span data-ttu-id="fdac3-166">Indica se sia abilitata la [delega](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) per questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fdac3-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="fdac3-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="fdac3-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="fdac3-168">string</span><span class="sxs-lookup"><span data-stu-id="fdac3-168">string</span></span>|<span data-ttu-id="fdac3-169">Se è abilitata la delega, hello delegata URL di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fdac3-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="fdac3-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="fdac3-170">IsAgreed</span></span>|<span data-ttu-id="fdac3-171">boolean</span><span class="sxs-lookup"><span data-stu-id="fdac3-171">boolean</span></span>|<span data-ttu-id="fdac3-172">Se il prodotto hello è termini, se hello corrente utente ha accettato i termini di toohello.</span><span class="sxs-lookup"><span data-stu-id="fdac3-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="fdac3-173">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="fdac3-173">Subscriptions</span></span>|<span data-ttu-id="fdac3-174">Raccolta di entità [Riepilogo della sottoscrizione](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="fdac3-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="fdac3-175">prodotto di toohello Hello sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="fdac3-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="fdac3-176">API</span><span class="sxs-lookup"><span data-stu-id="fdac3-176">Apis</span></span>|<span data-ttu-id="fdac3-177">Raccolta di entità [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="fdac3-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="fdac3-178">Hello API in questo prodotto.</span><span class="sxs-lookup"><span data-stu-id="fdac3-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="fdac3-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="fdac3-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="fdac3-180">boolean</span><span class="sxs-lookup"><span data-stu-id="fdac3-180">boolean</span></span>|<span data-ttu-id="fdac3-181">Indica se l'utente corrente hello è toosubscribe idonei toothis prodotto con limite della sottoscrizione toohello considerare.</span><span class="sxs-lookup"><span data-stu-id="fdac3-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="fdac3-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="fdac3-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="fdac3-183">boolean</span><span class="sxs-lookup"><span data-stu-id="fdac3-183">boolean</span></span>|<span data-ttu-id="fdac3-184">Indica se l'utente corrente hello è idoneo toosubscribe toothis prodotto con sottoscrizioni toomultiple considerare consentite o non.</span><span class="sxs-lookup"><span data-stu-id="fdac3-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="fdac3-185">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="fdac3-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="fdac3-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdac3-186">Next steps</span></span>
<span data-ttu-id="fdac3-187">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fdac3-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
