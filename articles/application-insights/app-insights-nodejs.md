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
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Monitorare servizi e app Node.js con Application Insights

[Azure Application Insights](app-insights-overview.md) consente di monitorare i servizi back-end e componenti dopo aver distribuito le toohelp si [rilevare e diagnosticare rapidamente le prestazioni e altri problemi](app-insights-detect-triage-diagnose.md). Usare Azure Application Insights per servizi Node.js ospitati ovunque: nel data center, in app Web e VM di Azure e anche in altri cloud pubblici.

tooreceive, archiviare, esplorare i dati di monitoraggio, seguire hello seguendo le istruzioni tooinclude un agente nel codice e impostare una risorsa di Application Insights corrispondente in Azure. agente di Hello invia risorsa toothat dati per un'ulteriore analisi ed esplorazione.

agente di Node.js Hello automaticamente è possibile monitorare in ingresso e in uscita richieste HTTP, diverse misurazioni di sistema e le eccezioni. A partire dalla versione 0.20, può monitorare anche alcuni pacchetti comuni di terze parti come `mongodb`, `mysql` e `redis`. Tutti gli eventi correlati di richiesta HTTP in ingresso tooan sono correlati per la risoluzione dei problemi più velocemente.

È possibile monitorare altri aspetti dell'applicazione e sistema eseguendo manualmente la strumentazione di loro tramite API dell'agente hello descritti di seguito.

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Introduzione

Verrà ora illustrata la configurazione del monitoraggio per un'app o un servizio.

### <a name="resource"></a> Configurare una risorsa di Application Insights

**Prima di iniziare**, verificare di avere una sottoscrizione di Azure oppure [ottenerne una nuova gratuitamente][azure-free-offer]. Se l'organizzazione ha già una sottoscrizione di Azure, gli amministratori possono seguire [queste istruzioni] [ add-aad-user] tooadd è tooit.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Ora accedere toohello [portale di Azure] [ portal] e creare una risorsa di Application Insights, come illustrato nell'esempio hello: fare clic su "Nuovo" > "Developer tools" > "Application Insights". risorsa di Hello include un endpoint per la ricezione di dati di telemetria, l'archiviazione dei dati, salvata i report e dashboard, regola e configurazione degli avvisi e altro ancora.

![Creare una risorsa di Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Nella pagina di creazione di risorse hello, scegliere "Node.js applicazione" hello applicazione tipo elenco a discesa. tipo di app Hello determina il set predefinito hello di dashboard e report creati automaticamente. Qualsiasi risorsa di Application Insights, tuttavia, può di fatto raccogliere dati da qualsiasi linguaggio e piattaforma.

![Modulo per una nuova risorsa di Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Impostare l'agente di Node.js hello

Ora è agente hello tooinclude di tempo nell'applicazione in modo da poter raccogliere i dati.
Per iniziare, copiare la chiave di strumentazione della risorsa (qui tooas il `ikey`) dal portale di hello, come illustrato di seguito. Hello App Insights sistema Usa questo tooyour dati chiave toomap risorse di Azure, pertanto è necessario toospecify in una variabile di ambiente o il codice per toouse agente hello.  

![Copiare la chiave di strumentazione](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Successivamente, aggiungere le dipendenze di hello Node.js agente libreria tooyour dell'app tramite file package. JSON. Dalla cartella radice di hello dell'app, eseguire:

```bash
npm install applicationinsights --save
```

È ora necessario tooexplicitly caricamento della libreria hello nel codice. Poiché l'agente di hello inserisce strumentazione in molte altre librerie, è necessario caricare il prima possibile, anche prima delle altre `require` istruzioni. avvio tooget, nella parte superiore di hello del primo file. js aggiungere:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Hello `setup` metodo consente di configurare la chiave di strumentazione hello (e pertanto risorse di Azure) toobe utilizzato per impostazione predefinita per gli elementi di tutte le revisioni. Chiamare `start` dopo la configurazione è la raccolta di toobegin completato e l'invio di dati di telemetria.

È anche possibile fornire un ikey tramite la variabile di ambiente hello APPINSIGHTS\_manualmente INSTRUMENTATIONKEY anziché passarlo manualmente troppo `setup()` o `getClient()`. Questa procedura consente di mantenere ikeys fuori dal codice sorgente eseguito il commit e toospecify ikeys diversi per diversi ambienti.

Di seguito sono documentate le opzioni di configurazione aggiuntive.

È possibile provare agente hello senza l'invio di dati di telemetria impostando hello strumentazione tooany chiave non è una stringa vuota.

### <a name="monitor"></a> Monitorare l'app

agente Hello raccoglie automaticamente dati di telemetria su runtime Node.js hello e alcuni moduli di terze parti comuni. Utilizzare il toogenerate ora applicazione alcuni di questi dati.

Quindi, nel hello [portale di Azure] [ portal] Sfoglia risorsa di Application Insights toohello creato in precedenza e cercare il primo pochi punti dati nella sequenza temporale di panoramica hello, come illustrato di seguito immagine hello. Fare clic sui grafici hello per altri dettagli.

![Primi punti dati](./media/app-insights-nodejs/12-first-perf.png)

Fare clic su hello applicazione mappa pulsante tooview hello topologia individuata per l'app, come illustrato di seguito immagine hello. Fare clic sui componenti nella mappa hello per altri dettagli.

![Mappa app di esempio](./media/app-insights-nodejs/06-appinsights_appmap.png)

Ulteriori informazioni sull'app e risolvere i problemi usando hello altre viste disponibili nella sezione "Verificare" hello.

![Sezione Analisi](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Dati non visualizzati

Perché l'agente di hello di batch di dati per l'invio di potrebbe verificarsi un ritardo prima gli elementi vengono visualizzati nel portale di hello. Se non viene visualizzato nella risorsa dati provare hello correzioni seguenti:

* Utilizzare un'applicazione hello ulteriormente; eseguire altre azioni toogenerate ulteriori dati di telemetria.
* Fare clic su **aggiornamento** in visualizzazione di risorse portale hello. Grafici di aggiornamento automatico periodicamente ma aggiornamento impone questo toohappen immediatamente.
* Verificare che le [porte in uscita necessarie](app-insights-ip-addresses.md) siano aperte.
* Aprire hello [ricerca](app-insights-diagnostic-search.md) riquadro e cercare i singoli eventi.
* Controllare hello [domande frequenti su][].


## <a name="agent-configuration"></a>Configurazione dell'agente

Di seguito sono metodi di configurazione dell'agente di hello e i valori predefiniti.

gli eventi di correlare toofully in un servizio, essere tooset che `.setAutoDependencyCorrelation(true)`. In questo modo agente hello tootrack contesto nelle richiamate asincrone in Node.js.

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

## <a name="agent-api"></a>API dell'agente

<!-- TODO: Fully document agent API. -->

.NET API dell'agente Hello è descritto [qui](app-insights-api-custom-events-metrics.md).

È possibile registrare qualsiasi richiesta, eventi, metrica o eccezione utilizzando il client di Application Insights Node.js hello. Hello esempio seguente vengono illustrate alcune delle hello API disponibili.

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

### <a name="track-your-dependencies"></a>Tenere traccia delle dipendenze

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

### <a name="add-a-custom-property-tooall-events"></a>Aggiungere gli eventi tooall una proprietà personalizzata

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Tenere traccia delle richieste HTTP GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Tenere traccia del tempo di avvio del server

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Altre risorse

* [Monitorare la telemetria nel portale di hello](app-insights-dashboards.md)
* [Presentazione dello strumento Analisi in Application Insights](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[domande frequenti su]: app-insights-troubleshoot-faq.md
