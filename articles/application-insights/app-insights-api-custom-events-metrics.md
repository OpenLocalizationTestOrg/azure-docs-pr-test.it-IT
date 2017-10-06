---
title: aaaApplication Insights API per gli eventi personalizzati e le metriche | Documenti Microsoft
description: Inserire alcune righe di codice in uso tootrack dispositivo o app desktop, pagina Web o servizio e diagnosticare i problemi.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API di Application Insights per metriche ed eventi personalizzati

Inserire alcune righe di codice in toofind l'applicazione out operazioni con gli utenti o toohelp diagnosticare i problemi. È possibile inviare i dati di telemetria dalle app desktop e per dispositivi, dai client Web e dai server Web. Hello utilizzare [Azure Application Insights](app-insights-overview.md) principali di eventi di telemetria API toosend personalizzati e le metriche e le versioni personalizzate di telemetria standard. Questa API è hello stessa API standard di hello usare agenti di raccolta dati Application Insights.

## <a name="api-summary"></a>Riepilogo dell'API
API Hello è uniforme in tutte le piattaforme, a parte alcune piccole variazioni.

| Metodo | Usato per |
| --- | --- |
| [`TrackPageView`](#page-views) |Pagine, schermate, pannelli o form. |
| [`TrackEvent`](#trackevent) |Azioni dell'utente e altri eventi. Utilizzato tootrack utente toomonitor o il comportamento delle prestazioni. |
| [`TrackMetric`](#trackmetric) |Misurazioni delle prestazioni, ad esempio lunghezza della coda di eventi di toospecific non correlati. |
| [`TrackException`](#trackexception) |Registrare le eccezioni per la diagnosi. Traccia in cui si verificano eventi tooother relazione e come esaminare le tracce dello stack. |
| [`TrackRequest`](#trackrequest) |Registrazione hello frequenza e durata delle richieste del server per l'analisi delle prestazioni. |
| [`TrackTrace`](#tracktrace) |Messaggi nei log di diagnostica. È anche possibile acquisire log di terze parti. |
| [`TrackDependency`](#trackdependency) |La registrazione hello durata e frequenza dei componenti tooexternal chiamate che l'applicazione dipende. |

È possibile [associare proprietà e le metriche](#properties) toomost di queste chiamate di telemetria.

## <a name="prep"></a>Prima di iniziare
Se non si ha ancora un riferimento in Application Insights SDK:

* Aggiungere hello Application Insights SDK tooyour progetto:

  * [Progetto ASP.NET](app-insights-asp-net.md)
  * [Progetto Java](app-insights-java-get-started.md)
  * [JavaScript in ogni pagina Web](app-insights-javascript.md) 
* Nel dispositivo o nel codice del server Web includere:

    *C#:* `using Microsoft.ApplicationInsights;`

    *Visual Basic:* `Imports Microsoft.ApplicationInsights`

    *Java:* `import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Costruzione di un'istanza di TelemetryClient
Costruire un'istanza di `TelemetryClient` (tranne che in JavaScript nelle pagine Web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient è thread-safe.

È consigliabile usare un'istanza di TelemetryClient per ogni modulo dell'app. Ad esempio, potrebbe essere un'istanza di TelemetryClient il web tooreport richieste HTTP in arrivo e un altro in un middleware classe tooreport business logica gli eventi. È possibile impostare proprietà, ad esempio `TelemetryClient.Context.User.Id` tootrack utenti e sessioni, o `TelemetryClient.Context.Device.Id` macchina hello tooidentify. Queste informazioni sono hello istanza invia gli eventi tooall associata.

## <a name="trackevent"></a>TrackEvent
In Application Insights un *evento personalizzato* è un punto dati che è possibile visualizzare in [Esplora metriche](app-insights-metrics-explorer.md) come conteggio aggregato e in [Ricerca diagnostica](app-insights-diagnostic-search.md) come singole occorrenze. (Se non è correlato tooMVC o altri framework "eventi.")

Inserisci `TrackEvent` chiama il codice toocount vari eventi. La frequenza d'uso di una particolare funzionalità, la frequenza di raggiungimento di obiettivi specifici o la frequenza di particolari tipi di errore.

Ad esempio, in un'app di gioco, inviare un evento ogni volta che un utente wins gioco hello:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Visualizzare gli eventi nel portale di Microsoft Azure hello
toosee un conteggio degli eventi, aprire un [Esplora metriche](app-insights-metrics-explorer.md) pannello, aggiungere un nuovo grafico e selezionare **eventi**.  

![Visualizzare il conteggio degli eventi personalizzati](./media/app-insights-api-custom-events-metrics/01-custom.png)

conteggi di hello toocompare di eventi differenti, impostare il tipo di grafico hello troppo**griglia**e di gruppo in base al nome evento:

![Impostare il tipo di grafico hello e raggruppamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

Nella griglia di hello, fare clic su tramite un evento nome toosee singole occorrenze di tale evento. toosee ulteriori dettagli, fare clic su qualsiasi occorrenza nell'elenco di hello.

![Drill-through eventi hello](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus su eventi specifici per ricerche o Esplora metriche, filtro toohello i nomi degli eventi del set hello pannello che si è interessati:

![Aprire i filtri, espandere il nome dell’evento e selezionare uno o più valori](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Eventi personalizzati in Analytics

dati di telemetria Hello è disponibile in hello `customEvents` tabella [Application Insights Analitica](app-insights-analytics.md). Ogni riga rappresenta una chiamata troppo`trackEvent(..)` nell'app. 

Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1. Per esempio itemCount = = 10 significa che di 10 chiamate tootrackEvent(), il processo di campionamento hello trasmesso solo uno di essi. tooget un conteggio corretto di eventi personalizzati, è necessario utilizzare pertanto il codice, ad esempio `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights può grafico delle metriche che non sono collegati tooparticular eventi. Ad esempio, è possibile monitorare la lunghezza di una coda a intervalli regolari. Con le metriche, corrisponderanno hello è meno interessanti di varianti hello e le tendenze e pertanto statistici grafici sono utili.

In ordine metriche toosend tooApplication Insights, è possibile usare hello `TrackMetric(..)` API. Esistono due modi toosend una metrica: 

* Valore singolo. Ogni volta che si esegue una misurazione nell'applicazione, inviare il valore corrispondente hello tooApplication Insights. Ad esempio, si supponga di disporre di una metrica che descrive il numero di hello di elementi in un contenitore. Durante un periodo di tempo specifico, inserire innanzitutto tre elementi contenitore hello e quindi si rimuove due elementi. Di conseguenza, è necessario chiamare `TrackMetric` due volte: prima di tutto se si passa il valore di hello `3` e quindi hello valore `-2`. Application Insights memorizza entrambi i valori per conto dell'utente. 

* Aggregazione. Quando si usano le metriche non si considera mai una sola misura. È importante invece il riepilogo delle operazioni eseguite in un periodo di tempo specifico. Tale riepilogo viene chiamato _aggregazione_. In hello sopra riportato, hello aggregazione Somma di metrica per quel periodo di tempo è `1` e conteggio hello di valori della metrica hello è `2`. Quando si utilizza l'approccio di aggregazione hello, richiamare solo `TrackMetric` una volta ogni ora periodo e trasmissione hello valori aggregati. Si tratta di hello approccio consigliato poiché può ridurre notevolmente il costo di hello e prestazioni overhead inviando i dati meno punti Insights tooApplication, durante la raccolta ancora tutte le informazioni pertinenti.

### <a name="examples"></a>Esempi:

#### <a name="single-values"></a>Valori singoli

toosend un singolo valore di metrica:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Aggregazione delle metriche

È consigliabile prima di inviarli dall'app, tooreduce della larghezza di banda, le prestazioni di costo e tooimprove tooaggregate metriche.
Di seguito è riportato un esempio di codice di aggregazione:

*C#*

```C#
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
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
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
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
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

risultati di hello toosee, aprire Esplora metriche e aggiungere un nuovo grafico. Modificare hello grafico tooshow l'unità di misura.

> [!NOTE]
> La metrica personalizzata potrebbe richiedere diversi minuti tooappear nell'elenco di hello delle metriche disponibili.
>

![Aggiungere un nuovo grafico o selezionare un grafico e selezionare le metriche in Personalizzato](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Metriche personalizzate in Analytics

dati di telemetria Hello è disponibile in hello `customMetrics` tabella [Application Insights Analitica](app-insights-analytics.md). Ogni riga rappresenta una chiamata troppo`trackMetric(..)` nell'app.
* `valueSum`-Indica la somma di hello di misurazioni hello. valore medio tooget hello, divisione per `valueCount`.
* `valueCount`-numero di misure che sono stati aggregati in questo hello `trackMetric(..)` chiamare.

## <a name="page-views"></a>Visualizzazioni pagina
In un'app per dispositivo o pagine Web i dati di telemetria delle visualizzazioni pagina vengono inviati per impostazione predefinita quando viene caricata ogni schermata o pagina. Ma è possibile modificare tale viste pagina tootrack in momenti aggiuntive o diverse. Ad esempio, in un'applicazione che consente di visualizzare le schede o sui pannelli, è consigliabile tootrack una pagina ogni volta che l'utente di hello apre un nuovo pannello.

![Sezione Utilizzo nel pannello Panoramica](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Dati utente e della sessione vengono inviati come proprietà con le visualizzazioni di pagina, pertanto hello grafici utente e sessione vive quando è telemetria di visualizzazione pagina.

### <a name="custom-page-views"></a>Visualizzazioni pagina personalizzate
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Se si dispone di diverse schede nelle diverse pagine HTML, è possibile specificare URL hello troppo:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Temporizzazione delle visualizzazioni delle pagine
Per impostazione predefinita, i tempi di hello segnalati come **visualizzare il tempo di caricamento pagina** vengono misurate da quando il browser hello Invia richiesta hello, fino a quando non viene chiamato l'evento di caricamento pagina del browser hello.

In alternativa, è possibile:

* Impostare una durata esplicita in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chiamare: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Utilizzare le chiamate di temporizzazione hello pagina visualizzazione `startTrackPage` e `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

nome utilizzato come primo parametro hello associa inizio hello Hello e arrestare le chiamate. Per impostazione predefinita toohello nome della pagina corrente.

caricamento pagina risultante Hello durate visualizzate in Esplora metriche sono derivate dall'intervallo di hello tra hello avviare e arrestare le chiamate. È attivo tooyou quale intervallo di tempo effettivamente necessario.

### <a name="page-telemetry-in-analytics"></a>Dati di telemetria della pagina in Analytics

In [Analytics](app-insights-analytics.md) due tabelle mostrano i dati delle operazioni del browser:

* Hello `pageViews` tabella contiene dati relativi a titolo di pagina e URL hello
* Hello `browserTimings` tabella contiene dati sulle prestazioni del client, ad esempio hello scattato tooprocess hello dati in ingresso

toofind quanto tempo browser hello accetta tooprocess diverse pagine:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities di hello dei diversi browser:

```
pageViews | summarize count() by client_Browser
```

tooassociate pagina viste tooAJAX chiamate, creare un join con dipendenze:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
il server di Hello SDK utilizza le richieste HTTP di TrackRequest toolog.

È inoltre possibile chiamarlo manualmente se si desidera che le richieste di toosimulate in un contesto in cui non è in esecuzione modulo di servizio web di hello.

Tuttavia, hello consiglia di telemetria delle ricerche toosend modo in cui la richiesta hello agisce come un <a href="#operation-context">contesto dell'operazione</a>.

## <a name="operation-context"></a>Contesto dell'operazione
È possibile associare elementi di dati di telemetria collegando toothem un ID dell'operazione comune. modulo di registrazione delle richieste standard Hello avviene per le eccezioni e altri eventi che vengono inviati durante l'elaborazione di una richiesta HTTP. In [ricerca](app-insights-diagnostic-search.md) e [Analitica](app-insights-analytics.md), è possibile utilizzare tutti gli eventi associati alla richiesta hello hello ID tooeasily trova.

ID Hello più semplice modo tooset hello è tooset un contesto dell'operazione utilizzando questo modello:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Con l'impostazione di un contesto dell'operazione, `StartOperation` crea un elemento di dati di telemetria di hello di tipo specificato. Invia dati di telemetria hello elemento quando si elimina l'operazione di hello o se si chiama in modo esplicito `StopOperation`. Se si utilizza `RequestTelemetry` come tipo di dati di telemetria hello, la durata è impostare l'intervallo di timeout toohello tra inizio e fine.

I contesti dell’operazione non possono essere annidati. Se è già presente un contesto dell'operazione, quindi è associata a tutti gli elementi contenuto hello, inclusi elementi hello creato con l'ID `StartOperation`.

In ricerca di contesto dell'operazione hello è hello toocreate utilizzati **elementi correlati** elenco:

![Elementi correlati](./media/app-insights-api-custom-events-metrics/21.png)

Per altre informazioni sulle operazioni di rilevamento personalizzate, vedere [application-insights-custom-operations-tracking.md].

### <a name="requests-in-analytics"></a>Richieste in Analytics 

In [Application Insights Analitica](app-insights-analytics.md), richieste Mostra backup in hello `requests` tabella.

Se [campionamento](app-insights-sampling.md) è nell'operazione, la proprietà itemCount hello verrà visualizzato un valore maggiore di 1. Per esempio itemCount = = 10 significa che di 10 chiamate tootrackRequest(), il processo di campionamento hello trasmesso solo uno di essi. un numero corretto di richieste e durata media di tooget segmentate per i nomi di richiesta, usare codice, ad esempio:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Inviare le eccezioni tooApplication Insights:

* troppo[contarli](app-insights-metrics-explorer.md), come indicazione della frequenza di hello di un problema.
* troppo[esaminare le singole occorrenze](app-insights-diagnostic-search.md).

i report di Hello includono le analisi dello stack hello.

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

SDK Hello catch molte eccezioni automaticamente, non vi è sempre toocall TrackException in modo esplicito.

* ASP.NET: [scrivere codice eccezioni toocatch](app-insights-asp-net-exceptions.md).
* J2EE: [Le eccezioni vengono rilevate automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Le eccezioni vengono rilevate automaticamente. Se si desidera la raccolta automatica di toodisable, aggiungere un frammento di codice toohello riga da inserire nelle pagine Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Eccezioni in Analytics

In [Application Insights Analitica](app-insights-analytics.md), le eccezioni visualizzata in hello `exceptions` tabella.

Se [campionamento](app-insights-sampling.md) è in esecuzione, hello `itemCount` proprietà Mostra un valore maggiore di 1. Per esempio itemCount = = 10 significa che di 10 chiamate tootrackException(), il processo di campionamento hello trasmesso solo uno di essi. tooget un conteggio corretto delle eccezioni segmentate per tipo di eccezione, usare codice, ad esempio:

```
exceptions | summarize sum(itemCount) by type
```

La maggior parte delle hello importante informazioni sullo stack sono già estratto in variabili distinte, ma è possibile effettuare il pull hello lontani `details` tooget struttura altre. Poiché questa struttura è dinamica, è necessario eseguire il cast di tipo toohello di hello risultato che previsto. ad esempio:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

le eccezioni tooassociate con le richieste correlate, è possibile utilizzare un join:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Utilizzare TrackTrace toohelp diagnosticare i problemi mediante l'invio di un tooApplication "percorso" informazioni dettagliate. È possibile inviare blocchi di dati di diagnostica e controllarli in [Ricerca diagnostica](app-insights-diagnostic-search.md).

[Gli adattatori di log](app-insights-asp-net-trace-logs.md) usare questo portale di toohello API toosend i log di terze parti.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


È possibile eseguire ricerche nel contenuto del messaggio, ma, a differenza dei valori delle proprietà, non è possibile filtrarlo.

Limite dimensione Hello `message` è molto più elevate rispetto al limite di hello per le proprietà.
Un vantaggio TrackTrace è possibile inserire dati relativamente lunghi nel messaggio hello. Ad esempio è possibile codificare dati POST.  

Inoltre, è possibile aggiungere un messaggio tooyour livello di gravità. E, come gli altri dati di telemetria, è possibile aggiungere toohelp di valori di proprietà che è applicare un filtro o ricerca per diversi set di tracce. ad esempio:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

In [ricerca](app-insights-diagnostic-search.md), è quindi possibile filtrare facilmente tutti i messaggi hello di un livello di gravità specifico correlati tooa particolare database.


### <a name="traces-in-analytics"></a>Tracce in Analytics

In [Application Insights Analitica](app-insights-analytics.md), chiama tooTrackTrace Mostra hello `traces` tabella.

Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1. Per esempio itemCount = = 10 significa che di 10 chiamate troppo`trackTrace()`, il processo di campionamento hello trasmesso solo uno di essi. tooget un conteggio corretto delle chiamate di traccia, è consigliabile utilizzare pertanto codice, ad esempio `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Hello utilizzare TrackDependency chiamare tempi di risposta tootrack hello e percentuali di successo di parte esterna tooan di chiamate del codice. risultati di Hello vengono visualizzati nei grafici dipendenza hello nel portale di hello.

```C#
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

Tenere presente che il server hello SDK includono un [modulo dipendenza](app-insights-asp-net-dependencies.md) che consente di individuare e tiene traccia di determinate chiamate a dipendenze automaticamente, ad esempio toodatabases e le API REST. È necessario un agente su un modulo hello toomake server tooinstall di lavoro. Utilizzare questa chiamata, se si desidera non intercettare chiamate tootrack hello rilevamento automatico o se non si desidera agente hello tooinstall.

Modifica tooturn off modulo di rilevamento delle dipendenze hello standard, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) ed eliminare il riferimento hello troppo`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dipendenze in Analytics

In [Application Insights Analitica](app-insights-analytics.md), trackDependency chiamate visualizzati nella hello `dependencies` tabella.

Se [campionamento](app-insights-sampling.md) è in esecuzione, la proprietà itemCount hello Mostra un valore maggiore di 1. Per esempio itemCount = = 10 significa che di 10 chiamate tootrackDependency(), il processo di campionamento hello trasmesso solo uno di essi. un conteggio corretto delle dipendenze di tooget segmentate per componente di destinazione, usare codice, ad esempio:

```
dependencies | summarize sum(itemCount) by target
```

dipendenze tooassociate con le richieste correlate, è possibile utilizzare un join:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Scaricamento dei dati
In genere, hello SDK invia i dati in alcuni casi scelti impatto hello toominimize utente hello. Tuttavia, in alcuni casi, è consigliabile buffer hello tooflush, ad esempio, se si utilizza hello SDK in un'applicazione che viene chiuso.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Si noti che la funzione hello è asincrona per hello [canale dati di telemetria server](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>utenti autenticati
In un'app Web gli utenti sono identificati dai cookie per impostazione predefinita. Un utente può essere conteggiato più volte se accede all'app da un computer o da un browser diverso o se elimina i cookie.

Se gli utenti accedono tooyour app, è possibile ottenere un conteggio più preciso impostando l'ID utente hello autenticato nel codice browser hello:

*JavaScript*

```JS
// Called when my app has identified hello user.
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

Non è effettivo nome di accesso toouse necessario hello utente. Include solo un ID utente univoco toothat toobe. Non deve includere spazi o caratteri hello `,;=|`.

ID utente Hello viene anche impostato in un cookie di sessione e inviati toohello server. Se è installato il server di hello SDK, hello l'utente autenticato che ID viene inviato come parte delle proprietà di contesto hello del client e server dati di telemetria. Quindi sarà possibile filtrarlo ed eseguire ricerche al suo interno.

Se l'app gruppi di utenti nell'account, è anche possibile passare un identificatore per l'account di hello (con hello stesso restrizioni relative ai caratteri).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

In [Esplora metriche](app-insights-metrics-explorer.md) è possibile creare un grafico che conta i valori **Utenti, Autenticati** e **Account utente**.

È anche possibile [cercare](app-insights-diagnostic-search.md) i punti dati del client con account e nomi utente specifici.

## <a name="properties"></a>Filtro, ricerca e segmentazione dei dati mediante le proprietà
È possibile associare proprietà e le misurazioni tooyour eventi (e anche toometrics, visualizzazioni di pagina, le eccezioni e altri dati di telemetria).

*Proprietà* sono valori stringa che è possibile utilizzare toofilter dati di telemetria nei report di utilizzo di hello. Ad esempio, se l'app fornisce numerosi giochi di tipo, è possibile collegare il nome di hello dell'evento di gioco tooeach hello in modo da poter visualizzare giochi vengono utilizzati più di frequente.

È previsto un limite di 8192 nella lunghezza della stringa hello. (Se si desidera toosend grandi quantità di dati, utilizzare il parametro messaggio hello del [TrackTrace](#track-trace).)

*metriche* sono valori numerici che possono essere rappresentati graficamente. Ad esempio, è consigliabile toosee se è presente un aumento graduale punteggi hello che raggiungono i giocatori. grafici di Hello possono essere segmentati per separano le proprietà che vengono inviate con evento hello, in modo che sia possibile ottenere hello o in pila grafici per i giochi di diversi tipo.

Per i valori della metrica toobe visualizzato correttamente, dovrebbero essere maggiore o uguale too0.

Esistono tuttavia alcuni [limiti sul numero di hello di proprietà, i valori delle proprietà e le metriche](#limits) che è possibile utilizzare.

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

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
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
> Prestare attenzione toolog informazioni personali nelle proprietà.
>
>

*Se è stata utilizzata la metrica*, aprire Esplora metriche e selezionare la metrica hello hello **personalizzato** gruppo:

![Aprire Esplora metriche, grafico selezionare hello e selezionare la metrica hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Se non viene visualizzata l'unità di misura, o se hello **personalizzato** intestazione non è presente, il pannello di selezione Chiudi hello e riprovare più tardi. Metriche talvolta possono richiedere un'ora toobe aggregati tramite pipeline hello.

*Se si utilizza le proprietà e le metriche*, segmento metrica hello dalla proprietà hello:

![Impostare il raggruppamento e quindi selezionare proprietà hello in Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*Nella ricerca diagnostica*, è possibile visualizzare le proprietà di hello e le metriche di singole occorrenze di un evento.

![Selezionare un'istanza e quindi scegliere "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Hello utilizzare **ricerca** toosee occorrenze dell'evento che hanno un valore di determinate proprietà di campo.

![Digitare un termine in Ricerca](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Altre informazioni sulle espressioni di ricerca](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Le metriche e le proprietà di tooset alternativa
Se è più semplice, è possibile raccogliere i parametri di hello di un evento in un oggetto separato:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Non riutilizzare hello stessa istanza dell'elemento di dati di telemetria (`event` in questo esempio) toocall Track*() più volte. Ciò potrebbe causare toobe telemetria inviati con una configurazione errata.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Misure e proprietà personalizzate in Analytics

In [Analitica](app-insights-analytics.md), metriche personalizzate e le proprietà vengono visualizzati in hello `customMeasurements` e `customDimensions` gli attributi di ogni record di dati di telemetria.

Ad esempio, se è stata aggiunta una proprietà denominata "gioco" tooyour telemetria di richiesta, questa query conta le occorrenze di hello dei diversi valori di "gioco" e Mostra la media hello di hello metrica personalizzata "punteggio":

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Si noti che:

* Quando si estrae un valore da hello customDimensions o customMeasurements JSON, è di tipo dinamico e pertanto è necessario eseguirne il cast `tostring` o `todouble`.
* account tootake della probabilità hello [campionamento](app-insights-sampling.md), si consiglia di utilizzare `sum(itemCount)`, non `count()`.



## <a name="timed"></a> Temporizzazione degli eventi
Talvolta toochart il tempo necessario tooperform un'azione. Ad esempio, è possibile tooknow quanti utenti acquisire scelte tooconsider un gioco. È possibile utilizzare il parametro di misura hello per questo oggetto.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Proprietà predefinite per i dati di telemetria personalizzati
Se si desidera tooset valori di proprietà predefiniti per alcuni eventi hello personalizzati scritti, è possibile impostare tali in un'istanza di TelemetryClient. Si tratta di elemento di dati di telemetria tooevery allegato inviato dal client.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Telemetria singole chiamate possono eseguire l'override di valori predefiniti di hello nei dizionari loro proprietà.

*Per i client Web di JavaScript*, [usare gli inizializzatori di telemetria JavaScript](#js-initializer).

*dati di telemetria tooall proprietà tooadd*, compresi i dati hello moduli di raccolta standard, [implementare `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Campionamento, filtri ed elaborazione dei dati di telemetria
È possibile scrivere codice tooprocess dati di telemetria prima che venga inviato da hello SDK. l'elaborazione di Hello include i dati inviati dai moduli di telemetria standard hello, ad esempio l'insieme di richiesta HTTP e raccolta di dipendenze.

[Aggiungere proprietà](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`. Ad esempio è possibile aggiungere numeri di versione o valori calcolati da altre proprietà.

[Filtro](app-insights-api-filtering-sampling.md#filtering) può modificare o eliminare dati di telemetria prima che venga inviato da hello SDK implementando `ITelemetryProcesor`. Controllare gli elementi inviati o eliminati, ma è necessario tooaccount per effetto di hello per le misurazioni. A seconda di come si elimina gli elementi, si potrebbe perdere hello possibilità toonavigate tra gli elementi correlati.

[Campionamento](app-insights-api-filtering-sampling.md) è un volume di hello tooreduce soluzione nel pacchetto di dati inviati dal portale toohello app. Esegue l'operazione senza influire sulle metriche hello visualizzato. E a tale scopo senza influire sulla risoluzione dei problemi di toodiagnose possibilità passando tra gli elementi correlati, ad esempio eccezioni, le richieste e le visualizzazioni di pagina.

[Altre informazioni](app-insights-api-filtering-sampling.md)

## <a name="disabling-telemetry"></a>Disabilitazione della telemetria
troppo*dinamicamente arrestare e avviare* hello raccolta e la trasmissione di dati di telemetria:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

troppo*disabilitare gli agenti di raccolta standard selezionati*, ad esempio, i contatori delle prestazioni, le richieste HTTP o dipendenze, eliminare o impostare come commento le righe rilevanti hello in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). È possibile farlo, ad esempio, se si desidera toosend TrackRequest dati personalizzati.

## <a name="debug"></a>Modalità di sviluppo
Durante il debug, è utile toohave dati di telemetria inviati attraverso la pipeline hello in modo che sia possibile osservare immediatamente i risultati. È inoltre get altri messaggi che consentono di analizzare i problemi di telemetria hello. Disattivare questa modalità in fase di produzione poiché potrebbe rallentare l'app.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Impostazione chiave di strumentazione hello per dati di telemetria personalizzati selezionato
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Chiave di strumentazione dinamica
tooavoid combinazione di dati di telemetria di sviluppo, test e ambienti di produzione, è possibile [creare risorse di Application Insights distinte](app-insights-create-new-resource.md) e modificare le relative chiavi, a seconda di ambiente hello.

Anziché la chiave di strumentazione hello dal file di configurazione di hello, è possibile impostarlo nel codice. Impostare la chiave di hello in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:

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



Nelle pagine Web, è possibile tooset dal server hello web, anziché codifica letteralmente in script hello. Ad esempio, in una pagina Web generata in un'app ASP.NET:

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
TelemetryClient dispone di una proprietà Context contenente valori che vengono inviati insieme a tutti i dati di telemetria. In genere impostati dai moduli di hello telemetria standard, ma è anche possibile impostarle personalmente. ad esempio:

    telemetry.Context.Operation.Name = "MyOperationName";

Impostando uno di questi valori manualmente, si consiglia di rimuovere hello rilevanti riga [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), in modo che i valori e valori standard hello non confusione.

* **Componente**: hello app e la relativa versione.
* **Dispositivo**: dati sul dispositivo hello in cui è in esecuzione l'applicazione hello. (In applicazioni web, questo è server hello o un dispositivo client inviate da dati di telemetria hello).
* **Manualmente InstrumentationKey**: risorsa di Application Insights in Azure in cui vengono visualizzati dati di telemetria hello hello. Viene in genere presa dal file ApplicationInsights.config.
* **Percorso**: hello posizione geografica del dispositivo hello.
* **Operazione**: nelle App web, hello richiesta HTTP corrente. In altri tipi di app, è possibile impostare questo toogroup di eventi.
  * **ID**: un valore generato che mette in correlazione eventi diversi, in modo che quando si analizza qualsiasi evento in Ricerca diagnostica, è possibile trovare elementi correlati.
  * **Nome**: un identificatore, in genere hello URL della richiesta HTTP hello.
  * **SyntheticSource**: se non null o vuoto, una stringa che indica che tale origine hello della richiesta di hello è stata identificata come un test web o robot. Per impostazione predefinita viene esclusa dai calcoli in Esplora metriche.
* **Proprietà**: proprietà che vengono inviate con tutti i dati di telemetria. È possibile eseguire l'override di questo valore in singole chiamate di Track*.
* **Sessione**: hello sessione utente. ID Hello è impostato un valore di tooa generato, che viene modificato quando l'utente hello non è stato attivo per un periodo di tempo.
* **Utente**: le informazioni dell'utente.

## <a name="limits"></a>Limiti
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

raggiungimento di limite di velocità dati hello, utilizzare tooavoid [campionamento](app-insights-sampling.md).

toodetermine come dati di tipo long viene mantenuti, vedere [conservazione dei dati e la privacy](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documentazione di riferimento
* [Riferimento ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Riferimento Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Informazioni di riferimento su JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Codice SDK
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Pacchetti per Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [SDK per Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)
* [Tutte le piattaforme](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Domande
* *Quali eccezioni potrebbero essere generate dalle chiamate Track_()?*

    Nessuna. Non è necessario toowrap usarle nelle clausole try-catch. Se hello SDK si verificano problemi, messaggi vengono registrati nell'output di console debug hello e --se hello messaggi ottenere mediante - ricerca di diagnostica.
* *È una data tooget API REST dal portale hello?*

    Sì, hello [API di accesso ai dati](https://dev.applicationinsights.io/). Includono altri dati tooextract modi [esportare da Analitica tooPower BI](app-insights-export-power-bi.md) e [l'esportazione continua](app-insights-export-telemetry.md).

## <a name="next"></a>Passaggi successivi
* [Ricerca di eventi e log](app-insights-diagnostic-search.md)

* [Risoluzione dei problemi](app-insights-troubleshoot-faq.md)


