---
title: prestazioni dell'applicazione web di Azure aaaMonitor | Documenti Microsoft
description: Monitoraggio delle prestazioni applicative per le app Web di Azure. Tempo di caricamento e risposta del grafico, informazioni sulle dipendenze e impostazione di avvisi sulle prestazioni.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="2d319-104">Monitoraggio delle prestazioni dell'applicazione web di Azure</span><span class="sxs-lookup"><span data-stu-id="2d319-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="2d319-105">In hello [portale Azure](https://portal.azure.com) è possibile impostare il monitoraggio delle prestazioni dell'applicazione per il [App web di Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="2d319-106">[Azure Application Insights](app-insights-overview.md) Instrumenta la telemetria dell'app toosend sui relativi toohello attività servizio di Application Insights, in cui sono stati archiviato e analizzato.</span><span class="sxs-lookup"><span data-stu-id="2d319-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="2d319-107">Non esiste, metrica grafici e strumenti di ricerca possono essere utilizzati toohelp diagnosticare i problemi, migliorare le prestazioni e valutare l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="2d319-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="2d319-108">Fase di esecuzione o fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="2d319-108">Run time or build time</span></span>
<span data-ttu-id="2d319-109">È possibile configurare il monitoraggio tramite la strumentazione dell'applicazione hello in uno dei due modi:</span><span class="sxs-lookup"><span data-stu-id="2d319-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="2d319-110">**Fase di esecuzione** : è possibile selezionare un'estensione di monitoraggio delle prestazioni quando l'app Web è già attiva.</span><span class="sxs-lookup"><span data-stu-id="2d319-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="2d319-111">Non è necessario toorebuild oppure reinstallare l'app.</span><span class="sxs-lookup"><span data-stu-id="2d319-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="2d319-112">Si ottiene un set di pacchetti standard che monitorano i tempi di risposta, le percentuali di riuscita, le eccezioni, le dipendenze e così via.</span><span class="sxs-lookup"><span data-stu-id="2d319-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="2d319-113">**Fase di compilazione** : è possibile installare un pacchetto nell'app durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2d319-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="2d319-114">Questa opzione è più versatile.</span><span class="sxs-lookup"><span data-stu-id="2d319-114">This option is more versatile.</span></span> <span data-ttu-id="2d319-115">In aggiunta toohello stessi pacchetti standard, è possibile scrivere dati di telemetria hello codice toocustomize o toosend propri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2d319-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="2d319-116">È possibile registrare le attività specifiche o registrare gli eventi in base toohello semantica del dominio applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d319-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="2d319-117">Strumentazione della fase di esecuzione con Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d319-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="2d319-118">Se si esegue già un'App Web in Azure, vengono già visualizzati alcuni dati di monitoraggio, cioè la frequenza di esecuzione con errori e la frequenza delle richieste.</span><span class="sxs-lookup"><span data-stu-id="2d319-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="2d319-119">Aggiungere altre, ad esempio tempi di risposta, monitoraggio chiamate toodependencies, rilevamento intelligente e potente linguaggio di query Log Analitica hello tooget di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d319-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="2d319-120">**Selezionare Application Insights** nel Pannello di controllo Azure hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="2d319-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![In Monitoraggio scegliere Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="2d319-122">Scegliere toocreate una nuova risorsa, a meno che non è già stata configurata una risorsa di Application Insights per l'app da un'altra route.</span><span class="sxs-lookup"><span data-stu-id="2d319-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="2d319-123">**Instrumentare l'App Web** dopo l'installazione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d319-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentazione dell'App Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="2d319-125">**Abilitare il monitoraggio lato client** per la visualizzazione delle pagine e la telemetria utente.</span><span class="sxs-lookup"><span data-stu-id="2d319-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="2d319-126">Selezionare Impostazioni > Impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="2d319-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="2d319-127">In Impostazioni app aggiungere una nuova coppia chiave-valore:</span><span class="sxs-lookup"><span data-stu-id="2d319-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="2d319-128">Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="2d319-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="2d319-129">Valore: `true`</span><span class="sxs-lookup"><span data-stu-id="2d319-129">Value: `true`</span></span>
   * <span data-ttu-id="2d319-130">**Salvare** hello impostazioni e **riavviare** l'app.</span><span class="sxs-lookup"><span data-stu-id="2d319-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="2d319-131">**Monitorare l'app**.</span><span class="sxs-lookup"><span data-stu-id="2d319-131">**Monitor your app**.</span></span>  <span data-ttu-id="2d319-132">[Dati hello Expore](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="2d319-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="2d319-133">In un secondo momento, è possibile compilare app hello con Application Insights, se si desidera.</span><span class="sxs-lookup"><span data-stu-id="2d319-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="2d319-134">*Come rimuovere Application Insights, o passare toosending tooanother risorse?*</span><span class="sxs-lookup"><span data-stu-id="2d319-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="2d319-135">In Azure, pannello di controllo aprire hello web app e in strumenti di sviluppo, aprire **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="2d319-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="2d319-136">Eliminare l'estensione Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="2d319-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="2d319-137">Quindi sotto monitoraggio, scegliere Application Insights e creare o selezionare hello risorsa desiderata.</span><span class="sxs-lookup"><span data-stu-id="2d319-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="2d319-138">Compilare l'applicazione hello con Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d319-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="2d319-139">Application Insights può fornire ulteriori dati di telemetria installando un SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d319-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="2d319-140">In particolare, è possibile raccogliere i log di traccia, [scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md) e ottenere report di eccezione più dettagliati.</span><span class="sxs-lookup"><span data-stu-id="2d319-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="2d319-141">**In Visual Studio** 2013 Update 2 o versione successiva configurare Application Insights per il progetto.</span><span class="sxs-lookup"><span data-stu-id="2d319-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="2d319-142">Progetto web hello e scegliere **Aggiungi > Application Insights** o **Configura Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2d319-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Fare clic sul progetto web hello e scegliere di aggiungere o configurare Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="2d319-144">Se viene chiesto toosign in, utilizzare le credenziali di hello per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d319-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="2d319-145">operazione Hello ha due effetti:</span><span class="sxs-lookup"><span data-stu-id="2d319-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="2d319-146">Crea una risorsa di Application Insights in Azure, in cui vengono archiviati, analizzati e visualizzati i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="2d319-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="2d319-147">Aggiunge hello NuGet di Application Insights tooyour codice di pacchetto (se non è presente già) e lo configura toosend telemetria toohello risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d319-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="2d319-148">**Verificare i dati di telemetria hello** da app di hello in esecuzione nel computer di sviluppo (F5).</span><span class="sxs-lookup"><span data-stu-id="2d319-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="2d319-149">**Pubblicare l'applicazione hello** tooAzure in hello come di consueto.</span><span class="sxs-lookup"><span data-stu-id="2d319-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="2d319-150">*Come passare risorsa di Application Insights toosending tooa diversi?*</span><span class="sxs-lookup"><span data-stu-id="2d319-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="2d319-151">In Visual Studio, progetto hello pulsante destro del mouse, scegliere **Configura Application Insights** e scegliere hello risorsa desiderata.</span><span class="sxs-lookup"><span data-stu-id="2d319-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="2d319-152">È possibile ottenere hello opzione toocreate una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="2d319-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="2d319-153">Ricompilare e ridistribuire.</span><span class="sxs-lookup"><span data-stu-id="2d319-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="2d319-154">Esplorare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="2d319-154">Explore hello data</span></span>
1. <span data-ttu-id="2d319-155">Nel Pannello di Application Insights hello del Pannello di controllo di app web, consente di visualizzare metriche in tempo reale, che mostra le richieste e gli errori all'interno di un secondo o due di essi in corso.</span><span class="sxs-lookup"><span data-stu-id="2d319-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="2d319-156">È molto utile visualizzare questi dati quando si esegue di nuovo la pubblicazione di un'app, perché eventuali problemi sono immediatamente visibili.</span><span class="sxs-lookup"><span data-stu-id="2d319-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="2d319-157">Fare clic sulle toohello completo della risorsa Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2d319-157">Click through toohello full Application Insights resource.</span></span>

    ![Fare clic](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="2d319-159">È anche possibile accedervi direttamente dal riquadro di esplorazione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d319-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="2d319-160">Fare clic sulle tooget qualsiasi grafico dettaglio:</span><span class="sxs-lookup"><span data-stu-id="2d319-160">Click through any chart tooget more detail:</span></span>
   
    ![Nel pannello della panoramica hello Application Insights, fare clic su un grafico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="2d319-162">È possibile [personalizzare i pannelli delle metriche](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="2d319-163">Fare clic sulle altre toosee singoli eventi e le relative proprietà:</span><span class="sxs-lookup"><span data-stu-id="2d319-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Fare clic su una ricerca filtrata su tale tipo di un tooopen di tipo evento](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="2d319-165">Si noti hello "..." tooopen collegamento tutte le proprietà.</span><span class="sxs-lookup"><span data-stu-id="2d319-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="2d319-166">È possibile [personalizzare le ricerche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="2d319-167">Per le ricerche più potenti su dati di telemetria, utilizzare hello [il linguaggio di query Log Analitica](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="2d319-168">Altri dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="2d319-168">More telemetry</span></span>

* [<span data-ttu-id="2d319-169">Dati di caricamento della pagina Web</span><span class="sxs-lookup"><span data-stu-id="2d319-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="2d319-170">Telemetria personalizzata</span><span class="sxs-lookup"><span data-stu-id="2d319-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="2d319-171">Video</span><span class="sxs-lookup"><span data-stu-id="2d319-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="2d319-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d319-172">Next steps</span></span>
* <span data-ttu-id="2d319-173">[Eseguire il profiler di hello nella tua app in tempo reale](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="2d319-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="2d319-174">[Funzioni di Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample): monitorare Funzioni di Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="2d319-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="2d319-175">[Abilitare diagnostica di Azure](app-insights-azure-diagnostics.md) tooApplication toobe inviate informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2d319-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="2d319-176">[Monitorare le metriche di integrità servizio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.</span><span class="sxs-lookup"><span data-stu-id="2d319-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="2d319-177">[Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ogni volta che si verificano eventi operativi o le metriche superano una soglia.</span><span class="sxs-lookup"><span data-stu-id="2d319-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="2d319-178">Utilizzare [Application Insights per le app JavaScript e pagine web](app-insights-javascript.md) telemetria client tooget dai browser hello che visita una pagina web.</span><span class="sxs-lookup"><span data-stu-id="2d319-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="2d319-179">[Configurare i test web disponibilità](app-insights-monitor-web-app-availability.md) toobe ricevere un avviso se il sito è inattivo.</span><span class="sxs-lookup"><span data-stu-id="2d319-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

