---
title: Monitorare Funzioni di Azure
description: Imparare a usare Azure Application Insights con Funzioni di Azure per il monitoraggio dell'esecuzione delle funzioni.
services: functions
author: tdykstra
manager: cfowler
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/15/2017
ms.author: tdykstra
ms.openlocfilehash: 355cb2cef52b5dfecddae228d0cc24a069d3b695
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="monitor-azure-functions"></a>Monitorare Funzioni di Azure

## <a name="overview"></a>Panoramica 

[Funzioni di Azure](functions-overview.md) offre l'integrazione predefinita con [Azure Application Insights](../application-insights/app-insights-overview.md) per il monitoraggio delle funzioni. Questo articolo illustra come configurare Funzioni per inviare i dati di telemetria ad Application Insights.

![Esplora metriche di Application Insights](media/functions-monitoring/metrics-explorer.png)

Funzioni dispone anche di funzionalità di monitoraggio incorporate che non usano Application Insights. Si consiglia di usare Application Insights perché offre un numero maggiore di dati e modalità di analisi dei dati migliori. Per informazioni sul monitoraggio predefinito, vedere l'[ultima sezione di questo articolo](#monitoring-without-application-insights).

## <a name="enable-application-insights-integration"></a>Abilitare l'integrazione di Application Insights

