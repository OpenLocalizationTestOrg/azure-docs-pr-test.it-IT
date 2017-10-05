---
title: Navigazione e dashboard in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="80e12-103">Navigazione e dashboard nel portale Application Insights</span><span class="sxs-lookup"><span data-stu-id="80e12-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="80e12-104">Dopo aver [impostato Application Insights nel progetto](app-insights-overview.md), i dati di telemetria sull'uso e le prestazioni dell'app verranno visualizzati nella risorsa di Application Insights del progetto nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80e12-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="80e12-105">Trovare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="80e12-105">Find your telemetry</span></span>
<span data-ttu-id="80e12-106">Nel [portale di Azure](https://portal.azure.com) passare alla risorsa di Application Insights creata per la propria app.</span><span class="sxs-lookup"><span data-stu-id="80e12-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Fare clic su Sfoglia, selezionare Application Insights, quindi fare clic sull'app.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="80e12-108">Il pannello (pagina) Panoramica dell'app mostra un riepilogo della metrica di diagnostica chiave dell'app e permette di accedere alle altre funzionalità del portale.</span><span class="sxs-lookup"><span data-stu-id="80e12-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Route principali per visualizzare i dati di telemetria](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="80e12-110">È possibile personalizzare tutti i grafici e le griglie e aggiungerli a un dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e12-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="80e12-111">In questo modo è possibile raccogliere i dati di telemetria chiave da diverse app in un dashboard centrale.</span><span class="sxs-lookup"><span data-stu-id="80e12-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="80e12-112">Dashboard</span><span class="sxs-lookup"><span data-stu-id="80e12-112">Dashboards</span></span>
<span data-ttu-id="80e12-113">Il primo oggetto visualizzato dopo l'accesso al [portale di Microsoft Azure](https://portal.azure.com) è un dashboard,</span><span class="sxs-lookup"><span data-stu-id="80e12-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="80e12-114">in cui è possibile raggruppare i grafici più importanti di tutte le risorse di Azure, inclusi i dati di telemetria di [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Un dashboard personalizzato.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="80e12-116">**Passare a risorse specifiche** ad esempio l'app in Application Insights: usare la barra di sinistra.</span><span class="sxs-lookup"><span data-stu-id="80e12-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="80e12-117">**Tornare al dashboard corrente** o passare ad altre visualizzazioni recenti: usare il menu a discesa in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="80e12-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="80e12-118">**Cambiare dashboard**: usare il menu a discesa nel titolo del dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e12-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="80e12-119">**Modificare, creare e condividere dashboard** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="80e12-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="80e12-120">**Modificare il dashboard**: passare il puntatore del mouse su un riquadro e usare la relativa barra superiore per spostarlo, personalizzarlo o rimuoverlo.</span><span class="sxs-lookup"><span data-stu-id="80e12-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="80e12-121">Aggiungere elementi a un dashboard</span><span class="sxs-lookup"><span data-stu-id="80e12-121">Add to a dashboard</span></span>
<span data-ttu-id="80e12-122">I pannelli o i set di grafici particolarmente interessanti possono essere aggiunti al dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e12-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="80e12-123">Saranno visibili al successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="80e12-123">You'll see it next time you return there.</span></span>

![Per aggiungere un grafico, passare il mouse su di esso e fare clic su "..." nell'intestazione.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="80e12-125">Aggiungere il grafico al dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e12-125">Pin chart to dashboard.</span></span> <span data-ttu-id="80e12-126">Una copia del grafico viene visualizzata nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="80e12-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="80e12-127">Aggiungere l'intero pannello al dashboard. Il pannello viene visualizzato nel dashboard sotto forma di riquadro su cui è possibile fare clic.</span><span class="sxs-lookup"><span data-stu-id="80e12-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="80e12-128">Fare clic nell'angolo superiore sinistro per tornare al dashboard corrente.</span><span class="sxs-lookup"><span data-stu-id="80e12-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="80e12-129">A questo punto è possibile usare il menu a discesa per tornare alla visualizzazione corrente.</span><span class="sxs-lookup"><span data-stu-id="80e12-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="80e12-130">Si noti che i grafici sono raggruppati in riquadri e che un riquadro può contenere più di un grafico.</span><span class="sxs-lookup"><span data-stu-id="80e12-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="80e12-131">Viene aggiunto al dashboard l'intero riquadro.</span><span class="sxs-lookup"><span data-stu-id="80e12-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="80e12-132">Il grafico viene aggiornato automaticamente con una frequenza che dipende dall'intervallo di tempo del grafico:</span><span class="sxs-lookup"><span data-stu-id="80e12-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="80e12-133">Intervallo di tempo fino ad un'ora: viene aggiornato ogni 5 minuti</span><span class="sxs-lookup"><span data-stu-id="80e12-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="80e12-134">Intervallo di tempo da una a 24 ore: viene aggiornato ogni 15 minuti</span><span class="sxs-lookup"><span data-stu-id="80e12-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="80e12-135">Intervallo di tempo superiore a 24 ore: (intervallo di tempo) / 60.</span><span class="sxs-lookup"><span data-stu-id="80e12-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="80e12-136">Aggiungere query in Analisi</span><span class="sxs-lookup"><span data-stu-id="80e12-136">Pin any query in Analytics</span></span>
<span data-ttu-id="80e12-137">È anche possibile aggiungere grafici di [Analisi](app-insights-analytics-using.md#pin-to-dashboard) a un dashboard [condiviso](#share-dashboards-with-your-team).</span><span class="sxs-lookup"><span data-stu-id="80e12-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="80e12-138">In questo modo è possibile aggiungere grafici di una query arbitraria insieme alle metriche standard.</span><span class="sxs-lookup"><span data-stu-id="80e12-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="80e12-139">I risultati vengono ricalcolati automaticamente ogni ora.</span><span class="sxs-lookup"><span data-stu-id="80e12-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="80e12-140">Fare clic sull'icona Aggiorna del grafico per un ricalcolo immediato.</span><span class="sxs-lookup"><span data-stu-id="80e12-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="80e12-141">(L'aggiornamento del browser non esegue il ricalcolo).</span><span class="sxs-lookup"><span data-stu-id="80e12-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="80e12-142">Modificare un riquadro nel dashboard</span><span class="sxs-lookup"><span data-stu-id="80e12-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="80e12-143">Dopo aver aggiunto un riquadro al dashboard, è possibile modificarlo.</span><span class="sxs-lookup"><span data-stu-id="80e12-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Passare il puntatore del mouse su un grafico per modificarlo.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="80e12-145">Aggiungere un grafico al riquadro.</span><span class="sxs-lookup"><span data-stu-id="80e12-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="80e12-146">Impostare la metrica, la dimensione group-by e lo stile (tabella, grafico) di un grafico.</span><span class="sxs-lookup"><span data-stu-id="80e12-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="80e12-147">Trascinare il diagramma per ingrandire; fare clic sul pulsante di annullamento per reimpostare l'intervallo di tempo; impostare le proprietà di filtro per i grafici nel riquadro.</span><span class="sxs-lookup"><span data-stu-id="80e12-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="80e12-148">Impostare il titolo del riquadro.</span><span class="sxs-lookup"><span data-stu-id="80e12-148">Set tile title.</span></span>

<span data-ttu-id="80e12-149">I riquadri aggiunti dai pannelli di Esplora metriche hanno più opzioni di modifica rispetto ai riquadri aggiunti da un pannello Panoramica.</span><span class="sxs-lookup"><span data-stu-id="80e12-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="80e12-150">Il riquadro originale aggiunto non è interessato dalle modifiche.</span><span class="sxs-lookup"><span data-stu-id="80e12-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="80e12-151">Passare da un dashboard all'altro</span><span class="sxs-lookup"><span data-stu-id="80e12-151">Switch between dashboards</span></span>
<span data-ttu-id="80e12-152">È possibile salvare più dashboard e passare da un dashboard all'altro.</span><span class="sxs-lookup"><span data-stu-id="80e12-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="80e12-153">Quando si aggiunge un grafico o un pannello, l'aggiunta viene eseguita nel dashboard corrente.</span><span class="sxs-lookup"><span data-stu-id="80e12-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Per passare da un dashboard all'altro, fare clic su Dashboard e selezionare un dashboard salvato.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="80e12-157">È possibile ad esempio usare un dashboard per la visualizzazione a schermo intero nell'area del team e un altro dashboard per lo sviluppo generale.</span><span class="sxs-lookup"><span data-stu-id="80e12-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="80e12-158">Nel dashboard i pannelli vengono visualizzati sotto forma di riquadri: fare clic sul riquadro desiderato per passare al pannello.</span><span class="sxs-lookup"><span data-stu-id="80e12-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="80e12-159">I grafici sono una replica dei grafici che si trovano nel percorso originale.</span><span class="sxs-lookup"><span data-stu-id="80e12-159">A chart replicates the chart in its original location.</span></span>

![Fare clic su un riquadro per aprire il pannello che rappresenta](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="80e12-161">Condividere dashboard</span><span class="sxs-lookup"><span data-stu-id="80e12-161">Share dashboards</span></span>
<span data-ttu-id="80e12-162">Dopo aver creato un dashboard, è possibile condividerlo con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="80e12-162">When you've created a dashboard, you can share it with other users.</span></span>

![Fare clic su Condividi nell'intestazione del dashboard](./media/app-insights-dashboards/41.png)

<span data-ttu-id="80e12-164">Altre informazioni su [ruoli e controllo di accesso](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="80e12-165">Esplorazione delle app</span><span class="sxs-lookup"><span data-stu-id="80e12-165">App navigation</span></span>
<span data-ttu-id="80e12-166">Il pannello Panoramica è il gateway per altre informazioni sull'app.</span><span class="sxs-lookup"><span data-stu-id="80e12-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="80e12-167">**Qualsiasi grafico o riquadro**: fare clic su qualsiasi riquadro o grafico per vedere altri dettagli sugli elementi visualizzati.</span><span class="sxs-lookup"><span data-stu-id="80e12-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="80e12-168">Pulsanti del pannello Panoramica</span><span class="sxs-lookup"><span data-stu-id="80e12-168">Overview blade buttons</span></span>
![Barra di spostamento superiore del pannello Panoramica](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="80e12-170">[**Esplora metriche**](app-insights-metrics-explorer.md): consente di creare grafici su prestazioni e uso.</span><span class="sxs-lookup"><span data-stu-id="80e12-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="80e12-171">[**Cerca**](app-insights-diagnostic-search.md): consente di analizzare istanze specifiche di eventi, ad esempio richieste, eccezioni o tracce di log.</span><span class="sxs-lookup"><span data-stu-id="80e12-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="80e12-172">[**Analisi**](app-insights-analytics.md): consente di eseguire query avanzate con i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="80e12-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="80e12-173">**Intervallo di tempo**: consente di regolare l'intervallo visualizzato da tutti i grafici nel pannello.</span><span class="sxs-lookup"><span data-stu-id="80e12-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="80e12-174">**Elimina**: consente di eliminare la risorsa di Application Insights per l'app.</span><span class="sxs-lookup"><span data-stu-id="80e12-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="80e12-175">È necessario anche rimuovere i pacchetti di Application Insights dal codice dell'app o modificare la [chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key) nell'app per indirizzare i dati di telemetria a una risorsa di Application Insights diversa.</span><span class="sxs-lookup"><span data-stu-id="80e12-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="80e12-176">Scheda Informazioni di base</span><span class="sxs-lookup"><span data-stu-id="80e12-176">Essentials tab</span></span>
* <span data-ttu-id="80e12-177">[Chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica la risorsa dell'app.</span><span class="sxs-lookup"><span data-stu-id="80e12-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="80e12-178">Prezzi: rende disponibili le funzionalità e imposta i limiti per i volumi.</span><span class="sxs-lookup"><span data-stu-id="80e12-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="80e12-179">Barra di spostamento delle app</span><span class="sxs-lookup"><span data-stu-id="80e12-179">App navigation bar</span></span>
![Barra di spostamento sinistra](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="80e12-181">**Panoramica**: consente di tornare al pannello Panoramica delle app.</span><span class="sxs-lookup"><span data-stu-id="80e12-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="80e12-182">**Log attività**: fornisce avvisi e informazioni su eventi amministrativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="80e12-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="80e12-183">[**Controllo di accesso**](app-insights-resources-roles-access-control.md): fornire l'accesso a membri del team e altri utenti.</span><span class="sxs-lookup"><span data-stu-id="80e12-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="80e12-184">[**Tag**](../azure-resource-manager/resource-group-using-tags.md): consente di usare tag per raggruppare un'app con altre app.</span><span class="sxs-lookup"><span data-stu-id="80e12-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="80e12-185">RICERCA CAUSA</span><span class="sxs-lookup"><span data-stu-id="80e12-185">INVESTIGATE</span></span>

* <span data-ttu-id="80e12-186">[**Mappa delle applicazioni**](app-insights-app-map.md): una mappa attiva che mostra i componenti dell'applicazione, ricavata dalle informazioni sulle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="80e12-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="80e12-187">[**Rilevamento intelligente**](app-insights-proactive-diagnostics.md): consente di esaminare gli avvisi recenti sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="80e12-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="80e12-188">[**Flusso attivo**](app-insights-live-stream.md): un set fisso di metriche quasi istantanee, utile quando si distribuisce una nuova compilazione o si esegue il debug.</span><span class="sxs-lookup"><span data-stu-id="80e12-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="80e12-189">[**Test Web/disponibilità**](app-insights-monitor-web-app-availability.md): consente di inviare regolarmente richieste all'App Web da ogni parte del mondo.*</span><span class="sxs-lookup"><span data-stu-id="80e12-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="80e12-190">[**Errori, Prestazioni**](app-insights-web-monitor-performance.md): eccezioni, frequenze di errori e tempi di risposta per le richieste verso l'app e dall'app alle [dipendenze](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="80e12-191">[**Performance**](app-insights-web-monitor-performance.md): tempo di risposta e tempi di risposta delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="80e12-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="80e12-192">[Server](app-insights-web-monitor-performance.md) : contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="80e12-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="80e12-193">Disponibile se si [installa Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="80e12-194">**Browser** : prestazioni AJAX e di visualizzazione di pagine.</span><span class="sxs-lookup"><span data-stu-id="80e12-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="80e12-195">Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="80e12-196">**Utilizzo** : numero di sessioni, utenti e visualizzazioni di pagine.</span><span class="sxs-lookup"><span data-stu-id="80e12-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="80e12-197">Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="80e12-198">CONFIGURA</span><span class="sxs-lookup"><span data-stu-id="80e12-198">CONFIGURE</span></span>

* <span data-ttu-id="80e12-199">**Per iniziare** : esercitazione inline.</span><span class="sxs-lookup"><span data-stu-id="80e12-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="80e12-200">**Proprietà** : chiave di strumentazione, sottoscrizione e ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="80e12-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="80e12-201">[Avvisi](app-insights-alerts.md) : configurazione degli avvisi sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="80e12-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="80e12-202">[Esportazione continua](app-insights-export-telemetry.md) : configurazione dell'esportazione dei dati di telemetria nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="80e12-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="80e12-203">[Test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests) : impostazione di un carico sintetico nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="80e12-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="80e12-204">[Quota e prezzi](app-insights-pricing.md) e [campionamento per inserimento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="80e12-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="80e12-205">**Accesso API**: consente di creare [annotazioni sulla versione](app-insights-annotations.md) e per l'API di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="80e12-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="80e12-206">[**Elementi di lavoro**](app-insights-diagnostic-search.md#create-work-item): consente di connettersi a un sistema di verifica del lavoro per poter creare bug durante l'analisi dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="80e12-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="80e12-207">IMPOSTAZIONI</span><span class="sxs-lookup"><span data-stu-id="80e12-207">SETTINGS</span></span>

* <span data-ttu-id="80e12-208">[**Blocchi**](../azure-resource-manager/resource-group-lock-resources.md): bloccano le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="80e12-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="80e12-209">[**Script di automazione**](app-insights-powershell.md): consente di esportare una definizione della risorsa di Azure da usare come modello per la creazione di nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="80e12-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="80e12-210">Video</span><span class="sxs-lookup"><span data-stu-id="80e12-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="80e12-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="80e12-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="80e12-212">Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="80e12-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="80e12-213">Consente di filtrare e segmentare le metriche</span><span class="sxs-lookup"><span data-stu-id="80e12-213">Filter and segment metrics</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="80e12-215">Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="80e12-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="80e12-216">Consente di cercare e analizzare eventi ed eventi correlati e di creare bug</span><span class="sxs-lookup"><span data-stu-id="80e12-216">Find and inspect events, related events, and create bugs</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="80e12-218">Analisi</span><span class="sxs-lookup"><span data-stu-id="80e12-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="80e12-219">Linguaggio di query avanzato</span><span class="sxs-lookup"><span data-stu-id="80e12-219">Powerful query language</span></span> |![Esempio di ricerca](./media/app-insights-dashboards/63.png) |
