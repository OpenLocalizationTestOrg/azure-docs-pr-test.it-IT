---
title: API di Application Insights per metriche ed eventi personalizzati | Microsoft Docs
description: Inserire alcune righe di codice nell'app desktop o per dispositivi, nella pagina Web o nel servizio per tenere traccia dell'utilizzo e diagnosticare i problemi.
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
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="efd69-103">API di Application Insights per metriche ed eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="efd69-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="efd69-104">Inserire alcune righe di codice nell'applicazione per scoprire come viene usato dagli utenti o per agevolare la diagnosi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="efd69-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="efd69-105">È possibile inviare i dati di telemetria dalle app desktop e per dispositivi, dai client Web e dai server Web.</span><span class="sxs-lookup"><span data-stu-id="efd69-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="efd69-106">Usare l'API di telemetria principale di [Azure Application Insights](app-insights-overview.md) per inviare metriche ed eventi personalizzati e le versioni personalizzate dei dati di telemetria standard.</span><span class="sxs-lookup"><span data-stu-id="efd69-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="efd69-107">Questa API è la stessa utilizzata dagli agenti di raccolta dati di Application Insights standard.</span><span class="sxs-lookup"><span data-stu-id="efd69-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="efd69-108">Riepilogo dell'API</span><span class="sxs-lookup"><span data-stu-id="efd69-108">API summary</span></span>
<span data-ttu-id="efd69-109">L'API è uniforme in tutte le piattaforme, a parte alcune variazioni di lieve entità.</span><span class="sxs-lookup"><span data-stu-id="efd69-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="efd69-110">Metodo</span><span class="sxs-lookup"><span data-stu-id="efd69-110">Method</span></span> | <span data-ttu-id="efd69-111">Usato per</span><span class="sxs-lookup"><span data-stu-id="efd69-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="efd69-112">Pagine, schermate, pannelli o form.</span><span class="sxs-lookup"><span data-stu-id="efd69-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="efd69-113">Azioni dell'utente e altri eventi.</span><span class="sxs-lookup"><span data-stu-id="efd69-113">User actions and other events.</span></span> <span data-ttu-id="efd69-114">Usato per tenere traccia del comportamento dell'utente o per monitorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="efd69-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="efd69-115">Misurazioni delle prestazioni, ad esempio la lunghezza della coda, non correlate a eventi specifici.</span><span class="sxs-lookup"><span data-stu-id="efd69-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="efd69-116">Registrare le eccezioni per la diagnosi.</span><span class="sxs-lookup"><span data-stu-id="efd69-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="efd69-117">Tenere traccia del punto in cui si verificano in relazione ad altri eventi ed esaminare le analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="efd69-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="efd69-118">Registrare la frequenza e la durata delle richieste del server per l'analisi delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="efd69-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="efd69-119">Messaggi nei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="efd69-119">Diagnostic log messages.</span></span> <span data-ttu-id="efd69-120">È anche possibile acquisire log di terze parti.</span><span class="sxs-lookup"><span data-stu-id="efd69-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="efd69-121">Registrare la durata e la frequenza delle chiamate ai componenti esterni da cui dipende l'app.</span><span class="sxs-lookup"><span data-stu-id="efd69-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="efd69-122">È possibile [associare proprietà e metriche](#properties) alla maggior parte di queste chiamate di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="efd69-123"><a name="prep"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="efd69-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="efd69-124">Se non si ha ancora un riferimento in Application Insights SDK:</span><span class="sxs-lookup"><span data-stu-id="efd69-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="efd69-125">Aggiungere Application Insights SDK al progetto:</span><span class="sxs-lookup"><span data-stu-id="efd69-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="efd69-126">Progetto ASP.NET</span><span class="sxs-lookup"><span data-stu-id="efd69-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="efd69-127">Progetto Java</span><span class="sxs-lookup"><span data-stu-id="efd69-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="efd69-128">JavaScript in ogni pagina Web</span><span class="sxs-lookup"><span data-stu-id="efd69-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="efd69-129">Nel dispositivo o nel codice del server Web includere:</span><span class="sxs-lookup"><span data-stu-id="efd69-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="efd69-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="efd69-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="efd69-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="efd69-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="efd69-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="efd69-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="efd69-133">Costruzione di un'istanza di TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="efd69-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="efd69-134">Costruire un'istanza di `TelemetryClient` (tranne che in JavaScript nelle pagine Web):</span><span class="sxs-lookup"><span data-stu-id="efd69-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="efd69-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="efd69-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="efd69-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="efd69-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="efd69-138">TelemetryClient è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="efd69-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="efd69-139">È consigliabile usare un'istanza di TelemetryClient per ogni modulo dell'app.</span><span class="sxs-lookup"><span data-stu-id="efd69-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="efd69-140">Ad esempio è possibile che il servizio Web includa un'istanza di TelemetryClient per segnalare le richieste HTTP in entrata e un altro oggetto in una classe middleware per segnalare gli eventi di logica di business.</span><span class="sxs-lookup"><span data-stu-id="efd69-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="efd69-141">È possibile impostare proprietà quali `TelemetryClient.Context.User.Id` per tenere traccia degli utenti e delle sessioni o `TelemetryClient.Context.Device.Id` per identificare il computer.</span><span class="sxs-lookup"><span data-stu-id="efd69-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="efd69-142">Queste informazioni sono associate a tutti gli eventi inviati dall'istanza.</span><span class="sxs-lookup"><span data-stu-id="efd69-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="efd69-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="efd69-143">TrackEvent</span></span>
<span data-ttu-id="efd69-144">In Application Insights un *evento personalizzato* è un punto dati che è possibile visualizzare in [Esplora metriche](app-insights-metrics-explorer.md) come conteggio aggregato e in [Ricerca diagnostica](app-insights-diagnostic-search.md) come singole occorrenze.</span><span class="sxs-lookup"><span data-stu-id="efd69-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="efd69-145">Non è correlato a MVC o ad altri "eventi" del framework.</span><span class="sxs-lookup"><span data-stu-id="efd69-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="efd69-146">Inserire chiamate `TrackEvent` nel codice per contare i vari eventi.</span><span class="sxs-lookup"><span data-stu-id="efd69-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="efd69-147">La frequenza d'uso di una particolare funzionalità, la frequenza di raggiungimento di obiettivi specifici o la frequenza di particolari tipi di errore.</span><span class="sxs-lookup"><span data-stu-id="efd69-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="efd69-148">Ad esempio, in un'app di gioco è possibile inviare un evento ogni volta che un utente vince il gioco:</span><span class="sxs-lookup"><span data-stu-id="efd69-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="efd69-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="efd69-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="efd69-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="efd69-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="efd69-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="efd69-153">Visualizzare gli eventi nel portale di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="efd69-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="efd69-154">Per visualizzare un conteggio degli eventi, aprire un pannello [Esplora metriche](app-insights-metrics-explorer.md) , aggiungere un nuovo grafico e selezionare **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="efd69-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Visualizzare il conteggio degli eventi personalizzati](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="efd69-156">Per confrontare il conteggio di eventi diversi, impostare il tipo di grafico su **Griglia** e raggruppare in base al nome dell'evento:</span><span class="sxs-lookup"><span data-stu-id="efd69-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Impostare il tipo di grafico e il raggruppamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="efd69-158">Nella griglia, fare clic su un nome di evento per visualizzare le singole occorrenze di quell'evento.</span><span class="sxs-lookup"><span data-stu-id="efd69-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="efd69-159">Per altre informazioni, fare clic su qualsiasi occorrenza nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="efd69-159">To see more detail - click any occurrence in the list.</span></span>

