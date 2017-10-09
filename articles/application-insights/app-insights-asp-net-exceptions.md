---
title: aaaDiagnose errori ed eccezioni nei web App con Azure Application Insights | Documenti Microsoft
description: Acquisire le eccezioni da app ASP.NET insieme ai dati di telemetria della richiesta.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="70b5f-103">Diagnosticare eccezioni nelle app Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="70b5f-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="70b5f-104">Le eccezioni nell'applicazione Web attiva vengono segnalate da [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70b5f-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="70b5f-105">È possibile correlare le richieste non riuscite con le eccezioni e gli altri eventi di hello client e server, in modo che consente di individuare rapidamente le cause hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="70b5f-106">Configurare la creazione di report sulle eccezioni</span><span class="sxs-lookup"><span data-stu-id="70b5f-106">Set up exception reporting</span></span>
* <span data-ttu-id="70b5f-107">le eccezioni toohave segnalate dall'app server:</span><span class="sxs-lookup"><span data-stu-id="70b5f-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="70b5f-108">Installare [Application Insights SDK](app-insights-asp-net.md) nel codice dell'app, oppure</span><span class="sxs-lookup"><span data-stu-id="70b5f-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="70b5f-109">Server Web IIS: eseguire l'[Agente di Application Insights](app-insights-monitor-performance-live-website-now.md); o</span><span class="sxs-lookup"><span data-stu-id="70b5f-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="70b5f-110">App web di Azure: aggiungere hello [estensione Application Insights](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="70b5f-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="70b5f-111">Le applicazioni web Java: hello installazione [agente APM Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="70b5f-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="70b5f-112">Installare hello [frammento JavaScript](app-insights-javascript.md) in eccezioni browser toocatch pagine web.</span><span class="sxs-lookup"><span data-stu-id="70b5f-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="70b5f-113">In alcuni Framework dell'applicazione o con alcune impostazioni, è necessario tootake toocatch alcuni passaggi aggiuntivi altre eccezioni:</span><span class="sxs-lookup"><span data-stu-id="70b5f-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="70b5f-114">Web Form</span><span class="sxs-lookup"><span data-stu-id="70b5f-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="70b5f-115">MVC</span><span class="sxs-lookup"><span data-stu-id="70b5f-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="70b5f-116">API Web 1.*</span><span class="sxs-lookup"><span data-stu-id="70b5f-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="70b5f-117">API Web 2.*</span><span class="sxs-lookup"><span data-stu-id="70b5f-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="70b5f-118">WCF</span><span class="sxs-lookup"><span data-stu-id="70b5f-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="70b5f-119">Diagnosticare le eccezioni con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70b5f-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="70b5f-120">Apri soluzione dell'app hello in Visual Studio toohelp con il debug.</span><span class="sxs-lookup"><span data-stu-id="70b5f-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="70b5f-121">Eseguire app di hello, nel server o nel computer di sviluppo utilizzando F5.</span><span class="sxs-lookup"><span data-stu-id="70b5f-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="70b5f-122">Aprire una finestra di ricerca di Application Insights hello in Visual Studio e impostarlo eventi toodisplay dall'app.</span><span class="sxs-lookup"><span data-stu-id="70b5f-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="70b5f-123">Durante il debug, è possibile farlo solo facendo clic sul pulsante di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Fare clic sul progetto hello e Application Insights, scegliere Apri.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="70b5f-125">Si noti che è possibile filtrare le eccezioni di hello report tooshow solo.</span><span class="sxs-lookup"><span data-stu-id="70b5f-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="70b5f-126">*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="70b5f-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="70b5f-127">Fare clic su un tooshow report eccezione la traccia dello stack.</span><span class="sxs-lookup"><span data-stu-id="70b5f-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="70b5f-128">Fare clic su un riferimento della riga di traccia dello stack hello, file di codice pertinente tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="70b5f-129">Nel codice hello, si noti che CodeLens Mostra i dati relativi alle eccezioni di hello:</span><span class="sxs-lookup"><span data-stu-id="70b5f-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Notifica CodeLens di eccezioni.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="70b5f-131">La diagnosi di errori tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70b5f-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="70b5f-132">Panoramica di Application Insights hello dell'app, riquadro errori hello Visualizza i grafici di eccezioni e richieste HTTP non riuscite, insieme a un elenco di hello richiedere gli URL che causano errori più frequenti hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Selezionare Impostazioni, Errori.](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="70b5f-134">Fare clic su tramite uno di hello Impossibile tipi di eccezione nelle occorrenze di hello elenco tooget tooindividual di eccezione hello, in cui è possibile visualizzare i dettagli di hello e traccia dello stack:</span><span class="sxs-lookup"><span data-stu-id="70b5f-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Selezionare un'istanza di una richiesta non riuscita e con i dettagli dell'eccezione, ottenere tooinstances dell'eccezione hello.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="70b5f-136">**In alternativa,** è possibile iniziare dall'elenco di richieste a hello e trovare le eccezioni correlate tooit.</span><span class="sxs-lookup"><span data-stu-id="70b5f-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="70b5f-137">*Se non vengono visualizzate eccezioni, vedere la sezione [Acquisizione delle eccezioni](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="70b5f-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="70b5f-138">Dati di traccia e di log personalizzati</span><span class="sxs-lookup"><span data-stu-id="70b5f-138">Custom tracing and log data</span></span>
<span data-ttu-id="70b5f-139">tooget dati di diagnostica specifici tooyour app, è possibile inserire codice toosend i propri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="70b5f-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="70b5f-140">Questo nella ricerca diagnostica insieme richiesta hello, visualizzazione della pagina e altri dati raccolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="70b5f-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="70b5f-141">Sono disponibili diverse opzioni:</span><span class="sxs-lookup"><span data-stu-id="70b5f-141">You have several options:</span></span>

* <span data-ttu-id="70b5f-142">[Trackevent](app-insights-api-custom-events-metrics.md#trackevent) in genere utilizzata per il monitoraggio di modelli di utilizzo, ma hello invia anche dati viene visualizzata sotto gli eventi personalizzati nella ricerca di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="70b5f-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="70b5f-143">Gli eventi sono denominati e possono includere proprietà di stringa e metriche numeriche, in base alle quali è possibile [filtrare le ricerche diagnostiche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="70b5f-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="70b5f-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) permette di inviare dati più lunghi, ad esempio informazioni POST.</span><span class="sxs-lookup"><span data-stu-id="70b5f-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="70b5f-145">[TrackException()](#exceptions) invia analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="70b5f-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="70b5f-146">[Altre informazioni sulle eccezioni](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="70b5f-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="70b5f-147">Se si usa già un framework di registrazione come Log4Net o NLog, è possibile [acquisire tali log](app-insights-asp-net-trace-logs.md) e visualizzarli nella ricerca diagnostica insieme ai dati relativi alle richieste e alle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="70b5f-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="70b5f-148">aprire questi eventi, toosee [ricerca](app-insights-diagnostic-search.md), aprire filtro e quindi scegliere l'evento personalizzato, traccia o eccezione.</span><span class="sxs-lookup"><span data-stu-id="70b5f-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="70b5f-150">Se l'applicazione genera un grande quantità di dati di telemetria, modulo di campionamento adattivo hello ridurrà automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi.</span><span class="sxs-lookup"><span data-stu-id="70b5f-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="70b5f-151">Gli eventi che fanno parte di hello stessa operazione verrà selezionato o deselezionato come gruppo, in modo che è possibile spostarsi tra gli eventi correlati.</span><span class="sxs-lookup"><span data-stu-id="70b5f-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="70b5f-152">Informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="70b5f-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="70b5f-153">In che modo toosee richiedere dati POST</span><span class="sxs-lookup"><span data-stu-id="70b5f-153">How toosee request POST data</span></span>
<span data-ttu-id="70b5f-154">I dettagli della richiesta non includono dati di hello inviati tooyour app in una chiamata POST.</span><span class="sxs-lookup"><span data-stu-id="70b5f-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="70b5f-155">toohave segnalati da questo tipo di dati:</span><span class="sxs-lookup"><span data-stu-id="70b5f-155">toohave this data reported:</span></span>

* <span data-ttu-id="70b5f-156">[Installare SDK hello](app-insights-asp-net.md) nel progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="70b5f-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="70b5f-157">Inserire il codice in toocall l'applicazione [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="70b5f-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="70b5f-158">Inviare i dati POST hello nel parametro messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="70b5f-159">Non è un limite di dimensioni consentito toohello, è consigliabile provare dati essenziali di toosend solo hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="70b5f-160">Quando si analizza una richiesta non riuscita, è possibile trovare le tracce di hello associata.</span><span class="sxs-lookup"><span data-stu-id="70b5f-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Eseguire il drill-through](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="70b5f-162"><a name="exceptions"></a> Acquisizione delle eccezioni e dei relativi dati di diagnostica</span><span class="sxs-lookup"><span data-stu-id="70b5f-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="70b5f-163">Inizialmente, non verrà visualizzata nel portale di hello tutte le eccezioni di hello che causano errori nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="70b5f-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="70b5f-164">Si noterà che tutte le eccezioni del browser (se si usa hello [JavaScript SDK](app-insights-javascript.md) nelle pagine web).</span><span class="sxs-lookup"><span data-stu-id="70b5f-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="70b5f-165">Ma la maggior parte delle eccezioni di server vengono rilevate da IIS e si dispone di un bit di codice toosee toowrite li.</span><span class="sxs-lookup"><span data-stu-id="70b5f-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="70b5f-166">È possibile:</span><span class="sxs-lookup"><span data-stu-id="70b5f-166">You can:</span></span>

* <span data-ttu-id="70b5f-167">**Registrare le eccezioni in modo esplicito** mediante l'inserimento di codice nelle eccezioni hello tooreport gestori di eccezioni.</span><span class="sxs-lookup"><span data-stu-id="70b5f-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="70b5f-168">**Acquisire automaticamente le eccezioni** configurando il framework di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="70b5f-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="70b5f-169">indispensabile Hello sono diverse per diversi tipi di framework.</span><span class="sxs-lookup"><span data-stu-id="70b5f-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="70b5f-170">Segnalazione di eccezioni in modo esplicito</span><span class="sxs-lookup"><span data-stu-id="70b5f-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="70b5f-171">Hello più semplice è tooinsert tooTrackException() una chiamata in un gestore di eccezioni.</span><span class="sxs-lookup"><span data-stu-id="70b5f-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="70b5f-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70b5f-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="70b5f-173">C#</span><span class="sxs-lookup"><span data-stu-id="70b5f-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="70b5f-174">VB</span><span class="sxs-lookup"><span data-stu-id="70b5f-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="70b5f-175">Hello parametri di proprietà e le misure sono facoltativi, ma sono utili per [filtro e l'aggiunta di](app-insights-diagnostic-search.md) informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="70b5f-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="70b5f-176">Ad esempio, se si dispone di un'app che è possibile eseguire diversi giochi, è possibile trovare tutti hello eccezione report correlati tooa gioco.</span><span class="sxs-lookup"><span data-stu-id="70b5f-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="70b5f-177">È possibile aggiungere tutti gli elementi desiderati come dizionario tooeach.</span><span class="sxs-lookup"><span data-stu-id="70b5f-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="70b5f-178">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="70b5f-178">Browser exceptions</span></span>
<span data-ttu-id="70b5f-179">Viene segnalata la maggior parte delle eccezioni del browser.</span><span class="sxs-lookup"><span data-stu-id="70b5f-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="70b5f-180">Se la pagina web include i file di script di reti per la distribuzione del contenuto o altri domini, verificare che il tag di script con attributo hello ```crossorigin="anonymous"```, e invia tale server hello [intestazioni CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="70b5f-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="70b5f-181">In questo modo si tooget una traccia dello stack e i dettagli per le eccezioni JavaScript non gestite da queste risorse.</span><span class="sxs-lookup"><span data-stu-id="70b5f-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="70b5f-182">Web Form</span><span class="sxs-lookup"><span data-stu-id="70b5f-182">Web forms</span></span>
<span data-ttu-id="70b5f-183">Per web form, hello modulo HTTP sarà eccezioni hello in grado di toocollect quando non sono configurato con CustomErrors non effettua il reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="70b5f-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="70b5f-184">Ma se si dispone di reindirizzamenti active, aggiungere hello seguenti righe toohello Application_Error funzione Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="70b5f-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="70b5f-185">Aggiungere un file Global.asax se non ne esiste già uno.</span><span class="sxs-lookup"><span data-stu-id="70b5f-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="70b5f-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="70b5f-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="70b5f-187">MVC</span><span class="sxs-lookup"><span data-stu-id="70b5f-187">MVC</span></span>
<span data-ttu-id="70b5f-188">Se hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configurazione `Off`, quindi eccezioni risulteranno disponibili per hello [modulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="70b5f-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="70b5f-189">Tuttavia, se è `RemoteOnly` (impostazione predefinita), o `On`, verrà cancellata l'eccezione hello e raccogliere tooautomatically non disponibile per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="70b5f-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="70b5f-190">Per risolvere questo problema eseguendo l'override di hello [System.Web.Mvc.HandleErrorAttribute classe](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)e l'applicazione di classe hello sottoposto a override, come illustrato per hello MVC versioni diverse seguente ([github origine](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="70b5f-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="70b5f-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="70b5f-191">MVC 2</span></span>
<span data-ttu-id="70b5f-192">Sostituire l'attributo HandleError hello con il nuovo attributo nel controller.</span><span class="sxs-lookup"><span data-stu-id="70b5f-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="70b5f-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="70b5f-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="70b5f-194">MVC 3</span></span>
<span data-ttu-id="70b5f-195">Registrare `AiHandleErrorAttribute` come filtro globale in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="70b5f-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="70b5f-196">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="70b5f-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="70b5f-197">MVC 4, MVC5</span></span>
<span data-ttu-id="70b5f-198">Registrare AiHandleErrorAttribute come filtro globale in FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="70b5f-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="70b5f-199">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="70b5f-200">API Web 1.x</span><span class="sxs-lookup"><span data-stu-id="70b5f-200">Web API 1.x</span></span>
<span data-ttu-id="70b5f-201">Eseguire l'override di System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="70b5f-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="70b5f-202">È possibile aggiungere questo controller toospecific attributo sottoposto a override o aggiungerlo Configurazione filtro globale toohello alla classe WebApiConfig hello:</span><span class="sxs-lookup"><span data-stu-id="70b5f-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="70b5f-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="70b5f-204">Esistono un numero di case che non possono gestire i filtri eccezioni hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="70b5f-205">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="70b5f-205">For example:</span></span>

* <span data-ttu-id="70b5f-206">Eccezioni generate dai costruttori dei controller.</span><span class="sxs-lookup"><span data-stu-id="70b5f-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="70b5f-207">Eccezioni generate dai gestori di messaggi.</span><span class="sxs-lookup"><span data-stu-id="70b5f-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="70b5f-208">Eccezioni generate durante il routing.</span><span class="sxs-lookup"><span data-stu-id="70b5f-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="70b5f-209">Eccezioni generate durante la serializzazione del contenuto della risposta.</span><span class="sxs-lookup"><span data-stu-id="70b5f-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="70b5f-210">API Web 2.x</span><span class="sxs-lookup"><span data-stu-id="70b5f-210">Web API 2.x</span></span>
<span data-ttu-id="70b5f-211">Aggiungere un'implementazione di IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="70b5f-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="70b5f-212">Aggiungere questo servizi toohello WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="70b5f-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="70b5f-213">}</span><span class="sxs-lookup"><span data-stu-id="70b5f-213">}</span></span>

[<span data-ttu-id="70b5f-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="70b5f-215">In alternativa, è possibile:</span><span class="sxs-lookup"><span data-stu-id="70b5f-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="70b5f-216">Sostituire hello solo ExceptionHandler con un'implementazione personalizzata di IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="70b5f-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="70b5f-217">Viene chiamato solo quando il framework di hello è ancora in grado di toochoose la risposta del messaggio toosend (not quando connessione hello viene interrotta, ad esempio)</span><span class="sxs-lookup"><span data-stu-id="70b5f-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="70b5f-218">Filtri eccezioni (come descritto nella sezione hello sul controller 1. x API Web sopra) - non è stati chiamati in tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="70b5f-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="70b5f-219">WCF</span><span class="sxs-lookup"><span data-stu-id="70b5f-219">WCF</span></span>
<span data-ttu-id="70b5f-220">Aggiungere una classe che estenda Attribute e implementi IErrorHandler e IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="70b5f-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="70b5f-221">Aggiungere le implementazioni del servizio toohello hello attributo:</span><span class="sxs-lookup"><span data-stu-id="70b5f-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="70b5f-222">Esempio</span><span class="sxs-lookup"><span data-stu-id="70b5f-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="70b5f-223">Contatori delle prestazioni delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="70b5f-223">Exception performance counters</span></span>
<span data-ttu-id="70b5f-224">Se dispone di [installato l'agente di Application Insights hello](app-insights-monitor-performance-live-website-now.md) sul server, è possibile ottenere un grafico della frequenza di eccezioni hello, misurata da .NET.</span><span class="sxs-lookup"><span data-stu-id="70b5f-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="70b5f-225">Il grafico include le eccezioni .NET gestite e non gestite.</span><span class="sxs-lookup"><span data-stu-id="70b5f-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="70b5f-226">Aprire un pannello Esplora metrica, aggiungere un nuovo grafico e selezionare **Frequenza eccezione**, elencata sotto a Contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="70b5f-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="70b5f-227">.NET framework di Hello calcola il tasso di hello contando il numero di hello delle eccezioni in un intervallo e dividendo per lunghezza hello dell'intervallo di hello.</span><span class="sxs-lookup"><span data-stu-id="70b5f-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="70b5f-228">Si noti che questo sia diverso dal numero di eccezioni"hello" calcolato dal portale Application Insights hello contando TrackException report.</span><span class="sxs-lookup"><span data-stu-id="70b5f-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="70b5f-229">intervalli di campionamento Hello sono diversi e hello SDK non invia report a TrackException per tutte le eccezioni gestite e non gestite.</span><span class="sxs-lookup"><span data-stu-id="70b5f-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="70b5f-230">Video</span><span class="sxs-lookup"><span data-stu-id="70b5f-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="70b5f-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70b5f-231">Next steps</span></span>
* [<span data-ttu-id="70b5f-232">Monitorare REST, SQL e altre chiamate di toodependencies</span><span class="sxs-lookup"><span data-stu-id="70b5f-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="70b5f-233">Monitorare i tempi di caricamento delle pagina, le eccezioni del browser e le chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="70b5f-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="70b5f-234">Monitorare i contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="70b5f-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
