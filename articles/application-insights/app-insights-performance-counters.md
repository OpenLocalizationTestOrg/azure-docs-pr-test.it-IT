---
title: Contatori delle prestazioni in Application Insights | Documentazione Microsoft
description: Sistema di monitoraggio e contatori delle prestazioni .NET personalizzati in Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 038d6e051be8112b9264e7efa6485965d11e32c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="9f6c2-103">Contatori delle prestazioni di sistema in Application Insights</span><span class="sxs-lookup"><span data-stu-id="9f6c2-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="9f6c2-104">Windows offre un'ampia gamma di [contatori delle prestazioni](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), ad esempio su occupazione della CPU, memoria, disco e utilizzo di rete.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="9f6c2-105">È anche possibile definire contatori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-105">You can also define your own.</span></span> <span data-ttu-id="9f6c2-106">[Application Insights](app-insights-overview.md) può mostrare questi contatori delle prestazioni se l'applicazione viene eseguita in IIS in un host locale o in una macchina virtuale a cui si ha accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine to which you have administrative access.</span></span> <span data-ttu-id="9f6c2-107">I grafici indicano le risorse disponibili per l'applicazione live e possono aiutare a identificare un eventuale carico sbilanciato tra istanze del server.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-107">The charts indicate the resources available to your live application, and can help to identify unbalanced load between server instances.</span></span>

