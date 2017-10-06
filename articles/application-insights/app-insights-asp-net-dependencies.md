---
title: aaaDependency rilevamento in Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="46957-103">Impostare Application Insights: tenere traccia delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="46957-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="46957-104">Una *dipendenza* è un componente esterno chiamato dall'app.</span><span class="sxs-lookup"><span data-stu-id="46957-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="46957-105">In genere è un servizio chiamato con il protocollo HTTP, oppure un database o un file system.</span><span class="sxs-lookup"><span data-stu-id="46957-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="46957-106">[Application Insights](app-insights-overview.md) misura per quanto tempo l'applicazione attende le dipendenze e la frequenza con la quale una chiamata alle dipendenze non riesce.</span><span class="sxs-lookup"><span data-stu-id="46957-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="46957-107">È possibile provare a utilizzare chiamate specifiche e correlarle toorequests ed eccezioni.</span><span class="sxs-lookup"><span data-stu-id="46957-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![grafici di esempio](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="46957-109">attualmente, il monitoraggio delle dipendenze di casella Hello segnala chiamate toothese tipi di dipendenze:</span><span class="sxs-lookup"><span data-stu-id="46957-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="46957-110">Server</span><span class="sxs-lookup"><span data-stu-id="46957-110">Server</span></span>
  * <span data-ttu-id="46957-111">Database SQL</span><span class="sxs-lookup"><span data-stu-id="46957-111">SQL databases</span></span>
  * <span data-ttu-id="46957-112">Servizi Web ASP.NET e WCF che usano i binding basati su HTTP</span><span class="sxs-lookup"><span data-stu-id="46957-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="46957-113">Chiamate HTTP locali o remote</span><span class="sxs-lookup"><span data-stu-id="46957-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="46957-114">Azure Cosmos DB, tabelle, archiviazione BLOB e coda</span><span class="sxs-lookup"><span data-stu-id="46957-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="46957-115">Pagina Web</span><span class="sxs-lookup"><span data-stu-id="46957-115">Web pages</span></span>
  * <span data-ttu-id="46957-116">Chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="46957-116">AJAX calls</span></span>

