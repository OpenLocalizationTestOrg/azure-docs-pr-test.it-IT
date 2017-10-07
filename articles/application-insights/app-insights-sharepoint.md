---
title: aaaMonitor un sito di SharePoint con Application Insights
description: Avviare il monitoraggio di una nuova applicazione con una nuova chiave di strumentazione
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="9b5f4-103">Monitorare un sito di SharePoint con Application Insights</span><span class="sxs-lookup"><span data-stu-id="9b5f4-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="9b5f4-104">Azure Application Insights consente di monitorare la disponibilità di hello, prestazioni e utilizzo delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="9b5f4-105">Questo articolo si apprenderà come tooset è per un sito di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="9b5f4-106">Creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="9b5f4-106">Create an Application Insights resource</span></span>
<span data-ttu-id="9b5f4-107">In hello [portale di Azure](https://portal.azure.com), creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="9b5f4-108">Scegliere ASP.NET come tipo di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-108">Choose ASP.NET as hello application type.</span></span>

![Fare clic su proprietà, selezionare la chiave hello e premere ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="9b5f4-110">Pannello Hello visualizzato è il luogo di hello dove verrà visualizzato i dati di utilizzo e prestazioni sull'app.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="9b5f4-111">tooit indietro tooget successivo che accesso tooAzure, è necessario trovare un riquadro per tale nella schermata iniziale di hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="9b5f4-112">In alternativa fare clic su Sfoglia toofind è.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="9b5f4-113">Aggiungere le pagine web tooyour di script</span><span class="sxs-lookup"><span data-stu-id="9b5f4-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="9b5f4-114">Durante l'avvio rapido, ottenere script hello per le pagine web:</span><span class="sxs-lookup"><span data-stu-id="9b5f4-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="9b5f4-115">Inserire uno script di hello prima hello &lt;/head&gt; tag di ogni pagina desiderata tootrack.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="9b5f4-116">Se il sito Web dispone di una pagina master, è possibile inserire script hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="9b5f4-117">Ad esempio, in un progetto ASP.NET MVC inserire lo script in View\Shared\_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="9b5f4-118">script Hello contiene una chiave di strumentazione hello che indirizza una risorsa di Application Insights tooyour telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="9b5f4-119">Aggiungere pagine del sito di hello codice tooyour</span><span class="sxs-lookup"><span data-stu-id="9b5f4-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="9b5f4-120">Nella pagina master hello</span><span class="sxs-lookup"><span data-stu-id="9b5f4-120">On hello master page</span></span>
<span data-ttu-id="9b5f4-121">Se è possibile modificare una pagina master hello del sito, che fornirà il monitoraggio per ogni pagina del sito hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="9b5f4-122">Vedere la pagina master hello e modificarlo utilizzando SharePoint Designer o un altro editor.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="9b5f4-123">Aggiungere codice hello prima hello </head> tag.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="9b5f4-124">oppure nelle singole pagine</span><span class="sxs-lookup"><span data-stu-id="9b5f4-124">Or on individual pages</span></span>
<span data-ttu-id="9b5f4-125">toomonitor un set limitato di pagine, aggiungere uno script di hello separatamente tooeach pagina.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="9b5f4-126">Inserire una web part e incorporare il frammento di codice hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="9b5f4-127">Visualizza i dati sull'app</span><span class="sxs-lookup"><span data-stu-id="9b5f4-127">View data about your app</span></span>
<span data-ttu-id="9b5f4-128">Ridistribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-128">Redeploy your app.</span></span>

<span data-ttu-id="9b5f4-129">Pannello applicazione tooyour restituito in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b5f4-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9b5f4-130">gli eventi prima di Hello vengono visualizzati nella ricerca.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="9b5f4-131">Se si prevedono più dati, fare clic su Aggiorna dopo pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="9b5f4-132">Dal pannello della panoramica hello, fare clic su **analitica utilizzo** toocharts toosee di utenti, sessioni e le visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="9b5f4-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="9b5f4-133">Fare clic su qualsiasi toosee grafico ulteriori dettagli, ad esempio le visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="9b5f4-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="9b5f4-134">Oppure gli utenti:</span><span class="sxs-lookup"><span data-stu-id="9b5f4-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="9b5f4-135">Acquisizione dell'ID utente</span><span class="sxs-lookup"><span data-stu-id="9b5f4-135">Capturing User Id</span></span>
<span data-ttu-id="9b5f4-136">frammento di codice Hello pagina web standard non acquisisce l'id utente hello da SharePoint, ma è possibile farlo con una piccola modifica.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="9b5f4-137">Copiare la chiave di strumentazione dell'applicazione hello Essentials elenco a discesa in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="9b5f4-138">Sostituire con la chiave di strumentazione hello "XXXX" nel seguente frammento di hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="9b5f4-139">Incorporare script hello nell'applicazione SharePoint anziché frammento hello che si ottiene dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="9b5f4-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b5f4-140">Next Steps</span></span>
* <span data-ttu-id="9b5f4-141">[Test Web](app-insights-monitor-web-app-availability.md) disponibilità hello toomonitor del sito.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="9b5f4-142">[Application Insights](app-insights-overview.md) per altri tipi di app.</span><span class="sxs-lookup"><span data-stu-id="9b5f4-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


