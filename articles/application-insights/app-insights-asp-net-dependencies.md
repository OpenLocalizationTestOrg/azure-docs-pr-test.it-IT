---
title: Monitoraggio delle dipendenze in Azure Application Insights | Microsoft Docs
description: "Analizzare l'uso, la disponibilità e le prestazioni dell'applicazione locale o Web di Microsoft Azure con Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="9d9de-103">Impostare Application Insights: tenere traccia delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d9de-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="9d9de-104">Una *dipendenza* è un componente esterno chiamato dall'app.</span><span class="sxs-lookup"><span data-stu-id="9d9de-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="9d9de-105">In genere è un servizio chiamato con il protocollo HTTP, oppure un database o un file system.</span><span class="sxs-lookup"><span data-stu-id="9d9de-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="9d9de-106">[Application Insights](app-insights-overview.md) misura per quanto tempo l'applicazione attende le dipendenze e la frequenza con la quale una chiamata alle dipendenze non riesce.</span><span class="sxs-lookup"><span data-stu-id="9d9de-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="9d9de-107">È possibile esaminare chiamate specifiche e correlarle a richieste ed eccezioni.</span><span class="sxs-lookup"><span data-stu-id="9d9de-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![grafici di esempio](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="9d9de-109">Il monitoraggio predefinito delle dipendenze attualmente segnala chiamate ai seguenti tipi di dipendenze:</span><span class="sxs-lookup"><span data-stu-id="9d9de-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="9d9de-110">Server</span><span class="sxs-lookup"><span data-stu-id="9d9de-110">Server</span></span>
  * <span data-ttu-id="9d9de-111">Database SQL</span><span class="sxs-lookup"><span data-stu-id="9d9de-111">SQL databases</span></span>
  * <span data-ttu-id="9d9de-112">Servizi Web ASP.NET e WCF che usano i binding basati su HTTP</span><span class="sxs-lookup"><span data-stu-id="9d9de-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="9d9de-113">Chiamate HTTP locali o remote</span><span class="sxs-lookup"><span data-stu-id="9d9de-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="9d9de-114">Azure Cosmos DB, tabelle, archiviazione BLOB e coda</span><span class="sxs-lookup"><span data-stu-id="9d9de-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="9d9de-115">Pagina Web</span><span class="sxs-lookup"><span data-stu-id="9d9de-115">Web pages</span></span>
  * <span data-ttu-id="9d9de-116">Chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="9d9de-116">AJAX calls</span></span>

