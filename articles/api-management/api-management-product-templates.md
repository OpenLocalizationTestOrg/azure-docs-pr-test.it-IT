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
# <a name="product-templates-in-azure-api-management"></a>Modelli di prodotto in Gestione API di Azure
Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti. Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.  
  
 i modelli di Hello in questa sezione consentono di contenuto di hello toocustomize delle pagine di prodotto di hello nel portale per sviluppatori hello.  
  
-   [Elenco dei prodotti](#ProductList)  
  
-   [Prodotto](#Product)  
  
> [!NOTE]
>  Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti. È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato. Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a> Elenco prodotti  
 Hello **Product list** modello consente il corpo di hello toocustomize della pagina di elenco prodotto hello nel portale per sviluppatori hello.  
  
 ![Elenco prodotti](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Modello predefinito  
  
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
  
### <a name="controls"></a>Controlli  
 Hello `Product list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Modello di dati  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Paging|Entità [Paging](api-management-template-data-model-reference.md#Paging).|Hello paging le informazioni per la raccolta di prodotti hello.|  
|Filtri|Entità [Filtri](api-management-template-data-model-reference.md#Filtering).|Hello informazioni di filtro per i prodotti hello pagina di elenco.|  
|Prodotti|Raccolta di entità [Prodotto](api-management-template-data-model-reference.md#Product).|utente corrente toohello visibile prodotti Hello.|  
  
### <a name="sample-template-data"></a>Dati del modello di esempio  
  
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
  
##  <a name="Product"></a>Prodotto  
 Hello **prodotto** modello consente il corpo di hello toocustomize della pagina del prodotto hello nel portale per sviluppatori hello.  
  
 ![Pagina prodotto nel portale per sviluppatori](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Modello predefinito  
  
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
  
### <a name="controls"></a>Controlli  
 Hello `Product list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Modello di dati  
  
|Proprietà|Tipo|Descrizione|  
|--------------|----------|-----------------|  
|Prodotto|[Prodotto](api-management-template-data-model-reference.md#Product)|prodotto specificato Hello.|  
|IsDeveloperSubscribed|boolean|Indica se l'utente corrente hello è prodotto toothis sottoscritti.|  
|SubscriptionState|number|stato di Hello della sottoscrizione hello. Gli stati possibili sono elencati di seguito:<br /><br /> -   `0 - suspended`: hello sottoscrizione è bloccata e il sottoscrittore hello non è possibile chiamare le API del prodotto hello.<br />-   `1 - active`: hello sottoscrizione è attiva.<br />-   `2 - expired`: hello ha raggiunto la data di scadenza ed è stata disattivata.<br />-   `3 - submitted`: la richiesta di sottoscrizione hello è stata effettuata dallo sviluppatore di hello, ma non è ancora stata approvata o rifiutata.<br />-   `4 - rejected`: hello sottoscrizione richiesta è stata rifiutata da un amministratore.<br />-   `5 - cancelled`-sottoscrizione hello è stata annullata dallo sviluppatore hello o un amministratore.|  
|Limiti|array|Questa proprietà è deprecata e non deve essere usata.|  
|DelegatedSubscriptionEnabled|boolean|Indica se sia abilitata la [delega](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) per questa sottoscrizione.|  
|DelegatedSubscriptionUrl|string|Se è abilitata la delega, hello delegata URL di sottoscrizione.|  
|IsAgreed|boolean|Se il prodotto hello è termini, se hello corrente utente ha accettato i termini di toohello.|  
|Sottoscrizioni|Raccolta di entità [Riepilogo della sottoscrizione](api-management-template-data-model-reference.md#SubscriptionSummary).|prodotto di toohello Hello sottoscrizioni.|  
|API|Raccolta di entità [API](api-management-template-data-model-reference.md#API).|Hello API in questo prodotto.|  
|CannotAddBecauseSubscriptionNumberLimitReached|boolean|Indica se l'utente corrente hello è toosubscribe idonei toothis prodotto con limite della sottoscrizione toohello considerare.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|boolean|Indica se l'utente corrente hello è idoneo toosubscribe toothis prodotto con sottoscrizioni toomultiple considerare consentite o non.|  
  
### <a name="sample-template-data"></a>Dati del modello di esempio  
  
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

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).
