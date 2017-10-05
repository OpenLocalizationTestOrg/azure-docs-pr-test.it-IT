---
title: Monitorare le prestazioni dell'app Web di Azure | Microsoft Docs
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
ms.openlocfilehash: f2bbadfbcb93873ed910aeff050bd6896e2e8fec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="d4449-104">Monitoraggio delle prestazioni dell'applicazione web di Azure</span><span class="sxs-lookup"><span data-stu-id="d4449-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="d4449-105">Nel [portale di Azure](https://portal.azure.com) è possibile configurare il monitoraggio delle prestazioni applicative per le [App Web di Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4449-105">In the [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="d4449-106">[Application Insights di Azure](app-insights-overview.md) consente di instrumentare l'app per inviare dati di telemetria sulle proprie attività al servizio Application Insights, in cui verranno archiviati e analizzati.</span><span class="sxs-lookup"><span data-stu-id="d4449-106">[Azure Application Insights](app-insights-overview.md) instruments your app to send telemetry about its activities to the Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="d4449-107">Sarà quindi possibile usare grafici delle metriche e strumenti di ricerca per diagnosticare i problemi, migliorare le prestazioni e valutare l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="d4449-107">There, metric charts and search tools can be used to help diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="d4449-108">Fase di esecuzione o fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="d4449-108">Run time or build time</span></span>
<span data-ttu-id="d4449-109">È possibile configurare il monitoraggio instrumentando l'app in uno dei due modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4449-109">You can configure monitoring by instrumenting the app in either of two ways:</span></span>