<span data-ttu-id="9d9de-117">Il monitoraggio funziona tramite l'uso di [strumentazione con codice byte](https://msdn.microsoft.com/library/z9z62c29.aspx) basata su determinati metodo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="9d9de-118">L'overhead delle prestazioni è minimo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="9d9de-119">È anche possibile scrivere chiamate SDK per monitorare altre dipendenze, sia nel codice client che nel codice server, usando l'[API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="9d9de-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="9d9de-120">Configurare il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d9de-120">Set up dependency monitoring</span></span>
<span data-ttu-id="9d9de-121">Informazioni sulle dipendenze parziali vengono raccolte automaticamente da [Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9d9de-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="9d9de-122">Per ottenere dati completi, installare l'agente appropriato per il server host.</span><span class="sxs-lookup"><span data-stu-id="9d9de-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="9d9de-123">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="9d9de-123">Platform</span></span> | <span data-ttu-id="9d9de-124">Installa</span><span class="sxs-lookup"><span data-stu-id="9d9de-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="9d9de-125">Server IIS</span><span class="sxs-lookup"><span data-stu-id="9d9de-125">IIS Server</span></span> |<span data-ttu-id="9d9de-126">[Installare Status Monitor nel server](app-insights-monitor-performance-live-website-now.md) oppure [aggiornare l'applicazione a .NET Framework 4.6 o versione successiva](http://go.microsoft.com/fwlink/?LinkId=528259) e installare [Application Insights SDK](app-insights-asp-net.md) nell'app.</span><span class="sxs-lookup"><span data-stu-id="9d9de-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="9d9de-127">App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="9d9de-127">Azure Web App</span></span> |<span data-ttu-id="9d9de-128">[Aprire il pannello Application Insights nel pannello di controllo dell'app Web](app-insights-azure-web-apps.md) e scegliere Installa, se richiesto.</span><span class="sxs-lookup"><span data-stu-id="9d9de-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="9d9de-129">Servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="9d9de-129">Azure Cloud Service</span></span> |<span data-ttu-id="9d9de-130">[Usare l'attività di avvio](app-insights-cloudservices.md) oppure [installare .NET Framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9d9de-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="9d9de-131">Dove trovare i dati sulle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d9de-131">Where to find dependency data</span></span>
* <span data-ttu-id="9d9de-132">La [mappa delle applicazioni](#application-map) visualizza le dipendenze tra l'app e i componenti adiacenti.</span><span class="sxs-lookup"><span data-stu-id="9d9de-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="9d9de-133">I [pannelli Prestazioni, Browser ed Errori](#performance-and-blades) visualizzano i dati sulle dipendenze del server.</span><span class="sxs-lookup"><span data-stu-id="9d9de-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="9d9de-134">Il [pannello Browser](#ajax-calls) visualizza le chiamate AJAX dai browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9d9de-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="9d9de-135">[Fare clic sulle richieste lente o non riuscite](#diagnose-slow-requests) per controllare le chiamate alle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d9de-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="9d9de-136">L'[analisi](#analytics) può essere usata per effettuare una query dei dati sulle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d9de-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="9d9de-137">Mappa delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="9d9de-137">Application Map</span></span>
<span data-ttu-id="9d9de-138">La mappa delle applicazioni funge da strumento visivo per individuare le dipendenze tra i componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9d9de-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="9d9de-139">Viene generata automaticamente dai dati di telemetria provenienti dall'app.</span><span class="sxs-lookup"><span data-stu-id="9d9de-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="9d9de-140">Questo esempio illustra le chiamate AJAX dagli script del browser e le chiamate REST dall'app server a due servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="9d9de-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Mappa delle applicazioni](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="9d9de-142">**Passare dalle caselle** alla dipendenza pertinente e ad altri grafici.</span><span class="sxs-lookup"><span data-stu-id="9d9de-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="9d9de-143">**Aggiungere la mappa** al [dashboard](app-insights-dashboards.md), dove sarà completamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="9d9de-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="9d9de-144">[Altre informazioni](app-insights-app-map.md)</span><span class="sxs-lookup"><span data-stu-id="9d9de-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="9d9de-145">Pannelli Prestazioni ed Errori</span><span class="sxs-lookup"><span data-stu-id="9d9de-145">Performance and failure blades</span></span>
<span data-ttu-id="9d9de-146">Il pannello Prestazioni visualizza la durata delle chiamate alle dipendenze effettuate dall'app server.</span><span class="sxs-lookup"><span data-stu-id="9d9de-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="9d9de-147">Sono presenti un grafico di riepilogo e una tabella segmentata per chiamata.</span><span class="sxs-lookup"><span data-stu-id="9d9de-147">There's a summary chart and a table segmented by call.</span></span>

![Grafici delle dipendenze nel pannello Prestazioni](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="9d9de-149">Fare clic sui grafici di riepilogo o sugli elementi della tabella per cercare le occorrenze non elaborate di queste chiamate.</span><span class="sxs-lookup"><span data-stu-id="9d9de-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Istanze delle chiamate alle dipendenze](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="9d9de-151">I **numeri di errori** sono visualizzati nel pannello **Errori**.</span><span class="sxs-lookup"><span data-stu-id="9d9de-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="9d9de-152">Un errore è un codice restituito non compreso nell'intervallo 200-399 o sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="9d9de-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="9d9de-153">Il **100% di errori**</span><span class="sxs-lookup"><span data-stu-id="9d9de-153">**100% failures?**</span></span> <span data-ttu-id="9d9de-154">indica probabilmente che si stanno ricevendo solo dati parziali sulle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d9de-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="9d9de-155">È necessario [configurare il monitoraggio delle dipendenze appropriato per la piattaforma](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="9d9de-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="9d9de-156">Chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="9d9de-156">AJAX Calls</span></span>
<span data-ttu-id="9d9de-157">Il pannello Browser visualizza la durata e la frequenza di errori delle chiamate AJAX da [JavaScript nelle pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9d9de-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="9d9de-158">Sono visualizzate come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d9de-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="9d9de-159"><a name="diagnosis"></a> Diagnosticare le richieste lente</span><span class="sxs-lookup"><span data-stu-id="9d9de-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="9d9de-160">Ogni evento di richiesta è associato alle chiamate alle dipendenze, alle eccezioni e ad altri eventi registrati mentre l'app elabora la richiesta.</span><span class="sxs-lookup"><span data-stu-id="9d9de-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="9d9de-161">Se quindi alcune richieste non vengono eseguite correttamente, è possibile capire se il problema è causato dalle risposte lente da una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="9d9de-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="9d9de-162">Di seguito è illustrato un esempio.</span><span class="sxs-lookup"><span data-stu-id="9d9de-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="9d9de-163">Traccia dalle richieste alle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d9de-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="9d9de-164">Aprire il pannello Prestazioni ed esaminare la griglia delle richieste:</span><span class="sxs-lookup"><span data-stu-id="9d9de-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Elenco di richieste con conteggi e medie](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="9d9de-166">Quella superiore impiega molto tempo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-166">The top one is taking very long.</span></span> <span data-ttu-id="9d9de-167">È necessario indagare per scoprire in che modo viene impiegato il tempo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="9d9de-168">Fare clic su tale riga per visualizzare gli eventi di richiesta singola:</span><span class="sxs-lookup"><span data-stu-id="9d9de-168">Click that row to see individual request events:</span></span>

![Elenco di occorrenze di richiesta](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="9d9de-170">Fare clic su un'istanza a esecuzione prolungata per esaminarla meglio e scorrere in basso fino alle chiamate alle dipendenze remote correlate a questa richiesta:</span><span class="sxs-lookup"><span data-stu-id="9d9de-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Trovare le chiamate alle dipendenze remote, identificare una durata insolita](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="9d9de-172">Sembra che gran parte del tempo dedicato a questa richiesta sia stato impiegato in una chiamata a un servizio locale.</span><span class="sxs-lookup"><span data-stu-id="9d9de-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="9d9de-173">Selezionare la riga per ottenere altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="9d9de-173">Select that row to get more information:</span></span>

![Fare clic su tale dipendenza remota per identificare il motivo del problema](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="9d9de-175">L'origine del problema è simile a questa.</span><span class="sxs-lookup"><span data-stu-id="9d9de-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="9d9de-176">Dopo avere individuato il problema, rimane solo da capire perché la chiamata sta durando così tanto.</span><span class="sxs-lookup"><span data-stu-id="9d9de-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="9d9de-177">Sequenza temporale della richiesta</span><span class="sxs-lookup"><span data-stu-id="9d9de-177">Request timeline</span></span>
<span data-ttu-id="9d9de-178">In un altro caso non ci sono chiamate a dipendenze particolarmente lunghe,</span><span class="sxs-lookup"><span data-stu-id="9d9de-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="9d9de-179">ma, passando alla visualizzazione della sequenza temporale, è possibile vedere il punto in cui si è verificato il ritardo nell'elaborazione interna:</span><span class="sxs-lookup"><span data-stu-id="9d9de-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Trovare le chiamate alle dipendenze remote, identificare una durata insolita](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="9d9de-181">Dopo la prima chiamata alla dipendenza si verifica una lunga pausa, quindi è opportuno esaminare il codice per capirne il motivo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="9d9de-182">Profilatura del sito live</span><span class="sxs-lookup"><span data-stu-id="9d9de-182">Profile your live site</span></span>

<span data-ttu-id="9d9de-183">Se non si riesce a capire perché trascorre così tanto tempo,</span><span class="sxs-lookup"><span data-stu-id="9d9de-183">No idea where the time goes?</span></span> <span data-ttu-id="9d9de-184">il [profiler di Application Insights](app-insights-profiler.md) traccia le chiamate HTTP al sito live e mostra le funzioni del codice che richiedono più tempo.</span><span class="sxs-lookup"><span data-stu-id="9d9de-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="9d9de-185">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="9d9de-185">Failed requests</span></span>
<span data-ttu-id="9d9de-186">Le richieste non riuscite possono anche essere associate a chiamate non riuscite a dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9d9de-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="9d9de-187">Anche in questo caso è possibile fare clic per risalire al problema.</span><span class="sxs-lookup"><span data-stu-id="9d9de-187">Again, we can click through to track down the problem.</span></span>

![Fare clic sul grafico delle richieste non riuscite](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="9d9de-189">Fare clic su un'occorrenza di una richiesta non riuscita ed esaminare gli eventi associati.</span><span class="sxs-lookup"><span data-stu-id="9d9de-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Fare clic su un tipo di richiesta, fare clic sull'istanza per ottenere una vista diversa della stessa istanza, fare clic su di essa per ottenere informazioni dettagliate sull'eccezione.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="9d9de-191">Analytics</span><span class="sxs-lookup"><span data-stu-id="9d9de-191">Analytics</span></span>
<span data-ttu-id="9d9de-192">È possibile tenere traccia delle dipendenze nel [linguaggio di query di Log Analytics](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="9d9de-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="9d9de-193">Di seguito sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="9d9de-193">Here are some examples.</span></span>

* <span data-ttu-id="9d9de-194">Trovare eventuali chiamate alle dipendenze non riuscite:</span><span class="sxs-lookup"><span data-stu-id="9d9de-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="9d9de-195">Trovare le chiamate AJAX:</span><span class="sxs-lookup"><span data-stu-id="9d9de-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="9d9de-196">Trovare le chiamate alle dipendenze associate alle richieste:</span><span class="sxs-lookup"><span data-stu-id="9d9de-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="9d9de-197">Trovare le chiamate AJAX associate alle visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="9d9de-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="9d9de-198">Rilevamento personalizzato delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d9de-198">Custom dependency tracking</span></span>
<span data-ttu-id="9d9de-199">Il modulo standard per il rilevamento delle dipendenze rileva automaticamente le dipendenze esterne, ad esempio database e API REST.</span><span class="sxs-lookup"><span data-stu-id="9d9de-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="9d9de-200">È tuttavia possibile che si vogliano gestire allo stesso modo altri componenti.</span><span class="sxs-lookup"><span data-stu-id="9d9de-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="9d9de-201">È possibile scrivere il codice che invia informazioni sulle dipendenze, mediante la stessa [API TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency) usata dai moduli standard.</span><span class="sxs-lookup"><span data-stu-id="9d9de-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="9d9de-202">Ad esempio, se si compila il codice con un assembly non scritto personalmente, sarà possibile misurare il tempo necessario per tutte le chiamate all'assembly, per individuare il contributo dell'assembly ai tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="9d9de-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="9d9de-203">Per visualizzare i dati nei grafici relativi alle dipendenze in Application Insights, inviarli mediante `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="9d9de-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="9d9de-204">Per disattivare il modulo standard per il rilevamento delle dipendenze, rimuovere il riferimento a DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="9d9de-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9d9de-205">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9d9de-205">Troubleshooting</span></span>
<span data-ttu-id="9d9de-206">*Il flag di operazione riuscita della dipendenza visualizza sempre true o false.*</span><span class="sxs-lookup"><span data-stu-id="9d9de-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="9d9de-207">*Query SQL no visualizzate completamente.*</span><span class="sxs-lookup"><span data-stu-id="9d9de-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="9d9de-208">Eseguire l'aggiornamento alla versione più recente dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="9d9de-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="9d9de-209">Se la versione di .NET è precedente alla 4.6:</span><span class="sxs-lookup"><span data-stu-id="9d9de-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="9d9de-210">Host IIS: installare l'[agente di Application Insights](app-insights-monitor-performance-live-website-now.md) nei server host.</span><span class="sxs-lookup"><span data-stu-id="9d9de-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="9d9de-211">App Web di Azure: aprire la scheda Application Insights nel pannello di controllo dell'app Web e installare Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9d9de-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="9d9de-212">Video</span><span class="sxs-lookup"><span data-stu-id="9d9de-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="9d9de-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d9de-213">Next steps</span></span>
* [<span data-ttu-id="9d9de-214">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="9d9de-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="9d9de-215">Dati utente e di pagina</span><span class="sxs-lookup"><span data-stu-id="9d9de-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="9d9de-216">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="9d9de-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
