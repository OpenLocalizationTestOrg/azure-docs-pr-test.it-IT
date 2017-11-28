---
title: contatori aaaPerformance in Application Insights | Documenti Microsoft
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
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="6821d-103">Contatori delle prestazioni di sistema in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6821d-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="6821d-104">Windows offre un'ampia gamma di [contatori delle prestazioni](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters), ad esempio su occupazione della CPU, memoria, disco e utilizzo di rete.</span><span class="sxs-lookup"><span data-stu-id="6821d-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="6821d-105">È anche possibile definire contatori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6821d-105">You can also define your own.</span></span> <span data-ttu-id="6821d-106">[Application Insights](app-insights-overview.md) consente di visualizzare i contatori delle prestazioni se l'applicazione è in esecuzione in IIS in un toowhich di host o macchina virtuale locale si dispone dell'accesso amministrativo.</span><span class="sxs-lookup"><span data-stu-id="6821d-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="6821d-107">grafici di Hello indicano un'applicazione in tempo reale hello risorse tooyour disponibili e possono semplificare tooidentify sbilanciamento del carico tra le istanze del server.</span><span class="sxs-lookup"><span data-stu-id="6821d-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="6821d-108">I contatori delle prestazioni vengono visualizzati nel Pannello di server hello, che include una tabella che Segmenta dall'istanza del server.</span><span class="sxs-lookup"><span data-stu-id="6821d-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="6821d-110">I contatori delle prestazioni non sono disponibili per App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="6821d-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="6821d-111">Ma è possibile [inviare informazioni di diagnostica Azure tooApplication](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="6821d-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="6821d-112">Visualizzare i contatori</span><span class="sxs-lookup"><span data-stu-id="6821d-112">View counters</span></span>
<span data-ttu-id="6821d-113">Pannello server Hello viene illustrato un set predefinito di contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="6821d-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="6821d-114">toosee altri contatori, modificare i grafici di hello nel pannello server hello o aprire una nuova [Esplora metriche](app-insights-metrics-explorer.md) pannello e aggiungere nuovi grafici.</span><span class="sxs-lookup"><span data-stu-id="6821d-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="6821d-115">contatori di Hello disponibili sono elencati come metriche quando si modifica un grafico.</span><span class="sxs-lookup"><span data-stu-id="6821d-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Contatori delle prestazioni segnalati in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="6821d-117">creare tutti i grafici più utili in un'unica posizione, toosee un [dashboard](app-insights-dashboards.md) e aggiungerli tooit.</span><span class="sxs-lookup"><span data-stu-id="6821d-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="6821d-118">Aggiungere contatori</span><span class="sxs-lookup"><span data-stu-id="6821d-118">Add counters</span></span>
<span data-ttu-id="6821d-119">Se il contatore delle prestazioni hello desiderato non è visualizzato nell'elenco di hello delle metriche, sono perché hello Application Insights SDK non è raccolta nel server web.</span><span class="sxs-lookup"><span data-stu-id="6821d-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="6821d-120">È possibile configurarlo toodo così.</span><span class="sxs-lookup"><span data-stu-id="6821d-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="6821d-121">Scoprire quali i contatori sono disponibili nel server tramite questo comando di PowerShell nel server di hello:</span><span class="sxs-lookup"><span data-stu-id="6821d-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="6821d-122">Vedere [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).</span><span class="sxs-lookup"><span data-stu-id="6821d-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="6821d-123">Aprire ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="6821d-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="6821d-124">Se si aggiungono Application Insights tooyour app durante lo sviluppo, modificare Applicationinsights nel progetto e quindi ridistribuirlo tooyour server.</span><span class="sxs-lookup"><span data-stu-id="6821d-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="6821d-125">Se si utilizza monitoraggio stato tooinstrument un'app web in fase di esecuzione, è possibile trovare Applicationinsights nella directory radice hello dell'app hello in IIS.</span><span class="sxs-lookup"><span data-stu-id="6821d-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="6821d-126">Aggiornarlo qui in ogni istanza del server.</span><span class="sxs-lookup"><span data-stu-id="6821d-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="6821d-127">Modifica della direttiva di agente di raccolta dati prestazioni hello:</span><span class="sxs-lookup"><span data-stu-id="6821d-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="6821d-128">È possibile acquisire contatori standard e quelli implementati manualmente.</span><span class="sxs-lookup"><span data-stu-id="6821d-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="6821d-129">`\Objects\Processes` è un esempio di contatore standard, disponibile in tutti i sistemi Windows.</span><span class="sxs-lookup"><span data-stu-id="6821d-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="6821d-130">`\Sales(photo)\# Items Sold` è un esempio di contatore personalizzato che può essere implementato in un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6821d-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="6821d-131">formato hello è `\Category(instance)\Counter"`, o per le categorie che non includono istanze, semplicemente `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="6821d-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="6821d-132">`ReportAs`è necessario per i nomi dei contatori che non corrispondono a `[a-zA-Z()/-_ \.]+` -, ovvero contengono caratteri che non si trovano in hello set seguenti: lettere, arrotondare tra parentesi quadre, barra (/), trattino, carattere di sottolineatura, spazio, punto.</span><span class="sxs-lookup"><span data-stu-id="6821d-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="6821d-133">Se si specifica un'istanza, verranno raccolti come una dimensione "CounterInstanceName" di hello riportato metrica.</span><span class="sxs-lookup"><span data-stu-id="6821d-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="6821d-134">Raccogliere contatori delle prestazioni nel codice</span><span class="sxs-lookup"><span data-stu-id="6821d-134">Collecting performance counters in code</span></span>
<span data-ttu-id="6821d-135">le prestazioni del sistema toocollect contatori e inviarle tooApplication Insights, è possibile adattare frammento hello seguente:</span><span class="sxs-lookup"><span data-stu-id="6821d-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="6821d-136">Oppure è possibile eseguire la stessa cosa con metriche personalizzate creato hello:</span><span class="sxs-lookup"><span data-stu-id="6821d-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="6821d-137">Contatori delle prestazioni in Analytics</span><span class="sxs-lookup"><span data-stu-id="6821d-137">Performance counters in Analytics</span></span>
<span data-ttu-id="6821d-138">È possibile cercare e visualizzare report dei contatori delle prestazioni in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="6821d-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="6821d-139">Hello **performanceCounters** schema espone hello `category`, `counter` nome, e `instance` nome di ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="6821d-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="6821d-140">Nei dati di telemetria hello per ogni applicazione, verrà visualizzato solo i contatori di hello per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="6821d-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="6821d-141">Ad esempio, toosee i contatori sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="6821d-141">For example, toosee what counters are available:</span></span> 

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="6821d-143">("Instance" qui si riferisce toohello istanza del contatore delle prestazioni, non hello istanza macchina ruolo o del server.</span><span class="sxs-lookup"><span data-stu-id="6821d-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="6821d-144">nome dell'istanza del contatore delle prestazioni Hello in genere i segmenti di contatori, ad esempio il tempo del processore in base al nome hello del processo di hello o dell'applicazione.)</span><span class="sxs-lookup"><span data-stu-id="6821d-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="6821d-145">un grafico di memoria disponibile nel periodo recente hello tooget:</span><span class="sxs-lookup"><span data-stu-id="6821d-145">tooget a chart of available memory over hello recent period:</span></span> 

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="6821d-147">Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità di hello hello server dell'istanza dell'host in cui l'app è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6821d-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="6821d-148">Ad esempio, toocompare hello prestazioni dell'app in computer diversi hello:</span><span class="sxs-lookup"><span data-stu-id="6821d-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="6821d-150">Conteggi di ASP.NET e Application Insights</span><span class="sxs-lookup"><span data-stu-id="6821d-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="6821d-151">*Qual è la differenza hello tra velocità eccezione hello e metriche eccezioni?*</span><span class="sxs-lookup"><span data-stu-id="6821d-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="6821d-152">*Tasso di eccezione* è un contatore delle prestazioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="6821d-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="6821d-153">Hello CLR conta hello gestite le eccezioni non gestite che vengono generate e divide totale hello in un intervallo di campionamento per lunghezza hello dell'intervallo di hello.</span><span class="sxs-lookup"><span data-stu-id="6821d-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="6821d-154">raccoglie il risultato Hello Application Insights SDK e lo invia toohello portale.</span><span class="sxs-lookup"><span data-stu-id="6821d-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="6821d-155">*Eccezioni* è un conteggio di hello TrackException report ricevuti dal portale hello nell'intervallo di campionamento hello del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="6821d-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="6821d-156">Include solo hello gestite le eccezioni in cui è stato scritto TrackException chiama nel codice e non include tutti [le eccezioni non gestite](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="6821d-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="6821d-157">Avvisi</span><span class="sxs-lookup"><span data-stu-id="6821d-157">Alerts</span></span>
<span data-ttu-id="6821d-158">Ad esempio altre metriche, è possibile [impostare un avviso](app-insights-alerts.md) toowarn se un contatore delle prestazioni è di fuori di un limite specificato.</span><span class="sxs-lookup"><span data-stu-id="6821d-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="6821d-159">Aprire il pannello di avvisi hello e fare clic su Aggiungi avviso.</span><span class="sxs-lookup"><span data-stu-id="6821d-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="6821d-160"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6821d-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="6821d-161">Rilevamento delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="6821d-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="6821d-162">Rilevamento delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="6821d-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

