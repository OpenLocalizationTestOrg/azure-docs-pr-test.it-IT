---
title: Live Metrics Stream con diagnostica e metriche personalizzate in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="00a6c-103">Live Metrics Stream: monitorare e diagnosticare con una latenza di 1 secondo</span><span class="sxs-lookup"><span data-stu-id="00a6c-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="00a6c-104">Usando Live Metrics Stream da [Application Insights](app-insights-overview.md) è possibile testare il funzionamento dell'applicazione Web live nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="00a6c-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="00a6c-105">Selezionare e filtrare le metriche e i contatori delle prestazioni in tempo reale, senza distorsioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="00a6c-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="00a6c-106">Esaminare le analisi dello stack da richieste ed eccezioni di esempio non riuscite.</span><span class="sxs-lookup"><span data-stu-id="00a6c-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="00a6c-107">Insieme al [Profiler](app-insights-profiler.md), al [debugger di snapshot](app-insights-snapshot-debugger.md) e [al test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests), Live Metrics Stream offre uno strumento di diagnostica non invasivo e potente per il sito Web live.</span><span class="sxs-lookup"><span data-stu-id="00a6c-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="00a6c-108">Con Live Metrics Stream, è possibile:</span><span class="sxs-lookup"><span data-stu-id="00a6c-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="00a6c-109">Convalidare una correzione durante il rilasciato, osservando i contatori delle prestazioni e degli errori.</span><span class="sxs-lookup"><span data-stu-id="00a6c-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="00a6c-110">Osservare l'effetto dei carichi di test e diagnosticare i problemi live.</span><span class="sxs-lookup"><span data-stu-id="00a6c-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="00a6c-111">Concentrarsi sulle sessioni di test specifiche o filtrare i problemi noti, selezionando e filtrando le metriche che si desidera osservare.</span><span class="sxs-lookup"><span data-stu-id="00a6c-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="00a6c-112">Ottenere le eccezioni delle tracce in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="00a6c-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="00a6c-113">Provare a usare i filtri per individuare gli indicatori di prestazioni chiave più rilevanti.</span><span class="sxs-lookup"><span data-stu-id="00a6c-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="00a6c-114">Monitorare ogni contatore delle prestazioni di Windows live.</span><span class="sxs-lookup"><span data-stu-id="00a6c-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="00a6c-115">Identificare facilmente un server che presenta problemi e filtrare tutti gli indicatori KPI o i feed live solo per tale server.</span><span class="sxs-lookup"><span data-stu-id="00a6c-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="00a6c-116">[![Video di Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="00a6c-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="00a6c-117">Live Metrics Stream è attualmente disponibile nelle app ASP.NET in esecuzione in locale o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="00a6c-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="00a6c-118">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="00a6c-118">Get started</span></span>

1. <span data-ttu-id="00a6c-119">Se [Application Insights](app-insights-asp-net.md) non è stato ancora installato nell'app Web ASP.NET o nell'[app del server Windows](app-insights-windows-services.md), è possibile farlo ora.</span><span class="sxs-lookup"><span data-stu-id="00a6c-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="00a6c-120">**Eseguire l'aggiornamento alla versione più recente** del pacchetto Application Insights.</span><span class="sxs-lookup"><span data-stu-id="00a6c-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="00a6c-121">In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="00a6c-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="00a6c-122">Aprire la scheda **Aggiornamenti**, spuntare **Includi versione preliminare** e selezionare tutti i pacchetti Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="00a6c-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="00a6c-123">Ridistribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="00a6c-123">Redeploy your app.</span></span>

