---
title: aaaApplication Insights API per gli eventi personalizzati e le metriche | Documenti Microsoft
description: Inserire alcune righe di codice in uso tootrack dispositivo o app desktop, pagina Web o servizio e diagnosticare i problemi.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="765f6-103">API di Application Insights per metriche ed eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="765f6-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="765f6-104">Inserire alcune righe di codice in toofind l'applicazione out operazioni con gli utenti o toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="765f6-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="765f6-105">È possibile inviare i dati di telemetria dalle app desktop e per dispositivi, dai client Web e dai server Web.</span><span class="sxs-lookup"><span data-stu-id="765f6-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="765f6-106">Hello utilizzare [Azure Application Insights](app-insights-overview.md) principali di eventi di telemetria API toosend personalizzati e le metriche e le versioni personalizzate di telemetria standard.</span><span class="sxs-lookup"><span data-stu-id="765f6-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="765f6-107">Questa API è hello stessa API standard di hello usare agenti di raccolta dati Application Insights.</span><span class="sxs-lookup"><span data-stu-id="765f6-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="765f6-108">Riepilogo dell'API</span><span class="sxs-lookup"><span data-stu-id="765f6-108">API summary</span></span>
<span data-ttu-id="765f6-109">API Hello è uniforme in tutte le piattaforme, a parte alcune piccole variazioni.</span><span class="sxs-lookup"><span data-stu-id="765f6-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="765f6-110">Metodo</span><span class="sxs-lookup"><span data-stu-id="765f6-110">Method</span></span> | <span data-ttu-id="765f6-111">Usato per</span><span class="sxs-lookup"><span data-stu-id="765f6-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="765f6-112">Pagine, schermate, pannelli o form.</span><span class="sxs-lookup"><span data-stu-id="765f6-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="765f6-113">Azioni dell'utente e altri eventi.</span><span class="sxs-lookup"><span data-stu-id="765f6-113">User actions and other events.</span></span> <span data-ttu-id="765f6-114">Utilizzato tootrack utente toomonitor o il comportamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="765f6-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="765f6-115">Misurazioni delle prestazioni, ad esempio lunghezza della coda di eventi di toospecific non correlati.</span><span class="sxs-lookup"><span data-stu-id="765f6-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="765f6-116">Registrare le eccezioni per la diagnosi.</span><span class="sxs-lookup"><span data-stu-id="765f6-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="765f6-117">Traccia in cui si verificano eventi tooother relazione e come esaminare le tracce dello stack.</span><span class="sxs-lookup"><span data-stu-id="765f6-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="765f6-118">Registrazione hello frequenza e durata delle richieste del server per l'analisi delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="765f6-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="765f6-119">Messaggi nei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="765f6-119">Diagnostic log messages.</span></span> <span data-ttu-id="765f6-120">È anche possibile acquisire log di terze parti.</span><span class="sxs-lookup"><span data-stu-id="765f6-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="765f6-121">La registrazione hello durata e frequenza dei componenti tooexternal chiamate che l'applicazione dipende.</span><span class="sxs-lookup"><span data-stu-id="765f6-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="765f6-122">È possibile [associare proprietà e le metriche](#properties) toomost di queste chiamate di telemetria.</span><span class="sxs-lookup"><span data-stu-id="765f6-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="765f6-123"><a name="prep"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="765f6-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="765f6-124">Se non si ha ancora un riferimento in Application Insights SDK:</span><span class="sxs-lookup"><span data-stu-id="765f6-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="765f6-125">Aggiungere hello Application Insights SDK tooyour progetto:</span><span class="sxs-lookup"><span data-stu-id="765f6-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="765f6-126">Progetto ASP.NET</span><span class="sxs-lookup"><span data-stu-id="765f6-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="765f6-127">Progetto Java</span><span class="sxs-lookup"><span data-stu-id="765f6-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="765f6-128">JavaScript in ogni pagina Web</span><span class="sxs-lookup"><span data-stu-id="765f6-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="765f6-129">Nel dispositivo o nel codice del server Web includere:</span><span class="sxs-lookup"><span data-stu-id="765f6-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="765f6-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="765f6-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="765f6-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="765f6-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="765f6-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="765f6-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="765f6-133">Costruzione di un'istanza di TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="765f6-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="765f6-134">Costruire un'istanza di `TelemetryClient` (tranne che in JavaScript nelle pagine Web):</span><span class="sxs-lookup"><span data-stu-id="765f6-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="765f6-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="765f6-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="765f6-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="765f6-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="765f6-138">TelemetryClient è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="765f6-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="765f6-139">È consigliabile usare un'istanza di TelemetryClient per ogni modulo dell'app.</span><span class="sxs-lookup"><span data-stu-id="765f6-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="765f6-140">Ad esempio, potrebbe essere un'istanza di TelemetryClient il web tooreport richieste HTTP in arrivo e un altro in un middleware classe tooreport business logica gli eventi.</span><span class="sxs-lookup"><span data-stu-id="765f6-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="765f6-141">È possibile impostare proprietà, ad esempio `TelemetryClient.Context.User.Id` tootrack utenti e sessioni, o `TelemetryClient.Context.Device.Id` macchina hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="765f6-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="765f6-142">Queste informazioni sono hello istanza invia gli eventi tooall associata.</span><span class="sxs-lookup"><span data-stu-id="765f6-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="765f6-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="765f6-143">TrackEvent</span></span>
<span data-ttu-id="765f6-144">In Application Insights un *evento personalizzato* è un punto dati che è possibile visualizzare in [Esplora metriche](app-insights-metrics-explorer.md) come conteggio aggregato e in [Ricerca diagnostica](app-insights-diagnostic-search.md) come singole occorrenze.</span><span class="sxs-lookup"><span data-stu-id="765f6-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="765f6-145">(Se non è correlato tooMVC o altri framework "eventi.")</span><span class="sxs-lookup"><span data-stu-id="765f6-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="765f6-146">Inserisci `TrackEvent` chiama il codice toocount vari eventi.</span><span class="sxs-lookup"><span data-stu-id="765f6-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="765f6-147">La frequenza d'uso di una particolare funzionalità, la frequenza di raggiungimento di obiettivi specifici o la frequenza di particolari tipi di errore.</span><span class="sxs-lookup"><span data-stu-id="765f6-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="765f6-148">Ad esempio, in un'app di gioco, inviare un evento ogni volta che un utente wins gioco hello:</span><span class="sxs-lookup"><span data-stu-id="765f6-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="765f6-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="765f6-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="765f6-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="765f6-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="765f6-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="765f6-153">Visualizzare gli eventi nel portale di Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="765f6-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="765f6-154">toosee un conteggio degli eventi, aprire un [Esplora metriche](app-insights-metrics-explorer.md) pannello, aggiungere un nuovo grafico e selezionare **eventi**.</span><span class="sxs-lookup"><span data-stu-id="765f6-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Visualizzare il conteggio degli eventi personalizzati](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="765f6-156">conteggi di hello toocompare di eventi differenti, impostare il tipo di grafico hello troppo**griglia**e di gruppo in base al nome evento:</span><span class="sxs-lookup"><span data-stu-id="765f6-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Impostare il tipo di grafico hello e raggruppamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="765f6-158">Nella griglia di hello, fare clic su tramite un evento nome toosee singole occorrenze di tale evento.</span><span class="sxs-lookup"><span data-stu-id="765f6-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="765f6-159">toosee ulteriori dettagli, fare clic su qualsiasi occorrenza nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-159">toosee more detail - click any occurrence in hello list.</span></span>

![Drill-through eventi hello](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="765f6-161">toofocus su eventi specifici per ricerche o Esplora metriche, filtro toohello i nomi degli eventi del set hello pannello che si è interessati:</span><span class="sxs-lookup"><span data-stu-id="765f6-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Aprire i filtri, espandere il nome dell’evento e selezionare uno o più valori](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="765f6-163">Eventi personalizzati in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-163">Custom events in Analytics</span></span>

<span data-ttu-id="765f6-164">dati di telemetria Hello è disponibile in hello `customEvents` tabella [Application Insights Analitica](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="765f6-165">Ogni riga rappresenta una chiamata troppo`trackEvent(..)` nell'app.</span><span class="sxs-lookup"><span data-stu-id="765f6-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="765f6-166">Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="765f6-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="765f6-167">Per esempio itemCount = = 10 significa che di 10 chiamate tootrackEvent(), il processo di campionamento hello trasmesso solo uno di essi.</span><span class="sxs-lookup"><span data-stu-id="765f6-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="765f6-168">tooget un conteggio corretto di eventi personalizzati, è necessario utilizzare pertanto il codice, ad esempio `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="765f6-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="765f6-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="765f6-169">TrackMetric</span></span>

<span data-ttu-id="765f6-170">Application Insights può grafico delle metriche che non sono collegati tooparticular eventi.</span><span class="sxs-lookup"><span data-stu-id="765f6-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="765f6-171">Ad esempio, è possibile monitorare la lunghezza di una coda a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="765f6-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="765f6-172">Con le metriche, corrisponderanno hello è meno interessanti di varianti hello e le tendenze e pertanto statistici grafici sono utili.</span><span class="sxs-lookup"><span data-stu-id="765f6-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="765f6-173">In ordine metriche toosend tooApplication Insights, è possibile usare hello `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="765f6-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="765f6-174">Esistono due modi toosend una metrica:</span><span class="sxs-lookup"><span data-stu-id="765f6-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="765f6-175">Valore singolo.</span><span class="sxs-lookup"><span data-stu-id="765f6-175">Single value.</span></span> <span data-ttu-id="765f6-176">Ogni volta che si esegue una misurazione nell'applicazione, inviare il valore corrispondente hello tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="765f6-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="765f6-177">Ad esempio, si supponga di disporre di una metrica che descrive il numero di hello di elementi in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="765f6-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="765f6-178">Durante un periodo di tempo specifico, inserire innanzitutto tre elementi contenitore hello e quindi si rimuove due elementi.</span><span class="sxs-lookup"><span data-stu-id="765f6-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="765f6-179">Di conseguenza, è necessario chiamare `TrackMetric` due volte: prima di tutto se si passa il valore di hello `3` e quindi hello valore `-2`.</span><span class="sxs-lookup"><span data-stu-id="765f6-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="765f6-180">Application Insights memorizza entrambi i valori per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="765f6-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="765f6-181">Aggregazione.</span><span class="sxs-lookup"><span data-stu-id="765f6-181">Aggregation.</span></span> <span data-ttu-id="765f6-182">Quando si usano le metriche non si considera mai una sola misura.</span><span class="sxs-lookup"><span data-stu-id="765f6-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="765f6-183">È importante invece il riepilogo delle operazioni eseguite in un periodo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="765f6-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="765f6-184">Tale riepilogo viene chiamato _aggregazione_.</span><span class="sxs-lookup"><span data-stu-id="765f6-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="765f6-185">In hello sopra riportato, hello aggregazione Somma di metrica per quel periodo di tempo è `1` e conteggio hello di valori della metrica hello è `2`.</span><span class="sxs-lookup"><span data-stu-id="765f6-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="765f6-186">Quando si utilizza l'approccio di aggregazione hello, richiamare solo `TrackMetric` una volta ogni ora periodo e trasmissione hello valori aggregati.</span><span class="sxs-lookup"><span data-stu-id="765f6-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="765f6-187">Si tratta di hello approccio consigliato poiché può ridurre notevolmente il costo di hello e prestazioni overhead inviando i dati meno punti Insights tooApplication, durante la raccolta ancora tutte le informazioni pertinenti.</span><span class="sxs-lookup"><span data-stu-id="765f6-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="765f6-188">Esempi:</span><span class="sxs-lookup"><span data-stu-id="765f6-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="765f6-189">Valori singoli</span><span class="sxs-lookup"><span data-stu-id="765f6-189">Single values</span></span>

<span data-ttu-id="765f6-190">toosend un singolo valore di metrica:</span><span class="sxs-lookup"><span data-stu-id="765f6-190">toosend a single metric value:</span></span>

<span data-ttu-id="765f6-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="765f6-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="765f6-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="765f6-193">Aggregazione delle metriche</span><span class="sxs-lookup"><span data-stu-id="765f6-193">Aggregating metrics</span></span>

<span data-ttu-id="765f6-194">È consigliabile prima di inviarli dall'app, tooreduce della larghezza di banda, le prestazioni di costo e tooimprove tooaggregate metriche.</span><span class="sxs-lookup"><span data-stu-id="765f6-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="765f6-195">Di seguito è riportato un esempio di codice di aggregazione:</span><span class="sxs-lookup"><span data-stu-id="765f6-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="765f6-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="765f6-197">Metriche personalizzate in Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="765f6-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="765f6-198">risultati di hello toosee, aprire Esplora metriche e aggiungere un nuovo grafico.</span><span class="sxs-lookup"><span data-stu-id="765f6-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="765f6-199">Modificare hello grafico tooshow l'unità di misura.</span><span class="sxs-lookup"><span data-stu-id="765f6-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="765f6-200">La metrica personalizzata potrebbe richiedere diversi minuti tooappear nell'elenco di hello delle metriche disponibili.</span><span class="sxs-lookup"><span data-stu-id="765f6-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Aggiungere un nuovo grafico o selezionare un grafico e selezionare le metriche in Personalizzato](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="765f6-202">Metriche personalizzate in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="765f6-203">dati di telemetria Hello è disponibile in hello `customMetrics` tabella [Application Insights Analitica](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="765f6-204">Ogni riga rappresenta una chiamata troppo`trackMetric(..)` nell'app.</span><span class="sxs-lookup"><span data-stu-id="765f6-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="765f6-205">`valueSum`-Indica la somma di hello di misurazioni hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="765f6-206">valore medio tooget hello, divisione per `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="765f6-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="765f6-207">`valueCount`-numero di misure che sono stati aggregati in questo hello `trackMetric(..)` chiamare.</span><span class="sxs-lookup"><span data-stu-id="765f6-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="765f6-208">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="765f6-208">Page views</span></span>
<span data-ttu-id="765f6-209">In un'app per dispositivo o pagine Web i dati di telemetria delle visualizzazioni pagina vengono inviati per impostazione predefinita quando viene caricata ogni schermata o pagina.</span><span class="sxs-lookup"><span data-stu-id="765f6-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="765f6-210">Ma è possibile modificare tale viste pagina tootrack in momenti aggiuntive o diverse.</span><span class="sxs-lookup"><span data-stu-id="765f6-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="765f6-211">Ad esempio, in un'applicazione che consente di visualizzare le schede o sui pannelli, è consigliabile tootrack una pagina ogni volta che l'utente di hello apre un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="765f6-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Sezione Utilizzo nel pannello Panoramica](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="765f6-213">Dati utente e della sessione vengono inviati come proprietà con le visualizzazioni di pagina, pertanto hello grafici utente e sessione vive quando è telemetria di visualizzazione pagina.</span><span class="sxs-lookup"><span data-stu-id="765f6-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="765f6-214">Visualizzazioni pagina personalizzate</span><span class="sxs-lookup"><span data-stu-id="765f6-214">Custom page views</span></span>
<span data-ttu-id="765f6-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="765f6-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="765f6-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="765f6-218">Se si dispone di diverse schede nelle diverse pagine HTML, è possibile specificare URL hello troppo:</span><span class="sxs-lookup"><span data-stu-id="765f6-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="765f6-219">Temporizzazione delle visualizzazioni delle pagine</span><span class="sxs-lookup"><span data-stu-id="765f6-219">Timing page views</span></span>
<span data-ttu-id="765f6-220">Per impostazione predefinita, i tempi di hello segnalati come **visualizzare il tempo di caricamento pagina** vengono misurate da quando il browser hello Invia richiesta hello, fino a quando non viene chiamato l'evento di caricamento pagina del browser hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="765f6-221">In alternativa, è possibile:</span><span class="sxs-lookup"><span data-stu-id="765f6-221">Instead, you can either:</span></span>

* <span data-ttu-id="765f6-222">Impostare una durata esplicita in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chiamare: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="765f6-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="765f6-223">Utilizzare le chiamate di temporizzazione hello pagina visualizzazione `startTrackPage` e `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="765f6-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="765f6-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="765f6-225">...</span><span class="sxs-lookup"><span data-stu-id="765f6-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="765f6-226">nome utilizzato come primo parametro hello associa inizio hello Hello e arrestare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="765f6-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="765f6-227">Per impostazione predefinita toohello nome della pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="765f6-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="765f6-228">caricamento pagina risultante Hello durate visualizzate in Esplora metriche sono derivate dall'intervallo di hello tra hello avviare e arrestare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="765f6-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="765f6-229">È attivo tooyou quale intervallo di tempo effettivamente necessario.</span><span class="sxs-lookup"><span data-stu-id="765f6-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="765f6-230">Dati di telemetria della pagina in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="765f6-231">In [Analytics](app-insights-analytics.md) due tabelle mostrano i dati delle operazioni del browser:</span><span class="sxs-lookup"><span data-stu-id="765f6-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="765f6-232">Hello `pageViews` tabella contiene dati relativi a titolo di pagina e URL hello</span><span class="sxs-lookup"><span data-stu-id="765f6-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="765f6-233">Hello `browserTimings` tabella contiene dati sulle prestazioni del client, ad esempio hello scattato tooprocess hello dati in ingresso</span><span class="sxs-lookup"><span data-stu-id="765f6-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="765f6-234">toofind quanto tempo browser hello accetta tooprocess diverse pagine:</span><span class="sxs-lookup"><span data-stu-id="765f6-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="765f6-235">toodiscover popularities di hello dei diversi browser:</span><span class="sxs-lookup"><span data-stu-id="765f6-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="765f6-236">tooassociate pagina viste tooAJAX chiamate, creare un join con dipendenze:</span><span class="sxs-lookup"><span data-stu-id="765f6-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="765f6-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="765f6-237">TrackRequest</span></span>
<span data-ttu-id="765f6-238">il server di Hello SDK utilizza le richieste HTTP di TrackRequest toolog.</span><span class="sxs-lookup"><span data-stu-id="765f6-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="765f6-239">È inoltre possibile chiamarlo manualmente se si desidera che le richieste di toosimulate in un contesto in cui non è in esecuzione modulo di servizio web di hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="765f6-240">Tuttavia, hello consiglia di telemetria delle ricerche toosend modo in cui la richiesta hello agisce come un <a href="#operation-context">contesto dell'operazione</a>.</span><span class="sxs-lookup"><span data-stu-id="765f6-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="765f6-241">Contesto dell'operazione</span><span class="sxs-lookup"><span data-stu-id="765f6-241">Operation context</span></span>
<span data-ttu-id="765f6-242">È possibile associare elementi di dati di telemetria collegando toothem un ID dell'operazione comune.</span><span class="sxs-lookup"><span data-stu-id="765f6-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="765f6-243">modulo di registrazione delle richieste standard Hello avviene per le eccezioni e altri eventi che vengono inviati durante l'elaborazione di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="765f6-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="765f6-244">In [ricerca](app-insights-diagnostic-search.md) e [Analitica](app-insights-analytics.md), è possibile utilizzare tutti gli eventi associati alla richiesta hello hello ID tooeasily trova.</span><span class="sxs-lookup"><span data-stu-id="765f6-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="765f6-245">ID Hello più semplice modo tooset hello è tooset un contesto dell'operazione utilizzando questo modello:</span><span class="sxs-lookup"><span data-stu-id="765f6-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="765f6-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="765f6-247">Con l'impostazione di un contesto dell'operazione, `StartOperation` crea un elemento di dati di telemetria di hello di tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="765f6-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="765f6-248">Invia dati di telemetria hello elemento quando si elimina l'operazione di hello o se si chiama in modo esplicito `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="765f6-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="765f6-249">Se si utilizza `RequestTelemetry` come tipo di dati di telemetria hello, la durata è impostare l'intervallo di timeout toohello tra inizio e fine.</span><span class="sxs-lookup"><span data-stu-id="765f6-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="765f6-250">I contesti dell’operazione non possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="765f6-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="765f6-251">Se è già presente un contesto dell'operazione, quindi è associata a tutti gli elementi contenuto hello, inclusi elementi hello creato con l'ID `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="765f6-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="765f6-252">In ricerca di contesto dell'operazione hello è hello toocreate utilizzati **elementi correlati** elenco:</span><span class="sxs-lookup"><span data-stu-id="765f6-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Elementi correlati](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="765f6-254">Per altre informazioni sulle operazioni di rilevamento personalizzate, vedere [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="765f6-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="765f6-255">Richieste in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-255">Requests in Analytics</span></span> 

<span data-ttu-id="765f6-256">In [Application Insights Analitica](app-insights-analytics.md), richieste Mostra backup in hello `requests` tabella.</span><span class="sxs-lookup"><span data-stu-id="765f6-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="765f6-257">Se [campionamento](app-insights-sampling.md) è nell'operazione, la proprietà itemCount hello verrà visualizzato un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="765f6-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="765f6-258">Per esempio itemCount = = 10 significa che di 10 chiamate tootrackRequest(), il processo di campionamento hello trasmesso solo uno di essi.</span><span class="sxs-lookup"><span data-stu-id="765f6-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="765f6-259">un numero corretto di richieste e durata media di tooget segmentate per i nomi di richiesta, usare codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="765f6-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="765f6-260">TrackException</span></span>
<span data-ttu-id="765f6-261">Inviare le eccezioni tooApplication Insights:</span><span class="sxs-lookup"><span data-stu-id="765f6-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="765f6-262">troppo[contarli](app-insights-metrics-explorer.md), come indicazione della frequenza di hello di un problema.</span><span class="sxs-lookup"><span data-stu-id="765f6-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="765f6-263">troppo[esaminare le singole occorrenze](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="765f6-264">i report di Hello includono le analisi dello stack hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="765f6-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="765f6-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="765f6-267">SDK Hello catch molte eccezioni automaticamente, non vi è sempre toocall TrackException in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="765f6-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="765f6-268">ASP.NET: [scrivere codice eccezioni toocatch](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="765f6-269">J2EE: [Le eccezioni vengono rilevate automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="765f6-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="765f6-270">JavaScript: Le eccezioni vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="765f6-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="765f6-271">Se si desidera la raccolta automatica di toodisable, aggiungere un frammento di codice toohello riga da inserire nelle pagine Web:</span><span class="sxs-lookup"><span data-stu-id="765f6-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="765f6-272">Eccezioni in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-272">Exceptions in Analytics</span></span>

<span data-ttu-id="765f6-273">In [Application Insights Analitica](app-insights-analytics.md), le eccezioni visualizzata in hello `exceptions` tabella.</span><span class="sxs-lookup"><span data-stu-id="765f6-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="765f6-274">Se [campionamento](app-insights-sampling.md) è in esecuzione, hello `itemCount` proprietà Mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="765f6-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="765f6-275">Per esempio itemCount = = 10 significa che di 10 chiamate tootrackException(), il processo di campionamento hello trasmesso solo uno di essi.</span><span class="sxs-lookup"><span data-stu-id="765f6-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="765f6-276">tooget un conteggio corretto delle eccezioni segmentate per tipo di eccezione, usare codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="765f6-277">La maggior parte delle hello importante informazioni sullo stack sono già estratto in variabili distinte, ma è possibile effettuare il pull hello lontani `details` tooget struttura altre.</span><span class="sxs-lookup"><span data-stu-id="765f6-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="765f6-278">Poiché questa struttura è dinamica, è necessario eseguire il cast di tipo toohello di hello risultato che previsto.</span><span class="sxs-lookup"><span data-stu-id="765f6-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="765f6-279">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="765f6-280">le eccezioni tooassociate con le richieste correlate, è possibile utilizzare un join:</span><span class="sxs-lookup"><span data-stu-id="765f6-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="765f6-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="765f6-281">TrackTrace</span></span>
<span data-ttu-id="765f6-282">Utilizzare TrackTrace toohelp diagnosticare i problemi mediante l'invio di un tooApplication "percorso" informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="765f6-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="765f6-283">È possibile inviare blocchi di dati di diagnostica e controllarli in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="765f6-284">[Gli adattatori di log](app-insights-asp-net-trace-logs.md) usare questo portale di toohello API toosend i log di terze parti.</span><span class="sxs-lookup"><span data-stu-id="765f6-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="765f6-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="765f6-286">È possibile eseguire ricerche nel contenuto del messaggio, ma, a differenza dei valori delle proprietà, non è possibile filtrarlo.</span><span class="sxs-lookup"><span data-stu-id="765f6-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="765f6-287">Limite dimensione Hello `message` è molto più elevate rispetto al limite di hello per le proprietà.</span><span class="sxs-lookup"><span data-stu-id="765f6-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="765f6-288">Un vantaggio TrackTrace è possibile inserire dati relativamente lunghi nel messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="765f6-289">Ad esempio è possibile codificare dati POST.</span><span class="sxs-lookup"><span data-stu-id="765f6-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="765f6-290">Inoltre, è possibile aggiungere un messaggio tooyour livello di gravità.</span><span class="sxs-lookup"><span data-stu-id="765f6-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="765f6-291">E, come gli altri dati di telemetria, è possibile aggiungere toohelp di valori di proprietà che è applicare un filtro o ricerca per diversi set di tracce.</span><span class="sxs-lookup"><span data-stu-id="765f6-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="765f6-292">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="765f6-293">In [ricerca](app-insights-diagnostic-search.md), è quindi possibile filtrare facilmente tutti i messaggi hello di un livello di gravità specifico correlati tooa particolare database.</span><span class="sxs-lookup"><span data-stu-id="765f6-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="765f6-294">Tracce in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-294">Traces in Analytics</span></span>

<span data-ttu-id="765f6-295">In [Application Insights Analitica](app-insights-analytics.md), chiama tooTrackTrace Mostra hello `traces` tabella.</span><span class="sxs-lookup"><span data-stu-id="765f6-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="765f6-296">Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="765f6-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="765f6-297">Per esempio itemCount = = 10 significa che di 10 chiamate troppo`trackTrace()`, il processo di campionamento hello trasmesso solo uno di essi.</span><span class="sxs-lookup"><span data-stu-id="765f6-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="765f6-298">tooget un conteggio corretto delle chiamate di traccia, è consigliabile utilizzare pertanto codice, ad esempio `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="765f6-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="765f6-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="765f6-299">TrackDependency</span></span>
<span data-ttu-id="765f6-300">Hello utilizzare TrackDependency chiamare tempi di risposta tootrack hello e percentuali di successo di parte esterna tooan di chiamate del codice.</span><span class="sxs-lookup"><span data-stu-id="765f6-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="765f6-301">risultati di Hello vengono visualizzati nei grafici dipendenza hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="765f6-302">Tenere presente che il server hello SDK includono un [modulo dipendenza](app-insights-asp-net-dependencies.md) che consente di individuare e tiene traccia di determinate chiamate a dipendenze automaticamente, ad esempio toodatabases e le API REST.</span><span class="sxs-lookup"><span data-stu-id="765f6-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="765f6-303">È necessario un agente su un modulo hello toomake server tooinstall di lavoro.</span><span class="sxs-lookup"><span data-stu-id="765f6-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="765f6-304">Utilizzare questa chiamata, se si desidera non intercettare chiamate tootrack hello rilevamento automatico o se non si desidera agente hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="765f6-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="765f6-305">Modifica tooturn off modulo di rilevamento delle dipendenze hello standard, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) ed eliminare il riferimento hello troppo`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="765f6-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="765f6-306">Dipendenze in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-306">Dependencies in Analytics</span></span>

<span data-ttu-id="765f6-307">In [Application Insights Analitica](app-insights-analytics.md), trackDependency chiamate visualizzati nella hello `dependencies` tabella.</span><span class="sxs-lookup"><span data-stu-id="765f6-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="765f6-308">Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="765f6-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="765f6-309">Per esempio itemCount = = 10 significa che di 10 chiamate tootrackDependency(), il processo di campionamento hello trasmesso solo uno di essi.</span><span class="sxs-lookup"><span data-stu-id="765f6-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="765f6-310">un conteggio corretto delle dipendenze di tooget segmentate per componente di destinazione, usare codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="765f6-311">dipendenze tooassociate con le richieste correlate, è possibile utilizzare un join:</span><span class="sxs-lookup"><span data-stu-id="765f6-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="765f6-312">Scaricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="765f6-312">Flushing data</span></span>
<span data-ttu-id="765f6-313">In genere, hello SDK invia i dati in alcuni casi scelti impatto hello toominimize utente hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="765f6-314">Tuttavia, in alcuni casi, è consigliabile buffer hello tooflush, ad esempio, se si utilizza hello SDK in un'applicazione che viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="765f6-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="765f6-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="765f6-316">Si noti che la funzione hello è asincrona per hello [canale dati di telemetria server](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="765f6-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="765f6-317">utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="765f6-317">Authenticated users</span></span>
<span data-ttu-id="765f6-318">In un'app Web gli utenti sono identificati dai cookie per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="765f6-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="765f6-319">Un utente può essere conteggiato più volte se accede all'app da un computer o da un browser diverso o se elimina i cookie.</span><span class="sxs-lookup"><span data-stu-id="765f6-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="765f6-320">Se gli utenti accedono tooyour app, è possibile ottenere un conteggio più preciso impostando l'ID utente hello autenticato nel codice browser hello:</span><span class="sxs-lookup"><span data-stu-id="765f6-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="765f6-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="765f6-322">In un'applicazione MVC Web ASP.NET, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="765f6-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="765f6-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="765f6-324">Non è effettivo nome di accesso toouse necessario hello utente.</span><span class="sxs-lookup"><span data-stu-id="765f6-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="765f6-325">Include solo un ID utente univoco toothat toobe.</span><span class="sxs-lookup"><span data-stu-id="765f6-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="765f6-326">Non deve includere spazi o caratteri hello `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="765f6-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="765f6-327">ID utente Hello viene anche impostato in un cookie di sessione e inviati toohello server.</span><span class="sxs-lookup"><span data-stu-id="765f6-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="765f6-328">Se è installato il server di hello SDK, hello l'utente autenticato che ID viene inviato come parte delle proprietà di contesto hello del client e server dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="765f6-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="765f6-329">Quindi sarà possibile filtrarlo ed eseguire ricerche al suo interno.</span><span class="sxs-lookup"><span data-stu-id="765f6-329">You can then filter and search on it.</span></span>

<span data-ttu-id="765f6-330">Se l'app gruppi di utenti nell'account, è anche possibile passare un identificatore per l'account di hello (con hello stesso restrizioni relative ai caratteri).</span><span class="sxs-lookup"><span data-stu-id="765f6-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="765f6-331">In [Esplora metriche](app-insights-metrics-explorer.md) è possibile creare un grafico che conta i valori **Utenti, Autenticati** e **Account utente**.</span><span class="sxs-lookup"><span data-stu-id="765f6-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="765f6-332">È anche possibile [cercare](app-insights-diagnostic-search.md) i punti dati del client con account e nomi utente specifici.</span><span class="sxs-lookup"><span data-stu-id="765f6-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="765f6-333"><a name="properties"></a>Filtro, ricerca e segmentazione dei dati mediante le proprietà</span><span class="sxs-lookup"><span data-stu-id="765f6-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="765f6-334">È possibile associare proprietà e le misurazioni tooyour eventi (e anche toometrics, visualizzazioni di pagina, le eccezioni e altri dati di telemetria).</span><span class="sxs-lookup"><span data-stu-id="765f6-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="765f6-335">*Proprietà* sono valori stringa che è possibile utilizzare toofilter dati di telemetria nei report di utilizzo di hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="765f6-336">Ad esempio, se l'app fornisce numerosi giochi di tipo, è possibile collegare il nome di hello dell'evento di gioco tooeach hello in modo da poter visualizzare giochi vengono utilizzati più di frequente.</span><span class="sxs-lookup"><span data-stu-id="765f6-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="765f6-337">È previsto un limite di 8192 nella lunghezza della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="765f6-338">(Se si desidera toosend grandi quantità di dati, utilizzare il parametro messaggio hello del [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="765f6-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="765f6-339">*metriche* sono valori numerici che possono essere rappresentati graficamente.</span><span class="sxs-lookup"><span data-stu-id="765f6-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="765f6-340">Ad esempio, è consigliabile toosee se è presente un aumento graduale punteggi hello che raggiungono i giocatori.</span><span class="sxs-lookup"><span data-stu-id="765f6-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="765f6-341">grafici di Hello possono essere segmentati per separano le proprietà che vengono inviate con evento hello, in modo che sia possibile ottenere hello o in pila grafici per i giochi di diversi tipo.</span><span class="sxs-lookup"><span data-stu-id="765f6-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="765f6-342">Per i valori della metrica toobe visualizzato correttamente, dovrebbero essere maggiore o uguale too0.</span><span class="sxs-lookup"><span data-stu-id="765f6-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="765f6-343">Esistono tuttavia alcuni [limiti sul numero di hello di proprietà, i valori delle proprietà e le metriche](#limits) che è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="765f6-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="765f6-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="765f6-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="765f6-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="765f6-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="765f6-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="765f6-348">Prestare attenzione toolog informazioni personali nelle proprietà.</span><span class="sxs-lookup"><span data-stu-id="765f6-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="765f6-349">*Se è stata utilizzata la metrica*, aprire Esplora metriche e selezionare la metrica hello hello **personalizzato** gruppo:</span><span class="sxs-lookup"><span data-stu-id="765f6-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Aprire Esplora metriche, grafico selezionare hello e selezionare la metrica hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="765f6-351">Se non viene visualizzata l'unità di misura, o se hello **personalizzato** intestazione non è presente, il pannello di selezione Chiudi hello e riprovare più tardi.</span><span class="sxs-lookup"><span data-stu-id="765f6-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="765f6-352">Metriche talvolta possono richiedere un'ora toobe aggregati tramite pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="765f6-353">*Se si utilizza le proprietà e le metriche*, segmento metrica hello dalla proprietà hello:</span><span class="sxs-lookup"><span data-stu-id="765f6-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Impostare il raggruppamento e quindi selezionare proprietà hello in Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="765f6-355">*Nella ricerca diagnostica*, è possibile visualizzare le proprietà di hello e le metriche di singole occorrenze di un evento.</span><span class="sxs-lookup"><span data-stu-id="765f6-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Selezionare un'istanza e quindi scegliere "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="765f6-357">Hello utilizzare **ricerca** toosee occorrenze dell'evento che hanno un valore di determinate proprietà di campo.</span><span class="sxs-lookup"><span data-stu-id="765f6-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Digitare un termine in Ricerca](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="765f6-359">[Altre informazioni sulle espressioni di ricerca](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="765f6-360">Le metriche e le proprietà di tooset alternativa</span><span class="sxs-lookup"><span data-stu-id="765f6-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="765f6-361">Se è più semplice, è possibile raccogliere i parametri di hello di un evento in un oggetto separato:</span><span class="sxs-lookup"><span data-stu-id="765f6-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="765f6-362">Non riutilizzare hello stessa istanza dell'elemento di dati di telemetria (`event` in questo esempio) toocall Track*() più volte.</span><span class="sxs-lookup"><span data-stu-id="765f6-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="765f6-363">Ciò potrebbe causare toobe telemetria inviati con una configurazione errata.</span><span class="sxs-lookup"><span data-stu-id="765f6-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="765f6-364">Misure e proprietà personalizzate in Analytics</span><span class="sxs-lookup"><span data-stu-id="765f6-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="765f6-365">In [Analitica](app-insights-analytics.md), metriche personalizzate e le proprietà vengono visualizzati in hello `customMeasurements` e `customDimensions` gli attributi di ogni record di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="765f6-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="765f6-366">Ad esempio, se è stata aggiunta una proprietà denominata "gioco" tooyour telemetria di richiesta, questa query conta le occorrenze di hello dei diversi valori di "gioco" e Mostra la media hello di hello metrica personalizzata "punteggio":</span><span class="sxs-lookup"><span data-stu-id="765f6-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="765f6-367">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="765f6-367">Notice that:</span></span>

* <span data-ttu-id="765f6-368">Quando si estrae un valore da hello customDimensions o customMeasurements JSON, è di tipo dinamico e pertanto è necessario eseguirne il cast `tostring` o `todouble`.</span><span class="sxs-lookup"><span data-stu-id="765f6-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="765f6-369">account tootake della probabilità hello [campionamento](app-insights-sampling.md), si consiglia di utilizzare `sum(itemCount)`, non `count()`.</span><span class="sxs-lookup"><span data-stu-id="765f6-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="765f6-370"><a name="timed"></a> Temporizzazione degli eventi</span><span class="sxs-lookup"><span data-stu-id="765f6-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="765f6-371">Talvolta toochart il tempo necessario tooperform un'azione.</span><span class="sxs-lookup"><span data-stu-id="765f6-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="765f6-372">Ad esempio, è possibile tooknow quanti utenti acquisire scelte tooconsider un gioco.</span><span class="sxs-lookup"><span data-stu-id="765f6-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="765f6-373">È possibile utilizzare il parametro di misura hello per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="765f6-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="765f6-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="765f6-375"><a name="defaults"></a>Proprietà predefinite per i dati di telemetria personalizzati</span><span class="sxs-lookup"><span data-stu-id="765f6-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="765f6-376">Se si desidera tooset valori di proprietà predefiniti per alcuni eventi hello personalizzati scritti, è possibile impostare tali in un'istanza di TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="765f6-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="765f6-377">Si tratta di elemento di dati di telemetria tooevery allegato inviato dal client.</span><span class="sxs-lookup"><span data-stu-id="765f6-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="765f6-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="765f6-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="765f6-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="765f6-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="765f6-381">Telemetria singole chiamate possono eseguire l'override di valori predefiniti di hello nei dizionari loro proprietà.</span><span class="sxs-lookup"><span data-stu-id="765f6-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="765f6-382">*Per i client Web di JavaScript*, [usare gli inizializzatori di telemetria JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="765f6-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="765f6-383">*dati di telemetria tooall proprietà tooadd*, compresi i dati hello moduli di raccolta standard, [implementare `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="765f6-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="765f6-384">Campionamento, filtri ed elaborazione dei dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="765f6-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="765f6-385">È possibile scrivere codice tooprocess dati di telemetria prima che venga inviato da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="765f6-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="765f6-386">l'elaborazione di Hello include i dati inviati dai moduli di telemetria standard hello, ad esempio l'insieme di richiesta HTTP e raccolta di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="765f6-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="765f6-387">[Aggiungere proprietà](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="765f6-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="765f6-388">Ad esempio è possibile aggiungere numeri di versione o valori calcolati da altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="765f6-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="765f6-389">[Filtro](app-insights-api-filtering-sampling.md#filtering) può modificare o eliminare dati di telemetria prima che venga inviato da hello SDK implementando `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="765f6-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="765f6-390">Controllare gli elementi inviati o eliminati, ma è necessario tooaccount per effetto di hello per le misurazioni.</span><span class="sxs-lookup"><span data-stu-id="765f6-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="765f6-391">A seconda di come si elimina gli elementi, si potrebbe perdere hello possibilità toonavigate tra gli elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="765f6-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="765f6-392">[Campionamento](app-insights-api-filtering-sampling.md) è un volume di hello tooreduce soluzione nel pacchetto di dati inviati dal portale toohello app.</span><span class="sxs-lookup"><span data-stu-id="765f6-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="765f6-393">Esegue l'operazione senza influire sulle metriche hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="765f6-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="765f6-394">E a tale scopo senza influire sulla risoluzione dei problemi di toodiagnose possibilità passando tra gli elementi correlati, ad esempio eccezioni, le richieste e le visualizzazioni di pagina.</span><span class="sxs-lookup"><span data-stu-id="765f6-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="765f6-395">[Altre informazioni](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="765f6-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="765f6-396">Disabilitazione della telemetria</span><span class="sxs-lookup"><span data-stu-id="765f6-396">Disabling telemetry</span></span>
<span data-ttu-id="765f6-397">troppo*dinamicamente arrestare e avviare* hello raccolta e la trasmissione di dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="765f6-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="765f6-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="765f6-399">troppo*disabilitare gli agenti di raccolta standard selezionati*, ad esempio, i contatori delle prestazioni, le richieste HTTP o dipendenze, eliminare o impostare come commento le righe rilevanti hello in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). È possibile farlo, ad esempio, se si desidera toosend TrackRequest dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="765f6-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="765f6-400"><a name="debug"></a>Modalità di sviluppo</span><span class="sxs-lookup"><span data-stu-id="765f6-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="765f6-401">Durante il debug, è utile toohave dati di telemetria inviati attraverso la pipeline hello in modo che sia possibile osservare immediatamente i risultati.</span><span class="sxs-lookup"><span data-stu-id="765f6-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="765f6-402">È inoltre get altri messaggi che consentono di analizzare i problemi di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="765f6-403">Disattivare questa modalità in fase di produzione poiché potrebbe rallentare l'app.</span><span class="sxs-lookup"><span data-stu-id="765f6-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="765f6-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="765f6-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="765f6-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="765f6-406"><a name="ikey"></a>Impostazione chiave di strumentazione hello per dati di telemetria personalizzati selezionato</span><span class="sxs-lookup"><span data-stu-id="765f6-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="765f6-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="765f6-408"><a name="dynamic-ikey"></a> Chiave di strumentazione dinamica</span><span class="sxs-lookup"><span data-stu-id="765f6-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="765f6-409">tooavoid combinazione di dati di telemetria di sviluppo, test e ambienti di produzione, è possibile [creare risorse di Application Insights distinte](app-insights-create-new-resource.md) e modificare le relative chiavi, a seconda di ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="765f6-410">Anziché la chiave di strumentazione hello dal file di configurazione di hello, è possibile impostarlo nel codice.</span><span class="sxs-lookup"><span data-stu-id="765f6-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="765f6-411">Impostare la chiave di hello in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="765f6-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="765f6-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="765f6-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="765f6-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="765f6-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="765f6-414">Nelle pagine Web, è possibile tooset dal server hello web, anziché codifica letteralmente in script hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="765f6-415">Ad esempio, in una pagina Web generata in un'app ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="765f6-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="765f6-416">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="765f6-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="765f6-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="765f6-417">TelemetryContext</span></span>
<span data-ttu-id="765f6-418">TelemetryClient dispone di una proprietà Context contenente valori che vengono inviati insieme a tutti i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="765f6-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="765f6-419">In genere impostati dai moduli di hello telemetria standard, ma è anche possibile impostarle personalmente.</span><span class="sxs-lookup"><span data-stu-id="765f6-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="765f6-420">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="765f6-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="765f6-421">Impostando uno di questi valori manualmente, si consiglia di rimuovere hello rilevanti riga [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), in modo che i valori e valori standard hello non confusione.</span><span class="sxs-lookup"><span data-stu-id="765f6-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="765f6-422">**Componente**: hello app e la relativa versione.</span><span class="sxs-lookup"><span data-stu-id="765f6-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="765f6-423">**Dispositivo**: dati sul dispositivo hello in cui è in esecuzione l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="765f6-424">(In applicazioni web, questo è server hello o un dispositivo client inviate da dati di telemetria hello).</span><span class="sxs-lookup"><span data-stu-id="765f6-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="765f6-425">**Manualmente InstrumentationKey**: risorsa di Application Insights in Azure in cui vengono visualizzati dati di telemetria hello hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="765f6-426">Viene in genere presa dal file ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="765f6-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="765f6-427">**Percorso**: hello posizione geografica del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="765f6-428">**Operazione**: nelle App web, hello richiesta HTTP corrente.</span><span class="sxs-lookup"><span data-stu-id="765f6-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="765f6-429">In altri tipi di app, è possibile impostare questo toogroup di eventi.</span><span class="sxs-lookup"><span data-stu-id="765f6-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="765f6-430">**ID**: un valore generato che mette in correlazione eventi diversi, in modo che quando si analizza qualsiasi evento in Ricerca diagnostica, è possibile trovare elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="765f6-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="765f6-431">**Nome**: un identificatore, in genere hello URL della richiesta HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="765f6-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="765f6-432">**SyntheticSource**: se non null o vuoto, una stringa che indica che tale origine hello della richiesta di hello è stata identificata come un test web o robot.</span><span class="sxs-lookup"><span data-stu-id="765f6-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="765f6-433">Per impostazione predefinita viene esclusa dai calcoli in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="765f6-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="765f6-434">**Proprietà**: proprietà che vengono inviate con tutti i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="765f6-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="765f6-435">È possibile eseguire l'override di questo valore in singole chiamate di Track*.</span><span class="sxs-lookup"><span data-stu-id="765f6-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="765f6-436">**Sessione**: hello sessione utente.</span><span class="sxs-lookup"><span data-stu-id="765f6-436">**Session**: hello user's session.</span></span> <span data-ttu-id="765f6-437">ID Hello è impostato un valore di tooa generato, che viene modificato quando l'utente hello non è stato attivo per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="765f6-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="765f6-438">**Utente**: le informazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="765f6-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="765f6-439">Limiti</span><span class="sxs-lookup"><span data-stu-id="765f6-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="765f6-440">raggiungimento di limite di velocità dati hello, utilizzare tooavoid [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="765f6-441">toodetermine come dati di tipo long viene mantenuti, vedere [conservazione dei dati e la privacy](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="765f6-442">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="765f6-442">Reference docs</span></span>
* [<span data-ttu-id="765f6-443">Riferimento ASP.NET</span><span class="sxs-lookup"><span data-stu-id="765f6-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="765f6-444">Riferimento Java</span><span class="sxs-lookup"><span data-stu-id="765f6-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="765f6-445">Informazioni di riferimento su JavaScript</span><span class="sxs-lookup"><span data-stu-id="765f6-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="765f6-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="765f6-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="765f6-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="765f6-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="765f6-448">Codice SDK</span><span class="sxs-lookup"><span data-stu-id="765f6-448">SDK code</span></span>
* [<span data-ttu-id="765f6-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="765f6-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="765f6-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="765f6-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="765f6-451">Pacchetti per Windows Server</span><span class="sxs-lookup"><span data-stu-id="765f6-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="765f6-452">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="765f6-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="765f6-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="765f6-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="765f6-454">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="765f6-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="765f6-455">Domande</span><span class="sxs-lookup"><span data-stu-id="765f6-455">Questions</span></span>
* <span data-ttu-id="765f6-456">*Quali eccezioni potrebbero essere generate dalle chiamate Track_()?*</span><span class="sxs-lookup"><span data-stu-id="765f6-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="765f6-457">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="765f6-457">None.</span></span> <span data-ttu-id="765f6-458">Non è necessario toowrap usarle nelle clausole try-catch.</span><span class="sxs-lookup"><span data-stu-id="765f6-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="765f6-459">Se hello SDK si verificano problemi, messaggi vengono registrati nell'output di console debug hello e --se hello messaggi ottenere mediante - ricerca di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="765f6-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="765f6-460">*È una data tooget API REST dal portale hello?*</span><span class="sxs-lookup"><span data-stu-id="765f6-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="765f6-461">Sì, hello [API di accesso ai dati](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="765f6-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="765f6-462">Includono altri dati tooextract modi [esportare da Analitica tooPower BI](app-insights-export-power-bi.md) e [l'esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="765f6-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="765f6-463"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="765f6-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="765f6-464">Ricerca di eventi e log</span><span class="sxs-lookup"><span data-stu-id="765f6-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="765f6-465">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="765f6-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