<span data-ttu-id="46957-117">Il monitoraggio funziona tramite l'uso di [strumentazione con codice byte](https://msdn.microsoft.com/library/z9z62c29.aspx) basata su determinati metodo.</span><span class="sxs-lookup"><span data-stu-id="46957-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="46957-118">L'overhead delle prestazioni è minimo.</span><span class="sxs-lookup"><span data-stu-id="46957-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="46957-119">È anche possibile scrivere un proprio SDK chiama toomonitor altre dipendenze, sia nel codice client e server hello utilizzando hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="46957-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="46957-120">Configurare il monitoraggio delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="46957-120">Set up dependency monitoring</span></span>
<span data-ttu-id="46957-121">Dipendenza parziale vengono raccolti automaticamente mediante hello [Application Insights SDK](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="46957-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="46957-122">tooget completo dei dati, installare l'agente appropriato di hello per server host hello.</span><span class="sxs-lookup"><span data-stu-id="46957-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="46957-123">Piattaforma</span><span class="sxs-lookup"><span data-stu-id="46957-123">Platform</span></span> | <span data-ttu-id="46957-124">Installa</span><span class="sxs-lookup"><span data-stu-id="46957-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="46957-125">Server IIS</span><span class="sxs-lookup"><span data-stu-id="46957-125">IIS Server</span></span> |<span data-ttu-id="46957-126">Entrambi [installa Status Monitor nel server](app-insights-monitor-performance-live-website-now.md) o [l'aggiornamento del framework dell'applicazione too.NET 4.6 o versione successivo](http://go.microsoft.com/fwlink/?LinkId=528259) e installare hello [Application Insights SDK](app-insights-asp-net.md) nell'app.</span><span class="sxs-lookup"><span data-stu-id="46957-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="46957-127">App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="46957-127">Azure Web App</span></span> |<span data-ttu-id="46957-128">Nel Pannello di controllo per l'app web, [blade di Application Insights hello aperti nel Pannello di controllo di app web](app-insights-azure-web-apps.md) e scegliere Installa, se richiesto.</span><span class="sxs-lookup"><span data-stu-id="46957-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="46957-129">Servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="46957-129">Azure Cloud Service</span></span> |<span data-ttu-id="46957-130">[Usare l'attività di avvio](app-insights-cloudservices.md) oppure [installare .NET Framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="46957-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="46957-131">In dati sulle dipendenze toofind</span><span class="sxs-lookup"><span data-stu-id="46957-131">Where toofind dependency data</span></span>
* <span data-ttu-id="46957-132">La [mappa delle applicazioni](#application-map) visualizza le dipendenze tra l'app e i componenti adiacenti.</span><span class="sxs-lookup"><span data-stu-id="46957-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="46957-133">I [pannelli Prestazioni, Browser ed Errori](#performance-and-blades) visualizzano i dati sulle dipendenze del server.</span><span class="sxs-lookup"><span data-stu-id="46957-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="46957-134">Il [pannello Browser](#ajax-calls) visualizza le chiamate AJAX dai browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="46957-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="46957-135">[Fare clic su tramite richieste lente o non riuscite](#diagnose-slow-requests) chiama la relativa dipendenza toocheck.</span><span class="sxs-lookup"><span data-stu-id="46957-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="46957-136">[Analitica](#analytics) possono essere utilizzati tooquery dipendenza dati.</span><span class="sxs-lookup"><span data-stu-id="46957-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="46957-137">Mappa delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="46957-137">Application Map</span></span>
<span data-ttu-id="46957-138">Mappa delle applicazioni agisce come delle dipendenze toodiscovering visivo tra hello dei componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="46957-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="46957-139">Viene generato automaticamente da dati di telemetria hello dall'app.</span><span class="sxs-lookup"><span data-stu-id="46957-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="46957-140">Questo esempio mostra le chiamate AJAX dagli script browser hello e le chiamate REST dal server hello servizi esterni tootwo di app.</span><span class="sxs-lookup"><span data-stu-id="46957-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Mappa delle applicazioni](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="46957-142">**Passare dalle caselle hello** toorelevant dipendenza e altri grafici.</span><span class="sxs-lookup"><span data-stu-id="46957-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="46957-143">**Mappa di hello pin** toohello [dashboard](app-insights-dashboards.md), dove sarà completamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="46957-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="46957-144">[Altre informazioni](app-insights-app-map.md)</span><span class="sxs-lookup"><span data-stu-id="46957-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="46957-145">Pannelli Prestazioni ed Errori</span><span class="sxs-lookup"><span data-stu-id="46957-145">Performance and failure blades</span></span>
<span data-ttu-id="46957-146">Pannello prestazioni Hello Mostra la durata di hello delle chiamate di dipendenza effettuate dall'applicazione server hello.</span><span class="sxs-lookup"><span data-stu-id="46957-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="46957-147">Sono presenti un grafico di riepilogo e una tabella segmentata per chiamata.</span><span class="sxs-lookup"><span data-stu-id="46957-147">There's a summary chart and a table segmented by call.</span></span>

![Grafici delle dipendenze nel pannello Prestazioni](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="46957-149">Fare clic sui grafici di riepilogo hello o hello tabella elementi toosearch non elaborato le occorrenze di queste chiamate.</span><span class="sxs-lookup"><span data-stu-id="46957-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Istanze delle chiamate alle dipendenze](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="46957-151">**Numero di errori nei** vengono visualizzati nella hello **errori** blade.</span><span class="sxs-lookup"><span data-stu-id="46957-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="46957-152">Qualsiasi codice restituito non è in hello intervallo 200-399, o sconosciuto è un errore.</span><span class="sxs-lookup"><span data-stu-id="46957-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="46957-153">Il **100% di errori**</span><span class="sxs-lookup"><span data-stu-id="46957-153">**100% failures?**</span></span> <span data-ttu-id="46957-154">indica probabilmente che si stanno ricevendo solo dati parziali sulle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="46957-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="46957-155">È necessario troppo[impostare dipendenza monitoraggio piattaforma appropriata tooyour](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="46957-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="46957-156">Chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="46957-156">AJAX Calls</span></span>
<span data-ttu-id="46957-157">Pannello browser Hello Mostra la durata di hello e percentuale di errori di AJAX chiamate dal [JavaScript nelle pagine web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="46957-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="46957-158">Sono visualizzate come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="46957-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="46957-159"><a name="diagnosis"></a> Diagnosticare le richieste lente</span><span class="sxs-lookup"><span data-stu-id="46957-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="46957-160">Ogni evento di richiesta è associata a chiamate a dipendenze hello, eccezioni e altri eventi che vengono rilevati durante l'elaborazione dell'applicazione hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="46957-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="46957-161">Se alcune richieste esegue in modo errato, trovare, è possibile definire se si trova a causa di una risposta tooslow da una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="46957-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="46957-162">Di seguito è illustrato un esempio.</span><span class="sxs-lookup"><span data-stu-id="46957-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="46957-163">Esecuzione della traccia da toodependencies richieste</span><span class="sxs-lookup"><span data-stu-id="46957-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="46957-164">Aprire il pannello di prestazioni hello ed esaminare griglia hello di richieste:</span><span class="sxs-lookup"><span data-stu-id="46957-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Elenco di richieste con conteggi e medie](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="46957-166">inizio Hello uno sta richiedendo molto tempo.</span><span class="sxs-lookup"><span data-stu-id="46957-166">hello top one is taking very long.</span></span> <span data-ttu-id="46957-167">Vediamo se è possibile scoprire dove viene impiegato il tempo di hello.</span><span class="sxs-lookup"><span data-stu-id="46957-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="46957-168">Fare clic sulla riga toosee singola richiesta gli eventi:</span><span class="sxs-lookup"><span data-stu-id="46957-168">Click that row toosee individual request events:</span></span>

![Elenco di occorrenze di richiesta](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="46957-170">Fare clic su qualsiasi istanza di a esecuzione prolungata tooinspect ulteriormente e scorrere verso il basso toohello dipendenza remoto chiamate toothis correlati richiesta:</span><span class="sxs-lookup"><span data-stu-id="46957-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Trovare le dipendenze tooRemote chiamate, identificare insolita durata](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="46957-172">Sembra che la maggior parte delle hello ora manutenzione impiegato per la richiesta in un servizio locale tooa di chiamata.</span><span class="sxs-lookup"><span data-stu-id="46957-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="46957-173">Selezionare tale tooget riga per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="46957-173">Select that row tooget more information:</span></span>

![Fare clic su a causa di hello tooidentify tale dipendenza remoto](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="46957-175">Sembra che qui viene ospitata problema hello.</span><span class="sxs-lookup"><span data-stu-id="46957-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="46957-176">È stato individuare il problema di hello, pertanto ora è necessario toofind out perché la chiamata richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="46957-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="46957-177">Sequenza temporale della richiesta</span><span class="sxs-lookup"><span data-stu-id="46957-177">Request timeline</span></span>
<span data-ttu-id="46957-178">In un altro caso non ci sono chiamate a dipendenze particolarmente lunghe,</span><span class="sxs-lookup"><span data-stu-id="46957-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="46957-179">Tuttavia, passando alla visualizzazione cronologia toohello, possiamo vedere dove si è verificato il ritardo di hello l'elaborazione interna:</span><span class="sxs-lookup"><span data-stu-id="46957-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Trovare le dipendenze tooRemote chiamate, identificare insolita durata](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="46957-181">Ci toobe un grande spazio dopo la chiamata della dipendenza prima hello, in modo da esaminare toosee il nostro codice motivo che è.</span><span class="sxs-lookup"><span data-stu-id="46957-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="46957-182">Profilatura del sito live</span><span class="sxs-lookup"><span data-stu-id="46957-182">Profile your live site</span></span>

<span data-ttu-id="46957-183">Non è chiaro quale passare del tempo di hello? Hello [profiler Application Insights](app-insights-profiler.md) tracce HTTP chiama sito attivo tooyour e illustra le funzioni nel codice richiede tempo più lungo di hello.</span><span class="sxs-lookup"><span data-stu-id="46957-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="46957-184">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="46957-184">Failed requests</span></span>
<span data-ttu-id="46957-185">Richieste non riuscite potrebbero inoltre essere associate a toodependencies chiamate non riuscite.</span><span class="sxs-lookup"><span data-stu-id="46957-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="46957-186">Nuovamente, è possibile scorrere tootrack problema hello.</span><span class="sxs-lookup"><span data-stu-id="46957-186">Again, we can click through tootrack down hello problem.</span></span>

![Fare clic sul grafico di hello richieste non riuscite](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="46957-188">Fare clic sulle tooan occorrenza di una richiesta non riuscita ed esaminare gli eventi associati.</span><span class="sxs-lookup"><span data-stu-id="46957-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Fare clic su un tipo di richiesta, fare clic su hello istanza tooget tooa vista diversa della stessa istanza di hello, selezionarlo tooget i dettagli dell'eccezione.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="46957-190">Analytics</span><span class="sxs-lookup"><span data-stu-id="46957-190">Analytics</span></span>
<span data-ttu-id="46957-191">È possibile tenere traccia delle dipendenze in hello [il linguaggio di query Log Analitica](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="46957-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="46957-192">Di seguito sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="46957-192">Here are some examples.</span></span>

* <span data-ttu-id="46957-193">Trovare eventuali chiamate alle dipendenze non riuscite:</span><span class="sxs-lookup"><span data-stu-id="46957-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="46957-194">Trovare le chiamate AJAX:</span><span class="sxs-lookup"><span data-stu-id="46957-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="46957-195">Trovare le chiamate alle dipendenze associate alle richieste:</span><span class="sxs-lookup"><span data-stu-id="46957-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="46957-196">Trovare le chiamate AJAX associate alle visualizzazioni di pagina:</span><span class="sxs-lookup"><span data-stu-id="46957-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="46957-197">Rilevamento personalizzato delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="46957-197">Custom dependency tracking</span></span>
<span data-ttu-id="46957-198">modulo di rilevamento delle dipendenze standard Hello individua automaticamente le dipendenze esterne quali database e le API REST.</span><span class="sxs-lookup"><span data-stu-id="46957-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="46957-199">Ma è possibile che alcuni componenti aggiuntivi di toobe trattate hello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="46957-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="46957-200">È possibile scrivere codice che invia le informazioni sulle dipendenze, utilizzando hello stesso [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) utilizzato dai moduli standard hello.</span><span class="sxs-lookup"><span data-stu-id="46957-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="46957-201">Ad esempio, se si compila il codice con un assembly che non scritto personalmente, è possibile ora tutti hello chiamate tooit, toofind out il contributo che rende la risposta tooyour volte.</span><span class="sxs-lookup"><span data-stu-id="46957-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="46957-202">toohave dati visualizzati nei grafici dipendenza hello in Application Insights, inviarlo tramite `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="46957-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="46957-203">Se si desidera tooswitch off modulo di rilevamento di hello dipendenza standard, rimuovere hello riferimento tooDependencyTrackingTelemetryModule in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="46957-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="46957-204">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="46957-204">Troubleshooting</span></span>
<span data-ttu-id="46957-205">*Il flag di operazione riuscita della dipendenza visualizza sempre true o false.*</span><span class="sxs-lookup"><span data-stu-id="46957-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="46957-206">*Query SQL no visualizzate completamente.*</span><span class="sxs-lookup"><span data-stu-id="46957-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="46957-207">Eseguire l'aggiornamento più recente di hello SDK toohello.</span><span class="sxs-lookup"><span data-stu-id="46957-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="46957-208">Se la versione di .NET è precedente alla 4.6:</span><span class="sxs-lookup"><span data-stu-id="46957-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="46957-209">Host IIS: installare [agente di Application Insights](app-insights-monitor-performance-live-website-now.md) nei server host hello.</span><span class="sxs-lookup"><span data-stu-id="46957-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="46957-210">App web di Azure: Apri Application Insights scheda nel Pannello di controllo di hello web app e installare Application Insights.</span><span class="sxs-lookup"><span data-stu-id="46957-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="46957-211">Video</span><span class="sxs-lookup"><span data-stu-id="46957-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="46957-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46957-212">Next steps</span></span>
* [<span data-ttu-id="46957-213">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="46957-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="46957-214">Dati utente e di pagina</span><span class="sxs-lookup"><span data-stu-id="46957-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="46957-215">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="46957-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
