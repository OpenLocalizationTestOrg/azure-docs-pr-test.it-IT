---
title: Azure Application Insights per app Web JavaScript | Microsoft Docs
description: Ottenere i conteggi delle visualizzazioni pagina e delle sessioni, i dati client Web e la traccia dei modelli di utilizzo. Rilevare le eccezioni e i problemi di prestazioni nelle pagine Web JavaScript.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="e1793-104">Application Insights per pagine Web</span><span class="sxs-lookup"><span data-stu-id="e1793-104">Application Insights for web pages</span></span>
<span data-ttu-id="e1793-105">Scoprire le prestazioni e l'utilizzo della pagina Web o dell'app.</span><span class="sxs-lookup"><span data-stu-id="e1793-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="e1793-106">Se si aggiunge [Application Insights](app-insights-overview.md) allo script di pagina, si ottengono gli intervalli di tempo di caricamento delle pagine e delle chiamate AJAX, i conteggi e i dettagli delle eccezioni del browser e degli errori AJAX, nonché i conteggi relativi a utenti e sessioni.</span><span class="sxs-lookup"><span data-stu-id="e1793-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="e1793-107">Tutti questi elementi possono essere segmentati per pagina, sistema operativo client e versione del browser, posizione geografica e altre dimensioni.</span><span class="sxs-lookup"><span data-stu-id="e1793-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="e1793-108">È possibile impostare avvisi relativi al numero di errori o rallentare il caricamento delle pagine.</span><span class="sxs-lookup"><span data-stu-id="e1793-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="e1793-109">Inoltre, inserendo le chiamate di traccia nel codice JavaScript, è possibile rilevare come vengono usate le diverse funzionalità dell'applicazione della pagina Web.</span><span class="sxs-lookup"><span data-stu-id="e1793-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="e1793-110">Application Insights è compatibile con tutte le pagine Web, con una minima aggiunta di codice JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e1793-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="e1793-111">Se il servizio Web è [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), è possibile integrare i dati di telemetria dal server e dai client.</span><span class="sxs-lookup"><span data-stu-id="e1793-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![In portal.azure.com aprire la risorsa dell'app e fare clic su Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="e1793-113">È necessaria una sottoscrizione a [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1793-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="e1793-114">Se il team ha una sottoscrizione per l'organizzazione, chiedere al proprietario di aggiungervi l'account Microsoft dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e1793-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="e1793-115">Lo sviluppo e un uso su scala ridotta sono gratuiti.</span><span class="sxs-lookup"><span data-stu-id="e1793-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="e1793-116">Installare Application Insights per la pagina Web</span><span class="sxs-lookup"><span data-stu-id="e1793-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="e1793-117">Aggiungere il frammento di codice del caricatore alle pagine Web, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e1793-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="e1793-118">Aprire o creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="e1793-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="e1793-119">La risorsa di Application Insights è dove vengono visualizzati i dati sulle prestazioni e l'utilizzo della pagina.</span><span class="sxs-lookup"><span data-stu-id="e1793-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="e1793-120">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1793-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e1793-121">Se è già stato configurato il monitoraggio per il lato server dell'app, si ha già una risorsa:</span><span class="sxs-lookup"><span data-stu-id="e1793-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Scegliere Sfoglia, quindi Servizi per gli sviluppatori, Application Insights](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="e1793-123">Se non si ha un account, crearlo:</span><span class="sxs-lookup"><span data-stu-id="e1793-123">If you don't have one, create it:</span></span>

![Scegliere Nuovo, quindi Servizi per gli sviluppatori, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="e1793-125">*Altre domande?*</span><span class="sxs-lookup"><span data-stu-id="e1793-125">*Questions already?*</span></span> <span data-ttu-id="e1793-126">[Altre informazioni sulla creazione di una risorsa](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e1793-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="e1793-127">Aggiungere lo script SDK per l'app o pagine Web</span><span class="sxs-lookup"><span data-stu-id="e1793-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="e1793-128">In Avvio rapido ottenere lo script per le pagine Web:</span><span class="sxs-lookup"><span data-stu-id="e1793-128">In Quick Start, get the script for web pages:</span></span>

![Nel pannello di panoramica delle app, scegliere Avvio rapido, quindi ottenere il codice per monitorare le pagine Web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="e1793-131">Inserire lo script poco prima del tag `</head>` di ogni pagina di cui si vuole tenere traccia. Se il sito Web presenta una pagina master, è possibile inserire lo script in tale posizione.</span><span class="sxs-lookup"><span data-stu-id="e1793-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="e1793-132">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e1793-132">For example:</span></span>

* <span data-ttu-id="e1793-133">In un progetto ASP.NET MVC inserire lo script in `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="e1793-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="e1793-134">Nel pannello di controllo di un sito di SharePoint aprire [Impostazioni sito/pagina Master](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e1793-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="e1793-135">Lo script contiene la chiave di strumentazione che indirizza i dati alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e1793-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="e1793-136">[Spiegazione più approfondita dello script](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/).</span><span class="sxs-lookup"><span data-stu-id="e1793-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="e1793-137">*(Se si usa un framework di pagine Web noto, cercare adattatori Application Insights. Ad esempio, [un modulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="e1793-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="e1793-138">Configurazione dettagliata</span><span class="sxs-lookup"><span data-stu-id="e1793-138">Detailed configuration</span></span>
<span data-ttu-id="e1793-139">Sono disponibili diversi [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) che è possibile impostare, anche se nella maggior parte dei casi non è necessario farlo.</span><span class="sxs-lookup"><span data-stu-id="e1793-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="e1793-140">È ad esempio possibile disabilitare o limitare il numero di chiamate AJAX segnalate per visualizzazione pagina allo scopo di ridurre il traffico</span><span class="sxs-lookup"><span data-stu-id="e1793-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="e1793-141">oppure impostare la modalità di debug per velocizzare lo spostamento dei dati di telemetria nella pipeline senza che vengano divisi in batch.</span><span class="sxs-lookup"><span data-stu-id="e1793-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="e1793-142">Per impostare questi parametri, cercare la riga seguente nel frammento di codice e aggiungere altri elementi delimitati da virgole dopo la riga:</span><span class="sxs-lookup"><span data-stu-id="e1793-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="e1793-143">I [parametri disponibili](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) includono:</span><span class="sxs-lookup"><span data-stu-id="e1793-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="e1793-144"><a name="run"></a>Eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="e1793-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="e1793-145">Eseguire l'app Web, usarla un periodo di tempo per generare dati di telemetria e attendere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="e1793-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="e1793-146">È possibile eseguirla premendo **F5** sul computer di sviluppo o pubblicarla e metterla a disposizione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="e1793-147">Se si desidera controllare i dati di telemetria che un'app Web sta inviando ad Application Insights, usare gli strumenti di debug del browser (**F12** in molti browser).</span><span class="sxs-lookup"><span data-stu-id="e1793-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="e1793-148">I dati vengono inviati a dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="e1793-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="e1793-149">Esplorare i dati sulle prestazioni del browser</span><span class="sxs-lookup"><span data-stu-id="e1793-149">Explore your browser performance data</span></span>
<span data-ttu-id="e1793-150">Aprire il pannello Browser per visualizzare i dati sulle prestazioni aggregati relativi ai browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![In portal.azure.com aprire la risorsa dell'app e fare clic su Impostazioni, Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="e1793-152">*Ancora nessun dato? Fare clic su **Aggiorna** nella parte superiore della pagina. Ancora niente di fatto? Vedere [Risoluzione dei problemi](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="e1793-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="e1793-153">Il pannello Browser è un [pannello di Esplora metriche](app-insights-metrics-explorer.md) con selezioni di grafici e filtri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="e1793-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="e1793-154">È possibile modificare l'intervallo di tempo, i filtri e la configurazione del grafico e salvare il risultato tra i preferiti.</span><span class="sxs-lookup"><span data-stu-id="e1793-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="e1793-155">Fare clic su **Ripristina impostazioni predefinite** per tornare alla configurazione originale del pannello.</span><span class="sxs-lookup"><span data-stu-id="e1793-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="e1793-156">Prestazioni di caricamento delle pagine</span><span class="sxs-lookup"><span data-stu-id="e1793-156">Page load performance</span></span>
<span data-ttu-id="e1793-157">Nella parte superiore è presente un grafico segmentato relativo ai tempi di caricamento delle pagine.</span><span class="sxs-lookup"><span data-stu-id="e1793-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="e1793-158">L'altezza totale del grafico rappresenta il tempo medio di caricamento e visualizzazione delle pagine dall'app nel browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="e1793-159">Il tempo viene misurato dal momento in cui il browser invia la richiesta HTTP iniziale fino al termine dell'elaborazione di tutti gli eventi di caricamento sincrono, inclusi gli script di esecuzione e layout.</span><span class="sxs-lookup"><span data-stu-id="e1793-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="e1793-160">Non sono incluse le attività asincrone, ad esempio il caricamento di Web part da chiamate AJAX.</span><span class="sxs-lookup"><span data-stu-id="e1793-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="e1793-161">Il grafico segmenta il tempo totale di caricamento delle pagine negli [intervalli di tempo standard definiti da W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="e1793-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="e1793-162">Si noti che il tempo di *connessione alla rete* è spesso inferiore al previsto, perché è una media di tutte le richieste dal browser al server.</span><span class="sxs-lookup"><span data-stu-id="e1793-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="e1793-163">Molte richieste singole hanno un tempo di connessione pari a 0 perché esiste già una connessione attiva sul server.</span><span class="sxs-lookup"><span data-stu-id="e1793-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="e1793-164">Caricamento lento</span><span class="sxs-lookup"><span data-stu-id="e1793-164">Slow loading?</span></span>
<span data-ttu-id="e1793-165">Il caricamento lento delle pagine è tra le principali cause di insoddisfazione per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="e1793-166">Se il grafico indica caricamenti lenti delle pagine, è possibile eseguire delle semplici ricerche diagnostiche.</span><span class="sxs-lookup"><span data-stu-id="e1793-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="e1793-167">Il grafico mostra la media di tutti i caricamenti di pagina nell'app.</span><span class="sxs-lookup"><span data-stu-id="e1793-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="e1793-168">Per verificare se il problema è limitato a determinate pagine, vedere la griglia segmentata in base agli URL delle pagine più in basso nel pannello:</span><span class="sxs-lookup"><span data-stu-id="e1793-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="e1793-169">Si noti il conteggio delle visualizzazioni pagina e la deviazione standard.</span><span class="sxs-lookup"><span data-stu-id="e1793-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="e1793-170">Se il conteggio delle pagine è molto basso, il problema non influisce molto sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="e1793-171">Una deviazione standard elevata, paragonabile alla media stessa, indica grandi differenze tra le singole misure.</span><span class="sxs-lookup"><span data-stu-id="e1793-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="e1793-172">**Ingrandire un URL e una visualizzazione pagina.**</span><span class="sxs-lookup"><span data-stu-id="e1793-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="e1793-173">Fare clic su un nome di pagina per visualizzare un pannello relativo ai grafici del browser filtrati in base a tale URL e quindi fare clic sull'istanza di una visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="e1793-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="e1793-174">Fare clic su `...` per un elenco completo delle proprietà dell'evento oppure controllare le chiamate AJAX e gli eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="e1793-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="e1793-175">La lentezza delle chiamate AJAX influisce sul tempo di caricamento totale delle pagine se le chiamate sono sincrone.</span><span class="sxs-lookup"><span data-stu-id="e1793-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="e1793-176">Gli eventi correlati includono le richieste server per lo stesso URL, se Application Insights è stato configurato nel server Web.</span><span class="sxs-lookup"><span data-stu-id="e1793-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="e1793-177">**Prestazioni delle pagine nel tempo.**</span><span class="sxs-lookup"><span data-stu-id="e1793-177">**Page performance over time.**</span></span> <span data-ttu-id="e1793-178">Tornare al pannello Browser e trasformare la griglia del tempo di caricamento della visualizzazione pagina in un grafico a linee per verificare se ci sono stati picchi in orari specifici:</span><span class="sxs-lookup"><span data-stu-id="e1793-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Fare clic sull'intestazione della griglia e selezionare un nuovo tipo di grafico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="e1793-180">**Segmentare in base ad altre dimensioni.**</span><span class="sxs-lookup"><span data-stu-id="e1793-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="e1793-181">Il caricamento delle pagine potrebbe risultare più lento in un determinato browser, un sistema operativo client o una località utente.</span><span class="sxs-lookup"><span data-stu-id="e1793-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="e1793-182">Aggiungere un nuovo grafico e provare la dimensione **Raggruppamento** .</span><span class="sxs-lookup"><span data-stu-id="e1793-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="e1793-183">Prestazioni AJAX</span><span class="sxs-lookup"><span data-stu-id="e1793-183">AJAX Performance</span></span>
<span data-ttu-id="e1793-184">Assicurarsi che le prestazioni di tutte le chiamate AJAX nelle pagine Web siano soddisfacenti.</span><span class="sxs-lookup"><span data-stu-id="e1793-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="e1793-185">Spesso vengono usate per riempire parti della pagina in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="e1793-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="e1793-186">Anche se la pagina in generale viene caricata tempestivamente, gli utenti potrebbero non essere soddisfatti dei tempi di caricamento e visualizzazione troppo lenti di alcune Web part.</span><span class="sxs-lookup"><span data-stu-id="e1793-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="e1793-187">Le chiamate AJAX eseguite dalla pagina Web vengono visualizzate nel pannello Browser come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e1793-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="e1793-188">Sono disponibili grafici di riepilogo nella parte superiore del pannello:</span><span class="sxs-lookup"><span data-stu-id="e1793-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="e1793-189">e griglie dettagliate più in basso:</span><span class="sxs-lookup"><span data-stu-id="e1793-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="e1793-190">Fare clic su una riga per visualizzare i dettagli specifici.</span><span class="sxs-lookup"><span data-stu-id="e1793-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="e1793-191">Se si elimina il filtro Browser nel pannello, le dipendenze AJAX e server verranno incluse entrambe in questi grafici.</span><span class="sxs-lookup"><span data-stu-id="e1793-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="e1793-192">Fare clic su Ripristina impostazioni predefinite per riconfigurare il filtro.</span><span class="sxs-lookup"><span data-stu-id="e1793-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="e1793-193">**Per esaminare le chiamate AJAX non riuscite** , scorrere verso il basso fino alla griglia degli errori di dipendenza e quindi fare clic su una riga per visualizzare le istanze specifiche.</span><span class="sxs-lookup"><span data-stu-id="e1793-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="e1793-194">Fare clic su `...` per visualizzare i dati di telemetria completi per una chiamata AJAX.</span><span class="sxs-lookup"><span data-stu-id="e1793-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="e1793-195">Nessuna chiamata AJAX segnalata</span><span class="sxs-lookup"><span data-stu-id="e1793-195">No Ajax calls reported?</span></span>
<span data-ttu-id="e1793-196">Le chiamate AJAX includono tutte le chiamate HTTP/HTTPS inviate dallo script della pagina Web.</span><span class="sxs-lookup"><span data-stu-id="e1793-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="e1793-197">Se non vengono segnalate, controllare che nel frammento di codice non siano impostati i [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` o `maxAjaxCallsPerView` .</span><span class="sxs-lookup"><span data-stu-id="e1793-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="e1793-198">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="e1793-198">Browser exceptions</span></span>
<span data-ttu-id="e1793-199">Nel pannello Browser è presente un grafico di riepilogo delle eccezioni, una griglia dei tipi di eccezione è disponibile più in basso nel pannello.</span><span class="sxs-lookup"><span data-stu-id="e1793-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="e1793-200">Se le eccezioni del browser non vengono segnalate, controllare che nel frammento di codice non sia impostato il [parametro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="e1793-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="e1793-201">Esaminare singoli eventi di visualizzazione pagina</span><span class="sxs-lookup"><span data-stu-id="e1793-201">Inspect individual page view events</span></span>

<span data-ttu-id="e1793-202">In genere la telemetria delle visualizzazioni di pagina viene analizzata da Application Insights e vengono quindi visualizzati solo i report cumulativi, mediati su tutti gli utenti del sito.</span><span class="sxs-lookup"><span data-stu-id="e1793-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="e1793-203">A scopo di debug, tuttavia, è possibile visualizzare anche singoli eventi di visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="e1793-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="e1793-204">Nella falda di ricerca diagnostica, impostare Filtri su Visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="e1793-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="e1793-205">Selezionare qualsiasi evento per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="e1793-205">Select any event to see more detail.</span></span> <span data-ttu-id="e1793-206">Nella pagina dei dettagli fare clic su "..." per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="e1793-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="e1793-207">Se si usa [Ricerca](app-insights-diagnostic-search.md), si noti che è necessaria la corrispondenza dell'intera parola: "Informaz" e "Info" non corrispondono a "Informazioni".</span><span class="sxs-lookup"><span data-stu-id="e1793-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="e1793-208">Per eseguire ricerche sulle visualizzazioni di pagina, è anche possibile usare l'avanzato [linguaggio di query di Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table).</span><span class="sxs-lookup"><span data-stu-id="e1793-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="e1793-209">Proprietà delle visualizzazioni di pagina</span><span class="sxs-lookup"><span data-stu-id="e1793-209">Page view properties</span></span>
* <span data-ttu-id="e1793-210">**Durata della visualizzazione pagina**</span><span class="sxs-lookup"><span data-stu-id="e1793-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="e1793-211">Per impostazione predefinita, indica il tempo necessario per caricare la pagina, dalla richiesta del client al caricamento completo, inclusi i file ausiliari ma escludendo le attività asincrone come le chiamate Ajax.</span><span class="sxs-lookup"><span data-stu-id="e1793-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="e1793-212">Se si imposta `overridePageViewDuration` nella [configurazione della pagina](#detailed-configuration), indica l'intervallo tra la richiesta del client e l'esecuzione del primo `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="e1793-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="e1793-213">Se si sposta trackPageView dalla posizione consueta dopo l'inizializzazione dello script, rifletterà un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="e1793-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="e1793-214">Se viene impostato il valore `overridePageViewDuration` e viene specificato un argomento Duration nella chiamata `trackPageView()`, viene usato invece il valore dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="e1793-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="e1793-215">Conteggi di pagina personalizzati</span><span class="sxs-lookup"><span data-stu-id="e1793-215">Custom page counts</span></span>
<span data-ttu-id="e1793-216">Per impostazione predefinita, viene conteggiata una pagina ogni volta che una nuova pagina viene caricata nel browser client.</span><span class="sxs-lookup"><span data-stu-id="e1793-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="e1793-217">Potrebbero tuttavia essere utile conteggiare visualizzazioni di pagina aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="e1793-217">But you might want to count additional page views.</span></span> <span data-ttu-id="e1793-218">Ad esempio, il contenuto di una pagina potrebbe essere visualizzato in schede e si desidera conteggiare una pagina quando l'utente cambia scheda</span><span class="sxs-lookup"><span data-stu-id="e1793-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="e1793-219">oppure un codice JavaScript nella pagina potrebbe caricare nuovi contenuti senza cambiare l'URL del browser.</span><span class="sxs-lookup"><span data-stu-id="e1793-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="e1793-220">Inserire una chiamata JavaScript simile a questa nel punto appropriato nel codice del client:</span><span class="sxs-lookup"><span data-stu-id="e1793-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="e1793-221">Il nome della pagina può contenere gli stessi caratteri di un URL, ma i caratteri successivi a "#" o "?" vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="e1793-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="e1793-222">Monitoraggio dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="e1793-222">Usage tracking</span></span>
<span data-ttu-id="e1793-223">Per sapere in che modo gli utenti usano l'app,</span><span class="sxs-lookup"><span data-stu-id="e1793-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="e1793-224">Informazioni sul monitoraggio dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="e1793-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="e1793-225">[Altre informazioni sull'API per gli eventi e le metriche personalizzati](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e1793-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="e1793-226"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="e1793-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="e1793-227"><a name="next"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1793-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="e1793-228">Tenere traccia dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="e1793-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="e1793-229">Metriche ed eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="e1793-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="e1793-230">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="e1793-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