* <span data-ttu-id="d4449-110">**Fase di esecuzione** : è possibile selezionare un'estensione di monitoraggio delle prestazioni quando l'app Web è già attiva.</span><span class="sxs-lookup"><span data-stu-id="d4449-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="d4449-111">Non è necessario ricompilarla o reinstallarla.</span><span class="sxs-lookup"><span data-stu-id="d4449-111">It isn't necessary to rebuild or re-install your app.</span></span> <span data-ttu-id="d4449-112">Si ottiene un set di pacchetti standard che monitorano i tempi di risposta, le percentuali di riuscita, le eccezioni, le dipendenze e così via.</span><span class="sxs-lookup"><span data-stu-id="d4449-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="d4449-113">**Fase di compilazione** : è possibile installare un pacchetto nell'app durante lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d4449-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="d4449-114">Questa opzione è più versatile.</span><span class="sxs-lookup"><span data-stu-id="d4449-114">This option is more versatile.</span></span> <span data-ttu-id="d4449-115">Oltre agli stessi pacchetti standard, è possibile scrivere codice per personalizzare la telemetria o per inviare dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="d4449-115">In addition to the same standard packages, you can write code to customize the telemetry or to send your own telemetry.</span></span> <span data-ttu-id="d4449-116">È possibile registrare attività specifiche o registrare eventi in base alla semantica del dominio dell'app.</span><span class="sxs-lookup"><span data-stu-id="d4449-116">You can log specific activities or record events according to the semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="d4449-117">Strumentazione della fase di esecuzione con Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4449-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="d4449-118">Se si esegue già un'App Web in Azure, vengono già visualizzati alcuni dati di monitoraggio, cioè la frequenza di esecuzione con errori e la frequenza delle richieste.</span><span class="sxs-lookup"><span data-stu-id="d4449-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="d4449-119">Aggiungere Application Insights per usufruire di maggiori funzionalità, come i tempi di risposta, il monitoraggio delle chiamate alle dipendenze, il rilevamento intelligente e l'avanzato linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d4449-119">Add Application Insights to get more, such as response times, monitoring calls to dependencies, smart detection, and the powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="d4449-120">**Selezionare Application Insights** nel pannello di controllo di Azure per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="d4449-120">**Select Application Insights** in the Azure control panel for your web app.</span></span>
   
    ![In Monitoraggio scegliere Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="d4449-122">Scegliere di creare una nuova risorsa, a meno che non sia già stata impostata una risorsa di Application Insights per l'app da un'altra route.</span><span class="sxs-lookup"><span data-stu-id="d4449-122">Choose to create a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="d4449-123">**Instrumentare l'App Web** dopo l'installazione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d4449-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Instrumentazione dell'App Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="d4449-125">**Abilitare il monitoraggio lato client** per la visualizzazione delle pagine e la telemetria utente.</span><span class="sxs-lookup"><span data-stu-id="d4449-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="d4449-126">Selezionare Impostazioni > Impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="d4449-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="d4449-127">In Impostazioni app aggiungere una nuova coppia chiave-valore:</span><span class="sxs-lookup"><span data-stu-id="d4449-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="d4449-128">Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="d4449-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="d4449-129">Valore: `true`</span><span class="sxs-lookup"><span data-stu-id="d4449-129">Value: `true`</span></span>
   * <span data-ttu-id="d4449-130">Salvare le impostazioni scegliendo **Salva** e quindi fare clic su **Riavvia** per riavviare l'app.</span><span class="sxs-lookup"><span data-stu-id="d4449-130">**Save** the settings and **Restart** your app.</span></span>
3. <span data-ttu-id="d4449-131">**Monitorare l'app**.</span><span class="sxs-lookup"><span data-stu-id="d4449-131">**Monitor your app**.</span></span>  <span data-ttu-id="d4449-132">[Esplorare i dati](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="d4449-132">[Expore the data](#explore-the-data).</span></span>

<span data-ttu-id="d4449-133">In seguito, se necessario, sarà possibile creare l'app con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d4449-133">Later, you can build the app with Application Insights if you want.</span></span>

<span data-ttu-id="d4449-134">*Come è possibile rimuovere Application Insights o passare all'invio di un'altra risorsa?*</span><span class="sxs-lookup"><span data-stu-id="d4449-134">*How do I remove Application Insights, or switch to sending to another resource?*</span></span>

* <span data-ttu-id="d4449-135">In Azure aprire il pannello di controllo dell'App Web e aprire **Estensioni** in Strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d4449-135">In Azure, open the web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="d4449-136">Eliminare l'estensione di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d4449-136">Delete the Application Insights extension.</span></span> <span data-ttu-id="d4449-137">Quindi in Monitoraggio scegliere Application Insights e creare o selezionare la risorsa desiderata.</span><span class="sxs-lookup"><span data-stu-id="d4449-137">Then under Monitoring, choose Application Insights and create or select the resource you want.</span></span>

## <a name="build-the-app-with-application-insights"></a><span data-ttu-id="d4449-138">Compilare l'app con Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4449-138">Build the app with Application Insights</span></span>
<span data-ttu-id="d4449-139">Application Insights può fornire ulteriori dati di telemetria installando un SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4449-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="d4449-140">In particolare, è possibile raccogliere i log di traccia, [scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md) e ottenere report di eccezione più dettagliati.</span><span class="sxs-lookup"><span data-stu-id="d4449-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="d4449-141">**In Visual Studio** 2013 Update 2 o versione successiva configurare Application Insights per il progetto.</span><span class="sxs-lookup"><span data-stu-id="d4449-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="d4449-142">Fare clic con il pulsante destro del mouse sul progetto Web e scegliere **Configura Application Insights** o **Aggiungi > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="d4449-142">Right-click the web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Fare clic con il pulsante destro del mouse sul progetto Web e scegliere Aggiungi o Configura Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="d4449-144">Se viene chiesto di effettuare l'accesso, usare le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="d4449-144">If you're asked to sign in, use the credentials for your Azure account.</span></span>
   
    <span data-ttu-id="d4449-145">L'operazione ha due effetti:</span><span class="sxs-lookup"><span data-stu-id="d4449-145">The operation has two effects:</span></span>
   
   1. <span data-ttu-id="d4449-146">Crea una risorsa di Application Insights in Azure, in cui vengono archiviati, analizzati e visualizzati i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d4449-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="d4449-147">Se non è già presente, aggiunge il pacchetto NuGet di Application Insights al codice e lo configura per l'invio della telemetria alla risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4449-147">Adds the Application Insights NuGet package to your code (if it isn't there already), and configures it to send telemetry to the Azure resource.</span></span>
2. <span data-ttu-id="d4449-148">**Testare i dati di telemetria** eseguendo l'app nel computer di sviluppo (F5).</span><span class="sxs-lookup"><span data-stu-id="d4449-148">**Test the telemetry** by running the app in your development machine (F5).</span></span>
3. <span data-ttu-id="d4449-149">**Pubblicare l'app** in Azure nel modo consueto.</span><span class="sxs-lookup"><span data-stu-id="d4449-149">**Publish the app** to Azure in the usual way.</span></span> 

<span data-ttu-id="d4449-150">*Come è possibile passare all'invio a un'altra risorsa di Application Insights?*</span><span class="sxs-lookup"><span data-stu-id="d4449-150">*How do I switch to sending to a different Application Insights resource?*</span></span>

