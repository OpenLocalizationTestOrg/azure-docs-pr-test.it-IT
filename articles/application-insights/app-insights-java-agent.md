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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Monitorare dipendenze, eccezioni e tempi di esecuzione nelle app Web Java


Se dispone di [instrumentato app web Java con Application Insights][java], è possibile utilizzare hello agente Java tooget approfondite, senza alcuna modifica al codice:

* **Dipendenze:** dati relative chiamate effettuate dall'applicazione tooother componenti, tra cui:
  * **Chiamate REST** eseguite tramite HttpClient, OkHttp e RestTemplate (Spring).
  * **Redis** chiamate effettuate tramite hello Jedis client. Se chiamata hello richiede più tempo 10s, agente hello recupera anche gli argomenti di chiamata hello.
  * **[Chiamate JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**: MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB o Apache Derby DB. Sono supportate le chiamate "executeBatch". Per MySQL e PostgreSQL, se chiamata hello richiede più tempo 10s, hello agente riporta il piano di query hello.
* **Eccezioni rilevate:** dati sulle eccezioni gestite dal codice.
* **Metodo tempo di esecuzione:** dati relativi a hello ora accetta tooexecute specifici metodi.

agente APM Java hello toouse, si installarlo nel server. Le app web devono essere instrumentate con hello [Application Insights SDK per Java][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Installare l'agente di Application Insights hello per Java
1. Nel computer di hello esegue il server Java, [Scarica agente hello](https://aka.ms/aijavasdk).
2. Modifica di script di avvio server applicazione hello e aggiungere hello JVM seguente:
   
    `javaagent:`*file JAR agente toohello di percorso completo*
   
    Ad esempio, in Tomcat su un computer Linux:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Riavviare il server applicazioni.

## <a name="configure-hello-agent"></a>Configurare l'agente di hello
Creare un file denominato `AI-Agent.xml` e inserirle in hello stessa cartella del file JAR di hello agente.

Impostare hello il contenuto del file xml di hello. Modifica hello tooinclude riportato di seguito oppure omettere funzionalità hello desiderate.

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

È necessario tooenable report eccezione e la tempistica di metodo per i singoli metodi.

Per impostazione predefinita, `reportExecutionTime` è true e `reportCaughtExceptions` è false.

## <a name="view-hello-data"></a>Visualizzare i dati di hello
Nella risorsa di Application Insights hello, viene visualizzato l'aggregato remoto dipendenza e il metodo tempi di esecuzione [in hello prestazioni riquadro][metrics].

toosearch per singole istanze di relazioni di dipendenza, l'eccezione e il metodo, aprire [ricerca][diagnostic].

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