3. <span data-ttu-id="00a6c-124">Nel [portale di Azure](https://portal.azure.com) aprire la risorsa di Application Insights per l'app e quindi Live Stream.</span><span class="sxs-lookup"><span data-stu-id="00a6c-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="00a6c-125">[Proteggere il canale di controllo](#secure-the-control-channel) se è possibile usare i dati sensibili, ad esempio i nomi dei clienti, nei filtri.</span><span class="sxs-lookup"><span data-stu-id="00a6c-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Nel pannello Panoramica fare clic su Flusso attivo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="00a6c-127">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="00a6c-127">No data?</span></span> <span data-ttu-id="00a6c-128">Controllare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="00a6c-128">Check your server firewall</span></span>

<span data-ttu-id="00a6c-129">Controllare che [le porte in uscita di Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) siano aperte nel firewall del server.</span><span class="sxs-lookup"><span data-stu-id="00a6c-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="00a6c-130">Differenze tra Live Metrics Stream ed Esplora metriche e Analisi</span><span class="sxs-lookup"><span data-stu-id="00a6c-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="00a6c-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="00a6c-131">Live Stream</span></span> | <span data-ttu-id="00a6c-132">Esplora metriche e Analisi</span><span class="sxs-lookup"><span data-stu-id="00a6c-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="00a6c-133">Latency</span><span class="sxs-lookup"><span data-stu-id="00a6c-133">Latency</span></span>|<span data-ttu-id="00a6c-134">Dati visualizzati in un secondo</span><span class="sxs-lookup"><span data-stu-id="00a6c-134">Data displayed within one second</span></span>|<span data-ttu-id="00a6c-135">Aggregati in minuti</span><span class="sxs-lookup"><span data-stu-id="00a6c-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="00a6c-136">Nessuna conservazione</span><span class="sxs-lookup"><span data-stu-id="00a6c-136">No retention</span></span>|<span data-ttu-id="00a6c-137">I dati vengono mantenuti finché si trovano nel grafico, poi vengono eliminati</span><span class="sxs-lookup"><span data-stu-id="00a6c-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="00a6c-138">Dati mantenuti per 90 giorni</span><span class="sxs-lookup"><span data-stu-id="00a6c-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="00a6c-139">On demand</span><span class="sxs-lookup"><span data-stu-id="00a6c-139">On demand</span></span>|<span data-ttu-id="00a6c-140">I dati vengono trasmessi durante l'apertura di Live Metrics</span><span class="sxs-lookup"><span data-stu-id="00a6c-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="00a6c-141">I dati vengono inviati ogni volta che l'SDK viene installato e attivato</span><span class="sxs-lookup"><span data-stu-id="00a6c-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="00a6c-142">Gratuito</span><span class="sxs-lookup"><span data-stu-id="00a6c-142">Free</span></span>|<span data-ttu-id="00a6c-143">Non sono previste spese per i dati di Live Stream</span><span class="sxs-lookup"><span data-stu-id="00a6c-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="00a6c-144">Soggetto al [piano tariffario](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="00a6c-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="00a6c-145">Campionamento</span><span class="sxs-lookup"><span data-stu-id="00a6c-145">Sampling</span></span>|<span data-ttu-id="00a6c-146">Tutte le metriche selezionate e i contatori vengono trasmessi.</span><span class="sxs-lookup"><span data-stu-id="00a6c-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="00a6c-147">Gli errori e le analisi dello stack vengono usati come esempi.</span><span class="sxs-lookup"><span data-stu-id="00a6c-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="00a6c-148">TelemetryProcessors non viene applicato.</span><span class="sxs-lookup"><span data-stu-id="00a6c-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="00a6c-149">Eventi potrebbero essere usati come [esempi](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="00a6c-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="00a6c-150">Canale di controllo</span><span class="sxs-lookup"><span data-stu-id="00a6c-150">Control channel</span></span>|<span data-ttu-id="00a6c-151">I segnali di controllo del filtro vengono inviati all'SDK.</span><span class="sxs-lookup"><span data-stu-id="00a6c-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="00a6c-152">È consigliabile [proteggere questo canale](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="00a6c-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="00a6c-153">La comunicazione è unidirezionale al portale</span><span class="sxs-lookup"><span data-stu-id="00a6c-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="00a6c-154">Selezionare e filtrare le metriche</span><span class="sxs-lookup"><span data-stu-id="00a6c-154">Select and filter your metrics</span></span>

<span data-ttu-id="00a6c-155">(Disponibile in app ASP.NET classiche con l'SDK più recente.)</span><span class="sxs-lookup"><span data-stu-id="00a6c-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="00a6c-156">È possibile monitorare gli indicatori KPI personalizzati live applicando filtri arbitrari su eventuali dati di Application Insights Telemetry dal portale.</span><span class="sxs-lookup"><span data-stu-id="00a6c-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="00a6c-157">Fare clic sul controllo del filtro che viene mostrato quando il puntatore del mouse passa su un grafico.</span><span class="sxs-lookup"><span data-stu-id="00a6c-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="00a6c-158">Il grafico seguente traccia un indicatore KPI del conteggio di richieste personalizzato con filtri sugli attributi dell'URL e della durata.</span><span class="sxs-lookup"><span data-stu-id="00a6c-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="00a6c-159">Convalidare i filtri nella sezione Anteprima flusso che mostra un feed live di telemetria che corrisponde ai criteri specificati in qualsiasi punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="00a6c-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![Indicatore KPI di richieste personalizzato](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="00a6c-161">È possibile monitorare un valore diverso dal conteggio.</span><span class="sxs-lookup"><span data-stu-id="00a6c-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="00a6c-162">Le opzioni dipendono dal tipo di flusso, che può essere una qualsiasi Application Insights Telemetry: richieste, dipendenze, eccezioni, tracce, eventi o metriche.</span><span class="sxs-lookup"><span data-stu-id="00a6c-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="00a6c-163">Può essere la propria [misura personalizzata](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="00a6c-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opzioni del valore](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="00a6c-165">Oltre ai dati di Application Insights Telemetry, è anche possibile monitorare un contatore delle prestazioni di Windows selezionandolo dalle opzioni di flusso e inserendo il nome del contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="00a6c-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="00a6c-166">Le metriche attive vengono aggregate in due punti: in locale su ciascun server e quindi su tutti i server.</span><span class="sxs-lookup"><span data-stu-id="00a6c-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="00a6c-167">È possibile modificare l'impostazione predefinita per entrambi selezionando altre opzioni nei rispettivi elenchi a discesa.</span><span class="sxs-lookup"><span data-stu-id="00a6c-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="00a6c-168">Telemetria di esempio: eventi di diagnostica live personalizzati</span><span class="sxs-lookup"><span data-stu-id="00a6c-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="00a6c-169">Per impostazione predefinita, il feed live degli eventi mostra esempi di richieste non riuscite e chiamate di dipendenza, eccezioni, eventi e tracce.</span><span class="sxs-lookup"><span data-stu-id="00a6c-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="00a6c-170">Fare clic sull'icona del filtro per visualizzare i criteri applicati in un punto qualsiasi nel tempo.</span><span class="sxs-lookup"><span data-stu-id="00a6c-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Feed live predefinito](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="00a6c-172">Così come con le metriche, è possibile specificare i criteri arbitrari per i tipi di dati di Application Insights Telemetry.</span><span class="sxs-lookup"><span data-stu-id="00a6c-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="00a6c-173">In questo esempio, vengono selezionati eventi, tracce e richieste non riuscite specifiche.</span><span class="sxs-lookup"><span data-stu-id="00a6c-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="00a6c-174">Vengono selezionate anche tutte le eccezioni e gli errori di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="00a6c-174">We are also selecting all exceptions and dependency failures.</span></span>

![Feed live personalizzati](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="00a6c-176">Nota: attualmente, per i criteri di eccezione basati sul messaggio, usare il messaggio di eccezione più esterno.</span><span class="sxs-lookup"><span data-stu-id="00a6c-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="00a6c-177">Nell'esempio precedente, per filtrare l'eccezione di tipo benigno con messaggio di eccezione interna, segue il delimitatore "<--", "Il client si è disconnesso."</span><span class="sxs-lookup"><span data-stu-id="00a6c-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="00a6c-178">usare un criterio che non contiene il messaggio "Errore durante la lettura del contenuto della richiesta".</span><span class="sxs-lookup"><span data-stu-id="00a6c-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="00a6c-179">Visualizzare i dettagli di un elemento nel feed live facendovi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="00a6c-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="00a6c-180">È possibile sospendere il feed facendo clic su **Sospendi** o semplicemente scorrendo verso il basso o facendo clic su un elemento.</span><span class="sxs-lookup"><span data-stu-id="00a6c-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="00a6c-181">Il feed live verrà ripreso se, scorrendo, si torna all'inizio o facendo clic sul contatore degli elementi raccolti che era stato sospeso.</span><span class="sxs-lookup"><span data-stu-id="00a6c-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Errori live campionati](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="00a6c-183">Filtro per istanza di server</span><span class="sxs-lookup"><span data-stu-id="00a6c-183">Filter by server instance</span></span>

<span data-ttu-id="00a6c-184">Se si vuole monitorare un'istanza specifica del ruolo server, è possibile applicare un filtro per server.</span><span class="sxs-lookup"><span data-stu-id="00a6c-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Errori live campionati](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="00a6c-186">Requisiti SDK</span><span class="sxs-lookup"><span data-stu-id="00a6c-186">SDK Requirements</span></span>
<span data-ttu-id="00a6c-187">Live Metrics Stream personalizzato è disponibile con la versione 2.4.0-beta2 o più recente di [Application Insights SDK per il Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="00a6c-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="00a6c-188">Ricordarsi di selezionare l'opzione "Includi versione preliminare" da Gestione pacchetti di NuGet.</span><span class="sxs-lookup"><span data-stu-id="00a6c-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="00a6c-189">Proteggere il canale di controllo</span><span class="sxs-lookup"><span data-stu-id="00a6c-189">Secure the control channel</span></span>
<span data-ttu-id="00a6c-190">I criteri di filtri personalizzati specificati dall'utente vengono inviati al componente Metriche attive in Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="00a6c-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="00a6c-191">I filtri potrebbero contenere informazioni riservate, ad esempio ID cliente.</span><span class="sxs-lookup"><span data-stu-id="00a6c-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="00a6c-192">È possibile proteggere il canale con una chiave privata API e con la chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="00a6c-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="00a6c-193">Creare una chiave API</span><span class="sxs-lookup"><span data-stu-id="00a6c-193">Create an API Key</span></span>

![Creare una chiave API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="00a6c-195">Aggiungere una chiave API alla configurazione</span><span class="sxs-lookup"><span data-stu-id="00a6c-195">Add API key to Configuration</span></span>
<span data-ttu-id="00a6c-196">Nel file applicationinsights.config aggiungere AuthenticationApiKey a QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="00a6c-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="00a6c-197">Oppure nel codice impostarla in QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="00a6c-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="00a6c-198">Tuttavia, se l'utente riconosce tutti i server collegati e li ritiene affidabili, è possibile provare i filtri personalizzati senza il canale autenticato.</span><span class="sxs-lookup"><span data-stu-id="00a6c-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="00a6c-199">Questa opzione è disponibile per sei mesi.</span><span class="sxs-lookup"><span data-stu-id="00a6c-199">This option is available for six months.</span></span> <span data-ttu-id="00a6c-200">Questa sostituzione è necessaria una volta per ogni nuova sessione oppure quando un nuovo server è online.</span><span class="sxs-lookup"><span data-stu-id="00a6c-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opzioni di autenticazione delle metriche attive](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="00a6c-202">È consigliabile configurare il canale autenticato prima di immettere informazioni potenzialmente riservate, ad esempio CustomerID nei criteri di filtro.</span><span class="sxs-lookup"><span data-stu-id="00a6c-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="00a6c-203">Generazione di un carico di test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="00a6c-203">Generating a performance test load</span></span>

<span data-ttu-id="00a6c-204">Se si desidera osservare l'effetto di un aumento del carico, usare il pannello Test delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="00a6c-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="00a6c-205">Simula le richieste da un certo numero di utenti simultanei.</span><span class="sxs-lookup"><span data-stu-id="00a6c-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="00a6c-206">Può eseguire "test manuale", ovvero test ping, di un singolo URL o un [test delle prestazioni Web in più passaggi](app-insights-monitor-web-app-availability.md#multi-step-web-tests) caricato, proprio come un test di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="00a6c-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="00a6c-207">Dopo aver creato il test delle prestazioni, aprire il test e il pannello Live Stream in finestre distinte.</span><span class="sxs-lookup"><span data-stu-id="00a6c-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="00a6c-208">È possibile visualizzare l'avvio del test delle prestazioni in coda e il flusso live nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="00a6c-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="00a6c-209">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="00a6c-209">Troubleshooting</span></span>

<span data-ttu-id="00a6c-210">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="00a6c-210">No data?</span></span> <span data-ttu-id="00a6c-211">Se l'applicazione si trova in una rete protetta: Live Metrics Stream usa un indirizzo IP diverso dagli altri dati di Application Insights Telemetry.</span><span class="sxs-lookup"><span data-stu-id="00a6c-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="00a6c-212">Assicurarsi che [tali indirizzi IP](app-insights-ip-addresses.md) siano aperti nel firewall.</span><span class="sxs-lookup"><span data-stu-id="00a6c-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="00a6c-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00a6c-213">Next steps</span></span>
* [<span data-ttu-id="00a6c-214">Monitoraggio dell'utilizzo con Application Insights</span><span class="sxs-lookup"><span data-stu-id="00a6c-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="00a6c-215">Uso di Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="00a6c-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="00a6c-216">Profiler</span><span class="sxs-lookup"><span data-stu-id="00a6c-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="00a6c-217">Debugger di snapshot</span><span class="sxs-lookup"><span data-stu-id="00a6c-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