![Eseguire il drill-through degli eventi](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="efd69-161">Per concentrarsi sugli eventi specifici in Ricerca o in Esplora metriche, impostare il filtro del pannello sui nomi degli eventi a cui si è interessati:</span><span class="sxs-lookup"><span data-stu-id="efd69-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Aprire i filtri, espandere il nome dell’evento e selezionare uno o più valori](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="efd69-163">Eventi personalizzati in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-163">Custom events in Analytics</span></span>

<span data-ttu-id="efd69-164">I dati di telemetria sono disponibili nella tabella `customEvents` in [Analytics di Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="efd69-165">Ogni riga rappresenta una chiamata a `trackEvent(..)` nell'app in uso.</span><span class="sxs-lookup"><span data-stu-id="efd69-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="efd69-166">Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="efd69-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="efd69-167">Per esempio itemCount==10 indica che su 10 chiamate a trackEvent(), il processo di campionamento ne trasmette solo una.</span><span class="sxs-lookup"><span data-stu-id="efd69-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="efd69-168">Per ottenere un conteggio corretto degli eventi personalizzati, si consiglia di usare un codice, ad esempio `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="efd69-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="efd69-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="efd69-169">TrackMetric</span></span>

<span data-ttu-id="efd69-170">Application Insights è in grado di creare grafici in base a metriche non sono associate a determinati eventi.</span><span class="sxs-lookup"><span data-stu-id="efd69-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="efd69-171">Ad esempio, è possibile monitorare la lunghezza di una coda a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="efd69-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="efd69-172">Grazie alle metriche, le singole misurazioni sono meno interessanti rispetto alle variazioni e alle tendenze, i grafici statistici risultano pertanto utili.</span><span class="sxs-lookup"><span data-stu-id="efd69-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="efd69-173">Per inviare le metriche ad Application Insights, è possibile usare l'API `TrackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="efd69-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="efd69-174">Per inviare le metriche è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="efd69-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="efd69-175">Valore singolo.</span><span class="sxs-lookup"><span data-stu-id="efd69-175">Single value.</span></span> <span data-ttu-id="efd69-176">Ogni volta che si esegue una misurazione nell'applicazione, si invia il valore corrispondente ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="efd69-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="efd69-177">Ad esempio, si supponga di avere una metrica che descrive il numero di elementi in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="efd69-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="efd69-178">Durante un periodo di tempo specifico, inserire prima tre elementi nel contenitore e poi rimuoverne due.</span><span class="sxs-lookup"><span data-stu-id="efd69-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="efd69-179">Di conseguenza, è necessario chiamare `TrackMetric` due volte: prima passando il valore `3` e poi il valore `-2`.</span><span class="sxs-lookup"><span data-stu-id="efd69-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="efd69-180">Application Insights memorizza entrambi i valori per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="efd69-181">Aggregazione.</span><span class="sxs-lookup"><span data-stu-id="efd69-181">Aggregation.</span></span> <span data-ttu-id="efd69-182">Quando si usano le metriche non si considera mai una sola misura.</span><span class="sxs-lookup"><span data-stu-id="efd69-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="efd69-183">È importante invece il riepilogo delle operazioni eseguite in un periodo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="efd69-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="efd69-184">Tale riepilogo viene chiamato _aggregazione_.</span><span class="sxs-lookup"><span data-stu-id="efd69-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="efd69-185">Nell'esempio precedente la somma della metrica di aggregazione per quel periodo di tempo è `1` e il conteggio dei valori della metrica è `2`.</span><span class="sxs-lookup"><span data-stu-id="efd69-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="efd69-186">Quando si usa l'approccio di aggregazione, si chiama `TrackMetric` solo una volta per periodo di tempo e si inviano i valori di aggregazione.</span><span class="sxs-lookup"><span data-stu-id="efd69-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="efd69-187">Questo è l'approccio consigliato in quanto può ridurre notevolmente i costi e le prestazioni generali inviando meno punti dati ad Application Insights, durante la raccolta di tutte le informazioni pertinenti.</span><span class="sxs-lookup"><span data-stu-id="efd69-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="efd69-188">Esempi:</span><span class="sxs-lookup"><span data-stu-id="efd69-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="efd69-189">Valori singoli</span><span class="sxs-lookup"><span data-stu-id="efd69-189">Single values</span></span>

<span data-ttu-id="efd69-190">Per inviare un singolo valore di metrica:</span><span class="sxs-lookup"><span data-stu-id="efd69-190">To send a single metric value:</span></span>

<span data-ttu-id="efd69-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="efd69-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="efd69-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="efd69-193">Aggregazione delle metriche</span><span class="sxs-lookup"><span data-stu-id="efd69-193">Aggregating metrics</span></span>

<span data-ttu-id="efd69-194">È consigliabile aggregare le metriche prima di inviarle dall'app, al fine di ridurre la larghezza di banda, il costo e migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="efd69-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="efd69-195">Di seguito è riportato un esempio di codice di aggregazione:</span><span class="sxs-lookup"><span data-stu-id="efd69-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="efd69-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-196">*C#*</span></span>

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
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
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
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="efd69-197">Metriche personalizzate in Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="efd69-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="efd69-198">Per visualizzare i risultati, aprire Esplora metriche e aggiungere un nuovo grafico.</span><span class="sxs-lookup"><span data-stu-id="efd69-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="efd69-199">Modificare il grafico per visualizzare la metrica.</span><span class="sxs-lookup"><span data-stu-id="efd69-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="efd69-200">Potrebbero essere necessari alcuni minuti per visualizzare la metrica personalizzata nell'elenco delle metriche disponibili.</span><span class="sxs-lookup"><span data-stu-id="efd69-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Aggiungere un nuovo grafico o selezionare un grafico e selezionare le metriche in Personalizzato](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="efd69-202">Metriche personalizzate in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="efd69-203">I dati di telemetria sono disponibili nella tabella `customMetrics` in [Analytics di Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="efd69-204">Ogni riga rappresenta una chiamata a `trackMetric(..)` nell'app in uso.</span><span class="sxs-lookup"><span data-stu-id="efd69-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="efd69-205">`valueSum`: somma delle misurazioni.</span><span class="sxs-lookup"><span data-stu-id="efd69-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="efd69-206">Per ottenere il valore medio, dividere per `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="efd69-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="efd69-207">`valueCount`: numero delle misurazioni aggregate nella chiamata `trackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="efd69-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="efd69-208">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="efd69-208">Page views</span></span>
<span data-ttu-id="efd69-209">In un'app per dispositivo o pagine Web i dati di telemetria delle visualizzazioni pagina vengono inviati per impostazione predefinita quando viene caricata ogni schermata o pagina.</span><span class="sxs-lookup"><span data-stu-id="efd69-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="efd69-210">È tuttavia possibile modificare questa impostazione per tenere traccia delle visualizzazioni pagina in momenti diversi o aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="efd69-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="efd69-211">Ad esempio, in un'app che visualizza schede o pannelli, è possibile tenere traccia di una "pagina" ogni volta che l'utente apre un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="efd69-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Sezione Utilizzo nel pannello Panoramica](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="efd69-213">I dati relativi a utente e sessione vengono inviati come proprietà insieme alle visualizzazioni pagina, in modo che i grafici utente e sessione si attivino in presenza dei dati di telemetria delle visualizzazioni pagina.</span><span class="sxs-lookup"><span data-stu-id="efd69-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="efd69-214">Visualizzazioni pagina personalizzate</span><span class="sxs-lookup"><span data-stu-id="efd69-214">Custom page views</span></span>
<span data-ttu-id="efd69-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="efd69-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="efd69-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="efd69-218">Se sono presenti alcune schede in pagine HTML diverse, è possibile specificare anche l'URL:</span><span class="sxs-lookup"><span data-stu-id="efd69-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="efd69-219">Temporizzazione delle visualizzazioni delle pagine</span><span class="sxs-lookup"><span data-stu-id="efd69-219">Timing page views</span></span>
<span data-ttu-id="efd69-220">Per impostazione predefinita gli intervalli di tempo indicati come **Tempo di caricamento della visualizzazione pagina** sono misurati dal momento in cui il browser invia la richiesta al momento della chiamata dell'evento di caricamento pagina del browser.</span><span class="sxs-lookup"><span data-stu-id="efd69-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="efd69-221">In alternativa, è possibile:</span><span class="sxs-lookup"><span data-stu-id="efd69-221">Instead, you can either:</span></span>

* <span data-ttu-id="efd69-222">Impostare una durata esplicita nella chiamata di [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview): `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="efd69-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="efd69-223">Usare le chiamate relative ai tempi di visualizzazione della pagina `startTrackPage` e `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="efd69-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="efd69-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="efd69-225">...</span><span class="sxs-lookup"><span data-stu-id="efd69-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="efd69-226">Il nome che si usa come primo parametro associa le chiamate di avvio e arresto.</span><span class="sxs-lookup"><span data-stu-id="efd69-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="efd69-227">Il valore predefinito corrisponde al nome della pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="efd69-227">It defaults to the current page name.</span></span>

<span data-ttu-id="efd69-228">I tempi di caricamento delle pagine visualizzati in Esplora metriche sono calcolati in base all'intervallo tra la chiamata di avvio e la chiamata di arresto.</span><span class="sxs-lookup"><span data-stu-id="efd69-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="efd69-229">È possibile specificare l'intervallo effettivo calcolato desiderato.</span><span class="sxs-lookup"><span data-stu-id="efd69-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="efd69-230">Dati di telemetria della pagina in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="efd69-231">In [Analytics](app-insights-analytics.md) due tabelle mostrano i dati delle operazioni del browser:</span><span class="sxs-lookup"><span data-stu-id="efd69-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="efd69-232">La tabella `pageViews` contiene i dati relativi al titolo della pagina e all'URL</span><span class="sxs-lookup"><span data-stu-id="efd69-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="efd69-233">La tabella `browserTimings` contiene i dati sulle prestazioni del client, ad esempio il tempo impiegato per elaborare i dati in ingresso</span><span class="sxs-lookup"><span data-stu-id="efd69-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="efd69-234">Per trovare il tempo necessario al browser per elaborare pagine diverse:</span><span class="sxs-lookup"><span data-stu-id="efd69-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="efd69-235">Per individuare le popolarità dei diversi browser:</span><span class="sxs-lookup"><span data-stu-id="efd69-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="efd69-236">Per associare le visualizzazioni di pagina alle chiamate AJAX, unirle alle dipendenze:</span><span class="sxs-lookup"><span data-stu-id="efd69-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="efd69-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="efd69-237">TrackRequest</span></span>
<span data-ttu-id="efd69-238">Il server SDK usa TrackRequest per registrare le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="efd69-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="efd69-239">È anche possibile chiamarlo manualmente se si vogliono simulare le richieste in un contesto in cui il modulo del servizio Web non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="efd69-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="efd69-240">Il modo consigliato per inviare dati di telemetria della richiesta è quello in cui la richiesta agisce come un <a href="#operation-context">contesto dell'operazione</a>.</span><span class="sxs-lookup"><span data-stu-id="efd69-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="efd69-241">Contesto dell'operazione</span><span class="sxs-lookup"><span data-stu-id="efd69-241">Operation context</span></span>
<span data-ttu-id="efd69-242">È possibile associare gli elementi di telemetria tra loro mediante il collegamento di un ID operazione comune.</span><span class="sxs-lookup"><span data-stu-id="efd69-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="efd69-243">Il modulo di rilevamento delle richieste standard esegue questa operazione per le eccezioni e gli altri eventi inviati durante l'elaborazione di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="efd69-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="efd69-244">In [Ricerca](app-insights-diagnostic-search.md) e [Analisi](app-insights-analytics.md) è possibile usare l'ID per trovare facilmente gli eventi associati alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="efd69-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="efd69-245">Il modo più semplice per impostare l'ID è selezionare un contesto dell'operazione mediante questo modello:</span><span class="sxs-lookup"><span data-stu-id="efd69-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="efd69-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="efd69-247">Oltre a impostare un contesto operativo, `StartOperation` crea un elemento di telemetria del tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="efd69-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="efd69-248">Invia l'elemento di telemetria quando si elimina l'operazione o si chiama esplicitamente `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="efd69-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="efd69-249">Se si usa `RequestTelemetry` come tipo di telemetria, la sua durata viene impostata sull'intervallo di tempo compreso tra l'avvio e l'arresto.</span><span class="sxs-lookup"><span data-stu-id="efd69-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="efd69-250">I contesti dell’operazione non possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="efd69-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="efd69-251">Se è già presente un contesto dell'operazione, il suo ID corrispondente viene associato a tutti gli elementi contenuti, compreso l'elemento creato con `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="efd69-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="efd69-252">In Ricerca il contesto dell'operazione viene usato per creare l'elenco di **elementi correlati**:</span><span class="sxs-lookup"><span data-stu-id="efd69-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Elementi correlati](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="efd69-254">Per altre informazioni sulle operazioni di rilevamento personalizzate, vedere [application-insights-custom-operations-tracking.md].</span><span class="sxs-lookup"><span data-stu-id="efd69-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="efd69-255">Richieste in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-255">Requests in Analytics</span></span> 

<span data-ttu-id="efd69-256">In [Analytics di Application Insights](app-insights-analytics.md) le richieste vengono visualizzate nella tabella `requests`.</span><span class="sxs-lookup"><span data-stu-id="efd69-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="efd69-257">Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostrerà un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="efd69-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="efd69-258">Per esempio itemCount==10 indica che su 10 chiamate a trackRequest(), il processo di campionamento ne trasmette solo una.</span><span class="sxs-lookup"><span data-stu-id="efd69-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="efd69-259">Per ottenere un conteggio corretto delle richieste e della durata media segmentato in base ai nomi della richiesta, usare un codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="efd69-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="efd69-260">TrackException</span></span>
<span data-ttu-id="efd69-261">Inviare le eccezioni ad Application Insights:</span><span class="sxs-lookup"><span data-stu-id="efd69-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="efd69-262">Per [contarle](app-insights-metrics-explorer.md), come indicazione della frequenza di un problema.</span><span class="sxs-lookup"><span data-stu-id="efd69-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="efd69-263">Per [esaminare le singole occorrenze](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="efd69-264">I report includono le analisi dello stack.</span><span class="sxs-lookup"><span data-stu-id="efd69-264">The reports include the stack traces.</span></span>

<span data-ttu-id="efd69-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="efd69-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="efd69-267">Gli SDK rilevano molte eccezioni automaticamente, quindi non è sempre necessario richiamare TrackException in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="efd69-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="efd69-268">ASP.NET: [Scrivere codice per intercettare le eccezioni](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="efd69-269">J2EE: [Le eccezioni vengono rilevate automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="efd69-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="efd69-270">JavaScript: Le eccezioni vengono rilevate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="efd69-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="efd69-271">Se si vuole disabilitare la raccolta automatica, aggiungere una riga al frammento di codice che si inserisce nelle pagine Web:</span><span class="sxs-lookup"><span data-stu-id="efd69-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="efd69-272">Eccezioni in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-272">Exceptions in Analytics</span></span>

<span data-ttu-id="efd69-273">In [Analytics di Application Insights](app-insights-analytics.md) le eccezioni vengono visualizzate nella tabella `exceptions`.</span><span class="sxs-lookup"><span data-stu-id="efd69-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="efd69-274">Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà `itemCount` mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="efd69-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="efd69-275">Per esempio itemCount==10 indica che su 10 chiamate a trackException(), il processo di campionamento ne trasmette solo una.</span><span class="sxs-lookup"><span data-stu-id="efd69-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="efd69-276">Per ottenere un conteggio corretto delle eccezioni segmentate per tipo di eccezione, usare un codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="efd69-277">La maggior parte delle informazioni importanti dello stack è già stata estratta in variabili distinte, ma è possibile separare la struttura `details` per ottenerne altre.</span><span class="sxs-lookup"><span data-stu-id="efd69-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="efd69-278">Poiché si tratta di una struttura dinamica, è necessario eseguire il cast del risultato per il tipo previsto.</span><span class="sxs-lookup"><span data-stu-id="efd69-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="efd69-279">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="efd69-280">Per associare le richieste alle eccezioni correlate, è possibile usare un join:</span><span class="sxs-lookup"><span data-stu-id="efd69-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="efd69-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="efd69-281">TrackTrace</span></span>
<span data-ttu-id="efd69-282">Usare TrackTrace per diagnosticare i problemi mediante l'invio di una traccia di navigazione ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="efd69-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="efd69-283">È possibile inviare blocchi di dati di diagnostica e controllarli in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="efd69-284">Gli [adattatori di log](app-insights-asp-net-trace-logs.md) usano questa API per inviare i log di terze parti al portale.</span><span class="sxs-lookup"><span data-stu-id="efd69-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="efd69-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="efd69-286">È possibile eseguire ricerche nel contenuto del messaggio, ma, a differenza dei valori delle proprietà, non è possibile filtrarlo.</span><span class="sxs-lookup"><span data-stu-id="efd69-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="efd69-287">Il limite delle dimensioni per `message` è molto superiore al limite per le proprietà.</span><span class="sxs-lookup"><span data-stu-id="efd69-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="efd69-288">Un vantaggio di TrackTrace è che è possibile inserire dati relativamente lunghi nel messaggio.</span><span class="sxs-lookup"><span data-stu-id="efd69-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="efd69-289">Ad esempio è possibile codificare dati POST.</span><span class="sxs-lookup"><span data-stu-id="efd69-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="efd69-290">È anche possibile aggiungere al messaggio un livello di gravità.</span><span class="sxs-lookup"><span data-stu-id="efd69-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="efd69-291">E come per altri tipi di dati di telemetria è possibile aggiungere valori di proprietà utili per filtrare o cercare set di tracce diversi.</span><span class="sxs-lookup"><span data-stu-id="efd69-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="efd69-292">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="efd69-293">In [Ricerca](app-insights-diagnostic-search.md) sarà possibile filtrare facilmente tutti i messaggi di un determinato livello di gravità relativi a un database specifico.</span><span class="sxs-lookup"><span data-stu-id="efd69-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="efd69-294">Tracce in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-294">Traces in Analytics</span></span>

<span data-ttu-id="efd69-295">In [Analytics di Application Insights](app-insights-analytics.md) le chiamate a TrackTrace vengono visualizzate nella tabella `traces`.</span><span class="sxs-lookup"><span data-stu-id="efd69-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="efd69-296">Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="efd69-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="efd69-297">Per esempio itemCount==10 indica che, su 10 chiamate di `trackTrace()`, il processo di campionamento ne trasmette solo una.</span><span class="sxs-lookup"><span data-stu-id="efd69-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="efd69-298">Per ottenere un conteggio corretto delle chiamate delle tracce, si consiglia di usare un codice, ad esempio `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="efd69-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="efd69-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="efd69-299">TrackDependency</span></span>
<span data-ttu-id="efd69-300">Usare la chiamata di TrackDependency per rilevare i tempi di risposta e le percentuali di successo delle chiamate a un frammento di codice esterno.</span><span class="sxs-lookup"><span data-stu-id="efd69-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="efd69-301">I risultati vengono visualizzati nei grafici dipendenze nel portale.</span><span class="sxs-lookup"><span data-stu-id="efd69-301">The results appear in the dependency charts in the portal.</span></span>

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

<span data-ttu-id="efd69-302">Tenere presente che il server SDK include un [modulo dipendenza](app-insights-asp-net-dependencies.md) che consente di individuare e tracciare alcune chiamate di dipendenza automaticamente, ad esempio a database e API REST.</span><span class="sxs-lookup"><span data-stu-id="efd69-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="efd69-303">È necessario installare un agente nel server per consentire il funzionamento del modulo.</span><span class="sxs-lookup"><span data-stu-id="efd69-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="efd69-304">Usare questa chiamata se si vuole tenere traccia di chiamate che il rilevamento automatico non intercetta o se non si vuole installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="efd69-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="efd69-305">Per disattivare il modulo standard per il rilevamento delle dipendenze, modificare il file [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) ed eliminare il riferimento a `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="efd69-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="efd69-306">Dipendenze in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-306">Dependencies in Analytics</span></span>

<span data-ttu-id="efd69-307">In [Analytics di Application Insights](app-insights-analytics.md) le chiamate a trackDependency vengono visualizzate nella tabella `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="efd69-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="efd69-308">Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="efd69-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="efd69-309">Per esempio itemCount==10 indica che su 10 chiamate a trackDependency(), il processo di campionamento ne trasmette solo una.</span><span class="sxs-lookup"><span data-stu-id="efd69-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="efd69-310">Per ottenere un conteggio corretto delle dipendenze segmentate per componente di destinazione, usare un codice, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="efd69-311">Per associare le dipendenze alle richieste correlate, è possibile usare un join:</span><span class="sxs-lookup"><span data-stu-id="efd69-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="efd69-312">Scaricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="efd69-312">Flushing data</span></span>
<span data-ttu-id="efd69-313">In genere l'SDK invia i dati in momenti scelti per ridurre al minimo l'impatto sull'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="efd69-314">In alcuni casi tuttavia è possibile che si voglia scaricare il buffer, ad esempio se si sta usando l'SDK in un'applicazione che si arresta.</span><span class="sxs-lookup"><span data-stu-id="efd69-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="efd69-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="efd69-316">Si noti che la funzione è asincrona per il [canale di telemetria del server](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="efd69-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="efd69-317">utenti autenticati</span><span class="sxs-lookup"><span data-stu-id="efd69-317">Authenticated users</span></span>
<span data-ttu-id="efd69-318">In un'app Web gli utenti sono identificati dai cookie per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="efd69-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="efd69-319">Un utente può essere conteggiato più volte se accede all'app da un computer o da un browser diverso o se elimina i cookie.</span><span class="sxs-lookup"><span data-stu-id="efd69-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="efd69-320">Se gli utenti accedono all'app, è possibile ottenere un conteggio più preciso impostando l'ID dell'utente autenticato nel codice del browser:</span><span class="sxs-lookup"><span data-stu-id="efd69-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="efd69-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="efd69-322">In un'applicazione MVC Web ASP.NET, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="efd69-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="efd69-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="efd69-324">Non è necessario usare il nome di accesso effettivo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="efd69-325">È sufficiente usare un ID univoco per l'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="efd69-326">Non deve includere spazi o i caratteri `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="efd69-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="efd69-327">L'ID utente viene inoltre impostato in un cookie di sessione e inviato al server.</span><span class="sxs-lookup"><span data-stu-id="efd69-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="efd69-328">Se l'SDK del server è installato, l'ID dell'utente autenticato viene inviato come parte delle proprietà contestuali della telemetria del client e del server.</span><span class="sxs-lookup"><span data-stu-id="efd69-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="efd69-329">Quindi sarà possibile filtrarlo ed eseguire ricerche al suo interno.</span><span class="sxs-lookup"><span data-stu-id="efd69-329">You can then filter and search on it.</span></span>

<span data-ttu-id="efd69-330">Se l'app raggruppa gli utenti in account, è anche possibile passare un identificatore per l'account, con le stesse limitazioni di caratteri.</span><span class="sxs-lookup"><span data-stu-id="efd69-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="efd69-331">In [Esplora metriche](app-insights-metrics-explorer.md) è possibile creare un grafico che conta i valori **Utenti, Autenticati** e **Account utente**.</span><span class="sxs-lookup"><span data-stu-id="efd69-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="efd69-332">È anche possibile [cercare](app-insights-diagnostic-search.md) i punti dati del client con account e nomi utente specifici.</span><span class="sxs-lookup"><span data-stu-id="efd69-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="efd69-333"><a name="properties"></a>Filtro, ricerca e segmentazione dei dati mediante le proprietà</span><span class="sxs-lookup"><span data-stu-id="efd69-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="efd69-334">È possibile associare proprietà e misure agli eventi e anche a metriche, visualizzazioni pagine, eccezioni e altri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="efd69-335">*proprietà* sono valori di stringa che è possibile usare per filtrare i dati di telemetria nei report di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="efd69-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="efd69-336">Ad esempio, se l'app offre più giochi, è possibile associare il nome del gioco a ogni evento per vedere quali sono i giochi più diffusi.</span><span class="sxs-lookup"><span data-stu-id="efd69-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="efd69-337">Esiste un limite di 8192 per la lunghezza della stringa.</span><span class="sxs-lookup"><span data-stu-id="efd69-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="efd69-338">Se si vogliono inviare grandi quantità di dati, usare il parametro del messaggio di [TrackTrace](#track-trace).</span><span class="sxs-lookup"><span data-stu-id="efd69-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="efd69-339">*metriche* sono valori numerici che possono essere rappresentati graficamente.</span><span class="sxs-lookup"><span data-stu-id="efd69-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="efd69-340">Ad esempio è possibile verificare se esiste un aumento graduale nei punteggi raggiunti dai giocatori.</span><span class="sxs-lookup"><span data-stu-id="efd69-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="efd69-341">I grafici possono essere segmentati in base alle proprietà inviate con l'evento, in modo da ottenere grafici separati o in pila per giochi diversi.</span><span class="sxs-lookup"><span data-stu-id="efd69-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="efd69-342">Affinché i valori metrici siano visualizzati correttamente, devono essere maggiori o uguali a 0.</span><span class="sxs-lookup"><span data-stu-id="efd69-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="efd69-343">Esistono tuttavia alcuni [limiti sul numero di proprietà, di valori delle proprietà e di metriche](#limits) che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="efd69-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="efd69-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-344">*JavaScript*</span></span>

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


<span data-ttu-id="efd69-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="efd69-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="efd69-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="efd69-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="efd69-348">Assicurarsi di non registrare informazioni personali nelle proprietà.</span><span class="sxs-lookup"><span data-stu-id="efd69-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="efd69-349">*Se è stata usata la metrica*, aprire Esplora metriche e selezionare la metrica dal gruppo **personalizzato**:</span><span class="sxs-lookup"><span data-stu-id="efd69-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Aprire Esplora metrica, selezionare il grafico e selezionare la metrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="efd69-351">Se non viene visualizzata l'unità di misura o se l'intestazione **personalizzata** non è presente, chiudere il pannello di selezione e riprovare più tardi.</span><span class="sxs-lookup"><span data-stu-id="efd69-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="efd69-352">A volte potrebbe essere necessaria un'ora per l'aggregazione delle metriche attraverso la pipeline.</span><span class="sxs-lookup"><span data-stu-id="efd69-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="efd69-353">*Se si usano proprietà e metriche*, segmentare la metrica in base alla proprietà:</span><span class="sxs-lookup"><span data-stu-id="efd69-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Impostare il raggruppamento e quindi selezionare la proprietà in Raggruppa per](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="efd69-355">In *Ricerca diagnostica* è possibile visualizzare le proprietà e le metriche di singole occorrenze di un evento.</span><span class="sxs-lookup"><span data-stu-id="efd69-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Selezionare un'istanza e quindi scegliere "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="efd69-357">Usare il campo **Ricerca** per visualizzare le occorrenze di eventi con un valore della proprietà particolare.</span><span class="sxs-lookup"><span data-stu-id="efd69-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Digitare un termine in Ricerca](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="efd69-359">[Altre informazioni sulle espressioni di ricerca](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="efd69-360">Metodo alternativo per impostare proprietà e metriche</span><span class="sxs-lookup"><span data-stu-id="efd69-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="efd69-361">Se si preferisce, è possibile raccogliere i parametri di un evento in un oggetto separato:</span><span class="sxs-lookup"><span data-stu-id="efd69-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="efd69-362">Non riusare la stessa istanza dell'elemento di telemetria, `event` in questo esempio, per chiamare Track*() più volte.</span><span class="sxs-lookup"><span data-stu-id="efd69-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="efd69-363">Potrebbe causare l'invio della telemetria con una configurazione errata.</span><span class="sxs-lookup"><span data-stu-id="efd69-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="efd69-364">Misure e proprietà personalizzate in Analytics</span><span class="sxs-lookup"><span data-stu-id="efd69-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="efd69-365">In [Analytics](app-insights-analytics.md) le metriche e le proprietà personalizzate vengono mostrate negli attributi `customMeasurements` e `customDimensions` di ogni record di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="efd69-366">Ad esempio, se è stata aggiunta una proprietà denominata "game" ai dati di telemetria della richiesta, questa query conta le occorrenze di diversi valori di "game" e mostrerà la media del "punteggio" della metrica personalizzata:</span><span class="sxs-lookup"><span data-stu-id="efd69-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="efd69-367">Si noti che:</span><span class="sxs-lookup"><span data-stu-id="efd69-367">Notice that:</span></span>

* <span data-ttu-id="efd69-368">Quando si estrae un valore dal JSON customDimensions o customMeasurements, questo è di tipo dinamico e pertanto è necessario eseguirne il cast in `tostring` o `todouble`.</span><span class="sxs-lookup"><span data-stu-id="efd69-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="efd69-369">Per tener conto della possibilità di [campionamento](app-insights-sampling.md), si consiglia di usare `sum(itemCount)`, non `count()`.</span><span class="sxs-lookup"><span data-stu-id="efd69-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="efd69-370"><a name="timed"></a> Temporizzazione degli eventi</span><span class="sxs-lookup"><span data-stu-id="efd69-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="efd69-371">A volte si vuole rappresentare in un grafico il tempo necessario per eseguire un'azione.</span><span class="sxs-lookup"><span data-stu-id="efd69-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="efd69-372">Ad esempio si potrebbe voler sapere quanto tempo occorre agli utenti per scegliere tra le opzioni disponibili in un gioco.</span><span class="sxs-lookup"><span data-stu-id="efd69-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="efd69-373">Per questo è possibile usare il parametro di misurazione.</span><span class="sxs-lookup"><span data-stu-id="efd69-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="efd69-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="efd69-375"><a name="defaults"></a>Proprietà predefinite per i dati di telemetria personalizzati</span><span class="sxs-lookup"><span data-stu-id="efd69-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="efd69-376">Se si intende impostare solo i valori di proprietà predefiniti per alcuni degli eventi personalizzati scritti, è possibile impostarli in un'istanza di TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="efd69-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="efd69-377">Vengono associati a ogni elemento di telemetria inviato da quel client.</span><span class="sxs-lookup"><span data-stu-id="efd69-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="efd69-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="efd69-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="efd69-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="efd69-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="efd69-381">Le singole chiamate di telemetria possono sostituire i valori predefiniti nei relativi dizionari delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="efd69-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="efd69-382">*Per i client Web di JavaScript*, [usare gli inizializzatori di telemetria JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="efd69-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="efd69-383">*Per aggiungere proprietà a tutti i dati di telemetria*, inclusi i dati dei moduli di raccolta standard, [implementare `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="efd69-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="efd69-384">Campionamento, filtri ed elaborazione dei dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="efd69-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="efd69-385">È possibile scrivere il codice per elaborare i dati di telemetria prima che vengano inviati dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="efd69-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="efd69-386">L'elaborazione include i dati inviati dai moduli di telemetria standard, come la raccolta delle richieste HTTP e la raccolta delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="efd69-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="efd69-387">[Aggiungere proprietà](app-insights-api-filtering-sampling.md#add-properties) ai dati di telemetria implementando `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="efd69-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="efd69-388">Ad esempio è possibile aggiungere numeri di versione o valori calcolati da altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="efd69-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="efd69-389">L'[applicazione di filtri](app-insights-api-filtering-sampling.md#filtering) consente di modificare o rimuovere i dati di telemetria prima che vengano inviati dall'SDK implementando `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="efd69-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="efd69-390">È possibile controllare gli elementi inviati o eliminati, ma è necessario tenere conto dell'effetto sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="efd69-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="efd69-391">A seconda di come si eliminano gli elementi, si potrebbe perdere la possibilità di navigare tra elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="efd69-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="efd69-392">Il [campionamento](app-insights-api-filtering-sampling.md) è una soluzione in pacchetto che consente di ridurre il volume dei dati inviati dall'app al portale.</span><span class="sxs-lookup"><span data-stu-id="efd69-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="efd69-393">Lo fa senza influenzare le metriche visualizzate</span><span class="sxs-lookup"><span data-stu-id="efd69-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="efd69-394">e senza influire sulla possibilità di diagnosticare i problemi navigando tra elementi correlati, come eccezioni, richieste e visualizzazioni di pagina.</span><span class="sxs-lookup"><span data-stu-id="efd69-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="efd69-395">[Altre informazioni](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="efd69-396">Disabilitazione della telemetria</span><span class="sxs-lookup"><span data-stu-id="efd69-396">Disabling telemetry</span></span>
<span data-ttu-id="efd69-397">Per *avviare e arrestare in modo dinamico* la raccolta e la trasmissione di dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="efd69-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="efd69-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="efd69-399">Per *disabilitare gli agenti di raccolta standard selezionati*, ad esempio contatori delle prestazioni, richieste HTTP o dipendenze, eliminare o impostare come commento le righe pertinenti in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Ad esempio è possibile eseguire questa operazione se si desidera inviare i propri dati TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="efd69-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="efd69-400"><a name="debug"></a>Modalità di sviluppo</span><span class="sxs-lookup"><span data-stu-id="efd69-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="efd69-401">Durante il debug, è utile accelerare i dati di telemetria venga nella pipeline in modo da visualizzare immediatamente i risultati.</span><span class="sxs-lookup"><span data-stu-id="efd69-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="efd69-402">È possibile che vengano visualizzati anche altri messaggi che consentono di tracciare eventuali problemi con i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="efd69-403">Disattivare questa modalità in fase di produzione poiché potrebbe rallentare l'app.</span><span class="sxs-lookup"><span data-stu-id="efd69-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="efd69-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="efd69-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="efd69-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="efd69-406"><a name="ikey"></a> Impostazione della chiave di strumentazione per la telemetria personalizzata selezionata</span><span class="sxs-lookup"><span data-stu-id="efd69-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="efd69-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="efd69-408"><a name="dynamic-ikey"></a> Chiave di strumentazione dinamica</span><span class="sxs-lookup"><span data-stu-id="efd69-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="efd69-409">Per evitare di combinare i dati di telemetria di ambienti di sviluppo, test e produzione, è possibile [creare risorse distinte di Application Insights](app-insights-create-new-resource.md) e modificare le relative chiavi a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="efd69-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="efd69-410">Invece di ottenere la chiave di strumentazione dal file di configurazione, è possibile impostarla nel codice.</span><span class="sxs-lookup"><span data-stu-id="efd69-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="efd69-411">Impostare la chiave in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="efd69-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="efd69-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="efd69-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="efd69-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="efd69-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="efd69-414">Nelle pagine Web è possibile impostarla dallo stato del server Web anziché codificarla nello script.</span><span class="sxs-lookup"><span data-stu-id="efd69-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="efd69-415">Ad esempio, in una pagina Web generata in un'app ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="efd69-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="efd69-416">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="efd69-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="efd69-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="efd69-417">TelemetryContext</span></span>
<span data-ttu-id="efd69-418">TelemetryClient dispone di una proprietà Context contenente valori che vengono inviati insieme a tutti i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="efd69-419">Sono in genere impostati dai moduli di telemetria standard, ma è possibile anche impostarli manualmente.</span><span class="sxs-lookup"><span data-stu-id="efd69-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="efd69-420">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="efd69-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="efd69-421">Se si imposta uno di questi valori manualmente, provare a rimuovere la riga pertinente da [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), in modo che i valori personali e quelli standard non si confondano.</span><span class="sxs-lookup"><span data-stu-id="efd69-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="efd69-422">**Componente**: l'app e la relativa versione.</span><span class="sxs-lookup"><span data-stu-id="efd69-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="efd69-423">**Dispositivo**: dati relativi al dispositivo in cui l'applicazione è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="efd69-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="efd69-424">Nelle App Web questo è il server o dispositivo client da cui sono inviati i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="efd69-425">**InstrumentationKey**: la risorsa di Application Insights in Azure dove sono visualizzati i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="efd69-426">Viene in genere presa dal file ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="efd69-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="efd69-427">**Posizione**: la posizione geografica del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="efd69-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="efd69-428">**Operazione**: nelle App Web la richiesta HTTP corrente.</span><span class="sxs-lookup"><span data-stu-id="efd69-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="efd69-429">In altri tipi di app è possibile impostarla in modo da raggruppare gli eventi tra loro.</span><span class="sxs-lookup"><span data-stu-id="efd69-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="efd69-430">**ID**: un valore generato che mette in correlazione eventi diversi, in modo che quando si analizza qualsiasi evento in Ricerca diagnostica, è possibile trovare elementi correlati.</span><span class="sxs-lookup"><span data-stu-id="efd69-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="efd69-431">**Nome**: un identificatore, in genere l'URL della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="efd69-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="efd69-432">**SyntheticSource**: se non è null o vuota, una stringa indicante che l'origine della richiesta è stata identificata come un test Web o un robot.</span><span class="sxs-lookup"><span data-stu-id="efd69-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="efd69-433">Per impostazione predefinita viene esclusa dai calcoli in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="efd69-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="efd69-434">**Proprietà**: proprietà che vengono inviate con tutti i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="efd69-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="efd69-435">È possibile eseguire l'override di questo valore in singole chiamate di Track*.</span><span class="sxs-lookup"><span data-stu-id="efd69-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="efd69-436">**Sessione**: la sessione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-436">**Session**: The user's session.</span></span> <span data-ttu-id="efd69-437">L'ID viene impostato su un valore generato, che viene modificato quando l'utente non è stato attivo per un periodo di tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="efd69-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="efd69-438">**Utente**: le informazioni dell'utente.</span><span class="sxs-lookup"><span data-stu-id="efd69-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="efd69-439">Limiti</span><span class="sxs-lookup"><span data-stu-id="efd69-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="efd69-440">Per evitare di raggiungere il limite di velocità dei dati usare il [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="efd69-441">Per determinare quanto tempo vengono conservati i dati, vedere [Raccolta, conservazione e archiviazione di dati in Application Insights](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="efd69-442">Documentazione di riferimento</span><span class="sxs-lookup"><span data-stu-id="efd69-442">Reference docs</span></span>
* [<span data-ttu-id="efd69-443">Riferimento ASP.NET</span><span class="sxs-lookup"><span data-stu-id="efd69-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="efd69-444">Riferimento Java</span><span class="sxs-lookup"><span data-stu-id="efd69-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="efd69-445">Informazioni di riferimento su JavaScript</span><span class="sxs-lookup"><span data-stu-id="efd69-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="efd69-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="efd69-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="efd69-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="efd69-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="efd69-448">Codice SDK</span><span class="sxs-lookup"><span data-stu-id="efd69-448">SDK code</span></span>
* [<span data-ttu-id="efd69-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="efd69-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="efd69-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="efd69-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="efd69-451">Pacchetti per Windows Server</span><span class="sxs-lookup"><span data-stu-id="efd69-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="efd69-452">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="efd69-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="efd69-453">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="efd69-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="efd69-454">Tutte le piattaforme</span><span class="sxs-lookup"><span data-stu-id="efd69-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="efd69-455">Domande</span><span class="sxs-lookup"><span data-stu-id="efd69-455">Questions</span></span>
* <span data-ttu-id="efd69-456">*Quali eccezioni potrebbero essere generate dalle chiamate Track_()?*</span><span class="sxs-lookup"><span data-stu-id="efd69-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="efd69-457">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="efd69-457">None.</span></span> <span data-ttu-id="efd69-458">Non è necessario eseguirne il wrapping in clausole try-catch.</span><span class="sxs-lookup"><span data-stu-id="efd69-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="efd69-459">Se l'SDK rileva un problema, registrerà messaggi nell'output della console di debug e quindi in Ricerca diagnostica per approfondirne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="efd69-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="efd69-460">*Esiste un'API REST per ottenere dati dal portale?*</span><span class="sxs-lookup"><span data-stu-id="efd69-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="efd69-461">Sì, l'[API di accesso ai dati](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="efd69-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="efd69-462">Altri modi per estrarre i dati sono l'[esportazione da Analytics a Power BI](app-insights-export-power-bi.md) e l'[esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="efd69-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="efd69-463"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efd69-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="efd69-464">Ricerca di eventi e log</span><span class="sxs-lookup"><span data-stu-id="efd69-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="efd69-465">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="efd69-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


