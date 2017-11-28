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
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="45a24-103">Filtrare i dati di telemetria nell'App Web Java</span><span class="sxs-lookup"><span data-stu-id="45a24-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="45a24-104">I filtri forniscono una telemetria hello tooselect di modo che il [app web Java invia tooApplication Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45a24-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="45a24-105">Esistono alcuni filtri pronti da usare che è possibile applicare, inoltre è possibile creare filtri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="45a24-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="45a24-106">i filtri di casella Hello includono:</span><span class="sxs-lookup"><span data-stu-id="45a24-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="45a24-107">Livello di gravità della traccia</span><span class="sxs-lookup"><span data-stu-id="45a24-107">Trace severity level</span></span>
* <span data-ttu-id="45a24-108">URL, parole chiave o codici di risposta specifici</span><span class="sxs-lookup"><span data-stu-id="45a24-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="45a24-109">Tempi di risposta rapidi - ovvero richieste toowhich l'app ha risposto tooquickly</span><span class="sxs-lookup"><span data-stu-id="45a24-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="45a24-110">Nomi degli eventi specifici</span><span class="sxs-lookup"><span data-stu-id="45a24-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="45a24-111">I filtri distorcere metriche hello dell'app.</span><span class="sxs-lookup"><span data-stu-id="45a24-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="45a24-112">Ad esempio, si potrebbe decidere che, in una risposta lenta toodiagnose ordine, si imposteranno tempi di risposta rapidi toodiscard un filtro.</span><span class="sxs-lookup"><span data-stu-id="45a24-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="45a24-113">Ma è necessario essere consapevoli del fatto che i tempi di risposta medi hello segnalati da Application Insights potranno quindi essere più lenti rispetto a velocità true hello conteggio hello delle richieste sarà minore di count reale hello.</span><span class="sxs-lookup"><span data-stu-id="45a24-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="45a24-114">Se questo rappresenta un problema, usare il [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="45a24-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="45a24-115">Impostazione di filtri</span><span class="sxs-lookup"><span data-stu-id="45a24-115">Setting filters</span></span>

<span data-ttu-id="45a24-116">In ApplicationInsights.xml aggiungere una sezione `TelemetryProcessors` come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="45a24-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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




<span data-ttu-id="45a24-117">[Controllare il set completo di hello di processori incorporati](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="45a24-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="45a24-118">Filtri incorporati</span><span class="sxs-lookup"><span data-stu-id="45a24-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="45a24-119">Filtro Dati di telemetria metrica</span><span class="sxs-lookup"><span data-stu-id="45a24-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="45a24-120">`NotNeeded`: elenco delimitato da virgole con i nomi delle metriche personalizzate.</span><span class="sxs-lookup"><span data-stu-id="45a24-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="45a24-121">Filtro Dati di telemetria visualizzazione di pagina</span><span class="sxs-lookup"><span data-stu-id="45a24-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="45a24-122">`DurationThresholdInMS`-Durata si riferisce toohello tempo pagina hello tooload.</span><span class="sxs-lookup"><span data-stu-id="45a24-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="45a24-123">Se è impostato, le pagine caricate più velocemente del tempo definito non vengono segnalate.</span><span class="sxs-lookup"><span data-stu-id="45a24-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="45a24-124">`NotNeededNames`: elenco delimitato da virgole con i nomi delle pagine.</span><span class="sxs-lookup"><span data-stu-id="45a24-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="45a24-125">`NotNeededUrls`: elenco delimitato da virgole con i frammenti di URL.</span><span class="sxs-lookup"><span data-stu-id="45a24-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="45a24-126">Ad esempio, `"home"` esclude tutte le pagine contenenti "home" nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="45a24-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="45a24-127">Filtro Dati di telemetria richiesta</span><span class="sxs-lookup"><span data-stu-id="45a24-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="45a24-128">Filtro Origine sintetica</span><span class="sxs-lookup"><span data-stu-id="45a24-128">Synthetic Source filter</span></span>

<span data-ttu-id="45a24-129">Filtra tutti i dati di telemetria con valori di proprietà SyntheticSource hello.</span><span class="sxs-lookup"><span data-stu-id="45a24-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="45a24-130">Questi dati includono le richieste da bot, spider e test di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="45a24-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="45a24-131">Escludere i dati di telemetria per tutte le richieste sintetiche:</span><span class="sxs-lookup"><span data-stu-id="45a24-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="45a24-132">Escludere i dati di telemetria per le origini sintetiche specifiche:</span><span class="sxs-lookup"><span data-stu-id="45a24-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="45a24-133">`NotNeeded`: elenco delimitato da virgole con i nomi delle origini sintetiche.</span><span class="sxs-lookup"><span data-stu-id="45a24-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="45a24-134">Filtro Eventi di telemetria</span><span class="sxs-lookup"><span data-stu-id="45a24-134">Telemetry Event filter</span></span>

<span data-ttu-id="45a24-135">Esclude gli eventi personalizzati (registrati tramite [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="45a24-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="45a24-136">`NotNeededNames`: elenco delimitato da virgole con i nomi degli eventi.</span><span class="sxs-lookup"><span data-stu-id="45a24-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="45a24-137">Filtro Dati di telemetria traccia</span><span class="sxs-lookup"><span data-stu-id="45a24-137">Trace Telemetry filter</span></span>

<span data-ttu-id="45a24-138">Esclude le tracce di log (registrate tramite [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [agente di raccolta del framework di registrazione](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="45a24-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="45a24-139">I valori `FromSeverityLevel` validi sono:</span><span class="sxs-lookup"><span data-stu-id="45a24-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="45a24-140">OFF             - Esclude TUTTE le tracce</span><span class="sxs-lookup"><span data-stu-id="45a24-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="45a24-141">TRACE           - Non applica alcun filtro.</span><span class="sxs-lookup"><span data-stu-id="45a24-141">TRACE           - No filtering.</span></span> <span data-ttu-id="45a24-142">è uguale a livello di tooTrace</span><span class="sxs-lookup"><span data-stu-id="45a24-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="45a24-143">INFO            - Esclude il livello TRACE</span><span class="sxs-lookup"><span data-stu-id="45a24-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="45a24-144">WARN            - Esclude TRACE e INFO</span><span class="sxs-lookup"><span data-stu-id="45a24-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="45a24-145">ERROR           - Esclude WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="45a24-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="45a24-146">CRITICAL        - Esclude tutto tranne CRITICAL</span><span class="sxs-lookup"><span data-stu-id="45a24-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="45a24-147">Filtri personalizzati</span><span class="sxs-lookup"><span data-stu-id="45a24-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="45a24-148">1. Codificare il filtro</span><span class="sxs-lookup"><span data-stu-id="45a24-148">1. Code your filter</span></span>

<span data-ttu-id="45a24-149">Nel codice creare una classe che implementa `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="45a24-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="45a24-150">2. Richiamare il filtro nel file di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="45a24-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="45a24-151">In ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="45a24-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="45a24-152">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="45a24-152">Troubleshooting</span></span>

<span data-ttu-id="45a24-153">*Il filtro non funziona.*</span><span class="sxs-lookup"><span data-stu-id="45a24-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="45a24-154">Verificare che siano stati specificati valori di parametro validi.</span><span class="sxs-lookup"><span data-stu-id="45a24-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="45a24-155">Ad esempio, la durata deve essere espressa da numeri interi.</span><span class="sxs-lookup"><span data-stu-id="45a24-155">For example, durations should be integers.</span></span> <span data-ttu-id="45a24-156">Valori non validi causerà toobe filtro hello ignorato.</span><span class="sxs-lookup"><span data-stu-id="45a24-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="45a24-157">Se il filtro personalizzato genera un'eccezione da un costruttore o un metodo impostato, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="45a24-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a24-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45a24-158">Next steps</span></span>

* <span data-ttu-id="45a24-159">[Campionamento](app-insights-sampling.md): prendere in considerazione il campionamento come un'alternativa che non altera le metriche.</span><span class="sxs-lookup"><span data-stu-id="45a24-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
