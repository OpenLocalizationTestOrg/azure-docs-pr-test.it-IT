---
title: Modelli di applicazione in Gestione API di Azure | Microsoft Docs
description: Informazioni su come personalizzare il contenuto delle pagine Applicazione nel portale per sviluppatori in Gestione API di Azure.
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
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="c67f2-103">Modelli di applicazione in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="c67f2-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="c67f2-104">In Gestione API di Azure è possibile personalizzare le pagine del portale per sviluppatori usando un set di modelli che ne configurano il contenuto.</span><span class="sxs-lookup"><span data-stu-id="c67f2-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="c67f2-105">La sintassi [DotLiquid](http://dotliquidmarkup.org/) usata insieme all'editor di propria scelta, ad esempio [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e a un set di [risorse stringa](api-management-template-resources.md#strings) localizzate, [risorse Glifo](api-management-template-resources.md#glyphs) e [controlli di pagina](api-management-page-controls.md) offre una grande flessibilità nella configurazione personalizzata del contenuto delle pagine attraverso questi modelli.</span><span class="sxs-lookup"><span data-stu-id="c67f2-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="c67f2-106">I modelli in questa sezione consentono di personalizzare il contenuto delle pagine Applicazione del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="c67f2-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="c67f2-107">Elenco applicazioni</span><span class="sxs-lookup"><span data-stu-id="c67f2-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="c67f2-108">Applicazione</span><span class="sxs-lookup"><span data-stu-id="c67f2-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="c67f2-109">La documentazione seguente include alcuni modelli predefiniti di esempio. A causa dei continui miglioramenti che vengono apportati, questi modelli sono però soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="c67f2-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="c67f2-110">È possibile visualizzare i modelli predefiniti direttamente nel portale per sviluppatori accedendo ai singoli modelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="c67f2-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="c67f2-111">Per altre informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API di Azure con i modelli](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="c67f2-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="c67f2-112"><a name="ProductList"></a> Elenco applicazioni</span><span class="sxs-lookup"><span data-stu-id="c67f2-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="c67f2-113">Il modello **Elenco applicazioni** consente di personalizzare il corpo della pagina dell'elenco delle applicazioni nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="c67f2-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="c67f2-114">![Modelli della pagina Elenco applicazioni nel portale per sviluppatori](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modelli della pagina Elenco applicazioni nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="c67f2-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c67f2-115">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="c67f2-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="c67f2-116">Controlli</span><span class="sxs-lookup"><span data-stu-id="c67f2-116">Controls</span></span>  
 <span data-ttu-id="c67f2-117">Il modello `Product list` può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="c67f2-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="c67f2-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="c67f2-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="c67f2-119">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="c67f2-119">Data model</span></span>  
  
|<span data-ttu-id="c67f2-120">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c67f2-120">Property</span></span>|<span data-ttu-id="c67f2-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="c67f2-121">Type</span></span>|<span data-ttu-id="c67f2-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c67f2-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="c67f2-123">Paging</span><span class="sxs-lookup"><span data-stu-id="c67f2-123">Paging</span></span>|<span data-ttu-id="c67f2-124">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="c67f2-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="c67f2-125">Le informazioni di paging per la raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c67f2-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="c67f2-126">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="c67f2-126">Applications</span></span>|<span data-ttu-id="c67f2-127">Raccolta di entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="c67f2-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="c67f2-128">Le applicazioni visibili all'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="c67f2-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="c67f2-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="c67f2-129">CategoryName</span></span>|<span data-ttu-id="c67f2-130">string</span><span class="sxs-lookup"><span data-stu-id="c67f2-130">string</span></span>|<span data-ttu-id="c67f2-131">La categoria dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c67f2-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="c67f2-132">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="c67f2-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="c67f2-133"><a name="Application"></a> Applicazione</span><span class="sxs-lookup"><span data-stu-id="c67f2-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="c67f2-134">Il modello **Applicazione** consente di personalizzare il corpo della pagina dell'applicazione nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="c67f2-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="c67f2-135">![Modelli della pagina Applicazione nel portale per sviluppatori](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modelli della pagina Applicazione nel portale per sviluppatori di Gestione API")</span><span class="sxs-lookup"><span data-stu-id="c67f2-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c67f2-136">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="c67f2-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="c67f2-137">Controlli</span><span class="sxs-lookup"><span data-stu-id="c67f2-137">Controls</span></span>  
 <span data-ttu-id="c67f2-138">Il modello `Application` non consente l'uso di [controlli di pagina](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c67f2-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="c67f2-139">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="c67f2-139">Data model</span></span>  
 <span data-ttu-id="c67f2-140">Entità [Applicazione](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="c67f2-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="c67f2-141">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="c67f2-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="c67f2-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c67f2-142">Next steps</span></span>
<span data-ttu-id="c67f2-143">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c67f2-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>