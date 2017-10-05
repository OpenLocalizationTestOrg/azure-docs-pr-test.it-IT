---
title: Filtrare i dati di telemetria di Azure Application Insights nell'App Web Java | Microsoft Docs
description: "Ridurre il traffico di telemetria escludendo gli eventi che non è necessario monitorare."
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
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="f5c00-103">Filtrare i dati di telemetria nell'App Web Java</span><span class="sxs-lookup"><span data-stu-id="f5c00-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="f5c00-104">I filtri consentono di selezionare i dati di telemetria [inviati dall'App Web Java ad Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f5c00-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="f5c00-105">Esistono alcuni filtri pronti da usare che è possibile applicare, inoltre è possibile creare filtri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f5c00-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="f5c00-106">I filtri pronti da usare includono:</span><span class="sxs-lookup"><span data-stu-id="f5c00-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="f5c00-107">Livello di gravità della traccia</span><span class="sxs-lookup"><span data-stu-id="f5c00-107">Trace severity level</span></span>
* <span data-ttu-id="f5c00-108">URL, parole chiave o codici di risposta specifici</span><span class="sxs-lookup"><span data-stu-id="f5c00-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="f5c00-109">Risposte rapide, vale a dire richieste a cui l'app ha risposto rapidamente</span><span class="sxs-lookup"><span data-stu-id="f5c00-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="f5c00-110">Nomi degli eventi specifici</span><span class="sxs-lookup"><span data-stu-id="f5c00-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="f5c00-111">I filtri alterano le metriche dell'app.</span><span class="sxs-lookup"><span data-stu-id="f5c00-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="f5c00-112">Ad esempio, si potrebbe decidere che, per diagnosticare un problema di risposte lente, verrà impostato un filtro per ignorare i tempi di risposta rapidi.</span><span class="sxs-lookup"><span data-stu-id="f5c00-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="f5c00-113">È necessario però tenere presente che i tempi medi di risposta segnalati da Application Insights saranno così più lenti rispetto alla velocità effettiva e che il numero di richieste sarà inferiore rispetto al numero reale.</span><span class="sxs-lookup"><span data-stu-id="f5c00-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="f5c00-114">Se questo rappresenta un problema, usare il [campionamento](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f5c00-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="f5c00-115">Impostazione di filtri</span><span class="sxs-lookup"><span data-stu-id="f5c00-115">Setting filters</span></span>

<span data-ttu-id="f5c00-116">In ApplicationInsights.xml aggiungere una sezione `TelemetryProcessors` come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="f5c00-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want to see -->
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




<span data-ttu-id="f5c00-117">[Esaminare l'insieme completo dei processori incorporati](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="f5c00-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="f5c00-118">Filtri incorporati</span><span class="sxs-lookup"><span data-stu-id="f5c00-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="f5c00-119">Filtro Dati di telemetria metrica</span><span class="sxs-lookup"><span data-stu-id="f5c00-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="f5c00-120">`NotNeeded`: elenco delimitato da virgole con i nomi delle metriche personalizzate.</span><span class="sxs-lookup"><span data-stu-id="f5c00-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="f5c00-121">Filtro Dati di telemetria visualizzazione di pagina</span><span class="sxs-lookup"><span data-stu-id="f5c00-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="f5c00-122">`DurationThresholdInMS`: la durata si riferisce al tempo impiegato per caricare la pagina.</span><span class="sxs-lookup"><span data-stu-id="f5c00-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="f5c00-123">Se è impostato, le pagine caricate più velocemente del tempo definito non vengono segnalate.</span><span class="sxs-lookup"><span data-stu-id="f5c00-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="f5c00-124">`NotNeededNames`: elenco delimitato da virgole con i nomi delle pagine.</span><span class="sxs-lookup"><span data-stu-id="f5c00-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="f5c00-125">`NotNeededUrls`: elenco delimitato da virgole con i frammenti di URL.</span><span class="sxs-lookup"><span data-stu-id="f5c00-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="f5c00-126">Ad esempio, `"home"` esclude tutte le pagine il cui URL include il termine "home".</span><span class="sxs-lookup"><span data-stu-id="f5c00-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="f5c00-127">Filtro Dati di telemetria richiesta</span><span class="sxs-lookup"><span data-stu-id="f5c00-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="f5c00-128">Filtro Origine sintetica</span><span class="sxs-lookup"><span data-stu-id="f5c00-128">Synthetic Source filter</span></span>

<span data-ttu-id="f5c00-129">Esclude tutti i dati di telemetria che dispongono di valori nella proprietà SyntheticSource.</span><span class="sxs-lookup"><span data-stu-id="f5c00-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="f5c00-130">Questi dati includono le richieste da bot, spider e test di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="f5c00-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="f5c00-131">Escludere i dati di telemetria per tutte le richieste sintetiche:</span><span class="sxs-lookup"><span data-stu-id="f5c00-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="f5c00-132">Escludere i dati di telemetria per le origini sintetiche specifiche:</span><span class="sxs-lookup"><span data-stu-id="f5c00-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="f5c00-133">`NotNeeded`: elenco delimitato da virgole con i nomi delle origini sintetiche.</span><span class="sxs-lookup"><span data-stu-id="f5c00-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="f5c00-134">Filtro Eventi di telemetria</span><span class="sxs-lookup"><span data-stu-id="f5c00-134">Telemetry Event filter</span></span>

<span data-ttu-id="f5c00-135">Esclude gli eventi personalizzati (registrati tramite [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="f5c00-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="f5c00-136">`NotNeededNames`: elenco delimitato da virgole con i nomi degli eventi.</span><span class="sxs-lookup"><span data-stu-id="f5c00-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="f5c00-137">Filtro Dati di telemetria traccia</span><span class="sxs-lookup"><span data-stu-id="f5c00-137">Trace Telemetry filter</span></span>

<span data-ttu-id="f5c00-138">Esclude le tracce di log (registrate tramite [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [agente di raccolta del framework di registrazione](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="f5c00-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="f5c00-139">I valori `FromSeverityLevel` validi sono:</span><span class="sxs-lookup"><span data-stu-id="f5c00-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="f5c00-140">OFF             - Esclude TUTTE le tracce</span><span class="sxs-lookup"><span data-stu-id="f5c00-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="f5c00-141">TRACE           - Non applica alcun filtro.</span><span class="sxs-lookup"><span data-stu-id="f5c00-141">TRACE           - No filtering.</span></span> <span data-ttu-id="f5c00-142">Corrisponde al livello Trace</span><span class="sxs-lookup"><span data-stu-id="f5c00-142">equals to Trace level</span></span>
 *  <span data-ttu-id="f5c00-143">INFO            - Esclude il livello TRACE</span><span class="sxs-lookup"><span data-stu-id="f5c00-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="f5c00-144">WARN            - Esclude TRACE e INFO</span><span class="sxs-lookup"><span data-stu-id="f5c00-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="f5c00-145">ERROR           - Esclude WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="f5c00-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="f5c00-146">CRITICAL        - Esclude tutto tranne CRITICAL</span><span class="sxs-lookup"><span data-stu-id="f5c00-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="f5c00-147">Filtri personalizzati</span><span class="sxs-lookup"><span data-stu-id="f5c00-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="f5c00-148">1. Codificare il filtro</span><span class="sxs-lookup"><span data-stu-id="f5c00-148">1. Code your filter</span></span>

<span data-ttu-id="f5c00-149">Nel codice creare una classe che implementa `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="f5c00-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
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


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="f5c00-150">2. Richiamare il filtro nel file di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5c00-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="f5c00-151">In ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="f5c00-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="f5c00-152">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f5c00-152">Troubleshooting</span></span>

<span data-ttu-id="f5c00-153">*Il filtro non funziona.*</span><span class="sxs-lookup"><span data-stu-id="f5c00-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="f5c00-154">Verificare che siano stati specificati valori di parametro validi.</span><span class="sxs-lookup"><span data-stu-id="f5c00-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="f5c00-155">Ad esempio, la durata deve essere espressa da numeri interi.</span><span class="sxs-lookup"><span data-stu-id="f5c00-155">For example, durations should be integers.</span></span> <span data-ttu-id="f5c00-156">Se i valori non sono validi, il filtro verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="f5c00-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="f5c00-157">Se il filtro personalizzato genera un'eccezione da un costruttore o un metodo impostato, verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="f5c00-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c00-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5c00-158">Next steps</span></span>

* <span data-ttu-id="f5c00-159">[Campionamento](app-insights-sampling.md): prendere in considerazione il campionamento come un'alternativa che non altera le metriche.</span><span class="sxs-lookup"><span data-stu-id="f5c00-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
