---
title: Registra aaaExplore traccia Java in Azure Application Insights | Documenti Microsoft
description: Eseguire la ricerca di tracce Log4J o Logback in Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="fb68f-103">Esplorare i log di traccia Java in Application Insights</span><span class="sxs-lookup"><span data-stu-id="fb68f-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="fb68f-104">Se si usa Log4J o Logback (versione 1.2 o 2.0) per la traccia, è possibile utilizzare i log di traccia inviati automaticamente tooApplication informazioni dettagliate in cui è possibile esplorare e ricerche.</span><span class="sxs-lookup"><span data-stu-id="fb68f-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="fb68f-105">Installare hello SDK per Java</span><span class="sxs-lookup"><span data-stu-id="fb68f-105">Install hello Java SDK</span></span>

<span data-ttu-id="fb68f-106">Installare [Application Insights SDK per Java][java], se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="fb68f-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="fb68f-107">(Se non si desidera che le richieste di tootrack HTTP, è possibile omettere la maggior parte dei file di configurazione XML hello, ma è necessario includere almeno hello `InstrumentationKey` elemento.</span><span class="sxs-lookup"><span data-stu-id="fb68f-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="fb68f-108">È inoltre necessario chiamare `new TelemetryClient()` tooinitialize hello SDK.)</span><span class="sxs-lookup"><span data-stu-id="fb68f-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="fb68f-109">Aggiungere la registrazione delle librerie tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="fb68f-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="fb68f-110">*Scegliere hello modalità appropriata per il progetto.*</span><span class="sxs-lookup"><span data-stu-id="fb68f-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="fb68f-111">Se si usa Maven...</span><span class="sxs-lookup"><span data-stu-id="fb68f-111">If you're using Maven...</span></span>
<span data-ttu-id="fb68f-112">Se il progetto è già impostato toouse Maven per la compilazione, di tipo merge uno dei seguenti frammenti di codice nel file pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="fb68f-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="fb68f-113">Aggiornare quindi dipendenze progetto hello, i file binari hello tooget scaricati.</span><span class="sxs-lookup"><span data-stu-id="fb68f-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="fb68f-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="fb68f-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="fb68f-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="fb68f-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="fb68f-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="fb68f-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="fb68f-117">Se si usa Gradle...</span><span class="sxs-lookup"><span data-stu-id="fb68f-117">If you're using Gradle...</span></span>
<span data-ttu-id="fb68f-118">Se il progetto è già impostato toouse Gradle per la compilazione, aggiungere uno dei seguenti righe toohello hello `dependencies` gruppo nel file gradle:</span><span class="sxs-lookup"><span data-stu-id="fb68f-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="fb68f-119">Aggiornare quindi dipendenze progetto hello, i file binari hello tooget scaricati.</span><span class="sxs-lookup"><span data-stu-id="fb68f-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="fb68f-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="fb68f-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="fb68f-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="fb68f-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="fb68f-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="fb68f-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="fb68f-123">In caso contrario...</span><span class="sxs-lookup"><span data-stu-id="fb68f-123">Otherwise ...</span></span>
<span data-ttu-id="fb68f-124">Scaricare ed estrarre appender di hello appropriato, quindi aggiungere hello libreria appropriata tooyour progetto:</span><span class="sxs-lookup"><span data-stu-id="fb68f-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="fb68f-125">Logger</span><span class="sxs-lookup"><span data-stu-id="fb68f-125">Logger</span></span> | <span data-ttu-id="fb68f-126">Scaricare</span><span class="sxs-lookup"><span data-stu-id="fb68f-126">Download</span></span> | <span data-ttu-id="fb68f-127">Libreria</span><span class="sxs-lookup"><span data-stu-id="fb68f-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb68f-128">Logback</span><span class="sxs-lookup"><span data-stu-id="fb68f-128">Logback</span></span> |[<span data-ttu-id="fb68f-129">SDK con appender Logback</span><span class="sxs-lookup"><span data-stu-id="fb68f-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="fb68f-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="fb68f-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="fb68f-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="fb68f-131">Log4J v2.0</span></span> |[<span data-ttu-id="fb68f-132">SDK con appender Log4J v2</span><span class="sxs-lookup"><span data-stu-id="fb68f-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="fb68f-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="fb68f-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="fb68f-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="fb68f-134">Log4j v1.2</span></span> |[<span data-ttu-id="fb68f-135">SDK con appender Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="fb68f-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="fb68f-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="fb68f-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="fb68f-137">Aggiungere il framework di registrazione tooyour appender hello</span><span class="sxs-lookup"><span data-stu-id="fb68f-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="fb68f-138">toostart recupero tracce, importante frammento hello merge del codice toohello Log4J o Logback file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="fb68f-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="fb68f-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="fb68f-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="fb68f-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="fb68f-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="fb68f-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="fb68f-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="fb68f-142">appenders Application Insights Hello può fare riferimento da qualsiasi logger configurato e non necessariamente logger radice hello (come illustrato negli esempi di codice hello sopra).</span><span class="sxs-lookup"><span data-stu-id="fb68f-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="fb68f-143">Esplorare le tracce nel portale Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="fb68f-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="fb68f-144">Ora che è stato configurato il progetto toosend tracce tooApplication Insights, è possibile visualizzare e cercare le tracce nel hello del portale Application Insights hello [ricerca] [ diagnostic] blade.</span><span class="sxs-lookup"><span data-stu-id="fb68f-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![Nel portale Application Insights hello, aprire una ricerca](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="fb68f-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb68f-146">Next steps</span></span>
<span data-ttu-id="fb68f-147">[Ricerca diagnostica][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="fb68f-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


