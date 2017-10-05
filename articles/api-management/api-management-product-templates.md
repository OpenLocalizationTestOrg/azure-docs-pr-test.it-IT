---
title: Modelli di prodotto in Gestione API di Azure | Microsoft Docs
description: Informazioni su come personalizzare il contenuto delle pagine prodotto nel portale per sviluppatori in Gestione API di Azure.
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="7c98d-103">Modelli di prodotto in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="7c98d-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="7c98d-104">In Gestione API di Azure è possibile personalizzare le pagine del portale per sviluppatori usando un set di modelli che ne configurano il contenuto.</span><span class="sxs-lookup"><span data-stu-id="7c98d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7c98d-105">La sintassi [DotLiquid](http://dotliquidmarkup.org/) usata insieme a un editor di propria scelta, quale [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e a un set di [risorse stringa](api-management-template-resources.md#strings), [risorse Glifo](api-management-template-resources.md#glyphs) e [controlli di pagina](api-management-page-controls.md) offre una grande flessibilità nella configurazione personalizzata del contenuto delle pagine attraverso questi modelli.</span><span class="sxs-lookup"><span data-stu-id="7c98d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7c98d-106">I modelli in questa sezione consentono di personalizzare il contenuto delle pagine prodotto del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="7c98d-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="7c98d-107">Elenco dei prodotti</span><span class="sxs-lookup"><span data-stu-id="7c98d-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="7c98d-108">Prodotto</span><span class="sxs-lookup"><span data-stu-id="7c98d-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="7c98d-109">La documentazione seguente include alcuni modelli predefiniti di esempio. A causa dei continui miglioramenti che vengono apportati, questi modelli sono però soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="7c98d-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="7c98d-110">È possibile visualizzare i modelli predefiniti direttamente nel portale per sviluppatori accedendo ai singoli modelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="7c98d-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="7c98d-111">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="7c98d-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="7c98d-112"><a name="ProductList"></a> Elenco prodotti</span><span class="sxs-lookup"><span data-stu-id="7c98d-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="7c98d-113">Il modello **Elenco prodotti** consente di personalizzare il corpo della pagina di elenco prodotti nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="7c98d-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="7c98d-114">![Elenco prodotti](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="7c98d-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7c98d-115">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="7c98d-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7c98d-116">Controlli</span><span class="sxs-lookup"><span data-stu-id="7c98d-116">Controls</span></span>  
 <span data-ttu-id="7c98d-117">Il modello `Product list` può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="7c98d-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7c98d-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="7c98d-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="7c98d-119">search-control</span><span class="sxs-lookup"><span data-stu-id="7c98d-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="7c98d-120">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="7c98d-120">Data model</span></span>  
  
|<span data-ttu-id="7c98d-121">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7c98d-121">Property</span></span>|<span data-ttu-id="7c98d-122">Tipo</span><span class="sxs-lookup"><span data-stu-id="7c98d-122">Type</span></span>|<span data-ttu-id="7c98d-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7c98d-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7c98d-124">Paging</span><span class="sxs-lookup"><span data-stu-id="7c98d-124">Paging</span></span>|<span data-ttu-id="7c98d-125">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="7c98d-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="7c98d-126">Le informazioni di paging per la raccolta di prodotti.</span><span class="sxs-lookup"><span data-stu-id="7c98d-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="7c98d-127">Filtri</span><span class="sxs-lookup"><span data-stu-id="7c98d-127">Filtering</span></span>|<span data-ttu-id="7c98d-128">Entità [Filtri](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="7c98d-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="7c98d-129">Le informazioni dei filtri per la pagina di elenco proodtti.</span><span class="sxs-lookup"><span data-stu-id="7c98d-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="7c98d-130">Prodotti</span><span class="sxs-lookup"><span data-stu-id="7c98d-130">Products</span></span>|<span data-ttu-id="7c98d-131">Raccolta di entità [Prodotto](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="7c98d-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="7c98d-132">I prodotti visibili all'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="7c98d-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7c98d-133">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="7c98d-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="7c98d-134"><a name="Product"></a> Prodotto</span><span class="sxs-lookup"><span data-stu-id="7c98d-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="7c98d-135">Il modello **Prodotto** consente di personalizzare il corpo della pagina prodotto nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="7c98d-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="7c98d-136">![Pagina prodotto nel portale per sviluppatori](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="7c98d-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7c98d-137">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="7c98d-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7c98d-138">Controlli</span><span class="sxs-lookup"><span data-stu-id="7c98d-138">Controls</span></span>  
 <span data-ttu-id="7c98d-139">Il modello `Product list` può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="7c98d-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7c98d-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="7c98d-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="7c98d-141">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="7c98d-141">Data model</span></span>  
  
