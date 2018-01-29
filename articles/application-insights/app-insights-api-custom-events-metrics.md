---
title: API di Application Insights per metriche ed eventi personalizzati | Microsoft Docs
description: Inserire alcune righe di codice nell'app desktop o per dispositivi, nella pagina Web o nel servizio per tenere traccia dell'utilizzo e diagnosticare i problemi.
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: mbullwin
ms.openlocfilehash: 7d797716fb98ac85f11f956e732e08820b56affc
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2018
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API di Application Insights per metriche ed eventi personalizzati

Inserire alcune righe di codice nell'applicazione per scoprire come viene usato dagli utenti o per agevolare la diagnosi dei problemi. È possibile inviare i dati di telemetria dalle app desktop e per dispositivi, dai client Web e dai server Web. Usare l'API di telemetria principale di [Azure Application Insights](app-insights-overview.md) per inviare metriche ed eventi personalizzati e le versioni personalizzate dei dati di telemetria standard. Questa API è la stessa utilizzata dagli agenti di raccolta dati di Application Insights standard.

## <a name="api-summary"></a>Riepilogo dell'API
L'API è uniforme in tutte le piattaforme, a parte alcune variazioni di lieve entità.

| Metodo | Usato per |
| --- | --- |
| [`TrackPageView`](#page-views) |Pagine, schermate, pannelli o form. |
| [`TrackEvent`](#trackevent) |Azioni dell'utente e altri eventi. Usato per tenere traccia del comportamento dell'utente o per monitorare le prestazioni. |
| [`TrackMetric`](#trackmetric) |Misurazioni delle prestazioni, ad esempio la lunghezza della coda, non correlate a eventi specifici. |
| [`TrackException`](#trackexception) |Registrare le eccezioni per la diagnosi. Tenere traccia del punto in cui si verificano in relazione ad altri eventi ed esaminare le analisi dello stack. |
| [`TrackRequest`](#trackrequest) |Registrare la frequenza e la durata delle richieste del server per l'analisi delle prestazioni. |
| [`TrackTrace`](#tracktrace) |Messaggi nei log di diagnostica. È anche possibile acquisire log di terze parti. |
| [`TrackDependency`](#trackdependency) |Registrare la durata e la frequenza delle chiamate ai componenti esterni da cui dipende l'app. |

È possibile [associare proprietà e metriche](#properties) alla maggior parte di queste chiamate di telemetria.

## <a name="prep"></a>Prima di iniziare
Se non si ha ancora un riferimento in Application Insights SDK:

* Aggiungere Application Insights SDK al progetto:

  * [Progetto ASP.NET](app-insights-asp-net.md)
  * [Progetto Java](app-insights-java-get-started.md)
  * [Progetto Node.js](app-insights-nodejs.md)
  * [JavaScript in ogni pagina Web](app-insights-javascript.md) 
* Nel dispositivo o nel codice del server Web includere:

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic:* `Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`
    
    *Node.js:* `var applicationInsights = require("applicationinsights");`

## <a name="get-a-telemetryclient-instance"></a>Ottenere un'istanza di TelemetryClient
Ottenere un'istanza di `TelemetryClient` (tranne che in JavaScript nelle pagine Web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();
    
*Node.JS*

    var telemetry = applicationInsights.defaultClient;


TelemetryClient è thread-safe.

Per i progetti ASP.NET e Java è consigliabile creare un'istanza di TelemetryClient per ogni modulo dell'app. Ad esempio è possibile che il servizio Web includa un'istanza di TelemetryClient per segnalare le richieste HTTP in entrata e un altro oggetto in una classe middleware per segnalare gli eventi di logica di business. È possibile impostare proprietà quali `TelemetryClient.Context.User.Id` per tenere traccia degli utenti e delle sessioni o `TelemetryClient.Context.Device.Id` per identificare il computer. Queste informazioni sono associate a tutti gli eventi inviati dall'istanza.

Nei progetti Node.js è possibile usare `new applicationInsights.TelemetryClient(instrumentationKey?)` per creare una nuova istanza, ma questo è consigliato solo per scenari che richiedono la configurazione isolata dal `defaultClient` singleton.

## <a name="trackevent"></a>TrackEvent
In Application Insights un *evento personalizzato* è un punto dati che è possibile visualizzare in [Esplora metriche](app-insights-metrics-explorer.md) come conteggio aggregato e in [Ricerca diagnostica](app-insights-diagnostic-search.md) come singole occorrenze. Non è correlato a MVC o ad altri "eventi" del framework.

Inserire chiamate `TrackEvent` nel codice per contare i vari eventi. La frequenza d'uso di una particolare funzionalità, la frequenza di raggiungimento di obiettivi specifici o la frequenza di particolari tipi di errore.

Ad esempio, in un'app di gioco è possibile inviare un evento ogni volta che un utente vince il gioco:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");
    
*Node.JS*

    telemetry.trackEvent({name: "WinGame"});

### <a name="view-your-events-in-the-microsoft-azure-portal"></a>Visualizzare gli eventi nel portale di Microsoft Azure
Per visualizzare un conteggio degli eventi, aprire un pannello [Esplora metriche](app-insights-metrics-explorer.md) , aggiungere un nuovo grafico e selezionare **Eventi**.  

![Visualizzare il conteggio degli eventi personalizzati](./media/app-insights-api-custom-events-metrics/01-custom.png)

Per confrontare il conteggio di eventi diversi, impostare il tipo di grafico su **Griglia** e raggruppare in base al nome dell'evento:

![Impostare il tipo di grafico e il raggruppamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

Nella griglia, fare clic su un nome di evento per visualizzare le singole occorrenze di quell'evento. Per altre informazioni, fare clic su qualsiasi occorrenza nell'elenco.

![Eseguire il drill-through degli eventi](./media/app-insights-api-custom-events-metrics/03-instances.png)

Per concentrarsi sugli eventi specifici in Ricerca o in Esplora metriche, impostare il filtro del pannello sui nomi degli eventi a cui si è interessati:

![Aprire i filtri, espandere il nome dell’evento e selezionare uno o più valori](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Eventi personalizzati in Analytics

I dati di telemetria sono disponibili nella tabella `customEvents` in [Analytics di Application Insights](app-insights-analytics.md). Ogni riga rappresenta una chiamata a `trackEvent(..)` nell'app in uso. 

Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1. Per esempio itemCount==10 indica che su 10 chiamate a trackEvent(), il processo di campionamento ne trasmette solo una. Per ottenere un conteggio corretto degli eventi personalizzati, si consiglia di usare un codice, ad esempio `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights è in grado di creare grafici in base a metriche non sono associate a determinati eventi. Ad esempio, è possibile monitorare la lunghezza di una coda a intervalli regolari. Grazie alle metriche, le singole misurazioni sono meno interessanti rispetto alle variazioni e alle tendenze, i grafici statistici risultano pertanto utili.

Per inviare le metriche ad Application Insights, è possibile usare l'API `TrackMetric(..)`. Per inviare le metriche è possibile procedere in due modi: 

* Valore singolo. Ogni volta che si esegue una misurazione nell'applicazione, si invia il valore corrispondente ad Application Insights. Ad esempio, si supponga di avere una metrica che descrive il numero di elementi in un contenitore. Durante un periodo di tempo specifico, inserire prima tre elementi nel contenitore e poi rimuoverne due. Di conseguenza, è necessario chiamare `TrackMetric` due volte: prima passando il valore `3` e poi il valore `-2`. Application Insights memorizza entrambi i valori per conto dell'utente. 

* Aggregazione. Quando si usano le metriche non si considera mai una sola misura. È importante invece il riepilogo delle operazioni eseguite in un periodo di tempo specifico. Tale riepilogo viene chiamato _aggregazione_. Nell'esempio precedente la somma della metrica di aggregazione per quel periodo di tempo è `1` e il conteggio dei valori della metrica è `2`. Quando si usa l'approccio di aggregazione, si chiama `TrackMetric` solo una volta per periodo di tempo e si inviano i valori di aggregazione. Questo è l'approccio consigliato in quanto può ridurre notevolmente i costi e le prestazioni generali inviando meno punti dati ad Application Insights, durante la raccolta di tutte le informazioni pertinenti.

### <a name="examples"></a>Esempi:

#### <a name="single-values"></a>Valori singoli

Per inviare un singolo valore di metrica:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```csharp
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

*Node.JS*

 ```Javascript
     telemetry.trackMetric({name: "queueLength", value: 42.0});
 ```

#### <a name="aggregating-metrics"></a>Aggregazione delle metriche

È consigliabile aggregare le metriche prima di inviarle dall'app, al fine di ridurre la larghezza di banda, il costo e migliorare le prestazioni.
Di seguito è riportato un esempio di codice di aggregazione:

*C#*

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Metriche personalizzate in Esplora metriche

Per visualizzare i risultati, aprire Esplora metriche e aggiungere un nuovo grafico. Modificare il grafico per visualizzare la metrica.

> [!NOTE]
> Potrebbero essere necessari alcuni minuti per visualizzare la metrica personalizzata nell'elenco delle metriche disponibili.
>

![Aggiungere un nuovo grafico o selezionare un grafico e selezionare le metriche in Personalizzato](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Metriche personalizzate in Analytics

I dati di telemetria sono disponibili nella tabella `customMetrics` in [Analytics di Application Insights](app-insights-analytics.md). Ogni riga rappresenta una chiamata a `trackMetric(..)` nell'app in uso.
* `valueSum`: somma delle misurazioni. Per ottenere il valore medio, dividere per `valueCount`.
* `valueCount`: numero delle misurazioni aggregate nella chiamata `trackMetric(..)`.

## <a name="page-views"></a>Visualizzazioni pagina
In un'app per dispositivo o pagine Web i dati di telemetria delle visualizzazioni pagina vengono inviati per impostazione predefinita quando viene caricata ogni schermata o pagina. È tuttavia possibile modificare questa impostazione per tenere traccia delle visualizzazioni pagina in momenti diversi o aggiuntivi. Ad esempio, in un'app che visualizza schede o pannelli, è possibile tenere traccia di una "pagina" ogni volta che l'utente apre un nuovo pannello.

![Sezione Utilizzo nel pannello Panoramica](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

I dati relativi a utente e sessione vengono inviati come proprietà insieme alle visualizzazioni pagina, in modo che i grafici utente e sessione si attivino in presenza dei dati di telemetria delle visualizzazioni pagina.

### <a name="custom-page-views"></a>Visualizzazioni pagina personalizzate
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Se sono presenti alcune schede in pagine HTML diverse, è possibile specificare anche l'URL:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Temporizzazione delle visualizzazioni delle pagine
Per impostazione predefinita gli intervalli di tempo indicati come **Tempo di caricamento della visualizzazione pagina** sono misurati dal momento in cui il browser invia la richiesta al momento della chiamata dell'evento di caricamento pagina del browser.

In alternativa, è possibile:

* Impostare una durata esplicita nella chiamata di [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview): `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Usare le chiamate relative ai tempi di visualizzazione della pagina `startTrackPage` e `stopTrackPage`.

*JavaScript*

    // To start timing a page:
    appInsights.startTrackPage("Page1");

...

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Il nome che si usa come primo parametro associa le chiamate di avvio e arresto. Il valore predefinito corrisponde al nome della pagina corrente.

I tempi di caricamento delle pagine visualizzati in Esplora metriche sono calcolati in base all'intervallo tra la chiamata di avvio e la chiamata di arresto. È possibile specificare l'intervallo effettivo calcolato desiderato.

### <a name="page-telemetry-in-analytics"></a>Dati di telemetria della pagina in Analytics

In [Analytics](app-insights-analytics.md) due tabelle mostrano i dati delle operazioni del browser:

* La tabella `pageViews` contiene i dati relativi al titolo della pagina e all'URL
* La tabella `browserTimings` contiene i dati sulle prestazioni del client, ad esempio il tempo impiegato per elaborare i dati in ingresso

Per trovare il tempo necessario al browser per elaborare pagine diverse:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

Per individuare le popolarità dei diversi browser:

```
pageViews | summarize count() by client_Browser
```

Per associare le visualizzazioni di pagina alle chiamate AJAX, unirle alle dipendenze:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
Il server SDK usa TrackRequest per registrare le richieste HTTP.

È anche possibile chiamarlo manualmente se si vogliono simulare le richieste in un contesto in cui il modulo del servizio Web non è in esecuzione.

Il modo consigliato per inviare dati di telemetria della richiesta è quello in cui la richiesta agisce come un <a href="#operation-context">contesto dell'operazione</a>.

## <a name="operation-context"></a>Contesto dell'operazione
È possibile mettere in correlazione gli elementi di telemetria associandoli al contesto dell'operazione. Il modulo di rilevamento delle richieste standard esegue questa operazione per le eccezioni e gli altri eventi inviati durante l'elaborazione di una richiesta HTTP. In [Ricerca](app-insights-diagnostic-search.md) e [Analisi](app-insights-analytics.md) è possibile trovare facilmente gli eventi associati alla richiesta usando l'ID operazione.

Per altre informazioni sulla correlazione, vedere [Correlazione di dati di telemetria in Application Insights](application-insights-correlation.md).

Quando si tiene traccia dei dati di telemetria manualmente, il modo più semplice per garantire la correlazione dei dati di telemetria consiste nell'usare questo modello:

*C#*

```csharp
// Establish an operation context and associated telemetry item:
using (var operation = telemetryClient.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetryClient.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetryClient.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Oltre a impostare un contesto operativo, `StartOperation` crea un elemento di telemetria del tipo specificato. Invia l'elemento di telemetria quando si elimina l'operazione o si chiama esplicitamente `StopOperation`. Se si usa `RequestTelemetry` come tipo di telemetria, la sua durata viene impostata sull'intervallo di tempo compreso tra l'avvio e l'arresto.

Gli elementi di telemetria segnalati in un ambito dell'operazione diventano elementi "figlio" di tale operazione. I contesti dell'operazione possono essere annidati. 

In Ricerca il contesto dell'operazione viene usato per creare l'elenco di **elementi correlati**:

![Elementi correlati](./media/app-insights-api-custom-events-metrics/21.png)

Per altre informazioni sulle operazioni di rilevamento personalizzate, vedere [Tenere traccia delle operazioni personalizzate con Application Insights .NET SDK](application-insights-custom-operations-tracking.md).

### <a name="requests-in-analytics"></a>Richieste in Analytics 

In [Analytics di Application Insights](app-insights-analytics.md) le richieste vengono visualizzate nella tabella `requests`.

Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostrerà un valore maggiore di 1. Per esempio itemCount==10 indica che su 10 chiamate a trackRequest(), il processo di campionamento ne trasmette solo una. Per ottenere un conteggio corretto delle richieste e della durata media segmentato in base ai nomi della richiesta, usare un codice, ad esempio:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Inviare le eccezioni ad Application Insights:

* Per [contarle](app-insights-metrics-explorer.md), come indicazione della frequenza di un problema.
* Per [esaminare le singole occorrenze](app-insights-diagnostic-search.md).

I report includono le analisi dello stack.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }
    
*Node.js*

    try
    {
       ...
    }
    catch (ex)
    {
       telemetry.trackException({exception: ex});
    }

Gli SDK rilevano molte eccezioni automaticamente, quindi non è sempre necessario richiamare TrackException in modo esplicito.

* ASP.NET: [Scrivere codice per intercettare le eccezioni](app-insights-asp-net-exceptions.md).
* J2EE: [Le eccezioni vengono rilevate automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Le eccezioni vengono rilevate automaticamente. Se si vuole disabilitare la raccolta automatica, aggiungere una riga al frammento di codice che si inserisce nelle pagine Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Eccezioni in Analytics

In [Analytics di Application Insights](app-insights-analytics.md) le eccezioni vengono visualizzate nella tabella `exceptions`.

Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà `itemCount` mostra un valore maggiore di 1. Per esempio itemCount==10 indica che su 10 chiamate a trackException(), il processo di campionamento ne trasmette solo una. Per ottenere un conteggio corretto delle eccezioni segmentate per tipo di eccezione, usare un codice, ad esempio:

```
exceptions | summarize sum(itemCount) by type
```

La maggior parte delle informazioni importanti dello stack è già stata estratta in variabili distinte, ma è possibile separare la struttura `details` per ottenerne altre. Poiché si tratta di una struttura dinamica, è necessario eseguire il cast del risultato per il tipo previsto. Ad esempio: 

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

Per associare le richieste alle eccezioni correlate, è possibile usare un join:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Usare TrackTrace per diagnosticare i problemi mediante l'invio di una traccia di navigazione ad Application Insights. È possibile inviare blocchi di dati di diagnostica e controllarli in [Ricerca diagnostica](app-insights-diagnostic-search.md).

Gli [adattatori di log](app-insights-asp-net-trace-logs.md) usano questa API per inviare i log di terze parti al portale.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);
    
*Node.JS*

    telemetry.trackTrace({message: message, severity:applicationInsights.Contracts.SeverityLevel.Warning, properties:properties});


È possibile eseguire ricerche nel contenuto del messaggio, ma, a differenza dei valori delle proprietà, non è possibile filtrarlo.

Il limite delle dimensioni per `message` è molto superiore al limite per le proprietà.
Un vantaggio di TrackTrace è che è possibile inserire dati relativamente lunghi nel messaggio. Ad esempio è possibile codificare dati POST.  

È anche possibile aggiungere al messaggio un livello di gravità. E come per altri tipi di dati di telemetria è possibile aggiungere valori di proprietà utili per filtrare o cercare set di tracce diversi. Ad esempio: 

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

In [Ricerca](app-insights-diagnostic-search.md) sarà possibile filtrare facilmente tutti i messaggi di un determinato livello di gravità relativi a un database specifico.


### <a name="traces-in-analytics"></a>Tracce in Analytics

In [Analytics di Application Insights](app-insights-analytics.md) le chiamate a TrackTrace vengono visualizzate nella tabella `traces`.

Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1. Per esempio itemCount==10 indica che, su 10 chiamate di `trackTrace()`, il processo di campionamento ne trasmette solo una. Per ottenere un conteggio corretto delle chiamate delle tracce, si consiglia di usare un codice, ad esempio `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Usare la chiamata di TrackDependency per rilevare i tempi di risposta e le percentuali di successo delle chiamate a un frammento di codice esterno. I risultati vengono visualizzati nei grafici dipendenze nel portale.

```csharp
var success = false;
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

```Javascript
var success = false;
var startTime = new Date().getTime();
try
{
    success = dependency.Call();
}
finally
{
    var elapsed = new Date() - startTime;
    telemetry.trackDependency({dependencyTypeName: "myDependency", name: "myCall", duration: elapsed, success:success});
}
```

Tenere presente che il server SDK include un [modulo dipendenza](app-insights-asp-net-dependencies.md) che consente di individuare e tracciare alcune chiamate di dipendenza automaticamente, ad esempio a database e API REST. È necessario installare un agente nel server per consentire il funzionamento del modulo. Usare questa chiamata se si vuole tenere traccia di chiamate che il rilevamento automatico non intercetta o se non si vuole installare l'agente.

Per disattivare il modulo standard per il rilevamento delle dipendenze, modificare il file [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) ed eliminare il riferimento a `DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dipendenze in Analytics

In [Analytics di Application Insights](app-insights-analytics.md) le chiamate a trackDependency vengono visualizzate nella tabella `dependencies`.

Se il [campionamento](app-insights-sampling.md) è attivo, la proprietà itemCount mostra un valore maggiore di 1. Per esempio itemCount==10 indica che su 10 chiamate a trackDependency(), il processo di campionamento ne trasmette solo una. Per ottenere un conteggio corretto delle dipendenze segmentate per componente di destinazione, usare un codice, ad esempio:

```
dependencies | summarize sum(itemCount) by target
```

Per associare le dipendenze alle richieste correlate, è possibile usare un join:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Scaricamento dei dati
In genere l'SDK invia i dati in momenti scelti per ridurre al minimo l'impatto sull'utente. In alcuni casi tuttavia è possibile che si voglia scaricare il buffer, ad esempio se si sta usando l'SDK in un'applicazione che si arresta.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);
    
*Node.JS*

    telemetry.flush();

Si noti che la funzione è asincrona per il [canale di telemetria del server](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>utenti autenticati
In un'app Web gli utenti sono identificati dai cookie per impostazione predefinita. Un utente può essere conteggiato più volte se accede all'app da un computer o da un browser diverso o se elimina i cookie.

Se gli utenti accedono all'app, è possibile ottenere un conteggio più preciso impostando l'ID dell'utente autenticato nel codice del browser:

*JavaScript*

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

In un'applicazione MVC Web ASP.NET, ad esempio:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Non è necessario usare il nome di accesso effettivo dell'utente. È sufficiente usare un ID univoco per l'utente. Non deve includere spazi o i caratteri `,;=|`.

L'ID utente viene inoltre impostato in un cookie di sessione e inviato al server. Se l'SDK del server è installato, l'ID dell'utente autenticato viene inviato come parte delle proprietà contestuali della telemetria del client e del server. Quindi sarà possibile filtrarlo ed eseguire ricerche al suo interno.

Se l'app raggruppa gli utenti in account, è anche possibile passare un identificatore per l'account, con le stesse limitazioni di caratteri.

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

In [Esplora metriche](app-insights-metrics-explorer.md) è possibile creare un grafico che conta i valori **Utenti, Autenticati** e **Account utente**.

È anche possibile [cercare](app-insights-diagnostic-search.md) i punti dati del client con account e nomi utente specifici.

## <a name="properties"></a>Filtro, ricerca e segmentazione dei dati mediante le proprietà
È possibile associare proprietà e misure agli eventi e anche a metriche, visualizzazioni pagine, eccezioni e altri dati di telemetria.

*proprietà* sono valori di stringa che è possibile usare per filtrare i dati di telemetria nei report di utilizzo. Ad esempio, se l'app offre più giochi, è possibile associare il nome del gioco a ogni evento per vedere quali sono i giochi più diffusi.

Esiste un limite di 8192 per la lunghezza della stringa. Se si vogliono inviare grandi quantità di dati, usare il parametro del messaggio di [TrackTrace](#track-trace).

*metriche* sono valori numerici che possono essere rappresentati graficamente. Ad esempio è possibile verificare se esiste un aumento graduale nei punteggi raggiunti dai giocatori. I grafici possono essere segmentati in base alle proprietà inviate con l'evento, in modo da ottenere grafici separati o in pila per giochi diversi.

Affinché i valori metrici siano visualizzati correttamente, devono essere maggiori o uguali a 0.

Esistono tuttavia alcuni [limiti sul numero di proprietà, di valori delle proprietà e di metriche](#limits) che è possibile usare.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);

*Node.js*

    // Set up some properties and metrics:
    var properties = {"game": currentGame.Name, "difficulty": currentGame.Difficulty};
    var metrics = {"Score": currentGame.Score, "Opponents": currentGame.OpponentCount};

    // Send the event:
    telemetry.trackEvent({name: "WinGame", properties: properties, measurements: metrics});


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Assicurarsi di non registrare informazioni personali nelle proprietà.
>
>

*Se è stata usata la metrica*, aprire Esplora metriche e selezionare la metrica dal gruppo **personalizzato**:

![Aprire Esplora metrica, selezionare il grafico e selezionare la metrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Se non viene visualizzata l'unità di misura o se l'intestazione **personalizzata** non è presente, chiudere il pannello di selezione e riprovare più tardi. A volte potrebbe essere necessaria un'ora per l'aggregazione delle metriche attraverso la pipeline.

*Se si usano proprietà e metriche*, segmentare la metrica in base alla proprietà:

![Impostare il raggruppamento e quindi selezionare la proprietà in Raggruppa per](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

In *Ricerca diagnostica* è possibile visualizzare le proprietà e le metriche di singole occorrenze di un evento.

![Selezionare un'istanza e quindi scegliere "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Usare il campo **Ricerca** per visualizzare le occorrenze di eventi con un valore della proprietà particolare.

![Digitare un termine in Ricerca](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Altre informazioni sulle espressioni di ricerca](app-insights-diagnostic-search.md).

### <a name="alternative-way-to-set-properties-and-metrics"></a>Metodo alternativo per impostare proprietà e metriche
Se si preferisce, è possibile raccogliere i parametri di un evento in un oggetto separato:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Non riusare la stessa istanza dell'elemento di telemetria, `event` in questo esempio, per chiamare Track*() più volte. Potrebbe causare l'invio della telemetria con una configurazione errata.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Misure e proprietà personalizzate in Analytics

In [Analytics](app-insights-analytics.md) le metriche e le proprietà personalizzate vengono mostrate negli attributi `customMeasurements` e `customDimensions` di ogni record di dati di telemetria.

Ad esempio, se è stata aggiunta una proprietà denominata "game" ai dati di telemetria della richiesta, questa query conta le occorrenze di diversi valori di "game" e mostrerà la media del "punteggio" della metrica personalizzata:

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Si noti che:

* Quando si estrae un valore dal JSON customDimensions o customMeasurements, questo è di tipo dinamico e pertanto è necessario eseguirne il cast in `tostring` o `todouble`.
* Per tener conto della possibilità di [campionamento](app-insights-sampling.md), si consiglia di usare `sum(itemCount)`, non `count()`.



## <a name="timed"></a> Temporizzazione degli eventi
A volte si vuole rappresentare in un grafico il tempo necessario per eseguire un'azione. Ad esempio si potrebbe voler sapere quanto tempo occorre agli utenti per scegliere tra le opzioni disponibili in un gioco. Per questo è possibile usare il parametro di misurazione.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Proprietà predefinite per i dati di telemetria personalizzati
Se si intende impostare solo i valori di proprietà predefiniti per alcuni degli eventi personalizzati scritti, è possibile impostarli in un'istanza di TelemetryClient. Vengono associati a ogni elemento di telemetria inviato da quel client.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");
    
*Node.JS*

    var gameTelemetry = new applicationInsights.TelemetryClient();
    gameTelemetry.commonProperties["Game"] = currentGame.Name;

    gameTelemetry.TrackEvent({name: "WinGame"});



Le singole chiamate di telemetria possono sostituire i valori predefiniti nei relativi dizionari delle proprietà.

*Per i client Web di JavaScript*, [usare gli inizializzatori di telemetria JavaScript](#js-initializer).

*Per aggiungere proprietà a tutti i dati di telemetria*, inclusi i dati dei moduli di raccolta standard, [implementare `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Campionamento, filtri ed elaborazione dei dati di telemetria
È possibile scrivere il codice per elaborare i dati di telemetria prima che vengano inviati dall'SDK. L'elaborazione include i dati inviati dai moduli di telemetria standard, come la raccolta delle richieste HTTP e la raccolta delle dipendenze.

[Aggiungere proprietà](app-insights-api-filtering-sampling.md#add-properties) ai dati di telemetria implementando `ITelemetryInitializer`. Ad esempio è possibile aggiungere numeri di versione o valori calcolati da altre proprietà.

L'[applicazione di filtri](app-insights-api-filtering-sampling.md#filtering) consente di modificare o rimuovere i dati di telemetria prima che vengano inviati dall'SDK implementando `ITelemetryProcesor`. È possibile controllare gli elementi inviati o eliminati, ma è necessario tenere conto dell'effetto sulle metriche. A seconda di come si eliminano gli elementi, si potrebbe perdere la possibilità di navigare tra elementi correlati.

Il [campionamento](app-insights-api-filtering-sampling.md) è una soluzione in pacchetto che consente di ridurre il volume dei dati inviati dall'app al portale. Lo fa senza influenzare le metriche visualizzate e senza influire sulla possibilità di diagnosticare i problemi navigando tra elementi correlati, come eccezioni, richieste e visualizzazioni di pagina.

[Altre informazioni](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Disabilitazione della telemetria
Per *avviare e arrestare in modo dinamico* la raccolta e la trasmissione di dati di telemetria:

*C#*

```csharp

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

Per *disabilitare gli agenti di raccolta standard selezionati*, ad esempio contatori delle prestazioni, richieste HTTP o dipendenze, eliminare o impostare come commento le righe pertinenti in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Ad esempio è possibile eseguire questa operazione se si desidera inviare i propri dati TrackRequest.

*Node.js*

```Javascript

    telemetry.config.disableAppInsights = true;
```

Per *disabilitare gli agenti di raccolta standard selezionati* (ad esempio, i contatori delle prestazioni, le richieste HTTP o le dipendenze, in fase di inizializzazione), concatenare i metodi di configurazione con il codice di inizializzazione SDK:

```Javascript

    applicationInsights.setup()
        .setAutoCollectRequests(false)
        .setAutoCollectPerformance(false)
        .setAutoCollectExceptions(false)
        .setAutoCollectDependencies(false)
        .setAutoCollectConsole(false)
        .start();
```

Per disabilitare questi agenti di raccolta dopo l'inizializzazione, usare l'oggetto Configuration:`applicationInsights.Configuration.setAutoCollectRequests(false)`

## <a name="debug"></a>Modalità di sviluppo
Durante il debug, è utile accelerare i dati di telemetria venga nella pipeline in modo da visualizzare immediatamente i risultati. È possibile che vengano visualizzati anche altri messaggi che consentono di tracciare eventuali problemi con i dati di telemetria. Disattivare questa modalità in fase di produzione poiché potrebbe rallentare l'app.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a> Impostazione della chiave di strumentazione per la telemetria personalizzata selezionata
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Chiave di strumentazione dinamica
Per evitare di combinare i dati di telemetria di ambienti di sviluppo, test e produzione, è possibile [creare risorse distinte di Application Insights](app-insights-create-new-resource.md) e modificare le relative chiavi a seconda dell'ambiente.

Invece di ottenere la chiave di strumentazione dal file di configurazione, è possibile impostarla nel codice. Impostare la chiave in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Nelle pagine Web è possibile impostarla dallo stato del server Web anziché codificarla nello script. Ad esempio, in una pagina Web generata in un'app ASP.NET:

*JavaScript in Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient dispone di una proprietà Context contenente valori che vengono inviati insieme a tutti i dati di telemetria. Sono in genere impostati dai moduli di telemetria standard, ma è possibile anche impostarli manualmente. Ad esempio: 

    telemetry.Context.Operation.Name = "MyOperationName";

Se si imposta uno di questi valori manualmente, provare a rimuovere la riga pertinente da [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), in modo che i valori personali e quelli standard non si confondano.

* **Componente**: l'app e la relativa versione.
* **Dispositivo**: dati relativi al dispositivo in cui l'applicazione è in esecuzione. Nelle App Web questo è il server o dispositivo client da cui sono inviati i dati di telemetria.
* **InstrumentationKey**: la risorsa di Application Insights in Azure dove sono visualizzati i dati di telemetria. Viene in genere presa dal file ApplicationInsights.config.
* **Posizione**: la posizione geografica del dispositivo.
* **Operazione**: nelle App Web la richiesta HTTP corrente. In altri tipi di app è possibile impostarla in modo da raggruppare gli eventi tra loro.
  * **ID**: un valore generato che mette in correlazione eventi diversi, in modo che quando si analizza qualsiasi evento in Ricerca diagnostica, è possibile trovare elementi correlati.
  * **Nome**: un identificatore, in genere l'URL della richiesta HTTP.
  * **SyntheticSource**: se non è null o vuota, una stringa indicante che l'origine della richiesta è stata identificata come un test Web o un robot. Per impostazione predefinita viene esclusa dai calcoli in Esplora metriche.
* **Proprietà**: proprietà che vengono inviate con tutti i dati di telemetria. È possibile eseguire l'override di questo valore in singole chiamate di Track*.
* **Sessione**: la sessione dell'utente. L'ID viene impostato su un valore generato, che viene modificato quando l'utente non è stato attivo per un periodo di tempo specifico.
* **Utente**: le informazioni dell'utente.

## <a name="limits"></a>Limiti
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

Per evitare di raggiungere il limite di velocità dei dati usare il [campionamento](app-insights-sampling.md).

Per determinare quanto tempo vengono conservati i dati, vedere [Raccolta, conservazione e archiviazione di dati in Application Insights](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documentazione di riferimento
* [Riferimento ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Riferimento Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Informazioni di riferimento su JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Codice SDK
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-aspnetcore)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [Pacchetti per Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [Node.js SDK](https://github.com/Microsoft/ApplicationInsights-Node.js)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)
* [Tutte le piattaforme](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Domande
* *Quali eccezioni potrebbero essere generate dalle chiamate Track_()?*

    No. Non è necessario eseguirne il wrapping in clausole try-catch. Se l'SDK rileva un problema, registrerà messaggi nell'output della console di debug e quindi in Ricerca diagnostica per approfondirne i dettagli.
* *Esiste un'API REST per ottenere dati dal portale?*

    Sì, l'[API di accesso ai dati](https://dev.applicationinsights.io/). Altri modi per estrarre i dati sono l'[esportazione da Analytics a Power BI](app-insights-export-power-bi.md) e l'[esportazione continua](app-insights-export-telemetry.md).

## <a name="next"></a>Passaggi successivi
* [Ricerca di eventi e log](app-insights-diagnostic-search.md)

* [Risoluzione dei problemi](app-insights-troubleshoot-faq.md)


