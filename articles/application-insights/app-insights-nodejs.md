---
title: aaaMonitor Node.js servizi con Azure Application Insights | Documenti Microsoft
description: Monitorare le prestazioni e diagnosticare i problemi dei servizi Node.js con Application Insights.
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="0e373-103">Monitorare servizi e app Node.js con Application Insights</span><span class="sxs-lookup"><span data-stu-id="0e373-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="0e373-104">[Azure Application Insights](app-insights-overview.md) consente di monitorare i servizi back-end e componenti dopo aver distribuito le toohelp si [rilevare e diagnosticare rapidamente le prestazioni e altri problemi](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="0e373-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="0e373-105">Usare Azure Application Insights per servizi Node.js ospitati ovunque: nel data center, in app Web e VM di Azure e anche in altri cloud pubblici.</span><span class="sxs-lookup"><span data-stu-id="0e373-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="0e373-106">tooreceive, archiviare, esplorare i dati di monitoraggio, seguire hello seguendo le istruzioni tooinclude un agente nel codice e impostare una risorsa di Application Insights corrispondente in Azure.</span><span class="sxs-lookup"><span data-stu-id="0e373-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="0e373-107">agente di Hello invia risorsa toothat dati per un'ulteriore analisi ed esplorazione.</span><span class="sxs-lookup"><span data-stu-id="0e373-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="0e373-108">agente di Node.js Hello automaticamente è possibile monitorare in ingresso e in uscita richieste HTTP, diverse misurazioni di sistema e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="0e373-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="0e373-109">A partire dalla versione 0.20, può monitorare anche alcuni pacchetti comuni di terze parti come `mongodb`, `mysql` e `redis`.</span><span class="sxs-lookup"><span data-stu-id="0e373-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="0e373-110">Tutti gli eventi correlati di richiesta HTTP in ingresso tooan sono correlati per la risoluzione dei problemi più velocemente.</span><span class="sxs-lookup"><span data-stu-id="0e373-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="0e373-111">È possibile monitorare altri aspetti dell'applicazione e sistema eseguendo manualmente la strumentazione di loro tramite API dell'agente hello descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="0e373-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="0e373-113">Introduzione</span><span class="sxs-lookup"><span data-stu-id="0e373-113">Getting Started</span></span>

