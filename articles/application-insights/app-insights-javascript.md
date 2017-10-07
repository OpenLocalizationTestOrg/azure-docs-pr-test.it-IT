---
title: le app web aaaAzure Application Insights per JavaScript | Documenti Microsoft
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
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="3281b-104">Application Insights per pagine Web</span><span class="sxs-lookup"><span data-stu-id="3281b-104">Application Insights for web pages</span></span>
<span data-ttu-id="3281b-105">Informazioni sulle prestazioni di hello e l'utilizzo di una pagina web o dell'app.</span><span class="sxs-lookup"><span data-stu-id="3281b-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="3281b-106">Se si aggiungono [Application Insights](app-insights-overview.md) tooyour lo script della pagina, si ottiene gli intervalli di tempo di caricamento pagina e le chiamate AJAX, conteggi e i dettagli delle eccezioni del browser e gli errori di AJAX, nonché gli utenti e i conteggi di sessione.</span><span class="sxs-lookup"><span data-stu-id="3281b-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="3281b-107">Tutti questi elementi possono essere segmentati per pagina, sistema operativo client e versione del browser, posizione geografica e altre dimensioni.</span><span class="sxs-lookup"><span data-stu-id="3281b-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="3281b-108">È possibile impostare avvisi relativi al numero di errori o rallentare il caricamento delle pagine.</span><span class="sxs-lookup"><span data-stu-id="3281b-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="3281b-109">E inserendo le chiamate di traccia nel codice JavaScript, è possibile monitorare le modalità di utilizzo delle diverse funzionalità di hello dell'applicazione a pagina web.</span><span class="sxs-lookup"><span data-stu-id="3281b-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="3281b-110">Application Insights è compatibile con tutte le pagine Web, con una minima aggiunta di codice JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3281b-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="3281b-111">Se il servizio Web è [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), è possibile integrare i dati di telemetria dal server e dai client.</span><span class="sxs-lookup"><span data-stu-id="3281b-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![In portal.azure.com aprire la risorsa dell'app e fare clic su Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="3281b-113">È necessaria una sottoscrizione troppo[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="3281b-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="3281b-114">Se il team dispone di una sottoscrizione azienda, chiedere hello proprietario tooadd tooit l'Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3281b-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="3281b-115">Lo sviluppo e un uso su scala ridotta sono gratuiti.</span><span class="sxs-lookup"><span data-stu-id="3281b-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="3281b-116">Installare Application Insights per la pagina Web</span><span class="sxs-lookup"><span data-stu-id="3281b-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="3281b-117">Aggiungere hello caricatore codice frammento tooyour pagine web, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3281b-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="3281b-118">Aprire o creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="3281b-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="3281b-119">Hello risorsa di Application Insights è in cui vengono visualizzati i dati sulle prestazioni e sull'utilizzo della pagina.</span><span class="sxs-lookup"><span data-stu-id="3281b-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="3281b-120">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3281b-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3281b-121">Se è già configurato il monitoraggio per il lato server hello dell'app, si dispone già di una risorsa:</span><span class="sxs-lookup"><span data-stu-id="3281b-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Scegliere Sfoglia, quindi Servizi per gli sviluppatori, Application Insights](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="3281b-123">Se non si ha un account, crearlo:</span><span class="sxs-lookup"><span data-stu-id="3281b-123">If you don't have one, create it:</span></span>

![Scegliere Nuovo, quindi Servizi per gli sviluppatori, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="3281b-125">*Altre domande?*</span><span class="sxs-lookup"><span data-stu-id="3281b-125">*Questions already?*</span></span> <span data-ttu-id="3281b-126">[Altre informazioni sulla creazione di una risorsa](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3281b-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="3281b-127">Aggiungere app tooyour di hello SDK script o pagine web</span><span class="sxs-lookup"><span data-stu-id="3281b-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="3281b-128">Durante l'avvio rapido, ottenere script hello per le pagine web:</span><span class="sxs-lookup"><span data-stu-id="3281b-128">In Quick Start, get hello script for web pages:</span></span>

![Nel pannello della panoramica app, scegliere l'avvio rapido, ottenere codice toomonitor le pagine web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="3281b-131">Inserire uno script di hello prima hello `</head>` tag di ogni pagina desiderata tootrack.</span><span class="sxs-lookup"><span data-stu-id="3281b-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="3281b-132">Se il sito Web dispone di una pagina master, è possibile inserire script hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="3281b-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="3281b-133">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3281b-133">For example:</span></span>

* <span data-ttu-id="3281b-134">In un progetto ASP.NET MVC inserire lo script in `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="3281b-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="3281b-135">In un sito di SharePoint, nel Pannello di controllo hello, aprire [Impostazioni sito o pagina Master](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3281b-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="3281b-136">script Hello contiene una chiave di strumentazione hello che indirizza una risorsa di Application Insights tooyour dati hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="3281b-137">([Script hello spiegazione più approfondita. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="3281b-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="3281b-138">*(Se si usa un framework di pagine Web noto, cercare adattatori Application Insights. Ad esempio, [un modulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="3281b-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="3281b-139">Configurazione dettagliata</span><span class="sxs-lookup"><span data-stu-id="3281b-139">Detailed configuration</span></span>
<span data-ttu-id="3281b-140">Sono disponibili diversi [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) che è possibile impostare, anche se nella maggior parte dei casi non è necessario farlo.</span><span class="sxs-lookup"><span data-stu-id="3281b-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="3281b-141">Ad esempio, è possibile disabilitare o limitare il numero di hello di chiamate Ajax segnalato per la visualizzazione di pagina (tooreduce traffico).</span><span class="sxs-lookup"><span data-stu-id="3281b-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="3281b-142">Oppure è possibile impostare spostamento di dati di telemetria toohave modalità debug rapidamente tramite la pipeline hello senza essere eseguite in batch.</span><span class="sxs-lookup"><span data-stu-id="3281b-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="3281b-143">tooset questi parametri, cercare la seguente riga nel frammento di codice hello e aggiungere più elementi separati da virgola dopo di esso:</span><span class="sxs-lookup"><span data-stu-id="3281b-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="3281b-144">Hello [parametri disponibili](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) includono:</span><span class="sxs-lookup"><span data-stu-id="3281b-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="3281b-145"><a name="run"></a>Eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="3281b-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="3281b-146">Eseguire l'app web, usare un toogenerate telemetria e attendere qualche alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="3281b-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="3281b-147">È possibile eseguire utilizzando hello **F5** chiave nel computer di sviluppo, o pubblicarla e consentire agli utenti di modificarlo nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="3281b-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="3281b-148">Se si desidera telemetria hello toocheck che un'app web stia inviando informazioni tooApplication, utilizzare gli strumenti di debug del browser (**F12** in molti browser).</span><span class="sxs-lookup"><span data-stu-id="3281b-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="3281b-149">Dati inviati toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="3281b-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="3281b-150">Esplorare i dati sulle prestazioni del browser</span><span class="sxs-lookup"><span data-stu-id="3281b-150">Explore your browser performance data</span></span>
<span data-ttu-id="3281b-151">Aprire hello Browser pannello tooshow aggregato i dati sulle prestazioni dal browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3281b-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![In portal.azure.com aprire la risorsa dell'app e fare clic su Impostazioni, Browser](./media/app-insights-javascript/03.png)

<span data-ttu-id="3281b-153">*Ancora nessun dato? Fare clic su **aggiornamento** nella parte superiore di hello della pagina hello. Ancora niente di fatto? Vedere [Risoluzione dei problemi](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="3281b-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="3281b-154">pannello Browser Hello è un [pannello Esplora metriche](app-insights-metrics-explorer.md) con filtri predefiniti e le selezioni di grafico.</span><span class="sxs-lookup"><span data-stu-id="3281b-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="3281b-155">È possibile modificare l'intervallo di tempo hello, filtri e configurazione del grafico se si desidera e salvare il risultato di hello come preferito.</span><span class="sxs-lookup"><span data-stu-id="3281b-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="3281b-156">Fare clic su **Ripristina impostazioni predefinite** configurazione di blade tooget toohello indietro originale.</span><span class="sxs-lookup"><span data-stu-id="3281b-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="3281b-157">Prestazioni di caricamento delle pagine</span><span class="sxs-lookup"><span data-stu-id="3281b-157">Page load performance</span></span>
<span data-ttu-id="3281b-158">Hello superiore è un grafico segmentato dei tempi di caricamento pagina.</span><span class="sxs-lookup"><span data-stu-id="3281b-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="3281b-159">altezza totale del Hello del grafico hello rappresenta pagine tooload e la visualizzazione del tempo medio hello dall'app nei browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3281b-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="3281b-160">tempo di Hello viene misurato dal momento browser hello invia una richiesta HTTP iniziale hello fino al carico sincrono tutti gli eventi sono stati elaborati, inclusi i layout e l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="3281b-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="3281b-161">Non sono incluse le attività asincrone, ad esempio il caricamento di Web part da chiamate AJAX.</span><span class="sxs-lookup"><span data-stu-id="3281b-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="3281b-162">grafico Hello segmenti di tempo totale di caricamento hello in hello [gli intervalli di tempo standard definiti da W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="3281b-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="3281b-163">Si noti che hello *la connessione di rete* ora è inferiore al previsto, spesso perché è una media su tutte le richieste dal server di toohello browser hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="3281b-164">Numero di richieste singoli più Connetti pari a 0 perché esiste già un server di toohello connessione attiva.</span><span class="sxs-lookup"><span data-stu-id="3281b-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="3281b-165">Caricamento lento</span><span class="sxs-lookup"><span data-stu-id="3281b-165">Slow loading?</span></span>
<span data-ttu-id="3281b-166">Il caricamento lento delle pagine è tra le principali cause di insoddisfazione per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="3281b-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="3281b-167">Se il grafico hello indica caricamento pagina lento, è facile toodo alcune ricerche di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="3281b-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="3281b-168">grafico di Hello Mostra Media hello di tutti i caricamenti di pagina nell'app.</span><span class="sxs-lookup"><span data-stu-id="3281b-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="3281b-169">toosee se il problema di hello è confinata tooparticular pagine, esaminare ulteriormente verso il basso il pannello hello, URL della pagina in cui è presente una griglia segmentata per:</span><span class="sxs-lookup"><span data-stu-id="3281b-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="3281b-170">Si noti il conteggio delle viste pagina hello e deviazione standard.</span><span class="sxs-lookup"><span data-stu-id="3281b-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="3281b-171">Se il conteggio delle pagine hello è molto basso, quindi problema hello non è interessata utenti molto.</span><span class="sxs-lookup"><span data-stu-id="3281b-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="3281b-172">La deviazione standard elevata (Media toohello confrontabili stesso) indica molte variazioni tra singole misure.</span><span class="sxs-lookup"><span data-stu-id="3281b-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="3281b-173">**Ingrandire un URL e una visualizzazione pagina.**</span><span class="sxs-lookup"><span data-stu-id="3281b-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="3281b-174">Fare clic su qualsiasi toosee nome pagina un pannello del browser grafici filtrati toothat solo URL; e quindi in un'istanza di una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="3281b-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="3281b-175">Fare clic su `...` per un elenco completo delle proprietà per tale evento, o di controllare le chiamate Ajax hello e gli eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="3281b-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="3281b-176">Chiamate Ajax lente interessano hello complessiva pagina tempo di caricamento, se sono sincroni.</span><span class="sxs-lookup"><span data-stu-id="3281b-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="3281b-177">Gli eventi sono le richieste per hello server stesso URL (se impostati Application Insights sul server web).</span><span class="sxs-lookup"><span data-stu-id="3281b-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="3281b-178">**Prestazioni delle pagine nel tempo.**</span><span class="sxs-lookup"><span data-stu-id="3281b-178">**Page performance over time.**</span></span> <span data-ttu-id="3281b-179">Tornare al pannello browser hello modificare griglia tempo di caricamento pagina visualizzazione hello in toosee di grafico a una riga se sono stati picchi in determinati momenti:</span><span class="sxs-lookup"><span data-stu-id="3281b-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Fare clic sull'intestazione della griglia hello hello e selezionare un nuovo tipo di grafico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="3281b-181">**Segmentare in base ad altre dimensioni.**</span><span class="sxs-lookup"><span data-stu-id="3281b-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="3281b-182">Forse le pagine sono più lenti tooload in una località di browser, del sistema operativo client o utente specifica?</span><span class="sxs-lookup"><span data-stu-id="3281b-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="3281b-183">Aggiungere un nuovo grafico e sperimentare hello **Group by** dimensione.</span><span class="sxs-lookup"><span data-stu-id="3281b-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="3281b-184">Prestazioni AJAX</span><span class="sxs-lookup"><span data-stu-id="3281b-184">AJAX Performance</span></span>
<span data-ttu-id="3281b-185">Assicurarsi che le prestazioni di tutte le chiamate AJAX nelle pagine Web siano soddisfacenti.</span><span class="sxs-lookup"><span data-stu-id="3281b-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="3281b-186">Sono spesso utilizzati toofill parti della pagina in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="3281b-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="3281b-187">Sebbene hello pagina generale potrebbe caricare immediatamente, agli utenti potrebbero essere frustrati dai veniva visualizzata vuota web part, in attesa di tooappear di dati in essi contenuti.</span><span class="sxs-lookup"><span data-stu-id="3281b-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="3281b-188">Chiamate AJAX dalla pagina web vengono visualizzate nel pannello browser hello con dipendenze.</span><span class="sxs-lookup"><span data-stu-id="3281b-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="3281b-189">Sono disponibili grafici di riepilogo nella parte superiore di hello del pannello hello:</span><span class="sxs-lookup"><span data-stu-id="3281b-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="3281b-190">e griglie dettagliate più in basso:</span><span class="sxs-lookup"><span data-stu-id="3281b-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="3281b-191">Fare clic su una riga per visualizzare i dettagli specifici.</span><span class="sxs-lookup"><span data-stu-id="3281b-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="3281b-192">Se si elimina filtro browser hello nel Pannello di hello, in questi grafici sono inclusi sia i server e le dipendenze AJAX.</span><span class="sxs-lookup"><span data-stu-id="3281b-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="3281b-193">Fare clic su Ripristina impostazioni predefinite tooreconfigure hello filtro.</span><span class="sxs-lookup"><span data-stu-id="3281b-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="3281b-194">**toodrill le chiamate Ajax non riuscite di** scorrere verso il basso della griglia di errori di toohello dipendenza e quindi fare clic su istanze specifiche di toosee una riga.</span><span class="sxs-lookup"><span data-stu-id="3281b-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="3281b-195">Fare clic su `...` per dati di telemetria completo hello per una chiamata Ajax.</span><span class="sxs-lookup"><span data-stu-id="3281b-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="3281b-196">Nessuna chiamata AJAX segnalata</span><span class="sxs-lookup"><span data-stu-id="3281b-196">No Ajax calls reported?</span></span>
<span data-ttu-id="3281b-197">Chiamate AJAX includono chiamate HTTP/HTTPS eseguite dallo script hello della pagina web.</span><span class="sxs-lookup"><span data-stu-id="3281b-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="3281b-198">Se non li segnalato, verificare il frammento di codice hello non imposta hello `disableAjaxTracking` o `maxAjaxCallsPerView` [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="3281b-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="3281b-199">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="3281b-199">Browser exceptions</span></span>
<span data-ttu-id="3281b-200">Nel Pannello di browser hello, non vi è un grafico di riepilogo di eccezioni e una griglia dei tipi di eccezione ulteriormente verso il basso il pannello hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="3281b-201">Se le eccezioni del browser segnalate non viene visualizzata, verificare il frammento di codice hello non impostato hello `disableExceptionTracking` [parametro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="3281b-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="3281b-202">Esaminare singoli eventi di visualizzazione pagina</span><span class="sxs-lookup"><span data-stu-id="3281b-202">Inspect individual page view events</span></span>

<span data-ttu-id="3281b-203">In genere la telemetria delle visualizzazioni di pagina viene analizzata da Application Insights e vengono quindi visualizzati solo i report cumulativi, mediati su tutti gli utenti del sito.</span><span class="sxs-lookup"><span data-stu-id="3281b-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="3281b-204">A scopo di debug, tuttavia, è possibile visualizzare anche singoli eventi di visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="3281b-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="3281b-205">Nel pannello diagnostica ricerca hello, impostare i filtri tooPage visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="3281b-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="3281b-206">Selezionare qualsiasi evento toosee maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="3281b-206">Select any event toosee more detail.</span></span> <span data-ttu-id="3281b-207">Nella pagina dettagli hello, fare clic su "…" toosee ancora più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="3281b-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="3281b-208">Se si utilizza [ricerca](app-insights-diagnostic-search.md), si noti la presenza di parole intere toomatch: "Informazioni" e "ulteriori informazioni sul" non corrispondono a "About".</span><span class="sxs-lookup"><span data-stu-id="3281b-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="3281b-209">È inoltre possibile utilizzare hello potente [il linguaggio di query Log Analitica](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch visualizzazioni di pagina.</span><span class="sxs-lookup"><span data-stu-id="3281b-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="3281b-210">Proprietà delle visualizzazioni di pagina</span><span class="sxs-lookup"><span data-stu-id="3281b-210">Page view properties</span></span>
* <span data-ttu-id="3281b-211">**Durata della visualizzazione pagina**</span><span class="sxs-lookup"><span data-stu-id="3281b-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="3281b-212">Per impostazione predefinita, hello tempo accetta tooload hello pagina, dal client richiesta toofull caricare (inclusi i file ausiliari ma escluse le attività asincrone, ad esempio le chiamate Ajax).</span><span class="sxs-lookup"><span data-stu-id="3281b-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="3281b-213">Se si imposta `overridePageViewDuration` in hello [configurazione pagina](#detailed-configuration), hello innanzitutto l'intervallo tra i client richiesta tooexecution di hello `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="3281b-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="3281b-214">Se è stato spostato trackPageView rispetto alla posizione normale dopo l'inizializzazione di hello dello script hello, riflette un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="3281b-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="3281b-215">Se `overridePageViewDuration` viene impostato e una durata viene fornito l'argomento in hello `trackPageView()` chiamare, quindi viene utilizzato il valore di argomento hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="3281b-216">Conteggi di pagina personalizzati</span><span class="sxs-lookup"><span data-stu-id="3281b-216">Custom page counts</span></span>
<span data-ttu-id="3281b-217">Per impostazione predefinita, un conteggio delle pagine si verifica ogni volta che viene caricata una nuova pagina nel browser client hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="3281b-218">Ma è possibile toocount visualizzazioni di pagina aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="3281b-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="3281b-219">Ad esempio, una pagina potrebbe visualizzare il relativo contenuto in schede e si desidera toocount una pagina quando hello utente passa da schede.</span><span class="sxs-lookup"><span data-stu-id="3281b-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="3281b-220">O codice JavaScript nella pagina hello potrebbe caricare nuovo contenuto senza modificare l'URL del browser hello.</span><span class="sxs-lookup"><span data-stu-id="3281b-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="3281b-221">Nel punto appropriato di hello nel codice client, inserire una chiamata di JavaScript simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3281b-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="3281b-222">nome della pagina Hello può contenere hello stesso caratteri sotto forma di URL, ma tutti gli elementi presenti dopo "#" o "?" viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="3281b-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="3281b-223">Monitoraggio dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="3281b-223">Usage tracking</span></span>
<span data-ttu-id="3281b-224">Desidera toofind le operazioni che gli utenti da eseguire con l'app?</span><span class="sxs-lookup"><span data-stu-id="3281b-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="3281b-225">Informazioni sul monitoraggio dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="3281b-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="3281b-226">[Altre informazioni sull'API per gli eventi e le metriche personalizzati](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3281b-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="3281b-227"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="3281b-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="3281b-228"><a name="next"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3281b-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="3281b-229">Tenere traccia dell'utilizzo</span><span class="sxs-lookup"><span data-stu-id="3281b-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="3281b-230">Metriche ed eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="3281b-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="3281b-231">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="3281b-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