Affinché un'app per le funzioni invii dati ad Application Insights, è necessario conoscere la chiave di strumentazione di un'istanza di Application Insights. Esistono due modi per realizzare tale connessione nel [portale di Azure](https://portal.azure.com):

* [Creare un'istanza di Application Insights collegata quando si crea l'app per le funzioni](#new-function-app).
* [Connettere un'istanza di Application Insights a un'app per le funzioni esistente](#existing-function-app).
 
### <a name="new-function-app"></a>Nuova app per le funzioni

Abilitare Application Insights nella pagina **Crea** dell'app per le funzioni:

1. Impostare l'interruttore di **Application Insights** su **On** (Attivo).

2. Selezionare una **Località di Application Insights**.

   ![Abilitare Application Insights mentre si crea un'app per le funzioni](media/functions-monitoring/enable-ai-new-function-app.png)

### <a name="existing-function-app"></a>App per le funzioni esistente

Ottenere una chiave di strumentazione e salvarla in un'app per le funzioni:

1. Creare l'istanza di Application Insights. Impostare il tipo di applicazione su **Generale**.

   ![Creare un'istanza di Application Insights di tipo Generale](media/functions-monitoring/ai-general.png)

2. Copiare la chiave di strumentazione dalla pagina **Informazioni di base** dell'istanza di Application Insights. Passare il mouse sulla parte finale del valore della chiave visualizzata per far comparire il pulsante **Fare clic per copiare**.

   ![Copiare la chiave di strumentazione di Application Insights](media/functions-monitoring/copy-ai-key.png)

1. Nella pagina **Impostazioni applicazione** dell'app per le funzioni [aggiungere un'impostazione dell'app](functions-how-to-use-azure-function-app-settings.md#settings) denominata APPINSIGHTS_INSTRUMENTATIONKEY e incollare la chiave di strumentazione.

   ![Aggiungere la chiave di strumentazione alle impostazioni dell'app](media/functions-monitoring/add-ai-key.png)

1. Fare clic su **Salva**.

## <a name="view-telemetry-data"></a>Visualizzare i dati di telemetria

Per passare da un'app per le funzioni nel portale ad Application Insights, selezionare il collegamento **Application Insights** nella pagina **Panoramica** dell'app per le funzioni.

Per informazioni su come usare Application Insights, vedere la [documentazione su Application Insights](https://docs.microsoft.com/azure/application-insights/). Questa sezione mostra alcuni esempi su come visualizzare i dati in Application Insights. Se si ha già familiarità con Application Insights, è possibile passare direttamente alle [sezioni sulla configurazione e la personalizzazione dei dati di telemetria](#configure-categories-and-log-levels).

In [Esplora metriche](../application-insights/app-insights-metrics-explorer.md) è possibile creare grafici e avvisi in base alle metriche ad esempio numero di chiamate alla funzione, tempo di esecuzione e percentuale di successo.

![Esplora metriche](media/functions-monitoring/metrics-explorer.png)

Nella scheda [Errori](../application-insights/app-insights-asp-net-exceptions.md) è possibile creare grafici e avvisi in base agli errori di funzione e alle eccezioni del server. Il **nome dell'operazione** corrisponde al nome della funzione. Gli errori nelle dipendenze non vengono mostrati a meno che non si implementino [i dati di telemetria personalizzati](#custom-telemetry-in-c-functions) per le dipendenze.

![Errori](media/functions-monitoring/failures.png)

Nella scheda [Prestazioni](../application-insights/app-insights-performance-counters.md) è possibile analizzare i problemi di prestazioni.

![Prestazioni](media/functions-monitoring/performance.png)

La scheda **Server** mostra l'uso delle risorse e la velocità effettiva per ogni server. Questi dati possono essere utili negli scenari di debug in cui le funzioni bloccano le risorse sottostanti. I server sono denominati *Istanze del ruolo del cloud*. 

![Server](media/functions-monitoring/servers.png)

La scheda [Live Metrics Stream](../application-insights/app-insights-live-stream.md) mostra i dati delle metriche man mano che vengono creati in tempo reale.

![Live stream](media/functions-monitoring/live-stream.png)

## <a name="query-telemetry-data"></a>Query sui dati di telemetria

[Analytics di Application Insights](../application-insights/app-insights-analytics.md) consente di accedere a tutti i dati di telemetria sotto forma di tabelle in un database. Analytics offre un linguaggio di query per l'estrazione e la manipolazione dei dati.

![Selezionare Analytics](media/functions-monitoring/select-analytics.png)

![Esempio di Analytics](media/functions-monitoring/analytics-traces.png)

Di seguito è riportato un esempio di query, che mostra la distribuzione delle richieste per ruolo di lavoro negli ultimi 30 minuti.

```
requests
| where timestamp > ago(30m) 
| summarize count() by cloud_RoleInstance, bin(timestamp, 1m)
| render timechart
```

Le tabelle disponibili vengono mostrate nella scheda **Schema** del riquadro a sinistra. Nelle tabelle seguenti è possibile trovare i dati generati dalle chiamate alla funzione:

* **tracce**: log creato dal runtime e dal codice della funzione.
* **richieste**: uno per ogni chiamata alla funzione.
* **eccezioni**: tutte le eccezioni generate dal runtime.
* **customMetrics**: numero di chiamate con esito positivo e negativo, percentuale di successo, durata.
* **customEvents**: eventi rilevati dal runtime, ad esempio richieste HTTP che attivano una funzione.
* **performanceCounters**: informazioni sulle prestazioni dei server su cui sono in esecuzione le funzioni.

Le altre tabelle sono riservate ai test di disponibilità e ai dati di telemetria del browser o del client. È possibile implementare i dati di telemetria personalizzati per aggiungerne altri.

All'interno di ogni tabella alcuni dati specifici per Funzioni si trovano nel campo `customDimensions`.  Ad esempio, la query seguente recupera tutte le tracce con livello di registrazione `Error`.

```
traces 
| where customDimensions.LogLevel == "Error"
```

Il runtime indica `customDimensions.LogLevel` e `customDimensions.Category`. È possibile specificare campi aggiuntivi nei log in cui si scrive il codice funzione. Vedere la sezione [Registrazione strutturata](#structured-logging) più avanti in questo articolo.

## <a name="configure-categories-and-log-levels"></a>Configurare le categorie e i livelli di registrazione

È possibile usare Application Insights senza una configurazione personalizzata, ma la configurazione predefinita può creare volumi elevati di dati. Se si usa una sottoscrizione di Azure di Visual Studio, si potrebbe raggiunge il limite d'uso dati per App Insights. La parte rstante di questo articolo illustra come configurare e personalizzare i dati inviati dalle funzioni ad Application Insights.

### <a name="categories"></a>Categorie

Il logger di Funzioni di Azure include un *categoria* per ogni log. La categoria indica quale parte del codice runtime o del codice funzione è stata scritta dal log. 

Il runtime di Funzioni crea log con una categoria che inizia con "Host". Ad esempio i log "funzione avviata," "funzione eseguita" e "funzione completata" rientrano nella categoria "Host.Executor". 

Se si scrivono i log nel codice funzione, la categoria è "Function".

### <a name="log-levels"></a>Livelli di registrazione

Il logger delle funzioni di Azure include anche un *livello di registrazione* per ogni log. [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel#Microsoft_Extensions_Logging_LogLevel) è un'enumerazione e il codice integer ne indica la relativa importanza:

|LogLevel    |Codice|
|------------|---|
|Trace       | 0 |
|Debug       | 1 |
|Informazioni | 2 |
|Avviso     | 3 |
|Errore       | 4 |
|Critico    | 5 |
|Nessuno        | 6 |

Il livello di registrazione `None` è illustrato nella sezione successiva. 

### <a name="configure-logging-in-hostjson"></a>Configurare la registrazione nel file host.json

Il file *host.json* configura il numero di registrazioni che un'app per le funzioni invia ad Application Insights. Per ogni categoria, si indica il livello di registrazione minimo da inviare. Ad esempio:

```json
{
  "logger": {
    "categoryFilter": {
      "defaultLevel": "Information",
      "categoryLevels": {
        "Host.Results": "Error",
        "Function": "Error",
        "Host.Aggregator": "Information"
      }
    }
  }
}
```

In questo esempio vengono impostate due regole:

1. Per i log con categoria "Host.Results" o "Function", inviare ad Application Insights solo i log di livello `Error` e livelli superiori. I log di livello `Information` e livelli inferiori vengono ignorati.
2. Per i log con categoria Host. Aggregator, inviare ad Application Insights solo i log di livello `Information` e superiori. I log di livello `Debug` e livelli inferiori vengono ignorati.
3. Per tutti gli altri log, inviare ad Application Insights solo i log di livello `Information` e superiori.

Il valore della categoria in *host.json* controlla la registrazione di tutte le categorie che iniziano con lo stesso valore. Ad esempio, "Host" in *host.json* controlla la registrazione di "Host.General", "Host.Executor", "Host.Results" e così via.

Se *host.json* include più categorie che iniziano con la stessa stringa, viene rilevata prima la corrispondenza con quelle più lunghe. Ad esempio, si supponga di volere che tutti gli elementi dalla fase di runtime, ad eccezione di "Host.Aggregator", siano registrati al livello `Error` mentre i log "Host.Aggregator" vengono registrati al livello `Information`:

```json
{
  "logger": {
    "categoryFilter": {
      "defaultLevel": "Information",
      "categoryLevels": {
        "Host": "Error",
        "Function": "Error",
        "Host.Aggregator": "Information"
      }
    }
  }
}
```

Per eliminare tutti i log di una categoria, è possibile usare il livello di registrazione `None`. Nessun log viene scritto con quella categoria e non vi è alcun livello di registrazione superiore.

Le sezioni seguenti descrivono le categorie principali di log create dal runtime. 

### <a name="category-hostresults"></a>Categoria Host.Results

Questi log vengono visualizzati come "richieste" in Application Insights. Indicano l'esito positivo o negativo di una funzione.

![Grafico delle richieste](media/functions-monitoring/requests-chart.png)

Tutti questi log vengono scritti al livello `Information`, pertanto se si applica un filtro al livello `Warning` o superiore, questi dati non verranno visualizzati.

### <a name="category-hostaggregator"></a>Categoria Host.Aggregator

Questi log indicano il numero e le medie di chiamate alla funzione in un periodo di tempo [configurabile](#configure-the-aggregator). Il periodo predefinito è 30 secondi o 1000 risultati, ovvero quello che viene prima. 

I log vengono visualizzati come "customMetrics" in Application Insights. Gli esempi indicano il numero di esecuzioni, la percentuale di successo e la durata.

![query customMetrics](media/functions-monitoring/custom-metrics-query.png)

Tutti questi log vengono scritti al livello `Information`, pertanto se si applica un filtro al livello `Warning` o superiore, questi dati non verranno visualizzati.

### <a name="other-categories"></a>Altre categorie

Tutti i log per le categorie diverse da quelle già elencate vengono visualizzate come "tracce" in Application Insights.

![query di tracce](media/functions-monitoring/analytics-traces.png)

Tutti i log con le categorie che iniziano con "Host" vengono scritti dal runtime di Funzioni. I log "Funzione avviata e "Funzione completata" rientrano nella categoria "Host.Executor". Affinché vengano eseguiti correttamente, questi log devono avere il livello `Information`, mentre le eccezioni vengono registrate al livello `Error`. Il runtime crea anche il livello di registrazione `Warning`, ad esempio: messaggi di coda inviati alla coda non elaborabile.

I log scritti dal codice funzione rientrano nella categoria "Function" e possono avere qualsiasi livello di registrazione.

## <a name="configure-the-aggregator"></a>Configurare l'aggregatore

Come indicato nella sezione precedente, il runtime aggrega i dati sulle esecuzioni di funzioni in un periodo di tempo. Il periodo predefinito è 30 secondi o 1000 esecuzioni, ovvero quello che viene prima. È possibile configurare questa impostazione nel file *host.json*.  Ad esempio:

```json
{
    "aggregator": {
      "batchSize": 1000,
      "flushTimeout": "00:00:30"
    }
}
```

## <a name="configure-sampling"></a>Configurare il campionamento

Application Insights ha una funzionalità di [campionamento](../application-insights/app-insights-sampling.md) che consente di evitare la produzione di un numero eccessivo di dati di telemetria nei picchi di carico. Quando il numero degli elementi di telemetria supera una frequenza specificata, Application Insights inizia a ignorare in modo casuale alcuni degli elementi in ingresso. È possibile configurare il campionamento nel file *host.json*.  Ad esempio:

```json
{
  "applicationInsights": {
    "sampling": {
      "isEnabled": true,
      "maxTelemetryItemsPerSecond" : 5
    }
  }
}
```

## <a name="write-logs-in-c-functions"></a>Scrivere i log nelle funzioni C#

È possibile scrivere log nel codice funzione che vengono visualizzati come tracce in Application Insights.

### <a name="ilogger"></a>ILogger

Usare il parametro [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) nelle funzioni anziché il parametro `TraceWriter`. I log creati con `TraceWriter` passano in Application Insights, ma `ILogger` consente di eseguire una [registrazione strutturata](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

Con un oggetto `ILogger` è possibile chiamare [i metodi di estensione ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions#Methods_) `Log<level>` per creare i log. Ad esempio, il codice seguente scrive i log `Information` con la categoria "Function".

```cs
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger logger)
{
    logger.LogInformation("Request for item with key={itemKey}.", id);
```

### <a name="structured-logging"></a>Registrazione strutturata

I parametri usati nel messaggio del log sono determinati dall'ordine dei segnaposto, non dai nomi. Ad esempio, si supponga di disporre del codice seguente:

```csharp
string partitionKey = "partitionKey";
string rowKey = "rowKey";
logger.LogInformation("partitionKey={partitionKey}, rowKey={rowKey}", partitionKey, rowKey);
```

Se si mantenere la stessa stringa del messaggio e si inverte l'ordine dei parametri, il testo del messaggio risultante mostrerebbe i valori in maniera errata.

I segnaposto vengono gestiti in modo da poter eseguire la registrazione strutturata. Oltre alla stringa del messaggio, Application Insights archivia le coppie nome-valore del parametro. Il risultato è che gli argomenti del messaggio diventano campi su cui è possibile eseguire delle query.

Ad esempio, se la chiamata al metodo del logger è simile all'esempio precedente, è possibile eseguire una query per il campo `customDimensions.prop__rowKey`. Il prefisso viene aggiunto per verificare che non ci siano conflitti tra i campi aggiunti dal runtime e i campi aggiunti dal codice funzione.

È anche possibile eseguire query sulla stringa del messaggio originale facendo riferimento al campo `customDimensions.prop__{OriginalFormat}`.  

Ecco una rappresentazione JSON di esempio dei dati `customDimensions`:

```json
{
  customDimensions: {
    "prop__{OriginalFormat}":"C# Queue trigger function processed: {message}",
    "Category":"Function",
    "LogLevel":"Information",
    "prop__message":"c9519cbf-b1e6-4b9b-bf24-cb7d10b1bb89"
  }
}
```

### <a name="logging-custom-metrics"></a>Registrazione delle metriche personalizzate  

Nelle funzioni di script C# è possibile usare il metodo di estensione `LogMetric` su `ILogger` per creare metriche personalizzate in Application Insights. Ecco un esempio di chiamata al metodo:

```csharp
logger.LogMetric("TestMetric", 1234); 
```

Questo codice è un'alternativa alla chiamata di `TrackMetric` con [l'API di Application Insights per .NET](#custom-telemetry-in-c-functions).

## <a name="write-logs-in-javascript-functions"></a>Scrivere i log in funzioni JavaScript

Nelle funzioni di Node.js usare `context.log` per scrivere i log. La registrazione strutturata non è abilitata.

```
context.log('JavaScript HTTP trigger function processed a request.' + context.invocationId);
```

### <a name="logging-custom-metrics"></a>Registrazione delle metriche personalizzate  

Nelle funzioni Node.js è possibile usare il metodo di estensione `context.log.metric` per creare metriche personalizzate in Application Insights. Ecco un esempio di chiamata al metodo:

```javascript
context.log.metric("TestMetric", 1234); 
```

Questo codice è un'alternativa alla chiamata di `trackMetric` con [l'SDK di Node.js per Application Insights](#custom-telemetry-in-javascript-functions).

## <a name="custom-telemetry-in-c-functions"></a>Dati di telemetria personalizzata nelle funzioni C#

È possibile usare il pacchetto NuGet [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) per inviare i dati di telemetria personalizzati ad Application Insights.

Di seguito è riportato un esempio di codice C# che usa l'[API di telemetria personalizzata](../application-insights/app-insights-api-custom-events-metrics.md). L'esempio fa riferimento a una libreria di classi .NET, ma il codice di Application Insights è lo stesso per lo script C#.

```cs
using System;
using System.Net;
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.Extensibility;
using Microsoft.Azure.WebJobs;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
using System.Linq;

namespace functionapp0915
{
    public static class HttpTrigger2
    {
        private static string key = TelemetryConfiguration.Active.InstrumentationKey = 
            System.Environment.GetEnvironmentVariable(
                "APPINSIGHTS_INSTRUMENTATIONKEY", EnvironmentVariableTarget.Process);

        private static TelemetryClient telemetry = 
            new TelemetryClient() { InstrumentationKey = key };

        [FunctionName("HttpTrigger2")]
        public static async Task<HttpResponseMessage> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
            HttpRequestMessage req, ExecutionContext context, ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");
            DateTime start = DateTime.UtcNow;

            // parse query parameter
            string name = req.GetQueryNameValuePairs()
                .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
                .Value;

            // Get request body
            dynamic data = await req.Content.ReadAsAsync<object>();

            // Set name to query string or body data
            name = name ?? data?.name;

            telemetry.Context.Operation.Id = context.InvocationId.ToString();
            telemetry.Context.Operation.Name = "cs-http";
            if (!String.IsNullOrEmpty(name))
            {
                telemetry.Context.User.Id = name;
            }
            telemetry.TrackEvent("Function called");
            telemetry.TrackMetric("Test Metric", DateTime.Now.Millisecond);
            telemetry.TrackDependency("Test Dependency", 
                "swapi.co/api/planets/1/", 
                start, DateTime.UtcNow - start, true);

            return name == null
                ? req.CreateResponse(HttpStatusCode.BadRequest, 
                    "Please pass a name on the query string or in the request body")
                : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
        }
    }
}
```

Non chiamare `TrackRequest` o `StartOperation<RequestTelemetry>`, in quanto compariranno le richieste di duplicazione per una chiamata alla funzione.  Il runtime di Funzioni rileva automaticamente le richieste.

Impostare `telemetry.Context.Operation.Id` sull'ID della chiamata ogni volta che viene avviata la funzione. In questo modo è possibile correlare tutti gli elementi di telemetria per una chiamata alla funzione specifica.

```cs
telemetry.Context.Operation.Id = context.InvocationId.ToString();
```

## <a name="custom-telemetry-in-javascript-functions"></a>Dati di telemetria personalizzati nelle funzioni JavaScript

L'[SDK di Node.js per Application Insights](https://www.npmjs.com/package/applicationinsights) è attualmente in versione beta. Di seguito è riportato un codice di esempio che invia i dati di telemetria personalizzati ad Application Insights:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup();
const client = appInsights.defaultClient;

module.exports = function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    client.trackEvent({name: "my custom event", tagOverrides:{"ai.operation.id": context.invocationId}, properties: {customProperty2: "custom property value"}});
    client.trackException({exception: new Error("handled exceptions can be logged with this method"), tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackMetric({name: "custom metric", value: 3, tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackTrace({message: "trace message", tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackDependency({target:"http://dbname", name:"select customers proc", data:"SELECT * FROM Customers", duration:231, resultCode:0, success: true, dependencyTypeName: "ZSQL", tagOverrides:{"ai.operation.id": context.invocationId}});
    client.trackRequest({name:"GET /customers", url:"http://myserver/customers", duration:309, resultCode:200, success:true, tagOverrides:{"ai.operation.id": context.invocationId}});

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```

Il parametro `tagOverrides` imposta `operation_Id` sull'ID di chiamata alla funzione. Questa impostazione consente di correlare tutti i dati di telemetria personalizzati e generati automaticamente per una chiamata alla funzione specifica.

## <a name="known-issues"></a>Problemi noti

### <a name="dependencies"></a>Dipendenze

Le dipendenze non vengono visualizzate automaticamente, ma è possibile scrivere il codice personalizzato per visualizzarle. Il codice di esempio nella [sezione relativa ai dati di telemetria personalizzati C#](#custom-telemetry-in-c-functions) ne illustra le modalità. Il codice di esempio crea una *mappa dell'applicazione* in Application Insights simile alla seguente:

![Mappa delle applicazioni](media/functions-monitoring/app-map.png)

### <a name="report-issues"></a>Segnalare i problemi

Per segnalare un problema con l'integrazione di Application Insights in Funzioni o per inviare un suggerimento o una richiesta, [creare un problema in GitHub](https://github.com/Azure/Azure-Functions/issues/new).

## <a name="monitoring-without-application-insights"></a>Monitoraggio senza Application Insights

Si consiglia di usare Application Insights per monitorare le funzioni perché offre un numero maggiore di dati e modalità di analisi dei dati migliori. Ma è anche possibile trovare dati di telemetria e di registrazione nelle pagine del portale di Azure per un'app per le funzioni. 

Selezionare la scheda **Monitoraggio** per una funzione per ottenere un elenco di esecuzioni della funzione. Selezionare l'esecuzione della funzione per esaminare la durata, i dati di input, gli errori e i file di log associati.

> [!IMPORTANT]
> Quando si usa il [piano di hosting a consumo](functions-overview.md#pricing) per Funzioni di Azure, il riquadro **Monitoraggio** nell'app per le funzioni non mostra alcun dato. Ciò avviene perché la piattaforma ridimensiona e gestisce automaticamente le istanze di calcolo. Queste metriche non sono quindi significative per un piano a consumo.

### <a name="real-time-monitoring"></a>Monitoraggio in tempo reale

Il monitoraggio in tempo reale è disponibile facendo clic su **flusso eventi live** nella scheda **Monitoraggio** della funzione. Il flusso di eventi live viene visualizzato in un grafico in una nuova scheda nel browser

> [!NOTE]
> A causa di un problema noto, è possibile che il popolamento dei dati abbia esito negativo. Potrebbe essere necessario chiudere la scheda del browser che include il flusso eventi live e quindi fare di nuovo clic su **flusso eventi live** per consentire il popolamento corretto dei dati del flusso di eventi. 

Queste statistiche sono in tempo reale, ma la creazione effettiva dei grafici relativi ai dati dell'esecuzione potrebbe comportare circa 10 secondi di latenza.

### <a name="monitor-log-files-from-a-command-line"></a>Monitorare i file di log da una riga di comando

È possibile trasmettere in streaming i file di log a una sessione della riga di comando su una workstation locale usando l'interfaccia della riga di comando di Azure 1.0 o PowerShell.

### <a name="monitor-function-app-log-files-with-the-azure-cli-10"></a>Monitorare i file di log dell'app per le funzioni con l'interfaccia della riga di comando di Azure 1.0

Per iniziare, [installare l'interfaccia della riga di comando di Azure 1.0](../cli-install-nodejs.md) e [accedere ad Azure](../xplat-cli-connect.md).

Usare i comandi seguenti per abilitare la modalità classica di Gestione servizi, scegliere la sottoscrizione e trasmettere in streaming i file di log:

```
azure config mode asm
azure account list
azure account set <subscriptionNameOrId>
azure site log tail -v <function app name>
```

### <a name="monitor-function-app-log-files-with-powershell"></a>Monitorare i file di log delle app per le funzioni tramite PowerShell

Per iniziare, [installare e configurare Azure PowerShell](/powershell/azure/overview).

Usare i comandi seguenti per aggiungere l'account di Azure, scegliere la sottoscrizione e trasmettere in streaming i file di log:

```
PS C:\> Add-AzureAccount
PS C:\> Get-AzureSubscription
PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription
PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail
```

Per altre informazioni, vedere [Procedura: Eseguire lo streaming dei log per le app Web](../app-service/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Altre informazioni su Application Insights](https://docs.microsoft.com/azure/application-insights/)

> [!div class="nextstepaction"]
> [Altre informazioni sul framework di registrazione che usa Funzioni](https://docs.microsoft.com/aspnet/core/fundamentals/logging?tabs=aspnetcore2x)
