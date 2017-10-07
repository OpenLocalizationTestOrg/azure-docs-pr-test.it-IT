---
title: il monitoraggio per le applicazioni web Java in Azure Application Insights aaaPerformance | Documenti Microsoft
description: Estendere il monitoraggio di prestazioni e utilizzo del sito Web Java con Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="82d6b-103">Monitorare dipendenze, eccezioni e tempi di esecuzione nelle app Web Java</span><span class="sxs-lookup"><span data-stu-id="82d6b-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="82d6b-104">Se dispone di [instrumentato app web Java con Application Insights][java], è possibile utilizzare hello agente Java tooget approfondite, senza alcuna modifica al codice:</span><span class="sxs-lookup"><span data-stu-id="82d6b-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="82d6b-105">**Dipendenze:** dati relative chiamate effettuate dall'applicazione tooother componenti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="82d6b-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="82d6b-106">**Chiamate REST** eseguite tramite HttpClient, OkHttp e RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="82d6b-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="82d6b-107">**Redis** chiamate effettuate tramite hello Jedis client.</span><span class="sxs-lookup"><span data-stu-id="82d6b-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="82d6b-108">Se chiamata hello richiede più tempo 10s, agente hello recupera anche gli argomenti di chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="82d6b-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="82d6b-109">**[Chiamate JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="82d6b-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="82d6b-110">Sono supportate le chiamate "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="82d6b-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="82d6b-111">Per MySQL e PostgreSQL, se chiamata hello richiede più tempo 10s, hello agente riporta il piano di query hello.</span><span class="sxs-lookup"><span data-stu-id="82d6b-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="82d6b-112">**Eccezioni rilevate:** dati sulle eccezioni gestite dal codice.</span><span class="sxs-lookup"><span data-stu-id="82d6b-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="82d6b-113">**Metodo tempo di esecuzione:** dati relativi a hello ora accetta tooexecute specifici metodi.</span><span class="sxs-lookup"><span data-stu-id="82d6b-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="82d6b-114">agente APM Java hello toouse, si installarlo nel server.</span><span class="sxs-lookup"><span data-stu-id="82d6b-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="82d6b-115">Le app web devono essere instrumentate con hello [Application Insights SDK per Java][java].</span><span class="sxs-lookup"><span data-stu-id="82d6b-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="82d6b-116">Installare l'agente di Application Insights hello per Java</span><span class="sxs-lookup"><span data-stu-id="82d6b-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="82d6b-117">Nel computer di hello esegue il server Java, [Scarica agente hello](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="82d6b-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="82d6b-118">Modifica di script di avvio server applicazione hello e aggiungere hello JVM seguente:</span><span class="sxs-lookup"><span data-stu-id="82d6b-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="82d6b-119">`javaagent:`*file JAR agente toohello di percorso completo*</span><span class="sxs-lookup"><span data-stu-id="82d6b-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="82d6b-120">Ad esempio, in Tomcat su un computer Linux:</span><span class="sxs-lookup"><span data-stu-id="82d6b-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="82d6b-121">Riavviare il server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="82d6b-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="82d6b-122">Configurare l'agente di hello</span><span class="sxs-lookup"><span data-stu-id="82d6b-122">Configure hello agent</span></span>
<span data-ttu-id="82d6b-123">Creare un file denominato `AI-Agent.xml` e inserirle in hello stessa cartella del file JAR di hello agente.</span><span class="sxs-lookup"><span data-stu-id="82d6b-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="82d6b-124">Impostare hello il contenuto del file xml di hello.</span><span class="sxs-lookup"><span data-stu-id="82d6b-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="82d6b-125">Modifica hello tooinclude riportato di seguito oppure omettere funzionalità hello desiderate.</span><span class="sxs-lookup"><span data-stu-id="82d6b-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="82d6b-126">È necessario tooenable report eccezione e la tempistica di metodo per i singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="82d6b-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="82d6b-127">Per impostazione predefinita, `reportExecutionTime` è true e `reportCaughtExceptions` è false.</span><span class="sxs-lookup"><span data-stu-id="82d6b-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="82d6b-128">Visualizzare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="82d6b-128">View hello data</span></span>
<span data-ttu-id="82d6b-129">Nella risorsa di Application Insights hello, viene visualizzato l'aggregato remoto dipendenza e il metodo tempi di esecuzione [in hello prestazioni riquadro][metrics].</span><span class="sxs-lookup"><span data-stu-id="82d6b-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="82d6b-130">toosearch per singole istanze di relazioni di dipendenza, l'eccezione e il metodo, aprire [ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="82d6b-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="82d6b-131">[Diagnosi dei problemi di dipendenza - ulteriori informazioni](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="82d6b-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="82d6b-132">Domande?</span><span class="sxs-lookup"><span data-stu-id="82d6b-132">Questions?</span></span> <span data-ttu-id="82d6b-133">Problemi?</span><span class="sxs-lookup"><span data-stu-id="82d6b-133">Problems?</span></span>
* <span data-ttu-id="82d6b-134">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="82d6b-134">No data?</span></span> [<span data-ttu-id="82d6b-135">Impostare le eccezioni del firewall</span><span class="sxs-lookup"><span data-stu-id="82d6b-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="82d6b-136">Risoluzione dei problemi Java</span><span class="sxs-lookup"><span data-stu-id="82d6b-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
