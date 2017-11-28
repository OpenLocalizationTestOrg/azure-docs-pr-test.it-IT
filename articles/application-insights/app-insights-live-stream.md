---
title: Flusso di metrica con metriche personalizzate e di diagnostica in Azure Application Insights aaaLive | Documenti Microsoft
description: Monitorare l'app Web in tempo reale, con metriche personalizzate e diagnosticare problemi con un feed live di errori, tracce ed eventi.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="b9c52-103">Live Metrics Stream: monitorare e diagnosticare con una latenza di 1 secondo</span><span class="sxs-lookup"><span data-stu-id="b9c52-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="b9c52-104">Probe cuore heartbeat hello dell'applicazione web in tempo reale, in produzione utilizzando il flusso di metriche in tempo reale da [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9c52-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b9c52-105">Selezionare e filtrare le metriche e le prestazioni toowatch contatori in tempo reale, senza alcun servizio tooyour disturbi.</span><span class="sxs-lookup"><span data-stu-id="b9c52-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="b9c52-106">Esaminare le analisi dello stack da richieste ed eccezioni di esempio non riuscite.</span><span class="sxs-lookup"><span data-stu-id="b9c52-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="b9c52-107">Insieme al [Profiler](app-insights-profiler.md), al [debugger di snapshot](app-insights-snapshot-debugger.md) e [al test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests), Live Metrics Stream offre uno strumento di diagnostica non invasivo e potente per il sito Web live.</span><span class="sxs-lookup"><span data-stu-id="b9c52-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="b9c52-108">Con Live Metrics Stream, è possibile:</span><span class="sxs-lookup"><span data-stu-id="b9c52-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="b9c52-109">Convalidare una correzione durante il rilasciato, osservando i contatori delle prestazioni e degli errori.</span><span class="sxs-lookup"><span data-stu-id="b9c52-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="b9c52-110">Guardare effetto hello del test di carico e diagnosticare i problemi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b9c52-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="b9c52-111">Concentrarsi sulle sessioni di test specifico o filtrare le problemi noti, selezione e filtro metriche hello da toowatch.</span><span class="sxs-lookup"><span data-stu-id="b9c52-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="b9c52-112">Ottenere le eccezioni delle tracce in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b9c52-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="b9c52-113">Provare varie combinazioni di filtri toofind hello KPI più rilevanti.</span><span class="sxs-lookup"><span data-stu-id="b9c52-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="b9c52-114">Monitorare ogni contatore delle prestazioni di Windows live.</span><span class="sxs-lookup"><span data-stu-id="b9c52-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="b9c52-115">Identificare un server che si verificano problemi e facilmente filtrare tutti hello KPI/live toojust feed che il server.</span><span class="sxs-lookup"><span data-stu-id="b9c52-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="b9c52-116">[![Video di Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="b9c52-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="b9c52-117">Flusso di metriche in tempo reale è attualmente disponibile per le app di ASP.NET in esecuzione in locale o nel Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="b9c52-118">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="b9c52-118">Get started</span></span>

1. <span data-ttu-id="b9c52-119">Se [Application Insights](app-insights-asp-net.md) non è stato ancora installato nell'app Web ASP.NET o nell'[app del server Windows](app-insights-windows-services.md), è possibile farlo ora.</span><span class="sxs-lookup"><span data-stu-id="b9c52-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="b9c52-120">**Versione più recente di aggiornamento toohello** del pacchetto di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="b9c52-121">In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b9c52-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="b9c52-122">Aprire hello **aggiornamenti** scheda **Includi versione preliminare**e selezionare tutti i pacchetti hello Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="b9c52-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="b9c52-123">Ridistribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="b9c52-123">Redeploy your app.</span></span>

3. <span data-ttu-id="b9c52-124">In hello [portale di Azure](https://portal.azure.com), aprire la risorsa di Application Insights hello per l'app e quindi aprire il flusso in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="b9c52-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="b9c52-125">[Il canale di controllo sicura hello](#secure-the-control-channel) se è possibile utilizzare i dati sensibili, ad esempio i nomi dei clienti nei filtri.</span><span class="sxs-lookup"><span data-stu-id="b9c52-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Nel pannello della panoramica hello, fare clic su un flusso in tempo reale](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="b9c52-127">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="b9c52-127">No data?</span></span> <span data-ttu-id="b9c52-128">Controllare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="b9c52-128">Check your server firewall</span></span>

<span data-ttu-id="b9c52-129">Controllare hello [in uscita di porte per il flusso di metriche in tempo reale](app-insights-ip-addresses.md#outgoing-ports) aperte nel firewall hello del server.</span><span class="sxs-lookup"><span data-stu-id="b9c52-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="b9c52-130">Differenze tra Live Metrics Stream ed Esplora metriche e Analisi</span><span class="sxs-lookup"><span data-stu-id="b9c52-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="b9c52-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="b9c52-131">Live Stream</span></span> | <span data-ttu-id="b9c52-132">Esplora metriche e Analisi</span><span class="sxs-lookup"><span data-stu-id="b9c52-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="b9c52-133">Latency</span><span class="sxs-lookup"><span data-stu-id="b9c52-133">Latency</span></span>|<span data-ttu-id="b9c52-134">Dati visualizzati in un secondo</span><span class="sxs-lookup"><span data-stu-id="b9c52-134">Data displayed within one second</span></span>|<span data-ttu-id="b9c52-135">Aggregati in minuti</span><span class="sxs-lookup"><span data-stu-id="b9c52-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="b9c52-136">Nessuna conservazione</span><span class="sxs-lookup"><span data-stu-id="b9c52-136">No retention</span></span>|<span data-ttu-id="b9c52-137">Dati persiste mentre nel grafico hello e viene eliminata</span><span class="sxs-lookup"><span data-stu-id="b9c52-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="b9c52-138">Dati mantenuti per 90 giorni</span><span class="sxs-lookup"><span data-stu-id="b9c52-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="b9c52-139">On demand</span><span class="sxs-lookup"><span data-stu-id="b9c52-139">On demand</span></span>|<span data-ttu-id="b9c52-140">I dati vengono trasmessi durante l'apertura di Live Metrics</span><span class="sxs-lookup"><span data-stu-id="b9c52-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="b9c52-141">I dati vengono inviati ogni volta che hello SDK viene installato e attivato</span><span class="sxs-lookup"><span data-stu-id="b9c52-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="b9c52-142">Free</span><span class="sxs-lookup"><span data-stu-id="b9c52-142">Free</span></span>|<span data-ttu-id="b9c52-143">Non sono previste spese per i dati di Live Stream</span><span class="sxs-lookup"><span data-stu-id="b9c52-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="b9c52-144">Oggetto troppo[prezzi](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="b9c52-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="b9c52-145">campionamento</span><span class="sxs-lookup"><span data-stu-id="b9c52-145">Sampling</span></span>|<span data-ttu-id="b9c52-146">Tutte le metriche selezionate e i contatori vengono trasmessi.</span><span class="sxs-lookup"><span data-stu-id="b9c52-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="b9c52-147">Gli errori e le analisi dello stack vengono usati come esempi.</span><span class="sxs-lookup"><span data-stu-id="b9c52-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="b9c52-148">TelemetryProcessors non viene applicato.</span><span class="sxs-lookup"><span data-stu-id="b9c52-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="b9c52-149">Eventi potrebbero essere usati come [esempi](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="b9c52-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="b9c52-150">Canale di controllo</span><span class="sxs-lookup"><span data-stu-id="b9c52-150">Control channel</span></span>|<span data-ttu-id="b9c52-151">I segnali di filtro vengono inviati toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="b9c52-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="b9c52-152">È consigliabile [proteggere questo canale](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="b9c52-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="b9c52-153">La comunicazione è unidirezionale, toohello portale</span><span class="sxs-lookup"><span data-stu-id="b9c52-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="b9c52-154">Selezionare e filtrare le metriche</span><span class="sxs-lookup"><span data-stu-id="b9c52-154">Select and filter your metrics</span></span>

<span data-ttu-id="b9c52-155">(Disponibile in versione classica App ASP.NET con hello SDK più recente.)</span><span class="sxs-lookup"><span data-stu-id="b9c52-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="b9c52-156">È possibile monitorare i KPI personalizzato in tempo reale applicando filtri arbitrari a qualsiasi telemetria di Application Insights dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="b9c52-157">Fare clic su controllo filtro hello che mostra quando si del puntatore del mouse uno qualsiasi dei grafici hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="b9c52-158">Hello seguente grafico viene tracciato un numero di richieste personalizzato KPI con filtri sugli attributi di URL e la durata.</span><span class="sxs-lookup"><span data-stu-id="b9c52-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="b9c52-159">Convalidare i filtri con hello sezione di anteprima di flusso che mostra un feed in tempo reale di dati di telemetria che corrisponde ai criteri di hello che è stato specificato in qualsiasi punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="b9c52-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![Indicatore KPI di richieste personalizzato](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="b9c52-161">È possibile monitorare un valore diverso dal conteggio.</span><span class="sxs-lookup"><span data-stu-id="b9c52-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="b9c52-162">opzioni di Hello dipendono dal tipo di hello del flusso, che può essere qualsiasi telemetria di Application Insights: le richieste, dipendenze, eccezioni, le tracce, eventi o metriche.</span><span class="sxs-lookup"><span data-stu-id="b9c52-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="b9c52-163">Può essere la propria [misura personalizzata](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="b9c52-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opzioni del valore](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="b9c52-165">Inoltre tooApplication telemetria Insights, è anche possibile monitorare qualsiasi contatore delle prestazioni di Windows che selezionando una delle opzioni flusso hello e fornendo il nome di hello hello del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b9c52-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="b9c52-166">Le metriche attive vengono aggregate in due punti: in locale su ciascun server e quindi su tutti i server.</span><span class="sxs-lookup"><span data-stu-id="b9c52-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="b9c52-167">È possibile modificare l'impostazione predefinita hello in è possibile selezionare altre opzioni in hello rispettivi elenchi a discesa.</span><span class="sxs-lookup"><span data-stu-id="b9c52-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="b9c52-168">Telemetria di esempio: eventi di diagnostica live personalizzati</span><span class="sxs-lookup"><span data-stu-id="b9c52-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="b9c52-169">Per impostazione predefinita, il feed in tempo reale di hello degli eventi vengono mostrati esempi di richieste non riuscite e chiamate a dipendenze, eccezioni, eventi e tracce.</span><span class="sxs-lookup"><span data-stu-id="b9c52-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="b9c52-170">Fare clic su hello icona toosee hello applicato criteri del filtro in qualsiasi punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="b9c52-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Feed live predefinito](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="b9c52-172">Come con le metriche, è possibile specificare qualsiasi tooany criteri arbitrari di tipi di dati di telemetria di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="b9c52-173">In questo esempio, vengono selezionati eventi, tracce e richieste non riuscite specifiche.</span><span class="sxs-lookup"><span data-stu-id="b9c52-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="b9c52-174">Vengono selezionate anche tutte le eccezioni e gli errori di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="b9c52-174">We are also selecting all exceptions and dependency failures.</span></span>

![Feed live personalizzati](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="b9c52-176">Nota: Attualmente, per i criteri basata su messaggi di eccezione, utilizzare il messaggio di eccezione più esterno hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="b9c52-177">Nell'esempio sopra riportato, hello toofilter out eccezione grave di hello con messaggio di eccezione interna (segue hello "<-" delimitatore) "hello client si è disconnesso."</span><span class="sxs-lookup"><span data-stu-id="b9c52-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="b9c52-178">usare un criterio che non contiene il messaggio "Errore durante la lettura del contenuto della richiesta".</span><span class="sxs-lookup"><span data-stu-id="b9c52-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="b9c52-179">Vedere i dettagli di hello di un elemento in hello live feed facendovi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="b9c52-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="b9c52-180">È possibile sospendere hello feed, fare clic su **sospendere** semplicemente scorrendo verso il basso o facendo clic su un elemento.</span><span class="sxs-lookup"><span data-stu-id="b9c52-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="b9c52-181">Feed Live verrà ripresa dopo lo scorrimento indietro toohello top o facendo clic sul contatore hello degli elementi raccolti mentre era stato sospeso.</span><span class="sxs-lookup"><span data-stu-id="b9c52-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Errori live campionati](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="b9c52-183">Filtro per istanza di server</span><span class="sxs-lookup"><span data-stu-id="b9c52-183">Filter by server instance</span></span>

<span data-ttu-id="b9c52-184">Se si desidera toomonitor un'istanza del ruolo server specifico, è possibile filtrare dal server.</span><span class="sxs-lookup"><span data-stu-id="b9c52-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Errori live campionati](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="b9c52-186">Requisiti SDK</span><span class="sxs-lookup"><span data-stu-id="b9c52-186">SDK Requirements</span></span>
<span data-ttu-id="b9c52-187">Live Metrics Stream personalizzato è disponibile con la versione 2.4.0-beta2 o più recente di [Application Insights SDK per il Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="b9c52-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="b9c52-188">Memorizza l'opzione "Includi versione provvisoria" tooselect da Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="b9c52-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="b9c52-189">Proteggere il canale di controllo di hello</span><span class="sxs-lookup"><span data-stu-id="b9c52-189">Secure hello control channel</span></span>
<span data-ttu-id="b9c52-190">Hello personalizzato i filtri i criteri specificati vengono inviati componente di metriche in tempo reale toohello indietro hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="b9c52-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="b9c52-191">i filtri di Hello potrebbero contenere informazioni riservate, ad esempio ID cliente.</span><span class="sxs-lookup"><span data-stu-id="b9c52-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="b9c52-192">È possibile apportare canale hello protetta con una chiave segreta di API inoltre toohello chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="b9c52-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="b9c52-193">Creare una chiave API</span><span class="sxs-lookup"><span data-stu-id="b9c52-193">Create an API Key</span></span>

![Creare una chiave API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="b9c52-195">Aggiungere tooConfiguration chiave API</span><span class="sxs-lookup"><span data-stu-id="b9c52-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="b9c52-196">Nel file applicationinsights config hello, aggiungere hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="b9c52-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="b9c52-197">O nel codice, impostare su hello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="b9c52-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="b9c52-198">Tuttavia, se e attendibile che tutti hello server collegati, è possibile provare i filtri personalizzati hello senza canale hello autenticato.</span><span class="sxs-lookup"><span data-stu-id="b9c52-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="b9c52-199">Questa opzione è disponibile per sei mesi.</span><span class="sxs-lookup"><span data-stu-id="b9c52-199">This option is available for six months.</span></span> <span data-ttu-id="b9c52-200">Questa sostituzione è necessaria una volta per ogni nuova sessione oppure quando un nuovo server è online.</span><span class="sxs-lookup"><span data-stu-id="b9c52-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opzioni di autenticazione delle metriche attive](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="b9c52-202">È consigliabile impostare canale hello autenticato prima di immettere informazioni potenzialmente riservate, ad esempio CustomerID in Criteri di filtro hello.</span><span class="sxs-lookup"><span data-stu-id="b9c52-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="b9c52-203">Generazione di un carico di test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="b9c52-203">Generating a performance test load</span></span>

<span data-ttu-id="b9c52-204">Se si desidera effetto hello toowatch di un carico aumenta, utilizzare hello Test delle prestazioni blade.</span><span class="sxs-lookup"><span data-stu-id="b9c52-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="b9c52-205">Simula le richieste da un certo numero di utenti simultanei.</span><span class="sxs-lookup"><span data-stu-id="b9c52-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="b9c52-206">È possibile eseguire entrambi "test manuale" (ping test) di un singolo URL o può essere eseguito un [test delle prestazioni web multipassaggio](app-insights-monitor-web-app-availability.md#multi-step-web-tests) caricare (in hello stesso modo come una disponibilità di test).</span><span class="sxs-lookup"><span data-stu-id="b9c52-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="b9c52-207">Dopo aver creato i test delle prestazioni di hello, aprire test hello e hello pannello flusso Live in finestre distinte.</span><span class="sxs-lookup"><span data-stu-id="b9c52-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="b9c52-208">È possibile vedere quando hello in coda Avvia test delle prestazioni e flusso in tempo reale di espressioni di controllo in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b9c52-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="b9c52-209">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b9c52-209">Troubleshooting</span></span>

<span data-ttu-id="b9c52-210">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="b9c52-210">No data?</span></span> <span data-ttu-id="b9c52-211">Se l'applicazione si trova in una rete protetta: Live Metrics Stream usa un indirizzo IP diverso dagli altri dati di Application Insights Telemetry.</span><span class="sxs-lookup"><span data-stu-id="b9c52-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="b9c52-212">Assicurarsi che [tali indirizzi IP](app-insights-ip-addresses.md) siano aperti nel firewall.</span><span class="sxs-lookup"><span data-stu-id="b9c52-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b9c52-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9c52-213">Next steps</span></span>
* [<span data-ttu-id="b9c52-214">Monitoraggio dell'utilizzo con Application Insights</span><span class="sxs-lookup"><span data-stu-id="b9c52-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="b9c52-215">Uso di Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="b9c52-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b9c52-216">Profiler</span><span class="sxs-lookup"><span data-stu-id="b9c52-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="b9c52-217">Debugger di snapshot</span><span class="sxs-lookup"><span data-stu-id="b9c52-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
