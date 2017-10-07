---
title: aaaFiltering e pre-elaborazione hello Azure Application Insights SDK | Documenti Microsoft
description: "Scrivere processori di telemetria e gli inizializzatori di telemetria per hello SDK toofilter o aggiungere dati di proprietà toohello prima dell'invio portale Application Insights toohello telemetria hello."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Applicazione di filtri e pre-elaborazione di dati di telemetria di Application Insights SDK hello


È possibile scrivere e configurare i plug-in per hello Application Insights SDK toocustomize come dati di telemetria vengono acquisiti ed elaborati prima che venga inviato toohello servizio Application Insights.

* [Campionamento](app-insights-sampling.md) riduce volume hello di telemetria senza alterare le statistiche. Tiene insieme i punti dati correlati per poter passare da uno all'altro quando si diagnostica un problema. Nel portale di hello nei conteggi totali hello sono toocompensate moltiplicato per il campionamento hello.
* Applicazione di filtri con processori di telemetria [per ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) consente di selezionare o modificare i dati di telemetria in hello SDK prima di inviarlo toohello server. Ad esempio, è possibile ridurre il volume di hello di telemetria escludendo le richieste da robot. Ma il filtro è un traffico di tooreducing approccio più semplice di campionamento. Consente un controllo maggiore su ciò che viene trasmesso, ma si dispone di toobe tenere presente che influisce sulle statistiche, ad esempio, se si esclude tutte le richieste riuscite.
* [Gli inizializzatori di telemetria aggiungono proprietà](#add-properties) tooany telemetria inviato dall'app, inclusi i dati di telemetria dai moduli standard hello. Ad esempio, è possibile aggiungere valori calcolati. o i numeri di versione per i dati di hello toofilter nel portale di hello.
* [Hello API SDK](app-insights-api-custom-events-metrics.md) è usato toosend di eventi personalizzati e le metriche.

Prima di iniziare:

* Installare hello Application Insights [SDK per ASP.NET](app-insights-asp-net.md) o [SDK per Java](app-insights-java-get-started.md) nell'app.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtro: ITelemetryProcessor
Questa tecnica consente di controllare più direttamente su ciò che è incluso o escluso dal flusso di dati di telemetria hello. È possibile usarla insieme al campionamento oppure separatamente.

telemetria toofilter, scrivere un processore di dati di telemetria e registrarlo con hello SDK. Tutti i dati di telemetria passa attraverso il processore, ed è possibile scegliere toodrop dalla hello stream o aggiungere proprietà. Include dati di telemetria dai moduli standard di hello come agente di raccolta richiesta HTTP hello e agente di raccolta dipendenza hello e telemetria che è stato scritto personalmente. È possibile, ad esempio, filtrare la telemetria sulle richieste dei robot o le chiamate di dipendenza riuscite.

> [!WARNING]
> Il filtro di dati di telemetria hello inviati da hello SDK usando processori può distorcere statistiche hello viene visualizzata nel portale di hello e renderlo difficile toofollow elementi correlati.
>
> In alternativa, valutare la possibilità di usare il [campionamento](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Creare un processore di telemetria (C#)
1. Verificare che hello Application Insights SDK nel progetto è versione 2.0.0 o versione successiva. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni di Visual Studio e scegliere Gestisci pacchetti NuGet. In Gestione pacchetti NuGet selezionare Microsoft.ApplicationInsights.Web.
2. toocreate un filtro, implementare ITelemetryProcessor. un altro punto di estendibilità come il modulo di telemetria, l'inizializzatore di telemetria e il canale di telemetria.

    Si noti che i processori di telemetria creano una catena di elaborazione. Quando si crea un'istanza di un processore di dati di telemetria, si passa un processore di collegamento toohello successivo nella catena di hello. Quando un punto dati di telemetria viene passato a metodo Process toohello, esegue il proprio lavoro e quindi chiama hello processore telemetria successivo nella catena di hello.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Inserirlo in ApplicationInsights.config:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Si tratta di hello stessa sezione utilizzato per inizializzare un filtro di campionamento.)

È possibile passare i valori stringa da file con estensione config hello fornendo proprietà denominate pubblica nella classe.

> [!WARNING]
> Prestare attenzione toomatch hello nome e tipo tutti i nomi delle proprietà nella classe toohello del file hello. config e i nomi delle proprietà nel codice hello. Se il file con estensione config hello fa riferimento a un tipo inesistente o una proprietà, hello SDK invisibile all'utente non riesca toosend eventuali dati di telemetria.
>
>

**In alternativa,** è possibile inizializzare il filtro hello nel codice. Inserire il processore in una classe di inizializzazione adatto, ad esempio AppStart in Global.asax.cs - catena hello:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Gli elementi TelemetryClient creati dopo questo punto useranno i processori dell'utente.

### <a name="example-filters"></a>Filtri di esempio
#### <a name="synthetic-requests"></a>Richieste sintetiche
Filtrare i robot e i test Web. Sebbene un Esplora metriche hello toofilter opzione out origini sintetiche, questa opzione riduce il traffico di filtrarli in hello SDK.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Autenticazione non riuscita
Filtrare le richieste con una risposta "401".

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Filtrare le chiamate di dipendenza remote rapide
Se si desidera solo chiamate toodiagnose che risultano lente, escludere quelli fast hello.

> [!NOTE]
> Questo alteri statistiche hello che viene visualizzato nel portale di hello. grafico delle dipendenze Hello apparirà come se tutti gli errori di chiamate a dipendenze hello.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Diagnosticare i problemi di dipendenza
[In questo blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) problemi di un progetto toodiagnose dipendenza inviando automaticamente toodependencies ping regolare.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Aggiungere proprietà: ITelemetryInitializer
Utilizzare i dati di telemetria inizializzatori toodefine le proprietà globali che vengono inviate con tutti i dati di telemetria; e il comportamento di toooverride selezionato di moduli standard telemetria hello.

Ad esempio, hello Application Insights per il pacchetto Web raccoglie dati di telemetria sulle richieste HTTP. per impostazione predefinita, contrassegna come non riuscita qualsiasi richiesta con un codice di risposta > = 400. Tuttavia se si desidera tootreat 400 come esito positivo, è possibile specificare un inizializzatore di telemetria che imposta proprietà Success hello.

Se viene fornito un inizializzatore di telemetria, viene chiamato ogni volta che uno qualsiasi dei hello Track*() metodi viene chiamato. Sono inclusi i metodi chiamati dai moduli di telemetria standard hello. Per convenzione, questi moduli non impostano le proprietà che sono già state impostate da un inizializzatore.

**Definire l'inizializzatore**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Caricare l'inizializzatore**

In ApplicationInsights.config:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*In alternativa,* è possibile creare un'istanza di inizializzatore hello nel codice, ad esempio in Global.aspx.cs:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Vedere questo esempio nel dettaglio.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Inizializzatori di telemetria JavaScript
*JavaScript*

Inserire un inizializzatore di telemetria immediatamente dopo il codice di inizializzazione hello che è stato ottenuto dal portale hello:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Per un riepilogo delle proprietà non personalizzata hello disponibile in telemetryItem hello, vedere [modello dati esportazione dell'applicazione Insights](app-insights-export-data-model.md).

È possibile aggiungere tutti gli inizializzatori desiderati.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor e ITelemetryInitializer
Qual è la differenza hello tra i processori di telemetria e gli inizializzatori di telemetria?

* Esistono alcune sovrapposizioni in operazioni eseguibili con tali: entrambi possono essere utilizzati tooadd tootelemetry di proprietà.
* Gli inizializzatori di telemetria vengono sempre eseguiti prima dei processori di telemetria.
* TelemetryProcessors consentono toocompletely sostituire o eliminare un elemento di dati di telemetria.
* I processori di telemetria non elaborano dati di telemetria dei contatori delle prestazioni.


## <a name="reference-docs"></a>Documentazione di riferimento
* [Panoramica API](app-insights-api-custom-events-metrics.md)
* [Riferimento ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Codice SDK
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Passaggi successivi
* [Ricerca di eventi e log](app-insights-diagnostic-search.md)
* [Campionamento](app-insights-sampling.md)
* [Risoluzione dei problemi](app-insights-troubleshoot-faq.md)
