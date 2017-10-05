---
title: Esaminare i log di traccia Java in Azure Application Insights | Documentazione Microsoft
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
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="20474-103">Esplorare i log di traccia Java in Application Insights</span><span class="sxs-lookup"><span data-stu-id="20474-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="20474-104">Se si usa Logback o Log4J (v1.2 o v2.0) per la traccia, è possibile inviare automaticamente i log di traccia ad Application Insights dove è possibile esplorarli e eseguirvi ricerche.</span><span class="sxs-lookup"><span data-stu-id="20474-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="20474-105">Installare Java SDK</span><span class="sxs-lookup"><span data-stu-id="20474-105">Install the Java SDK</span></span>

<span data-ttu-id="20474-106">Installare [Application Insights SDK per Java][java], se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="20474-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="20474-107">Se non si desidera tenere traccia delle richieste HTTP, è possibile omettere gran parte del file di configurazione .xml, ma è necessario includere almeno l'elemento `InstrumentationKey`.</span><span class="sxs-lookup"><span data-stu-id="20474-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="20474-108">È anche necessario chiamare `new TelemetryClient()` per inizializzare il SDK.</span><span class="sxs-lookup"><span data-stu-id="20474-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="20474-109">Aggiungere le librerie di registrazione al progetto</span><span class="sxs-lookup"><span data-stu-id="20474-109">Add logging libraries to your project</span></span>
<span data-ttu-id="20474-110">*Scegliere il modo più appropriato per il progetto.*</span><span class="sxs-lookup"><span data-stu-id="20474-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="20474-111">Se si usa Maven...</span><span class="sxs-lookup"><span data-stu-id="20474-111">If you're using Maven...</span></span>
<span data-ttu-id="20474-112">Se il progetto è già stato configurato per usare Maven per la compilazione, aggiungere uno dei frammenti di codice seguenti nel file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="20474-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="20474-113">Aggiornare quindi le dipendenze progetto per fare in modo che i file binari vengano scaricati.</span><span class="sxs-lookup"><span data-stu-id="20474-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="20474-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="20474-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="20474-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="20474-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="20474-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="20474-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="20474-117">Se si usa Gradle...</span><span class="sxs-lookup"><span data-stu-id="20474-117">If you're using Gradle...</span></span>
<span data-ttu-id="20474-118">Se il progetto è già configurato per usare Gradle per la compilazione, aggiungere una delle righe seguenti al gruppo `dependencies` nel file build.gradle:</span><span class="sxs-lookup"><span data-stu-id="20474-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="20474-119">Aggiornare quindi le dipendenze progetto per fare in modo che i file binari vengano scaricati.</span><span class="sxs-lookup"><span data-stu-id="20474-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="20474-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="20474-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="20474-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="20474-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="20474-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="20474-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="20474-123">In caso contrario...</span><span class="sxs-lookup"><span data-stu-id="20474-123">Otherwise ...</span></span>
<span data-ttu-id="20474-124">Scaricare ed estrarre l'appender appropriato e quindi aggiungere la libreria appropriata al progetto:</span><span class="sxs-lookup"><span data-stu-id="20474-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="20474-125">Logger</span><span class="sxs-lookup"><span data-stu-id="20474-125">Logger</span></span> | <span data-ttu-id="20474-126">Scaricare</span><span class="sxs-lookup"><span data-stu-id="20474-126">Download</span></span> | <span data-ttu-id="20474-127">Libreria</span><span class="sxs-lookup"><span data-stu-id="20474-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20474-128">Logback</span><span class="sxs-lookup"><span data-stu-id="20474-128">Logback</span></span> |[<span data-ttu-id="20474-129">SDK con appender Logback</span><span class="sxs-lookup"><span data-stu-id="20474-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="20474-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="20474-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="20474-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="20474-131">Log4J v2.0</span></span> |[<span data-ttu-id="20474-132">SDK con appender Log4J v2</span><span class="sxs-lookup"><span data-stu-id="20474-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="20474-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="20474-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="20474-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="20474-134">Log4j v1.2</span></span> |[<span data-ttu-id="20474-135">SDK con appender Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="20474-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="20474-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="20474-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="20474-137">Aggiungere l'appender per il framework di registrazione</span><span class="sxs-lookup"><span data-stu-id="20474-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="20474-138">Per iniziare la raccolta di tracce, unire il frammento di codice rilevante al file di configurazione Log4J o Logback:</span><span class="sxs-lookup"><span data-stu-id="20474-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="20474-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="20474-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="20474-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="20474-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="20474-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="20474-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="20474-142">È possibile fare riferimento agli appender di Application Insights da qualsiasi logger configurato e non necessariamente dal logger principale (come illustrato negli esempi di codice riportati sopra).</span><span class="sxs-lookup"><span data-stu-id="20474-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="20474-143">Esplorare le tracce nel portale Application Insights.</span><span class="sxs-lookup"><span data-stu-id="20474-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="20474-144">Ora che è stato configurato il progetto per inviare tracce in Application Insights, è possibile visualizzare e cercare queste tracce nel portale di Application Insights nel pannello [Ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="20474-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![Nel portale di Application Insights, aprire Ricerca diagnostica](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="20474-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20474-146">Next steps</span></span>
<span data-ttu-id="20474-147">[Ricerca diagnostica][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="20474-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


