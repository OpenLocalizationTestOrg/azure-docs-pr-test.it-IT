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
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights per le applicazioni web Java che sono già live


Se si dispone di un'applicazione web che è già in esecuzione sul server J2EE, è possibile avviare il monitoraggio con [Application Insights](app-insights-overview.md) senza hello necessario toomake alle modifiche al codice o ricompilare il progetto. Con questa opzione, sono disponibili informazioni sulle richieste HTTP inviate tooyour server, le eccezioni non gestite e i contatori delle prestazioni.

È necessario un abbonamento troppo[Microsoft Azure](https://azure.com).

> [!NOTE]
> procedura di Hello in questa pagina consente di aggiungere hello SDK tooyour web app in fase di esecuzione. La strumentazione di runtime è utile se si non desidera tooupdate o si ricompila il codice sorgente. Ma è possibile, è consigliabile [aggiungere codice sorgente di hello SDK toohello](app-insights-java-get-started.md) invece. Che offre più opzioni, ad esempio la scrittura di attività utente tootrack di codice.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Ottenere una chiave di strumentazione di Application Insights
1. Accedi toohello [portale Microsoft Azure](https://portal.azure.com)
2. Creare una nuova risorsa di Application Insights e impostare hello tipo tooJava applicazione web.
   
    ![Inserire un nome, scegliere l'app Web Java e fare clic su Crea](./media/app-insights-java-live/02-create.png)

    risorsa Hello viene creato in pochi secondi.

4. Aprire una nuova risorsa hello e ottenere la chiave di strumentazione. È necessario toopaste questa chiave nel progetto di codice a breve.
   
    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Scaricare il SDK di hello
1. Scaricare hello [Application Insights SDK per Java](https://aka.ms/aijavasdk). 
2. Nel server, estrarre directory toohello contenuto SDK hello da cui vengono caricati i file binari del progetto. Se si usa Tomcat, la directory si trova in genere in`webapps/<your_app_name>/WEB-INF/lib`

Si noti che è necessario toorepeat questo per ogni istanza del server e, per ogni app.

## <a name="3-add-an-application-insights-xml-file"></a>3. Aggiungere un file XML di Application Insights
Creare ApplicationInsights.xml nella cartella hello in cui è stato aggiunto hello SDK. Inserirvi hello seguenti XML.

Sostituire con chiave di strumentazione hello recuperato dal portale di Azure hello.

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

* chiave di strumentazione Hello viene inviata insieme a tutti gli elementi di dati di telemetria e indica toodisplay Application Insights nella risorsa.
* componente di richiesta HTTP Hello è facoltativo. Invia automaticamente i dati di telemetria sulle richieste e portale toohello tempi di risposta.
* Correlazione di eventi è un componente di richiesta di aggiunta toohello HTTP. Assegna una richiesta di tooeach identificatore ricevuta dal server hello e aggiunge questo identificatore come un elemento di dati di telemetria tooevery delle proprietà come proprietà hello 'Operation.Id'. Consente di telemetria hello toocorrelate associata a ogni richiesta impostando un filtro [ricerca diagnostica](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Aggiungere un filtro HTTP
Individuare e aprire i file Web. XML hello nel progetto e hello merge seguente frammento di codice nel nodo di app web hello, dove sono stati configurati i filtri di applicazione.

risultati più accurati tooget hello, filtro hello devono essere mappati prima tutti gli altri filtri.

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

## <a name="5-check-firewall-exceptions"></a>5. Verificare le eccezioni del firewall
Potrebbe essere troppo[set di dati in uscita toosend eccezioni](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Riavviare la propria app web.
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Visualizzare i dati di telemetria in Application Insights
Restituzione della risorsa di Application Insights tooyour in [portale Microsoft Azure](https://portal.azure.com).

Dati di telemetria sulle richieste HTTP viene visualizzata nel pannello della panoramica hello. Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.

![dati di esempio](./media/app-insights-java-live/5-results.png)

Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate. 

![](./media/app-insights-java-live/6-barchart.png)

E, quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.

![](./media/app-insights-java-live/7-instance.png)

[Altre informazioni sulle metriche.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere le pagine web di telemetria tooyour](app-insights-javascript.md) toomonitor pagina viste e le metriche di utente.
* [Configurare i test web](app-insights-monitor-web-app-availability.md) toomake che l'applicazione rimane in tempo reale e reattiva.
* [Acquisire le tracce dei log](app-insights-java-trace-logs.md)
* [Ricerca di eventi e log](app-insights-diagnostic-search.md) toohelp diagnosticare i problemi.

