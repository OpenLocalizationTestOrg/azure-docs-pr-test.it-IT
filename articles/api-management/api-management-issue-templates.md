---
title: Modelli di pagina dei problemi in Gestione API di Azure | Documentazione Microsoft
description: Informazioni su come personalizzare il contenuto delle pagine dei problemi nel portale per sviluppatori in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="9f561-103">Modelli di pagina dei problemi in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="9f561-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="9f561-104">In Gestione API di Azure è possibile personalizzare le pagine del portale per sviluppatori usando un set di modelli che ne configurano il contenuto.</span><span class="sxs-lookup"><span data-stu-id="9f561-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9f561-105">La sintassi [DotLiquid](http://dotliquidmarkup.org/) usata insieme all'editor di propria scelta, quale [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e a un set di [risorse stringa](api-management-template-resources.md#strings), [risorse Glifo](api-management-template-resources.md#glyphs) e [controlli di pagina](api-management-page-controls.md) offre una grande flessibilità nella configurazione personalizzata del contenuto delle pagine attraverso questi modelli.</span><span class="sxs-lookup"><span data-stu-id="9f561-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9f561-106">I modelli in questa sezione consentono di personalizzare il contenuto delle pagine dei problemi del portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9f561-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="9f561-107">Elenco di problemi</span><span class="sxs-lookup"><span data-stu-id="9f561-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="9f561-108">La documentazione seguente include alcuni modelli predefiniti di esempio. A causa dei continui miglioramenti che vengono apportati, questi modelli sono però soggetti a modifiche.</span><span class="sxs-lookup"><span data-stu-id="9f561-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="9f561-109">È possibile visualizzare i modelli predefiniti direttamente nel portale per sviluppatori accedendo ai singoli modelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="9f561-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="9f561-110">Per altre informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API di Azure con i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9f561-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="9f561-111"><a name="IssueList"></a> Elenco problemi</span><span class="sxs-lookup"><span data-stu-id="9f561-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="9f561-112">Il modello **Elenco problemi** consente di personalizzare il corpo della pagina di elenco problemi nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9f561-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="9f561-113">![Elenco problemi portale per sviluppatori](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Elenco problemi APIM portale per sviluppatori")</span><span class="sxs-lookup"><span data-stu-id="9f561-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9f561-114">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="9f561-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="9f561-115">Controlli</span><span class="sxs-lookup"><span data-stu-id="9f561-115">Controls</span></span>  
 <span data-ttu-id="9f561-116">Il modello `Issue list` può usare i [controlli di pagina](api-management-page-controls.md) seguenti.</span><span class="sxs-lookup"><span data-stu-id="9f561-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9f561-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="9f561-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="9f561-118">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="9f561-118">Data model</span></span>  
  
|<span data-ttu-id="9f561-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9f561-119">Property</span></span>|<span data-ttu-id="9f561-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="9f561-120">Type</span></span>|<span data-ttu-id="9f561-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9f561-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="9f561-122">Problemi</span><span class="sxs-lookup"><span data-stu-id="9f561-122">Issues</span></span>|<span data-ttu-id="9f561-123">Raccolta di entità [Problema](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="9f561-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="9f561-124">I problemi visibili all'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="9f561-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="9f561-125">Paging</span><span class="sxs-lookup"><span data-stu-id="9f561-125">Paging</span></span>|<span data-ttu-id="9f561-126">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="9f561-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="9f561-127">Le informazioni di paging per la raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9f561-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="9f561-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="9f561-128">IsAuthenticated</span></span>|<span data-ttu-id="9f561-129">boolean</span><span class="sxs-lookup"><span data-stu-id="9f561-129">boolean</span></span>|<span data-ttu-id="9f561-130">Se l'utente corrente ha effettuato l'accesso nel portale per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="9f561-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="9f561-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="9f561-131">CanReportIssues</span></span>|<span data-ttu-id="9f561-132">boolean</span><span class="sxs-lookup"><span data-stu-id="9f561-132">boolean</span></span>|<span data-ttu-id="9f561-133">Se l'utente corrente dispone delle autorizzazioni per presentare un problema.</span><span class="sxs-lookup"><span data-stu-id="9f561-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="9f561-134">Search</span><span class="sxs-lookup"><span data-stu-id="9f561-134">Search</span></span>|<span data-ttu-id="9f561-135">string</span><span class="sxs-lookup"><span data-stu-id="9f561-135">string</span></span>|<span data-ttu-id="9f561-136">Questa proprietà è deprecata e non deve essere usata.</span><span class="sxs-lookup"><span data-stu-id="9f561-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="9f561-137">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="9f561-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="9f561-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f561-138">Next steps</span></span>
<span data-ttu-id="9f561-139">Per ulteriori informazioni sull'uso dei modelli, vedere [Come personalizzare il portale per sviluppatori di Gestione API usando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9f561-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>