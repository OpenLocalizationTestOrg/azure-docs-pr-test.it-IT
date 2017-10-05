---
title: Monitorare i servizi Node.js con Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="d1802-103">Monitorare servizi e app Node.js con Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1802-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="d1802-104">[Azure Application Insights](app-insights-overview.md) monitora i componenti e i servizi back-end dopo che sono stati distribuiti consentendo così di [individuare e diagnosticare rapidamente i problemi di prestazioni e di altro tipo](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="d1802-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="d1802-105">Usare Azure Application Insights per servizi Node.js ospitati ovunque: nel data center, in app Web e VM di Azure e anche in altri cloud pubblici.</span><span class="sxs-lookup"><span data-stu-id="d1802-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="d1802-106">Per ricevere, archiviare ed esplorare i dati di monitoraggio, seguire le istruzioni riportate più avanti per includere un agente nel codice e configurare una risorsa di Application Insights corrispondente in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1802-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="d1802-107">L'agente invia i dati a tale risorsa per analisi ed esplorazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d1802-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="d1802-108">L'agente Node.js può monitorare automaticamente le richieste HTTP in ingresso e in uscita, diverse metriche di sistema e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="d1802-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="d1802-109">A partire dalla versione 0.20, può monitorare anche alcuni pacchetti comuni di terze parti come `mongodb`, `mysql` e `redis`.</span><span class="sxs-lookup"><span data-stu-id="d1802-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="d1802-110">Tutti gli eventi relativi a una richiesta HTTP in ingresso vengono correlati per velocizzare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d1802-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="d1802-111">È possibile monitorare aspetti aggiuntivi dell'app e del sistema instrumentandoli manualmente con l'API dell'agente descritta più avanti.</span><span class="sxs-lookup"><span data-stu-id="d1802-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="d1802-113">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d1802-113">Getting Started</span></span>

<span data-ttu-id="d1802-114">Verrà ora illustrata la configurazione del monitoraggio per un'app o un servizio.</span><span class="sxs-lookup"><span data-stu-id="d1802-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="d1802-115"><a name="resource"></a> Configurare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1802-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="d1802-116">**Prima di iniziare**, verificare di avere una sottoscrizione di Azure oppure [ottenerne una nuova gratuitamente][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="d1802-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="d1802-117">Se l'organizzazione ha già una sottoscrizione di Azure, un amministratore può aggiungere l'utente alla sottoscrizione seguendo [queste istruzioni][add-aad-user].</span><span class="sxs-lookup"><span data-stu-id="d1802-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="d1802-118">Accedere quindi al [portale di Azure][portal] e creare una risorsa di Application Insights come illustrato di seguito, facendo clic su "Nuovo" > "Strumenti di sviluppo" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="d1802-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="d1802-119">La risorsa include un endpoint per la ricezione dei dati di telemetria, l'archiviazione di tali dati, dei report salvati e dei dashboard, la configurazione di regole e avvisi e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="d1802-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Creare una risorsa di Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="d1802-121">Nella pagina di creazione della risorsa scegliere "Applicazione Node.js" nell'elenco a discesa Tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1802-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="d1802-122">Il tipo di app determina il set predefinito di dashboard e report creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d1802-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="d1802-123">Qualsiasi risorsa di Application Insights, tuttavia, può di fatto raccogliere dati da qualsiasi linguaggio e piattaforma.</span><span class="sxs-lookup"><span data-stu-id="d1802-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Modulo per una nuova risorsa di Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="d1802-125"><a name="agent"></a> Configurare l'agente Node.js</span><span class="sxs-lookup"><span data-stu-id="d1802-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="d1802-126">È ora possibile includere l'agente nell'app affinché possa raccogliere dati.</span><span class="sxs-lookup"><span data-stu-id="d1802-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="d1802-127">Per iniziare, copiare la chiave di strumentazione della risorsa (`ikey`) dal portale come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1802-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="d1802-128">Questa chiave viene usata dal sistema Application Insights per il mapping dei dati alla risorsa di Azure e deve quindi essere specificata in una variabile di ambiente o nel codice perché possa essere usata dall'agente.</span><span class="sxs-lookup"><span data-stu-id="d1802-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![Copiare la chiave di strumentazione](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="d1802-130">Aggiungere quindi la libreria dell'agente Node.js alle dipendenze dell'app tramite package.json.</span><span class="sxs-lookup"><span data-stu-id="d1802-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="d1802-131">Dalla cartella radice dell'app eseguire:</span><span class="sxs-lookup"><span data-stu-id="d1802-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="d1802-132">È ora necessario caricare in modo esplicito la libreria nel codice.</span><span class="sxs-lookup"><span data-stu-id="d1802-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="d1802-133">Dato che l'agente inserisce la strumentazione in molte altre librerie, è consigliabile eseguire il caricamento prima possibile e prima di altre istruzioni `require`.</span><span class="sxs-lookup"><span data-stu-id="d1802-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="d1802-134">Per iniziare, aggiungere quanto segue all'inizio del primo file con estensione js:</span><span class="sxs-lookup"><span data-stu-id="d1802-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="d1802-135">Il metodo `setup` configura la chiave di strumentazione e quindi la risorsa di Azure da usare per impostazione predefinita per tutti gli elementi rilevati.</span><span class="sxs-lookup"><span data-stu-id="d1802-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="d1802-136">Chiamare `start` al termine della configurazione per avviare la raccolta e l'invio dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d1802-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="d1802-137">È anche possibile specificare una chiave di strumentazione tramite la variabile di ambiente APPINSIGHTS\_INSTRUMENTATIONKEY, anziché passandola manualmente a `setup()` o `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="d1802-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="d1802-138">Questa procedura consente di non includere le chiavi di strumentazione nel codice sorgente sottoposto a commit e di specificare chiavi diverse per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="d1802-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="d1802-139">Di seguito sono documentate le opzioni di configurazione aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="d1802-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="d1802-140">È possibile provare l'agente senza inviare dati di telemetria impostando la chiave di strumentazione su qualsiasi stringa non vuota.</span><span class="sxs-lookup"><span data-stu-id="d1802-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="d1802-141"><a name="monitor"></a> Monitorare l'app</span><span class="sxs-lookup"><span data-stu-id="d1802-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="d1802-142">L'agente raccoglie automaticamente dati di telemetria sul runtime Node.js e su alcuni moduli comuni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="d1802-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="d1802-143">Usare ora l'applicazione per generare alcuni dati di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="d1802-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="d1802-144">Nel [portale di Azure][portal] passare quindi alla risorsa di Application Insights creata in precedenza e cercare i primi punti dati in Panoramica sequenza temporale, come nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="d1802-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="d1802-145">Per altri dettagli, fare clic sui grafici.</span><span class="sxs-lookup"><span data-stu-id="d1802-145">Click through the charts for more details.</span></span>

![Primi punti dati](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="d1802-147">Fare clic sul pulsante Mappa delle applicazioni per visualizzare la topologia individuata per l'app, come nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="d1802-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="d1802-148">Per altri dettagli, fare clic sui componenti riportati nella mappa.</span><span class="sxs-lookup"><span data-stu-id="d1802-148">Click through components in the map for more details.</span></span>

![Mappa app di esempio](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="d1802-150">È possibile ottenere altre informazioni sull'app e risolvere i problemi usando le altre visualizzazioni disponibili nella sezione "Analisi".</span><span class="sxs-lookup"><span data-stu-id="d1802-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![Sezione Analisi](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="d1802-152">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="d1802-152">No data?</span></span>

<span data-ttu-id="d1802-153">Dato che l'agente esegue l'invio dei dati in batch, potrebbe verificarsi un ritardo nella visualizzazione degli elementi nel portale.</span><span class="sxs-lookup"><span data-stu-id="d1802-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="d1802-154">Se i dati non sono visibili nella risorsa, provare alcune delle correzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1802-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="d1802-155">Continuare a usare l'applicazione ed eseguire altre azioni per generare dati di telemetria aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="d1802-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="d1802-156">Fare clic su **Aggiorna** nella visualizzazione della risorsa nel portale.</span><span class="sxs-lookup"><span data-stu-id="d1802-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="d1802-157">I grafici vengono aggiornati in modo automatico periodicamente, ma così è possibile forzare l'aggiornamento immediato.</span><span class="sxs-lookup"><span data-stu-id="d1802-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="d1802-158">Verificare che le [porte in uscita necessarie](app-insights-ip-addresses.md) siano aperte.</span><span class="sxs-lookup"><span data-stu-id="d1802-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="d1802-159">Aprire il riquadro [Ricerca](app-insights-diagnostic-search.md) e cercare singoli eventi.</span><span class="sxs-lookup"><span data-stu-id="d1802-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="d1802-160">Vedere le [domande frequenti][].</span><span class="sxs-lookup"><span data-stu-id="d1802-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="d1802-161">Configurazione dell'agente</span><span class="sxs-lookup"><span data-stu-id="d1802-161">Agent Configuration</span></span>

<span data-ttu-id="d1802-162">Di seguito sono riportati i metodi di configurazione dell'agente e i relativi valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="d1802-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="d1802-163">Per correlare completamente gli eventi in un servizio, assicurarsi di impostare `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="d1802-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="d1802-164">In questo modo, l'agente può tenere traccia del contesto tra callback asincroni in Node.js.</span><span class="sxs-lookup"><span data-stu-id="d1802-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="d1802-165">API dell'agente</span><span class="sxs-lookup"><span data-stu-id="d1802-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="d1802-166">Per una descrizione completa dell'API dell'agente .NET, vedere [qui](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d1802-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="d1802-167">Con il client Node.js di Application Insights è possibile tenere traccia di qualsiasi richiesta, evento, metrica o eccezione.</span><span class="sxs-lookup"><span data-stu-id="d1802-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="d1802-168">L'esempio seguente illustra alcune delle API disponibili.</span><span class="sxs-lookup"><span data-stu-id="d1802-168">The following example demonstrates some of the available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="d1802-169">Tenere traccia delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="d1802-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="d1802-170">Aggiungere una proprietà personalizzata a tutti gli eventi</span><span class="sxs-lookup"><span data-stu-id="d1802-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="d1802-171">Tenere traccia delle richieste HTTP GET</span><span class="sxs-lookup"><span data-stu-id="d1802-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="d1802-172">Tenere traccia del tempo di avvio del server</span><span class="sxs-lookup"><span data-stu-id="d1802-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="d1802-173">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="d1802-173">More resources</span></span>

* [<span data-ttu-id="d1802-174">Monitorare i dati di telemetria nel portale</span><span class="sxs-lookup"><span data-stu-id="d1802-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="d1802-175">Presentazione dello strumento Analisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1802-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="d1802-176">[domande frequenti]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="d1802-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>
