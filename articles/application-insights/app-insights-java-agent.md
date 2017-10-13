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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Monitorare dipendenze, eccezioni e tempi di esecuzione nelle app Web Java


Se l'[app Web Java è stata instrumentata con Application Insights][java], sarà possibile usare l'agente Java per ottenere informazioni più dettagliate, senza modificare il codice:

* **Dipendenze:** dati sulle chiamate effettuate dall'applicazione ad altri componenti, tra cui:
  * **Chiamate REST** eseguite tramite HttpClient, OkHttp e RestTemplate (Spring).
  * **Redis** effettuate tramite il client Jedis. Se la chiamata dura più di 10s, l'agente recupera anche gli argomenti della chiamata.
  * **[Chiamate JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o Apache Derby DB. Sono supportate le chiamate "executeBatch". Per MySQL e PostgreSQL, se la chiamata dura più di 10s, l'agente segnala il piano di query.
* **Eccezioni rilevate:** dati sulle eccezioni gestite dal codice.
* **Tempo di esecuzione dei metodi:** dati sul tempo necessario per eseguire metodi specifici.

Per usare l'agente Java, installarlo nel server. Le app Web devono essere instrumentate con [Application Insights Java SDK][java]. 

## <a name="install-the-application-insights-agent-for-java"></a>Installare l'agente di Application Insights per Java
1. [Scaricare l'agente](https://aka.ms/aijavasdk) sul computer che esegue il server Java.
2. Modificare lo script di avvio del server applicazioni e aggiungere il codice JVM seguente:
   
    `javaagent:`*percorso completo del file JAR dell'agente*
   
    Ad esempio, in Tomcat su un computer Linux:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. Riavviare il server applicazioni.

## <a name="configure-the-agent"></a>Configurare l'agente
Creare un file detto `AI-Agent.xml` e inserirlo nella stessa cartella che include il file JAR dell'agente.

Configurare il contenuto del file XML. Modificare l'esempio seguente in modo da includere o escludere le funzionalità desiderate.

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

È necessario abilitare le eccezioni dei report e la durata del metodo per i singoli metodi.

Per impostazione predefinita, `reportExecutionTime` è true e `reportCaughtExceptions` è false.

## <a name="view-the-data"></a>Visualizzare i dati
Nella risorsa Application Insights vengono visualizzate le dipendenze remote aggregate e i tempi di esecuzione dei metodi [nel riquadro Prestazioni][metrics].

Per cercare singole istanze di dipendenze, eccezioni e report sui metodi, aprire [Ricerca][diagnostic].

[Diagnosi dei problemi di dipendenza - ulteriori informazioni](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Domande? Problemi?
* Dati non visualizzati [Impostare le eccezioni del firewall](app-insights-ip-addresses.md)
* [Risoluzione dei problemi Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
