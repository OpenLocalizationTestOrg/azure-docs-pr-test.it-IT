---
title: dati di telemetria di Application Insights di Azure nell'app web Java aaaFilter | Documenti Microsoft
description: "Ridurre il traffico di dati di telemetria filtrando gli eventi di hello non è necessario toomonitor."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a>Filtrare i dati di telemetria nell'App Web Java

I filtri forniscono una telemetria hello tooselect di modo che il [app web Java invia tooApplication Insights](app-insights-java-get-started.md). Esistono alcuni filtri pronti da usare che è possibile applicare, inoltre è possibile creare filtri personalizzati.

i filtri di casella Hello includono:

* Livello di gravità della traccia
* URL, parole chiave o codici di risposta specifici
* Tempi di risposta rapidi - ovvero richieste toowhich l'app ha risposto tooquickly
* Nomi degli eventi specifici

> [!NOTE]
> I filtri distorcere metriche hello dell'app. Ad esempio, si potrebbe decidere che, in una risposta lenta toodiagnose ordine, si imposteranno tempi di risposta rapidi toodiscard un filtro. Ma è necessario essere consapevoli del fatto che i tempi di risposta medi hello segnalati da Application Insights potranno quindi essere più lenti rispetto a velocità true hello conteggio hello delle richieste sarà minore di count reale hello.
> Se questo rappresenta un problema, usare il [campionamento](app-insights-sampling.md).

## <a name="setting-filters"></a>Impostazione di filtri

In ApplicationInsights.xml aggiungere una sezione `TelemetryProcessors` come in questo esempio:


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




[Controllare il set completo di hello di processori incorporati](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Filtri incorporati

### <a name="metric-telemetry-filter"></a>Filtro Dati di telemetria metrica

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded`: elenco delimitato da virgole con i nomi delle metriche personalizzate.


### <a name="page-view-telemetry-filter"></a>Filtro Dati di telemetria visualizzazione di pagina

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-Durata si riferisce toohello tempo pagina hello tooload. Se è impostato, le pagine caricate più velocemente del tempo definito non vengono segnalate.
* `NotNeededNames`: elenco delimitato da virgole con i nomi delle pagine.
* `NotNeededUrls`: elenco delimitato da virgole con i frammenti di URL. Ad esempio, `"home"` esclude tutte le pagine contenenti "home" nell'URL hello.


### <a name="request-telemetry-filter"></a>Filtro Dati di telemetria richiesta


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Filtro Origine sintetica

Filtra tutti i dati di telemetria con valori di proprietà SyntheticSource hello. Questi dati includono le richieste da bot, spider e test di disponibilità.

Escludere i dati di telemetria per tutte le richieste sintetiche:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Escludere i dati di telemetria per le origini sintetiche specifiche:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded`: elenco delimitato da virgole con i nomi delle origini sintetiche.

### <a name="telemetry-event-filter"></a>Filtro Eventi di telemetria

Esclude gli eventi personalizzati (registrati tramite [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames`: elenco delimitato da virgole con i nomi degli eventi.


### <a name="trace-telemetry-filter"></a>Filtro Dati di telemetria traccia

Esclude le tracce di log (registrate tramite [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [agente di raccolta del framework di registrazione](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* I valori `FromSeverityLevel` validi sono:
 *  OFF             - Esclude TUTTE le tracce
 *  TRACE           - Non applica alcun filtro. è uguale a livello di tooTrace
 *  INFO            - Esclude il livello TRACE
 *  WARN            - Esclude TRACE e INFO
 *  ERROR           - Esclude WARN, INFO, TRACE
 *  CRITICAL        - Esclude tutto tranne CRITICAL


## <a name="custom-filters"></a>Filtri personalizzati

### <a name="1-code-your-filter"></a>1. Codificare il filtro

Nel codice creare una classe che implementa `TelemetryProcessor`:

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Richiamare il filtro nel file di configurazione hello

In ApplicationInsights.xml:

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a>Risoluzione dei problemi

*Il filtro non funziona.*

* Verificare che siano stati specificati valori di parametro validi. Ad esempio, la durata deve essere espressa da numeri interi. Valori non validi causerà toobe filtro hello ignorato. Se il filtro personalizzato genera un'eccezione da un costruttore o un metodo impostato, verrà ignorato.

## <a name="next-steps"></a>Passaggi successivi

* [Campionamento](app-insights-sampling.md): prendere in considerazione il campionamento come un'alternativa che non altera le metriche.
