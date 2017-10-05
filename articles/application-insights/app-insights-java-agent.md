---
title: Monitoraggio delle prestazioni per le app Web Java in Azure Application Insights | Documentazione Microsoft
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="ce9fc-103">Monitorare dipendenze, eccezioni e tempi di esecuzione nelle app Web Java</span><span class="sxs-lookup"><span data-stu-id="ce9fc-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="ce9fc-104">Se l'[app Web Java è stata instrumentata con Application Insights][java], sarà possibile usare l'agente Java per ottenere informazioni più dettagliate, senza modificare il codice:</span><span class="sxs-lookup"><span data-stu-id="ce9fc-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="ce9fc-105">**Dipendenze:** dati sulle chiamate effettuate dall'applicazione ad altri componenti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="ce9fc-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="ce9fc-106">**Chiamate REST** eseguite tramite HttpClient, OkHttp e RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="ce9fc-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="ce9fc-107">**Redis** effettuate tramite il client Jedis.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="ce9fc-108">Se la chiamata dura più di 10s, l'agente recupera anche gli argomenti della chiamata.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="ce9fc-109">**[Chiamate JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="ce9fc-110">Sono supportate le chiamate "executeBatch".</span><span class="sxs-lookup"><span data-stu-id="ce9fc-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="ce9fc-111">Per MySQL e PostgreSQL, se la chiamata dura più di 10s, l'agente segnala il piano di query.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="ce9fc-112">**Eccezioni rilevate:** dati sulle eccezioni gestite dal codice.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="ce9fc-113">**Tempo di esecuzione dei metodi:** dati sul tempo necessario per eseguire metodi specifici.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="ce9fc-114">Per usare l'agente Java, installarlo nel server.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="ce9fc-115">Le app Web devono essere instrumentate con [Application Insights Java SDK][java].</span><span class="sxs-lookup"><span data-stu-id="ce9fc-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="ce9fc-116">Installare l'agente di Application Insights per Java</span><span class="sxs-lookup"><span data-stu-id="ce9fc-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="ce9fc-117">[Scaricare l'agente](https://aka.ms/aijavasdk) sul computer che esegue il server Java.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="ce9fc-118">Modificare lo script di avvio del server applicazioni e aggiungere il codice JVM seguente:</span><span class="sxs-lookup"><span data-stu-id="ce9fc-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="ce9fc-119">`javaagent:`*percorso completo del file JAR dell'agente*</span><span class="sxs-lookup"><span data-stu-id="ce9fc-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="ce9fc-120">Ad esempio, in Tomcat su un computer Linux:</span><span class="sxs-lookup"><span data-stu-id="ce9fc-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="ce9fc-121">Riavviare il server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="ce9fc-122">Configurare l'agente</span><span class="sxs-lookup"><span data-stu-id="ce9fc-122">Configure the agent</span></span>
<span data-ttu-id="ce9fc-123">Creare un file detto `AI-Agent.xml` e inserirlo nella stessa cartella che include il file JAR dell'agente.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="ce9fc-124">Configurare il contenuto del file XML.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-124">Set the content of the xml file.</span></span> <span data-ttu-id="ce9fc-125">Modificare l'esempio seguente in modo da includere o escludere le funzionalità desiderate.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="ce9fc-126">È necessario abilitare le eccezioni dei report e la durata del metodo per i singoli metodi.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="ce9fc-127">Per impostazione predefinita, `reportExecutionTime` è true e `reportCaughtExceptions` è false.</span><span class="sxs-lookup"><span data-stu-id="ce9fc-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="ce9fc-128">Visualizzare i dati</span><span class="sxs-lookup"><span data-stu-id="ce9fc-128">View the data</span></span>
<span data-ttu-id="ce9fc-129">Nella risorsa Application Insights vengono visualizzate le dipendenze remote aggregate e i tempi di esecuzione dei metodi [nel riquadro Prestazioni][metrics].</span><span class="sxs-lookup"><span data-stu-id="ce9fc-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="ce9fc-130">Per cercare singole istanze di dipendenze, eccezioni e report sui metodi, aprire [Ricerca][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ce9fc-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="ce9fc-131">[Diagnosi dei problemi di dipendenza - ulteriori informazioni](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="ce9fc-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="ce9fc-132">Domande?</span><span class="sxs-lookup"><span data-stu-id="ce9fc-132">Questions?</span></span> <span data-ttu-id="ce9fc-133">Problemi?</span><span class="sxs-lookup"><span data-stu-id="ce9fc-133">Problems?</span></span>
* <span data-ttu-id="ce9fc-134">Dati non visualizzati</span><span class="sxs-lookup"><span data-stu-id="ce9fc-134">No data?</span></span> [<span data-ttu-id="ce9fc-135">Impostare le eccezioni del firewall</span><span class="sxs-lookup"><span data-stu-id="ce9fc-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="ce9fc-136">Risoluzione dei problemi Java</span><span class="sxs-lookup"><span data-stu-id="ce9fc-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