<span data-ttu-id="0e373-114">Verrà ora illustrata la configurazione del monitoraggio per un'app o un servizio.</span><span class="sxs-lookup"><span data-stu-id="0e373-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="0e373-115"><a name="resource"></a> Configurare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="0e373-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="0e373-116">**Prima di iniziare**, verificare di avere una sottoscrizione di Azure oppure [ottenerne una nuova gratuitamente][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="0e373-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="0e373-117">Se l'organizzazione ha già una sottoscrizione di Azure, gli amministratori possono seguire [queste istruzioni] [ add-aad-user] tooadd è tooit.</span><span class="sxs-lookup"><span data-stu-id="0e373-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="0e373-118">Ora accedere toohello [portale di Azure] [ portal] e creare una risorsa di Application Insights, come illustrato nell'esempio hello: fare clic su "Nuovo" > "Developer tools" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="0e373-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="0e373-119">risorsa di Hello include un endpoint per la ricezione di dati di telemetria, l'archiviazione dei dati, salvata i report e dashboard, regola e configurazione degli avvisi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="0e373-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Creare una risorsa di Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="0e373-121">Nella pagina di creazione di risorse hello, scegliere "Node.js applicazione" hello applicazione tipo elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="0e373-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="0e373-122">tipo di app Hello determina il set predefinito hello di dashboard e report creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0e373-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="0e373-123">Qualsiasi risorsa di Application Insights, tuttavia, può di fatto raccogliere dati da qualsiasi linguaggio e piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0e373-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Modulo per una nuova risorsa di Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="0e373-125"><a name="agent"></a>Impostare l'agente di Node.js hello</span><span class="sxs-lookup"><span data-stu-id="0e373-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="0e373-126">Ora è agente hello tooinclude di tempo nell'applicazione in modo da poter raccogliere i dati.</span><span class="sxs-lookup"><span data-stu-id="0e373-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="0e373-127">Per iniziare, copiare la chiave di strumentazione della risorsa (qui tooas il `ikey`) dal portale di hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0e373-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="0e373-128">Hello App Insights sistema Usa questo tooyour dati chiave toomap risorse di Azure, pertanto è necessario toospecify in una variabile di ambiente o il codice per toouse agente hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Copiare la chiave di strumentazione](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="0e373-130">Successivamente, aggiungere le dipendenze di hello Node.js agente libreria tooyour dell'app tramite file package. JSON.</span><span class="sxs-lookup"><span data-stu-id="0e373-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="0e373-131">Dalla cartella radice di hello dell'app, eseguire:</span><span class="sxs-lookup"><span data-stu-id="0e373-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="0e373-132">È ora necessario tooexplicitly caricamento della libreria hello nel codice.</span><span class="sxs-lookup"><span data-stu-id="0e373-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="0e373-133">Poiché l'agente di hello inserisce strumentazione in molte altre librerie, è necessario caricare il prima possibile, anche prima delle altre `require` istruzioni.</span><span class="sxs-lookup"><span data-stu-id="0e373-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="0e373-134">avvio tooget, nella parte superiore di hello del primo file. js aggiungere:</span><span class="sxs-lookup"><span data-stu-id="0e373-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="0e373-135">Hello `setup` metodo consente di configurare la chiave di strumentazione hello (e pertanto risorse di Azure) toobe utilizzato per impostazione predefinita per gli elementi di tutte le revisioni.</span><span class="sxs-lookup"><span data-stu-id="0e373-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="0e373-136">Chiamare `start` dopo la configurazione è la raccolta di toobegin completato e l'invio di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="0e373-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="0e373-137">È anche possibile fornire un ikey tramite la variabile di ambiente hello APPINSIGHTS\_manualmente INSTRUMENTATIONKEY anziché passarlo manualmente troppo `setup()` o `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="0e373-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="0e373-138">Questa procedura consente di mantenere ikeys fuori dal codice sorgente eseguito il commit e toospecify ikeys diversi per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="0e373-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="0e373-139">Di seguito sono documentate le opzioni di configurazione aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="0e373-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="0e373-140">È possibile provare agente hello senza l'invio di dati di telemetria impostando hello strumentazione tooany chiave non è una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="0e373-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="0e373-141"><a name="monitor"></a> Monitorare l'app</span><span class="sxs-lookup"><span data-stu-id="0e373-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="0e373-142">agente Hello raccoglie automaticamente dati di telemetria su runtime Node.js hello e alcuni moduli di terze parti comuni.</span><span class="sxs-lookup"><span data-stu-id="0e373-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="0e373-143">Utilizzare il toogenerate ora applicazione alcuni di questi dati.</span><span class="sxs-lookup"><span data-stu-id="0e373-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="0e373-144">Quindi, nel hello [portale di Azure] [ portal] Sfoglia risorsa di Application Insights toohello creato in precedenza e cercare il primo pochi punti dati nella sequenza temporale di panoramica hello, come illustrato di seguito immagine hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="0e373-145">Fare clic sui grafici hello per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="0e373-145">Click through hello charts for more details.</span></span>

![Primi punti dati](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="0e373-147">Fare clic su hello applicazione mappa pulsante tooview hello topologia individuata per l'app, come illustrato di seguito immagine hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="0e373-148">Fare clic sui componenti nella mappa hello per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="0e373-148">Click through components in hello map for more details.</span></span>

![Mappa app di esempio](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="0e373-150">Ulteriori informazioni sull'app e risolvere i problemi usando hello altre viste disponibili nella sezione "Verificare" hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Sezione Analisi](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="0e373-152">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="0e373-152">No data?</span></span>

<span data-ttu-id="0e373-153">Perché l'agente di hello di batch di dati per l'invio di potrebbe verificarsi un ritardo prima gli elementi vengono visualizzati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="0e373-154">Se non viene visualizzato nella risorsa dati provare hello correzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e373-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="0e373-155">Utilizzare un'applicazione hello ulteriormente; eseguire altre azioni toogenerate ulteriori dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="0e373-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="0e373-156">Fare clic su **aggiornamento** in visualizzazione di risorse portale hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="0e373-157">Grafici di aggiornamento automatico periodicamente ma aggiornamento impone questo toohappen immediatamente.</span><span class="sxs-lookup"><span data-stu-id="0e373-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="0e373-158">Verificare che le [porte in uscita necessarie](app-insights-ip-addresses.md) siano aperte.</span><span class="sxs-lookup"><span data-stu-id="0e373-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="0e373-159">Aprire hello [ricerca](app-insights-diagnostic-search.md) riquadro e cercare i singoli eventi.</span><span class="sxs-lookup"><span data-stu-id="0e373-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="0e373-160">Controllare hello [domande frequenti su][].</span><span class="sxs-lookup"><span data-stu-id="0e373-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="0e373-161">Configurazione dell'agente</span><span class="sxs-lookup"><span data-stu-id="0e373-161">Agent Configuration</span></span>

<span data-ttu-id="0e373-162">Di seguito sono metodi di configurazione dell'agente di hello e i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="0e373-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="0e373-163">gli eventi di correlare toofully in un servizio, essere tooset che `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="0e373-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="0e373-164">In questo modo agente hello tootrack contesto nelle richiamate asincrone in Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e373-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="0e373-165">API dell'agente</span><span class="sxs-lookup"><span data-stu-id="0e373-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="0e373-166">.NET API dell'agente Hello è descritto [qui](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0e373-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="0e373-167">È possibile registrare qualsiasi richiesta, eventi, metrica o eccezione utilizzando il client di Application Insights Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="0e373-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="0e373-168">Hello esempio seguente vengono illustrate alcune delle hello API disponibili.</span><span class="sxs-lookup"><span data-stu-id="0e373-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="0e373-169">Tenere traccia delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="0e373-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="0e373-170">Aggiungere gli eventi tooall una proprietà personalizzata</span><span class="sxs-lookup"><span data-stu-id="0e373-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="0e373-171">Tenere traccia delle richieste HTTP GET</span><span class="sxs-lookup"><span data-stu-id="0e373-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="0e373-172">Tenere traccia del tempo di avvio del server</span><span class="sxs-lookup"><span data-stu-id="0e373-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="0e373-173">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="0e373-173">More resources</span></span>

* [<span data-ttu-id="0e373-174">Monitorare la telemetria nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="0e373-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="0e373-175">Presentazione dello strumento Analisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="0e373-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[domande frequenti su]: app-insights-troubleshoot-faq.md