|<span data-ttu-id="7c98d-142">Proprietà</span><span class="sxs-lookup"><span data-stu-id="7c98d-142">Property</span></span>|<span data-ttu-id="7c98d-143">Tipo</span><span class="sxs-lookup"><span data-stu-id="7c98d-143">Type</span></span>|<span data-ttu-id="7c98d-144">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7c98d-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7c98d-145">Prodotto</span><span class="sxs-lookup"><span data-stu-id="7c98d-145">Product</span></span>|[<span data-ttu-id="7c98d-146">Prodotto</span><span class="sxs-lookup"><span data-stu-id="7c98d-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="7c98d-147">Il prodotto specificato.</span><span class="sxs-lookup"><span data-stu-id="7c98d-147">The specified product.</span></span>|  
|<span data-ttu-id="7c98d-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="7c98d-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="7c98d-149">boolean</span><span class="sxs-lookup"><span data-stu-id="7c98d-149">boolean</span></span>|<span data-ttu-id="7c98d-150">Indica se l'utente corrente è sottoscritto a questo prodotto.</span><span class="sxs-lookup"><span data-stu-id="7c98d-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="7c98d-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="7c98d-151">SubscriptionState</span></span>|<span data-ttu-id="7c98d-152">number</span><span class="sxs-lookup"><span data-stu-id="7c98d-152">number</span></span>|<span data-ttu-id="7c98d-153">Lo stato della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c98d-153">The state of the subscription.</span></span> <span data-ttu-id="7c98d-154">Gli stati possibili sono elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="7c98d-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="7c98d-155">-   `0 - suspended`: la sottoscrizione è bloccata e il sottoscrittore non può chiamare le API del prodotto.</span><span class="sxs-lookup"><span data-stu-id="7c98d-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="7c98d-156">-   `1 - active`: la sottoscrizione è attiva.</span><span class="sxs-lookup"><span data-stu-id="7c98d-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="7c98d-157">-   `2 - expired`: la sottoscrizione ha raggiunto la data di scadenza ed è stata disattivata.</span><span class="sxs-lookup"><span data-stu-id="7c98d-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="7c98d-158">-   `3 - submitted`: la richiesta di sottoscrizione è stata eseguita dallo sviluppatore, ma non è ancora stata approvata o rifiutata.</span><span class="sxs-lookup"><span data-stu-id="7c98d-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="7c98d-159">-   `4 - rejected`: la richiesta di sottoscrizione è stata rifiutata da un amministratore.</span><span class="sxs-lookup"><span data-stu-id="7c98d-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="7c98d-160">-   `5 - cancelled`: la sottoscrizione è stata annullata dallo sviluppatore o dall'amministratore.</span><span class="sxs-lookup"><span data-stu-id="7c98d-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="7c98d-161">limiti</span><span class="sxs-lookup"><span data-stu-id="7c98d-161">Limits</span></span>|<span data-ttu-id="7c98d-162">array</span><span class="sxs-lookup"><span data-stu-id="7c98d-162">array</span></span>|<span data-ttu-id="7c98d-163">Questa proprietà è deprecata e non deve essere usata.</span><span class="sxs-lookup"><span data-stu-id="7c98d-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="7c98d-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="7c98d-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="7c98d-165">boolean</span><span class="sxs-lookup"><span data-stu-id="7c98d-165">boolean</span></span>|<span data-ttu-id="7c98d-166">Indica se sia abilitata la [delega](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) per questa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="7c98d-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="7c98d-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="7c98d-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="7c98d-168">string</span><span class="sxs-lookup"><span data-stu-id="7c98d-168">string</span></span>|<span data-ttu-id="7c98d-169">Se è abilitata la delega, indica l'URL della sottoscrizione delegata.</span><span class="sxs-lookup"><span data-stu-id="7c98d-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="7c98d-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="7c98d-170">IsAgreed</span></span>|<span data-ttu-id="7c98d-171">boolean</span><span class="sxs-lookup"><span data-stu-id="7c98d-171">boolean</span></span>|<span data-ttu-id="7c98d-172">Se il prodotto presenta delle condizioni, indica se l'utente corrente le ha accettate.</span><span class="sxs-lookup"><span data-stu-id="7c98d-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="7c98d-173">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="7c98d-173">Subscriptions</span></span>|<span data-ttu-id="7c98d-174">Raccolta di entità [Riepilogo della sottoscrizione](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="7c98d-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="7c98d-175">Le sottoscrizioni al prodotto.</span><span class="sxs-lookup"><span data-stu-id="7c98d-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="7c98d-176">API</span><span class="sxs-lookup"><span data-stu-id="7c98d-176">Apis</span></span>|<span data-ttu-id="7c98d-177">Raccolta di entità [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="7c98d-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="7c98d-178">Le API in questo prodotto.</span><span class="sxs-lookup"><span data-stu-id="7c98d-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="7c98d-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="7c98d-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="7c98d-180">boolean</span><span class="sxs-lookup"><span data-stu-id="7c98d-180">boolean</span></span>|<span data-ttu-id="7c98d-181">Indica se l'utente corrente è idoneo per la sottoscrizione al prodotto per quanto riguarda il limite delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="7c98d-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="7c98d-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="7c98d-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="7c98d-183">boolean</span><span class="sxs-lookup"><span data-stu-id="7c98d-183">boolean</span></span>|<span data-ttu-id="7c98d-184">Indica se l'utente corrente è idoneo per la sottoscrizione al prodotto per quanto riguarda l'autorizzazione a effettuare più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="7c98d-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7c98d-185">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="7c98d-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="7c98d-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c98d-186">Next steps</span></span>
<span data-ttu-id="7c98d-187">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7c98d-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>