<span data-ttu-id="9f6c2-108">I contatori delle prestazioni sono visualizzati nel pannello Server, che include una tabella segmentata in base all'istanza del server.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-108">Performance counters appear in the Servers blade, which includes a table that segments by server instance.</span></span>

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="9f6c2-110">I contatori delle prestazioni non sono disponibili per App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="9f6c2-111">Tuttavia, è possibile [inviare i dati del servizio Diagnostica di Azure ad Application Insights](app-insights-azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9f6c2-111">But you can [send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="9f6c2-112">Visualizzare i contatori</span><span class="sxs-lookup"><span data-stu-id="9f6c2-112">View counters</span></span>
<span data-ttu-id="9f6c2-113">Il pannello Server mostra un set predefinito di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-113">The Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="9f6c2-114">Per visualizzare altri contatori, modificare i grafici nel pannello Server oppure aprire un altro riquadro [Esplora metriche](app-insights-metrics-explorer.md) e aggiungere nuovi grafici.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-114">To see other counters, either edit the charts on the Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="9f6c2-115">I contatori disponibili sono elencati come metriche quando si modifica un grafico.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-115">The available counters are listed as metrics when you edit a chart.</span></span>

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="9f6c2-117">Per visualizzare tutti i grafici più utili in un'unica posizione, creare un [dashboard](app-insights-dashboards.md) e aggiungervi i grafici.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-117">To see all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them to it.</span></span>

## <a name="add-counters"></a><span data-ttu-id="9f6c2-118">Aggiungere contatori</span><span class="sxs-lookup"><span data-stu-id="9f6c2-118">Add counters</span></span>
<span data-ttu-id="9f6c2-119">Se il contatore delle prestazioni desiderato non appare nell'elenco delle metriche, significa che non viene raccolto da Application Insights SDK nel server Web.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-119">If the performance counter you want isn't shown in the list of metrics, that's because the Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="9f6c2-120">È possibile configurare l'SDK a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-120">You can configure it to do so.</span></span>

1. <span data-ttu-id="9f6c2-121">È possibile identificare i contatori disponibili nel server usando questo comando di PowerShell nel server:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-121">Find out what counters are available in your server by using this PowerShell command at the server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="9f6c2-122">Vedere [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f6c2-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="9f6c2-123">Aprire ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="9f6c2-124">Se Application Insights è stato aggiunto all'app durante lo sviluppo, modificare ApplicationInsights.config nel progetto e quindi distribuirlo di nuovo nei server.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-124">If you added Application Insights to your app during development, edit ApplicationInsights.config in your project, and then re-deploy it to your servers.</span></span>
   * <span data-ttu-id="9f6c2-125">Se è stato usato Status Monitor per instrumentare un'app Web al runtime, trovare ApplicationInsights.config nella directory radice dell'app in IIS.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-125">If you used Status Monitor to instrument a web app at runtime, find ApplicationInsights.config in the root directory of the app in IIS.</span></span> <span data-ttu-id="9f6c2-126">Aggiornarlo qui in ogni istanza del server.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="9f6c2-127">Modificare la direttiva dell'agente di raccolta delle prestazioni:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-127">Edit the performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="9f6c2-128">È possibile acquisire contatori standard e quelli implementati manualmente.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="9f6c2-129">`\Objects\Processes` è un esempio di contatore standard, disponibile in tutti i sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="9f6c2-130">`\Sales(photo)\# Items Sold` è un esempio di contatore personalizzato che può essere implementato in un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="9f6c2-131">Il formato è `\Category(instance)\Counter"` oppure, per categorie non associate a istanze, solo `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-131">The format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="9f6c2-132">`ReportAs` è necessario per i nomi dei contatori che non corrispondono a `[a-zA-Z()/-_ \.]+`, ovvero che contengono caratteri che non sono inclusi in questi set: lettere, parentesi tonde, barra, trattino, carattere di sottolineatura, spazio e punto.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in the following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="9f6c2-133">Se si specifica un'istanza, questa verrà raccolta come dimensione "CounterInstanceName" della metrica indicata.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of the reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="9f6c2-134">Raccogliere contatori delle prestazioni nel codice</span><span class="sxs-lookup"><span data-stu-id="9f6c2-134">Collecting performance counters in code</span></span>
<span data-ttu-id="9f6c2-135">Per raccogliere i contatori delle prestazioni di sistema e inviarli ad Application Insights, è possibile adattare il frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-135">To collect system performance counters and send them to Application Insights, you can adapt the snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="9f6c2-136">In alternativa, è possibile eseguire la stessa operazione con le metriche personalizzate create:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-136">Or you can do the same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="9f6c2-137">Contatori delle prestazioni in Analytics</span><span class="sxs-lookup"><span data-stu-id="9f6c2-137">Performance counters in Analytics</span></span>
<span data-ttu-id="9f6c2-138">È possibile cercare e visualizzare report dei contatori delle prestazioni in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9f6c2-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="9f6c2-139">Lo schema **performanceCounters** espone `category`, il nome `counter` e il nome `instance` per ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-139">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="9f6c2-140">Nei dati di telemetria per ogni applicazione verranno visualizzati solo i contatori per l'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-140">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="9f6c2-141">Ad esempio, per visualizzare quali contatori sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-141">For example, to see what counters are available:</span></span> 

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="9f6c2-143">"Istanza" qui fa riferimento all'istanza del contatore delle prestazioni e non all'istanza del ruolo o del server.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-143">('Instance' here refers to the performance counter instance,  not the role or server machine instance.</span></span> <span data-ttu-id="9f6c2-144">Il nome dell'istanza del contatore delle prestazioni segmenta in genere i contatori, come quello per il tempo del processore, in base al nome del processo o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-144">The performance counter instance name typically segments counters such as processor time by the name of the process or application.)</span></span>

<span data-ttu-id="9f6c2-145">Per ottenere un grafico della memoria disponibile nel periodo recente:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-145">To get a chart of available memory over the recent period:</span></span> 

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="9f6c2-147">Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità dell'istanza del server host in cui viene eseguita l'app.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host server instance on which your app is running.</span></span> <span data-ttu-id="9f6c2-148">Ad esempio, per confrontare le prestazioni dell'applicazione su computer diversi:</span><span class="sxs-lookup"><span data-stu-id="9f6c2-148">For example, to compare the performance of your app on the different machines:</span></span> 

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="9f6c2-150">Conteggi di ASP.NET e Application Insights</span><span class="sxs-lookup"><span data-stu-id="9f6c2-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="9f6c2-151">*Qual è la differenza tra il tasso di eccezione e le metriche delle eccezioni?*</span><span class="sxs-lookup"><span data-stu-id="9f6c2-151">*What's the difference between the Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="9f6c2-152">*Tasso di eccezione* è un contatore delle prestazioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="9f6c2-153">Il CLR consente di contare tutte le eccezioni gestite e non gestite generate e divide il totale in un intervallo di campionamento per la lunghezza dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-153">The CLR counts all the handled and unhandled exceptions that are thrown, and divides the total in a sampling interval by the length of the interval.</span></span> <span data-ttu-id="9f6c2-154">SDK di Application Insights raccoglie questo risultato e lo invia al portale.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-154">The Application Insights SDK collects this result and sends it to the portal.</span></span>
* <span data-ttu-id="9f6c2-155">*Eccezioni* è un conteggio dei report TrackException ricevuti dal portale nell'intervallo di campionamento del grafico.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-155">*Exceptions* is a count of the TrackException reports received by the portal in the sampling interval of the chart.</span></span> <span data-ttu-id="9f6c2-156">Include solo le eccezioni gestite in cui sono state scritte chiamate TrackException nel codice e non include [le eccezioni non gestite](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9f6c2-156">It includes only the handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="9f6c2-157">Avvisi</span><span class="sxs-lookup"><span data-stu-id="9f6c2-157">Alerts</span></span>
<span data-ttu-id="9f6c2-158">Come per altre metriche, è possibile [impostare un avviso](app-insights-alerts.md) per ricevere una notifica se un contatore delle prestazioni supera un limite specificato.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-158">Like other metrics, you can [set an alert](app-insights-alerts.md) to warn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="9f6c2-159">Aprire il pannello Avvisi e fare clic su Aggiungi avviso.</span><span class="sxs-lookup"><span data-stu-id="9f6c2-159">Open the Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="9f6c2-160"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f6c2-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9f6c2-161">Rilevamento delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9f6c2-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="9f6c2-162">Rilevamento delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="9f6c2-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