* <span data-ttu-id="d4449-151">In Visual Studio fare clic con il pulsante destro del mouse sul progetto, scegliere **Configura Application Insights** e scegliere la risorsa desiderata.</span><span class="sxs-lookup"><span data-stu-id="d4449-151">In Visual Studio, right-click the project, choose **Configure Application Insights** and choose the resource you want.</span></span> <span data-ttu-id="d4449-152">Sarà possibile creare una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="d4449-152">You get the option to create a new resource.</span></span> <span data-ttu-id="d4449-153">Ricompilare e ridistribuire.</span><span class="sxs-lookup"><span data-stu-id="d4449-153">Rebuild and redeploy.</span></span>

## <a name="explore-the-data"></a><span data-ttu-id="d4449-154">Esplorare i dati</span><span class="sxs-lookup"><span data-stu-id="d4449-154">Explore the data</span></span>
1. <span data-ttu-id="d4449-155">In Application Insights, nel pannello di controllo dell'App Web, vengono visualizzate le metriche in tempo reale: ciò significa che le richieste e gli errori vengono mostrati uno o due secondi dopo che si verificano.</span><span class="sxs-lookup"><span data-stu-id="d4449-155">On the Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="d4449-156">È molto utile visualizzare questi dati quando si esegue di nuovo la pubblicazione di un'app, perché eventuali problemi sono immediatamente visibili.</span><span class="sxs-lookup"><span data-stu-id="d4449-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="d4449-157">Fare clic per visualizzare la risorsa Application Insights completa.</span><span class="sxs-lookup"><span data-stu-id="d4449-157">Click through to the full Application Insights resource.</span></span>

    ![Fare clic](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="d4449-159">È anche possibile accedervi direttamente dal riquadro di esplorazione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4449-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="d4449-160">Fare clic su qualsiasi grafico per visualizzare altri dettagli:</span><span class="sxs-lookup"><span data-stu-id="d4449-160">Click through any chart to get more detail:</span></span>
   
    ![Nel pannello di panoramica di Application Insights, fare clic su un grafico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="d4449-162">È possibile [personalizzare i pannelli delle metriche](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="d4449-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="d4449-163">Fare ancora clic per visualizzare i singoli eventi e le relative proprietà:</span><span class="sxs-lookup"><span data-stu-id="d4449-163">Click through further to see individual events and their properties:</span></span>
   
    ![Fare clic su un tipo di evento per aprire una ricerca filtrata su tale tipo](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="d4449-165">Si noti il collegamento "…" per aprire tutte le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d4449-165">Notice the "..." link to open all properties.</span></span>
   
    <span data-ttu-id="d4449-166">È possibile [personalizzare le ricerche](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="d4449-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="d4449-167">Per ricerche più avanzate sui dati di telemetria, usare il [linguaggio di query di Log Analytics](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="d4449-167">For more powerful searches over your telemetry, use the [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="d4449-168">Altri dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="d4449-168">More telemetry</span></span>

* [<span data-ttu-id="d4449-169">Dati di caricamento della pagina Web</span><span class="sxs-lookup"><span data-stu-id="d4449-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="d4449-170">Telemetria personalizzata</span><span class="sxs-lookup"><span data-stu-id="d4449-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="d4449-171">Video</span><span class="sxs-lookup"><span data-stu-id="d4449-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d4449-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4449-172">Next steps</span></span>
* <span data-ttu-id="d4449-173">[Eseguire il profiler sull'app live](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="d4449-173">[Run the profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="d4449-174">[Funzioni di Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample): monitorare Funzioni di Azure con Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4449-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="d4449-175">[Abilitare l'invio dei dati di diagnostica di Azure](app-insights-azure-diagnostics.md) ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d4449-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) to be sent to Application Insights.</span></span>
* <span data-ttu-id="d4449-176">[Monitorare le metriche di integrità del servizio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) per assicurarsi che il servizio sia disponibile e reattivo.</span><span class="sxs-lookup"><span data-stu-id="d4449-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="d4449-177">[Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ogni volta che si verificano eventi operativi o le metriche superano una soglia.</span><span class="sxs-lookup"><span data-stu-id="d4449-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="d4449-178">Usare [Analisi dell'utilizzo per applicazioni Web con Application Insights](app-insights-javascript.md) per ottenere i dati di telemetria dei client dai browser che visitano una pagina Web.</span><span class="sxs-lookup"><span data-stu-id="d4449-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) to get client telemetry from the browsers that visit a web page.</span></span>
* <span data-ttu-id="d4449-179">[Monitorare la disponibilità e la velocità di risposta dei siti Web](app-insights-monitor-web-app-availability.md) per ricevere un avviso se il sito è inattivo.</span><span class="sxs-lookup"><span data-stu-id="d4449-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) to be alerted if your site is down.</span></span>

