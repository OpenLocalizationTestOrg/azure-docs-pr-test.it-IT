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
# <a name="explore-java-trace-logs-in-application-insights"></a>Esplorare i log di traccia Java in Application Insights
Se si usa Log4J o Logback (versione 1.2 o 2.0) per la traccia, è possibile utilizzare i log di traccia inviati automaticamente tooApplication informazioni dettagliate in cui è possibile esplorare e ricerche.

## <a name="install-hello-java-sdk"></a>Installare hello SDK per Java

Installare [Application Insights SDK per Java][java], se questa operazione non è già stata eseguita.

(Se non si desidera che le richieste di tootrack HTTP, è possibile omettere la maggior parte dei file di configurazione XML hello, ma è necessario includere almeno hello `InstrumentationKey` elemento. È inoltre necessario chiamare `new TelemetryClient()` tooinitialize hello SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Aggiungere la registrazione delle librerie tooyour progetto
*Scegliere hello modalità appropriata per il progetto.*

#### <a name="if-youre-using-maven"></a>Se si usa Maven...
Se il progetto è già impostato toouse Maven per la compilazione, di tipo merge uno dei seguenti frammenti di codice nel file pom.xml hello.

Aggiornare quindi dipendenze progetto hello, i file binari hello tooget scaricati.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Se si usa Gradle...
Se il progetto è già impostato toouse Gradle per la compilazione, aggiungere uno dei seguenti righe toohello hello `dependencies` gruppo nel file gradle:

Aggiornare quindi dipendenze progetto hello, i file binari hello tooget scaricati.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>In caso contrario...
Scaricare ed estrarre appender di hello appropriato, quindi aggiungere hello libreria appropriata tooyour progetto:

| Logger | Scaricare | Libreria |
| --- | --- | --- |
| Logback |[SDK con appender Logback](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[SDK con appender Log4J v2](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[SDK con appender Log4J v1.2](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Aggiungere il framework di registrazione tooyour appender hello
toostart recupero tracce, importante frammento hello merge del codice toohello Log4J o Logback file di configurazione: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

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

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

appenders Application Insights Hello può fare riferimento da qualsiasi logger configurato e non necessariamente logger radice hello (come illustrato negli esempi di codice hello sopra).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Esplorare le tracce nel portale Application Insights hello
Ora che è stato configurato il progetto toosend tracce tooApplication Insights, è possibile visualizzare e cercare le tracce nel hello del portale Application Insights hello [ricerca] [ diagnostic] blade.

![Nel portale Application Insights hello, aprire una ricerca](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Passaggi successivi
[Ricerca diagnostica][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


