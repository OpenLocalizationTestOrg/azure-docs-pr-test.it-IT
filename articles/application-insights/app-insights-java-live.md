---
title: "aaaApplication Insights per Java web App che sono già in tempo reale"
description: "Avviare il monitoraggio di un'applicazione web che è già in esecuzione sul server"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="991c5-103">Application Insights per le applicazioni web Java che sono già live</span><span class="sxs-lookup"><span data-stu-id="991c5-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="991c5-104">Se si dispone di un'applicazione web che è già in esecuzione sul server J2EE, è possibile avviare il monitoraggio con [Application Insights](app-insights-overview.md) senza hello necessario toomake alle modifiche al codice o ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="991c5-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="991c5-105">Con questa opzione, sono disponibili informazioni sulle richieste HTTP inviate tooyour server, le eccezioni non gestite e i contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="991c5-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="991c5-106">È necessario un abbonamento troppo[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="991c5-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="991c5-107">procedura di Hello in questa pagina consente di aggiungere hello SDK tooyour web app in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="991c5-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="991c5-108">La strumentazione di runtime è utile se si non desidera tooupdate o si ricompila il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="991c5-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="991c5-109">Ma è possibile, è consigliabile [aggiungere codice sorgente di hello SDK toohello](app-insights-java-get-started.md) invece.</span><span class="sxs-lookup"><span data-stu-id="991c5-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="991c5-110">Che offre più opzioni, ad esempio la scrittura di attività utente tootrack di codice.</span><span class="sxs-lookup"><span data-stu-id="991c5-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="991c5-111">1. Ottenere una chiave di strumentazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="991c5-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="991c5-112">Accedi toohello [portale Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="991c5-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="991c5-113">Creare una nuova risorsa di Application Insights e impostare hello tipo tooJava applicazione web.</span><span class="sxs-lookup"><span data-stu-id="991c5-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Inserire un nome, scegliere l'app Web Java e fare clic su Crea](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="991c5-115">risorsa Hello viene creato in pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="991c5-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="991c5-116">Aprire una nuova risorsa hello e ottenere la chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="991c5-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="991c5-117">È necessario toopaste questa chiave nel progetto di codice a breve.</span><span class="sxs-lookup"><span data-stu-id="991c5-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="991c5-119">2. Scaricare il SDK di hello</span><span class="sxs-lookup"><span data-stu-id="991c5-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="991c5-120">Scaricare hello [Application Insights SDK per Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="991c5-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="991c5-121">Nel server, estrarre directory toohello contenuto SDK hello da cui vengono caricati i file binari del progetto.</span><span class="sxs-lookup"><span data-stu-id="991c5-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="991c5-122">Se si usa Tomcat, la directory si trova in genere in`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="991c5-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="991c5-123">Si noti che è necessario toorepeat questo per ogni istanza del server e, per ogni app.</span><span class="sxs-lookup"><span data-stu-id="991c5-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="991c5-124">3. Aggiungere un file XML di Application Insights</span><span class="sxs-lookup"><span data-stu-id="991c5-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="991c5-125">Creare ApplicationInsights.xml nella cartella hello in cui è stato aggiunto hello SDK.</span><span class="sxs-lookup"><span data-stu-id="991c5-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="991c5-126">Inserirvi hello seguenti XML.</span><span class="sxs-lookup"><span data-stu-id="991c5-126">Put into it hello following XML.</span></span>

<span data-ttu-id="991c5-127">Sostituire con chiave di strumentazione hello recuperato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="991c5-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="991c5-128">chiave di strumentazione Hello viene inviata insieme a tutti gli elementi di dati di telemetria e indica toodisplay Application Insights nella risorsa.</span><span class="sxs-lookup"><span data-stu-id="991c5-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="991c5-129">componente di richiesta HTTP Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="991c5-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="991c5-130">Invia automaticamente i dati di telemetria sulle richieste e portale toohello tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="991c5-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="991c5-131">Correlazione di eventi è un componente di richiesta di aggiunta toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="991c5-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="991c5-132">Assegna una richiesta di tooeach identificatore ricevuta dal server hello e aggiunge questo identificatore come un elemento di dati di telemetria tooevery delle proprietà come proprietà hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="991c5-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="991c5-133">Consente di telemetria hello toocorrelate associata a ogni richiesta impostando un filtro [ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="991c5-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="991c5-134">4. Aggiungere un filtro HTTP</span><span class="sxs-lookup"><span data-stu-id="991c5-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="991c5-135">Individuare e aprire i file Web. XML hello nel progetto e hello merge seguente frammento di codice nel nodo di app web hello, dove sono stati configurati i filtri di applicazione.</span><span class="sxs-lookup"><span data-stu-id="991c5-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="991c5-136">risultati più accurati tooget hello, filtro hello devono essere mappati prima tutti gli altri filtri.</span><span class="sxs-lookup"><span data-stu-id="991c5-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="991c5-137">5. Verificare le eccezioni del firewall</span><span class="sxs-lookup"><span data-stu-id="991c5-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="991c5-138">Potrebbe essere troppo[set di dati in uscita toosend eccezioni](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="991c5-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="991c5-139">6. Riavviare la propria app web.</span><span class="sxs-lookup"><span data-stu-id="991c5-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="991c5-140">7. Visualizzare i dati di telemetria in Application Insights</span><span class="sxs-lookup"><span data-stu-id="991c5-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="991c5-141">Restituzione della risorsa di Application Insights tooyour in [portale Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="991c5-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="991c5-142">Dati di telemetria sulle richieste HTTP viene visualizzata nel pannello della panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="991c5-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="991c5-143">Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="991c5-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![dati di esempio](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="991c5-145">Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate.</span><span class="sxs-lookup"><span data-stu-id="991c5-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="991c5-146">E, quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="991c5-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="991c5-147">Altre informazioni sulle metriche.</span><span class="sxs-lookup"><span data-stu-id="991c5-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="991c5-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="991c5-148">Next steps</span></span>
* <span data-ttu-id="991c5-149">[Aggiungere le pagine web di telemetria tooyour](app-insights-javascript.md) toomonitor pagina viste e le metriche di utente.</span><span class="sxs-lookup"><span data-stu-id="991c5-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="991c5-150">[Configurare i test web](app-insights-monitor-web-app-availability.md) toomake che l'applicazione rimane in tempo reale e reattiva.</span><span class="sxs-lookup"><span data-stu-id="991c5-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="991c5-151">Acquisire le tracce dei log</span><span class="sxs-lookup"><span data-stu-id="991c5-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="991c5-152">[Ricerca di eventi e log](app-insights-diagnostic-search.md) toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="991c5-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

