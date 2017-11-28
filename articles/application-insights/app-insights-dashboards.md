---
title: aaaDashboards e spostamento in hello Azure Application Insights | Documenti Microsoft
description: Creare visualizzazioni di query e grafici APM chiave.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="e6208-103">Spostamento e i dashboard nel portale Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="e6208-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="e6208-104">Dopo aver [configurare Application Insights al progetto](app-insights-overview.md), verranno visualizzati i dati di telemetria sull'utilizzo e delle prestazioni dell'app nella risorsa di Application Insights del progetto in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6208-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="e6208-105">Trovare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="e6208-105">Find your telemetry</span></span>
<span data-ttu-id="e6208-106">Accedi toohello [portale di Azure](https://portal.azure.com) e passare a risorsa di Application Insights toohello creato per l'app.</span><span class="sxs-lookup"><span data-stu-id="e6208-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Fare clic su Sfoglia, selezionare Application Insights, quindi fare clic sull'app.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="e6208-108">pannello della panoramica Hello (pagina) per l'app viene visualizzato un riepilogo delle metriche di diagnostica chiave hello dell'app ed è di altre funzionalità del portale hello toohello un gateway.</span><span class="sxs-lookup"><span data-stu-id="e6208-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![I principali di dati di telemetria tooview route](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="e6208-110">È possibile personalizzare le griglie e grafici hello e aggiungerli tooa dashboard.</span><span class="sxs-lookup"><span data-stu-id="e6208-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="e6208-111">In questo modo, è possibile unire dati di telemetria chiave hello da diverse App in un dashboard centrale.</span><span class="sxs-lookup"><span data-stu-id="e6208-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="e6208-112">Dashboard</span><span class="sxs-lookup"><span data-stu-id="e6208-112">Dashboards</span></span>
<span data-ttu-id="e6208-113">Hello in primo luogo viene visualizzato dopo l'accesso toohello [portale Microsoft Azure](https://portal.azure.com) è un dashboard.</span><span class="sxs-lookup"><span data-stu-id="e6208-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="e6208-114">Qui è possibile raggruppare i grafici di hello che sono più importanti tooyou tra tutte le risorse di Azure, inclusi i dati di telemetria da [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Un dashboard personalizzato.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="e6208-116">**Passare alle risorse toospecific** , ad esempio l'app in Application Insights: barra sinistra hello di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="e6208-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="e6208-117">**Dashboard corrente restituito toohello**, o cambiare vista recenti tooother: menu di scelta rapida utilizzare hello in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="e6208-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="e6208-118">**Passare i dashboard**: menu di scelta rapida utilizzare hello nel titolo del dashboard hello</span><span class="sxs-lookup"><span data-stu-id="e6208-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="e6208-119">**Creare, modificare e condividere i dashboard** nella barra degli strumenti del dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="e6208-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="e6208-120">**Modificare il dashboard di hello**: passare il mouse su un riquadro e quindi usare superiore barra toomove, personalizzare o rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="e6208-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="e6208-121">Aggiungere dashboard tooa</span><span class="sxs-lookup"><span data-stu-id="e6208-121">Add tooa dashboard</span></span>
<span data-ttu-id="e6208-122">Quando si cerca un pannello o un set di grafici che è particolarmente interessante, è possibile aggiungere una copia del dashboard toohello.</span><span class="sxs-lookup"><span data-stu-id="e6208-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="e6208-123">Saranno visibili al successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="e6208-123">You'll see it next time you return there.</span></span>

![toopin un grafico, passare il mouse su di essa e quindi fare clic su "…" nell'intestazione di hello.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="e6208-125">Aggiungi grafico toodashboard.</span><span class="sxs-lookup"><span data-stu-id="e6208-125">Pin chart toodashboard.</span></span> <span data-ttu-id="e6208-126">Una copia di hello grafico viene visualizzato nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="e6208-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="e6208-127">PIN hello intero pannello toohello - visualizzato nel dashboard hello sotto forma di riquadro che è possibile fare clic.</span><span class="sxs-lookup"><span data-stu-id="e6208-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="e6208-128">Fare clic su dashboard corrente toohello di hello tooreturn nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="e6208-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="e6208-129">È quindi possibile utilizzare visualizzazione corrente di hello dal menu a discesa tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="e6208-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="e6208-130">Si noti che i grafici sono raggruppati in riquadri e che un riquadro può contenere più di un grafico.</span><span class="sxs-lookup"><span data-stu-id="e6208-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="e6208-131">Si blocca hello intero riquadro toohello o un dashboard.</span><span class="sxs-lookup"><span data-stu-id="e6208-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="e6208-132">grafico Hello viene aggiornata automaticamente con una frequenza che dipende da intervallo di tempo del grafico hello:</span><span class="sxs-lookup"><span data-stu-id="e6208-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="e6208-133">Intervallo di ore too1 di tempo: aggiornare ogni 5 minuti</span><span class="sxs-lookup"><span data-stu-id="e6208-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="e6208-134">Intervallo di tempo da una a 24 ore: viene aggiornato ogni 15 minuti</span><span class="sxs-lookup"><span data-stu-id="e6208-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="e6208-135">Intervallo di tempo superiore a 24 ore: (intervallo di tempo) / 60.</span><span class="sxs-lookup"><span data-stu-id="e6208-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="e6208-136">Aggiungere query in Analisi</span><span class="sxs-lookup"><span data-stu-id="e6208-136">Pin any query in Analytics</span></span>
<span data-ttu-id="e6208-137">È anche possibile [aggiungere Analitica](app-insights-analytics-using.md#pin-to-dashboard) grafici tooa [condivisa](#share-dashboards-with-your-team) dashboard.</span><span class="sxs-lookup"><span data-stu-id="e6208-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="e6208-138">In questo modo tooadd grafici delle query insieme a metriche standard hello arbitrario.</span><span class="sxs-lookup"><span data-stu-id="e6208-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="e6208-139">I risultati vengono ricalcolati automaticamente ogni ora.</span><span class="sxs-lookup"><span data-stu-id="e6208-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="e6208-140">Clic sull'icona di aggiornamento di hello in hello grafico toorecalculate immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e6208-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="e6208-141">(L'aggiornamento del browser non esegue il ricalcolo).</span><span class="sxs-lookup"><span data-stu-id="e6208-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="e6208-142">Modificare un riquadro nel dashboard di hello</span><span class="sxs-lookup"><span data-stu-id="e6208-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="e6208-143">Una volta un riquadro nel dashboard di hello, è possibile modificare.</span><span class="sxs-lookup"><span data-stu-id="e6208-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Passare il mouse sopra un grafico in ordine tooedit.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="e6208-145">Aggiungere un riquadro toohello grafico.</span><span class="sxs-lookup"><span data-stu-id="e6208-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="e6208-146">Impostare la metrica hello, group by dimensione e lo stile (tabella, grafico) di un grafico.</span><span class="sxs-lookup"><span data-stu-id="e6208-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="e6208-147">Trascina toozoom diagramma hello. Fare clic su hello annullamento pulsante tooreset hello timespan; impostare le proprietà di filtro per i grafici di hello sul riquadro hello.</span><span class="sxs-lookup"><span data-stu-id="e6208-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="e6208-148">Impostare il titolo del riquadro.</span><span class="sxs-lookup"><span data-stu-id="e6208-148">Set tile title.</span></span>

<span data-ttu-id="e6208-149">I riquadri aggiunti dai pannelli di Esplora metriche hanno più opzioni di modifica rispetto ai riquadri aggiunti da un pannello Panoramica.</span><span class="sxs-lookup"><span data-stu-id="e6208-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="e6208-150">riquadro Hello originale è stato aggiunto non è influenzato da tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e6208-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="e6208-151">Passare da un dashboard all'altro</span><span class="sxs-lookup"><span data-stu-id="e6208-151">Switch between dashboards</span></span>
<span data-ttu-id="e6208-152">È possibile salvare più dashboard e passare da un dashboard all'altro.</span><span class="sxs-lookup"><span data-stu-id="e6208-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="e6208-153">Quando si aggiunge un grafico o un pannello, vengono aggiunte toohello dashboard corrente.</span><span class="sxs-lookup"><span data-stu-id="e6208-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch tra i dashboard, fare clic su Dashboard e selezionare un dashboard salvato.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="e6208-157">Ad esempio, potrebbe essere un dashboard per la visualizzazione a schermo intero nella chat team hello e l'altra per lo sviluppo generale.</span><span class="sxs-lookup"><span data-stu-id="e6208-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="e6208-158">Nel dashboard di hello, viene visualizzato un pannello sotto forma di riquadro: selezionarlo toogo toohello blade.</span><span class="sxs-lookup"><span data-stu-id="e6208-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="e6208-159">Un grafico consente di replicare il grafico hello nella posizione originale.</span><span class="sxs-lookup"><span data-stu-id="e6208-159">A chart replicates hello chart in its original location.</span></span>

![Fare clic su un pannello di hello tooopen riquadro che rappresenta](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="e6208-161">Condividere dashboard</span><span class="sxs-lookup"><span data-stu-id="e6208-161">Share dashboards</span></span>
<span data-ttu-id="e6208-162">Dopo aver creato un dashboard, è possibile condividerlo con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="e6208-162">When you've created a dashboard, you can share it with other users.</span></span>

![Nell'intestazione di hello dashboard, fare clic su Condividi](./media/app-insights-dashboards/41.png)

<span data-ttu-id="e6208-164">Altre informazioni su [ruoli e controllo di accesso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="e6208-165">Esplorazione delle app</span><span class="sxs-lookup"><span data-stu-id="e6208-165">App navigation</span></span>
<span data-ttu-id="e6208-166">pannello della panoramica Hello è hello gateway toomore informazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="e6208-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="e6208-167">**Qualsiasi riquadro o un grafico** : fare clic su qualsiasi riquadro o grafico toosee ulteriori dettagli sulla descrizione.</span><span class="sxs-lookup"><span data-stu-id="e6208-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="e6208-168">Pulsanti del pannello Panoramica</span><span class="sxs-lookup"><span data-stu-id="e6208-168">Overview blade buttons</span></span>
![Barra di spostamento superiore del pannello Panoramica](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="e6208-170">[**Esplora metriche**](app-insights-metrics-explorer.md): consente di creare grafici su prestazioni e uso.</span><span class="sxs-lookup"><span data-stu-id="e6208-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="e6208-171">[**Cerca**](app-insights-diagnostic-search.md): consente di analizzare istanze specifiche di eventi, ad esempio richieste, eccezioni o tracce di log.</span><span class="sxs-lookup"><span data-stu-id="e6208-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="e6208-172">[**Analisi**](app-insights-analytics.md): consente di eseguire query avanzate con i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="e6208-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="e6208-173">**Intervallo di tempo** -modificare l'intervallo di hello visualizzato da tutti i grafici di hello nel pannello hello.</span><span class="sxs-lookup"><span data-stu-id="e6208-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="e6208-174">**Eliminare** -eliminare la risorsa di Application Insights hello per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="e6208-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="e6208-175">È necessario anche rimuovere pacchetti di Application Insights hello dal codice dell'app oppure modificare hello [chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key) nell'app toodirect telemetria tooa diversi risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e6208-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="e6208-176">Scheda Informazioni di base</span><span class="sxs-lookup"><span data-stu-id="e6208-176">Essentials tab</span></span>
* <span data-ttu-id="e6208-177">[Chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica la risorsa dell'app.</span><span class="sxs-lookup"><span data-stu-id="e6208-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="e6208-178">Prezzi: rende disponibili le funzionalità e imposta i limiti per i volumi.</span><span class="sxs-lookup"><span data-stu-id="e6208-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="e6208-179">Barra di spostamento delle app</span><span class="sxs-lookup"><span data-stu-id="e6208-179">App navigation bar</span></span>
![Barra di spostamento sinistra](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="e6208-181">**Panoramica** -pannello della panoramica app toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="e6208-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="e6208-182">**Log attività**: fornisce avvisi e informazioni su eventi amministrativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6208-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="e6208-183">[**Controllo di accesso** ](app-insights-resources-roles-access-control.md) -forniscono accesso a membri tooteam e altri.</span><span class="sxs-lookup"><span data-stu-id="e6208-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="e6208-184">[**Tag** ](../azure-resource-manager/resource-group-using-tags.md) -utilizzare tag toogroup app con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="e6208-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="e6208-185">RICERCA CAUSA</span><span class="sxs-lookup"><span data-stu-id="e6208-185">INVESTIGATE</span></span>

* <span data-ttu-id="e6208-186">[**Mappa delle applicazioni** ](app-insights-app-map.md) -Active mappa con i componenti di hello dell'applicazione, è derivato dalle informazioni di dipendenza hello.</span><span class="sxs-lookup"><span data-stu-id="e6208-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="e6208-187">[**Rilevamento intelligente**](app-insights-proactive-diagnostics.md): consente di esaminare gli avvisi recenti sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e6208-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="e6208-188">[**Flusso attivo**](app-insights-live-stream.md): un set fisso di metriche quasi istantanee, utile quando si distribuisce una nuova compilazione o si esegue il debug.</span><span class="sxs-lookup"><span data-stu-id="e6208-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="e6208-189">[**Disponibilità / test Web** ](app-insights-monitor-web-app-availability.md) -invia richieste regolare tooyour app web da intorno mondo hello. *</span><span class="sxs-lookup"><span data-stu-id="e6208-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="e6208-190">[**Gli errori, prestazioni** ](app-insights-web-monitor-performance.md) -eccezioni, guasti e una risposta volte per le richieste tooyour app e per le richieste dall'app troppo[dipendenze](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="e6208-191">[**Performance**](app-insights-web-monitor-performance.md): tempo di risposta e tempi di risposta delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e6208-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="e6208-192">[Server](app-insights-web-monitor-performance.md) : contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e6208-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="e6208-193">Disponibile se si [installa Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="e6208-194">**Browser** : prestazioni AJAX e di visualizzazione di pagine.</span><span class="sxs-lookup"><span data-stu-id="e6208-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="e6208-195">Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="e6208-196">**Utilizzo** : numero di sessioni, utenti e visualizzazioni di pagine.</span><span class="sxs-lookup"><span data-stu-id="e6208-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="e6208-197">Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="e6208-198">CONFIGURA</span><span class="sxs-lookup"><span data-stu-id="e6208-198">CONFIGURE</span></span>

* <span data-ttu-id="e6208-199">**Per iniziare** : esercitazione inline.</span><span class="sxs-lookup"><span data-stu-id="e6208-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="e6208-200">**Proprietà** : chiave di strumentazione, sottoscrizione e ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="e6208-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="e6208-201">[Avvisi](app-insights-alerts.md) : configurazione degli avvisi sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="e6208-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="e6208-202">[L'esportazione continua](app-insights-export-telemetry.md) -configurare l'esportazione di archiviazione di dati di telemetria tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e6208-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="e6208-203">[Test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests) : impostazione di un carico sintetico nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="e6208-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="e6208-204">[Quota e prezzi](app-insights-pricing.md) e [campionamento per inserimento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="e6208-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="e6208-205">**L'accesso all'API** -creare [versione annotazioni](app-insights-annotations.md) e per hello API di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="e6208-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="e6208-206">[**Gli elementi di lavoro** ](app-insights-diagnostic-search.md#create-work-item) -connettersi in modo che è possibile creare bug durante l'analisi di dati di telemetria, sistema di verifica del lavoro tooa.</span><span class="sxs-lookup"><span data-stu-id="e6208-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="e6208-207">IMPOSTAZIONI</span><span class="sxs-lookup"><span data-stu-id="e6208-207">SETTINGS</span></span>

* <span data-ttu-id="e6208-208">[**Blocchi**](../azure-resource-manager/resource-group-lock-resources.md): bloccano le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6208-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="e6208-209">[**Script di automazione** ](app-insights-powershell.md) -esportare una definizione di risorsa di Azure hello in modo che è possibile utilizzarlo come un nuove risorse toocreate di modello.</span><span class="sxs-lookup"><span data-stu-id="e6208-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="e6208-210">Video</span><span class="sxs-lookup"><span data-stu-id="e6208-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="e6208-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6208-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="e6208-212">Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="e6208-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="e6208-213">Consente di filtrare e segmentare le metriche</span><span class="sxs-lookup"><span data-stu-id="e6208-213">Filter and segment metrics</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="e6208-215">Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="e6208-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="e6208-216">Consente di cercare e analizzare eventi ed eventi correlati e di creare bug</span><span class="sxs-lookup"><span data-stu-id="e6208-216">Find and inspect events, related events, and create bugs</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="e6208-218">Analisi</span><span class="sxs-lookup"><span data-stu-id="e6208-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="e6208-219">Linguaggio di query avanzato</span><span class="sxs-lookup"><span data-stu-id="e6208-219">Powerful query language</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/63.png) |
