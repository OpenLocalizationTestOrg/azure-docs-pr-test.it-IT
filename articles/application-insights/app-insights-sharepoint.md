---
title: Monitorare un sito di SharePoint con Application Insights
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
ms.openlocfilehash: a3b37674469a131016f46af590e1eee3ba4cdc73
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="82d17-103">Monitorare un sito di SharePoint con Application Insights</span><span class="sxs-lookup"><span data-stu-id="82d17-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="82d17-104">Azure Application Insights consente di monitorare disponibilità, prestazioni e utilizzo delle app.</span><span class="sxs-lookup"><span data-stu-id="82d17-104">Azure Application Insights monitors the availability, performance and usage of your apps.</span></span> <span data-ttu-id="82d17-105">Di seguito verrà illustrato come impostarlo per un sito di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82d17-105">Here you'll learn how to set it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="82d17-106">Creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="82d17-106">Create an Application Insights resource</span></span>
<span data-ttu-id="82d17-107">Nel [portale di Azure](https://portal.azure.com)creare una nuova risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="82d17-107">In the [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="82d17-108">Scegliere ASP.NET come tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="82d17-108">Choose ASP.NET as the application type.</span></span>

![Fare clic su Proprietà, selezionare il tasto e premere CTRL+C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="82d17-110">Viene visualizzato un pannello che mostra le prestazioni e i dati di utilizzo relativi all'app.</span><span class="sxs-lookup"><span data-stu-id="82d17-110">The blade that opens is the place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="82d17-111">Per visualizzare di nuovo questo pannello al successivo accesso ad Azure, nella schermata Start dovrebbe venire visualizzato un riquadro per l'app.</span><span class="sxs-lookup"><span data-stu-id="82d17-111">To get back to it next time you login to Azure, you should find a tile for it on the start screen.</span></span> <span data-ttu-id="82d17-112">In alternativa, fare clic su Sfoglia per cercarla.</span><span class="sxs-lookup"><span data-stu-id="82d17-112">Alternatively click Browse to find it.</span></span>

## <a name="add-our-script-to-your-web-pages"></a><span data-ttu-id="82d17-113">Aggiungere lo script alle pagine Web</span><span class="sxs-lookup"><span data-stu-id="82d17-113">Add our script to your web pages</span></span>
<span data-ttu-id="82d17-114">In Avvio rapido ottenere lo script per le pagine Web:</span><span class="sxs-lookup"><span data-stu-id="82d17-114">In Quick Start, get the script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="82d17-115">Inserire lo script immediatamente prima del tag &lt;/head&gt; di ogni pagina di cui si vuole tenere traccia. Se il sito Web presenta una pagina master, è possibile inserire lo script in tale posizione.</span><span class="sxs-lookup"><span data-stu-id="82d17-115">Insert the script just before the &lt;/head&gt; tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="82d17-116">Ad esempio, in un progetto ASP.NET MVC inserire lo script in View\Shared\_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="82d17-116">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="82d17-117">Lo script contiene la chiave di strumentazione che indirizza i dati di telemetria alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="82d17-117">The script contains the instrumentation key that directs the telemetry to your Application Insights resource.</span></span>

### <a name="add-the-code-to-your-site-pages"></a><span data-ttu-id="82d17-118">Aggiungere il codice alle pagine del sito</span><span class="sxs-lookup"><span data-stu-id="82d17-118">Add the code to your site pages</span></span>
#### <a name="on-the-master-page"></a><span data-ttu-id="82d17-119">Nella pagina master</span><span class="sxs-lookup"><span data-stu-id="82d17-119">On the master page</span></span>
<span data-ttu-id="82d17-120">Se è possibile modificare la pagina master del sito, che fornisce il monitoraggio per ogni pagina del sito.</span><span class="sxs-lookup"><span data-stu-id="82d17-120">If you can edit the site's master page, that will provide monitoring for every page in the site.</span></span>

<span data-ttu-id="82d17-121">Consultare la pagina master e modificarla mediante SharePoint Designer o un altro editor.</span><span class="sxs-lookup"><span data-stu-id="82d17-121">Check out the master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="82d17-122">Aggiungere il codice appena prima del tag </head> .</span><span class="sxs-lookup"><span data-stu-id="82d17-122">Add the code just before the </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="82d17-123">oppure nelle singole pagine</span><span class="sxs-lookup"><span data-stu-id="82d17-123">Or on individual pages</span></span>
<span data-ttu-id="82d17-124">Per monitorare un set limitato di pagine, aggiungere lo script separatamente a ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="82d17-124">To monitor a limited set of pages, add the script separately to each page.</span></span> 

<span data-ttu-id="82d17-125">Inserire una Web part e incorporarvi il frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="82d17-125">Insert a web part and embed the code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="82d17-126">Visualizza i dati sull'app</span><span class="sxs-lookup"><span data-stu-id="82d17-126">View data about your app</span></span>
<span data-ttu-id="82d17-127">Ridistribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="82d17-127">Redeploy your app.</span></span>

<span data-ttu-id="82d17-128">Tornare al pannello dell'applicazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82d17-128">Return to your application blade in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="82d17-129">I primi eventi verranno visualizzati nella ricerca.</span><span class="sxs-lookup"><span data-stu-id="82d17-129">The first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="82d17-130">Se si prevedono più dati, fare clic su Aggiorna dopo pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="82d17-130">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="82d17-131">Dal pannello Panoramica fare clic su **Analisi di utilizzo** per vedere i grafici di utenti, sessioni e visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="82d17-131">From the overview blade, click **Usage analytics** to see to charts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="82d17-132">Fare clic su qualsiasi grafico per vedere maggiori dettagli, ad esempio le visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="82d17-132">Click any chart to see more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="82d17-133">Oppure gli utenti:</span><span class="sxs-lookup"><span data-stu-id="82d17-133">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="82d17-134">Acquisizione dell'ID utente</span><span class="sxs-lookup"><span data-stu-id="82d17-134">Capturing User Id</span></span>
<span data-ttu-id="82d17-135">Il frammento di codice della pagina Web standard non acquisisce l'ID utente da SharePoint. Per l'acquisizione è necessario eseguire una piccola modifica.</span><span class="sxs-lookup"><span data-stu-id="82d17-135">The standard web page code snippet doesn't capture the user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="82d17-136">Copiare la chiave di strumentazione dell'app dall'elenco a discesa Informazioni di base in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="82d17-136">Copy your app's instrumentation key from the Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="82d17-137">Sostituire la chiave di strumentazione per "XXXX" nel frammento di codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="82d17-137">Substitute the instrumentation key for 'XXXX' in the snippet below.</span></span> 
2. <span data-ttu-id="82d17-138">Incorporare lo script nell'app di SharePoint anziché il frammento di codice ottenuto dal portale.</span><span class="sxs-lookup"><span data-stu-id="82d17-138">Embed the script in your SharePoint app instead of the snippet you get from the portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="82d17-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82d17-139">Next Steps</span></span>
* <span data-ttu-id="82d17-140">[Test web](app-insights-monitor-web-app-availability.md) per monitorare la disponibilità del sito.</span><span class="sxs-lookup"><span data-stu-id="82d17-140">[Web tests](app-insights-monitor-web-app-availability.md) to monitor the availability of your site.</span></span>
* <span data-ttu-id="82d17-141">[Application Insights](app-insights-overview.md) per altri tipi di app.</span><span class="sxs-lookup"><span data-stu-id="82d17-141">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


