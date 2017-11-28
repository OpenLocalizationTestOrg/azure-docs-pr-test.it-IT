---
title: modelli aaaIssue in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocustomize hello contenuto delle pagine di problema hello nel portale per sviluppatori hello in Gestione API di Azure.
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="9b8f5-103">Modelli di pagina dei problemi in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="9b8f5-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="9b8f5-104">Gestione API di Azure fornisce che si hello contenuto hello toocustomize di possibilità di pagine del portale per sviluppatori tramite un set di modelli che consentono di configurare i propri contenuti.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="9b8f5-105">Utilizzando [DotLiquid](http://dotliquidmarkup.org/) sintassi e hello editor di propria scelta, ad esempio [DotLiquid per i progettisti](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), e un set specificato di localizzato [risorse di stringa](api-management-template-resources.md#strings), [ Risorse glifo](api-management-template-resources.md#glyphs), e [pagina controlli](api-management-page-controls.md), una grande flessibilità tooconfigure hello alcuni contenuti sono di pagine hello secondo necessità utilizzando questi modelli.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="9b8f5-106">i modelli di Hello in questa sezione consentono di contenuto hello toocustomize pagine di un problema di hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="9b8f5-107">Elenco di problemi</span><span class="sxs-lookup"><span data-stu-id="9b8f5-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="9b8f5-108">Modelli predefiniti di esempio sono inclusi in hello seguente documentazione, ma sono soggetto toochange scadenza toocontinuous miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="9b8f5-109">È possibile visualizzare i modelli predefiniti in tempo reale di hello nel portale per sviluppatori di hello passando singoli modelli toohello desiderato.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="9b8f5-110">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b8f5-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="9b8f5-111"><a name="IssueList"></a> Elenco problemi</span><span class="sxs-lookup"><span data-stu-id="9b8f5-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="9b8f5-112">Hello **elenco di problemi di** modello consente il corpo di hello toocustomize della pagina di elenco problema hello nel portale per sviluppatori hello.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="9b8f5-113">![Elenco problemi portale per sviluppatori](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Elenco problemi APIM portale per sviluppatori")</span><span class="sxs-lookup"><span data-stu-id="9b8f5-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="9b8f5-114">Modello predefinito</span><span class="sxs-lookup"><span data-stu-id="9b8f5-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="9b8f5-115">Controlli</span><span class="sxs-lookup"><span data-stu-id="9b8f5-115">Controls</span></span>  
 <span data-ttu-id="9b8f5-116">Hello `Issue list` modello può utilizzare l'esempio hello [pagina controlli](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="9b8f5-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="9b8f5-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="9b8f5-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="9b8f5-118">Modello di dati</span><span class="sxs-lookup"><span data-stu-id="9b8f5-118">Data model</span></span>  
  
|<span data-ttu-id="9b8f5-119">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9b8f5-119">Property</span></span>|<span data-ttu-id="9b8f5-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="9b8f5-120">Type</span></span>|<span data-ttu-id="9b8f5-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9b8f5-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="9b8f5-122">Problemi</span><span class="sxs-lookup"><span data-stu-id="9b8f5-122">Issues</span></span>|<span data-ttu-id="9b8f5-123">Raccolta di entità [Problema](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="9b8f5-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="9b8f5-124">utente corrente toohello visibile problemi Hello.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="9b8f5-125">Paging</span><span class="sxs-lookup"><span data-stu-id="9b8f5-125">Paging</span></span>|<span data-ttu-id="9b8f5-126">Entità [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="9b8f5-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="9b8f5-127">Hello paging le informazioni per la raccolta di applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="9b8f5-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="9b8f5-128">IsAuthenticated</span></span>|<span data-ttu-id="9b8f5-129">boolean</span><span class="sxs-lookup"><span data-stu-id="9b8f5-129">boolean</span></span>|<span data-ttu-id="9b8f5-130">Indica se l'utente corrente hello è portale per sviluppatori toohello connesso.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="9b8f5-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="9b8f5-131">CanReportIssues</span></span>|<span data-ttu-id="9b8f5-132">boolean</span><span class="sxs-lookup"><span data-stu-id="9b8f5-132">boolean</span></span>|<span data-ttu-id="9b8f5-133">Se hello corrente utente dispone delle autorizzazioni toofile un problema.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="9b8f5-134">Ricerca</span><span class="sxs-lookup"><span data-stu-id="9b8f5-134">Search</span></span>|<span data-ttu-id="9b8f5-135">string</span><span class="sxs-lookup"><span data-stu-id="9b8f5-135">string</span></span>|<span data-ttu-id="9b8f5-136">Questa proprietà è deprecata e non deve essere usata.</span><span class="sxs-lookup"><span data-stu-id="9b8f5-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="9b8f5-137">Dati del modello di esempio</span><span class="sxs-lookup"><span data-stu-id="9b8f5-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="9b8f5-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b8f5-138">Next steps</span></span>
<span data-ttu-id="9b8f5-139">Per ulteriori informazioni sull'utilizzo dei modelli, vedere [come toocustomize hello portale di gestione API per gli sviluppatori utilizzando i modelli](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b8f5-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
