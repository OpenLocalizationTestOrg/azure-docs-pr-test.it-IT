---
title: modelli aaaApplication in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocustomize hello contenuto delle pagine di applicazione hello nel portale per sviluppatori hello in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="d3a8a-103">Modelli di applicazione in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="d3a8a-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="d3a8a-104">Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="d3a8a-105">Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="d3a8a-106">i modelli di Hello in questa sezione consentono di contenuto di hello toocustomize di pagine dell'applicazione hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="d3a8a-107">Elenco applicazioni</span><span class="sxs-lookup"><span data-stu-id="d3a8a-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="d3a8a-108">Applicazione</span><span class="sxs-lookup"><span data-stu-id="d3a8a-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="d3a8a-109">Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="d3a8a-110">È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="d3a8a-111">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="d3a8a-112"><a name="ProductList"></a> Elenco applicazioni</span><span class="sxs-lookup"><span data-stu-id="d3a8a-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="d3a8a-113">Hello **elenco di applicazioni** modello consente il corpo di hello toocustomize della pagina di elenco dell'applicazione hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d3a8a-114">![Modelli della pagina Elenco applicazioni nel portale per sviluppatori](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modelli della pagina Elenco applicazioni APIM nel portale per sviluppatori")</span><span class="sxs-lookup"><span data-stu-id="d3a8a-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d3a8a-115">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="d3a8a-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
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
  
### <a name="controls"></a><span data-ttu-id="d3a8a-116">Controlli</span><span class="sxs-lookup"><span data-stu-id="d3a8a-116">Controls</span></span>  
 <span data-ttu-id="d3a8a-117">Hello `Product list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d3a8a-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="d3a8a-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="d3a8a-119">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="d3a8a-119">Data model</span></span>  
  
|<span data-ttu-id="d3a8a-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d3a8a-120">Property</span></span>|<span data-ttu-id="d3a8a-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="d3a8a-121">Type</span></span>|<span data-ttu-id="d3a8a-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d3a8a-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d3a8a-123">Paging</span><span class="sxs-lookup"><span data-stu-id="d3a8a-123">Paging</span></span>|<span data-ttu-id="d3a8a-124">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="d3a8a-125">Hello paging le informazioni per la raccolta di applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="d3a8a-126">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="d3a8a-126">Applications</span></span>|<span data-ttu-id="d3a8a-127">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d3a8a-128">utente corrente toohello visibile applicazioni Hello.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="d3a8a-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="d3a8a-129">CategoryName</span></span>|<span data-ttu-id="d3a8a-130">string</span><span class="sxs-lookup"><span data-stu-id="d3a8a-130">string</span></span>|<span data-ttu-id="d3a8a-131">categoria di Hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d3a8a-132">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="d3a8a-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="d3a8a-133"><a name="Application"></a> Applicazione</span><span class="sxs-lookup"><span data-stu-id="d3a8a-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="d3a8a-134">Hello **applicazione** modello consente il corpo di hello toocustomize della pagina dell'applicazione hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="d3a8a-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d3a8a-135">![Modelli della pagina Applicazione nel portale per sviluppatori](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modelli della pagina Applicazione APIM nel portale per sviluppatori")</span><span class="sxs-lookup"><span data-stu-id="d3a8a-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d3a8a-136">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="d3a8a-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="d3a8a-137">Controlli</span><span class="sxs-lookup"><span data-stu-id="d3a8a-137">Controls</span></span>  
 <span data-ttu-id="d3a8a-138">Hello `Application` modello non consente l'uso di hello di qualsiasi [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d3a8a-139">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="d3a8a-139">Data model</span></span>  
 <span data-ttu-id="d3a8a-140">Entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d3a8a-141">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="d3a8a-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="d3a8a-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3a8a-142">Next steps</span></span>
<span data-ttu-id="d3a8a-143">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d3a8a-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
