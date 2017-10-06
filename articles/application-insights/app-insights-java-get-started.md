---
title: analitica di app web aaaJava con Azure Application Insights | Documenti Microsoft
description: 'Application Performance Monitoring per app Web Java con Application Insights. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Introduzione ad Application Insights in un progetto Web Java


[Application Insights](https://azure.microsoft.com/services/application-insights/) è un servizio estendibile analitica per gli sviluppatori web che consentono di comprendano le prestazioni di hello e l'utilizzo dell'applicazione in tempo reale. Utilizzarlo troppo[rilevare e diagnosticare i problemi di prestazioni ed eccezioni](app-insights-detect-triage-diagnose.md), e [scrivere codice] [ api] tootrack degli utenti a cui eseguire l'app.

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

Application Insights supporta le app Java in esecuzione in Linux, Unix o Windows.

Sono necessari:

* Oracle JRE 1.6 o versione successiva o isiZulu JRE 1.6 o versione successiva
* Una sottoscrizione troppo[Microsoft Azure](https://azure.microsoft.com/).

*Se si dispone di un'app web che è già in tempo reale, si può seguire la procedura alternativa hello troppo[aggiungere hello SDK in fase di esecuzione nel server web hello](app-insights-java-live.md). Tale alternativa consente di evitare la ricompilazione di codice hello, ma non si ottiene l'attività dell'utente tootrack toowrite codice hello opzione.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Ottenere una chiave di strumentazione di Application Insights
1. Accedi toohello [portale Microsoft Azure](https://portal.azure.com).
2. Creare una risorsa di Application Insights. Impostare hello tipo tooJava applicazione web.

    ![Inserire un nome, scegliere l'app Web Java e fare clic su Crea](./media/app-insights-java-get-started/02-create.png)
3. Trovare la chiave di strumentazione hello della nuova risorsa hello. È necessario toopaste questa chiave nel progetto di codice a breve.

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Aggiungere hello Application Insights SDK per il progetto tooyour Java
*Scegliere hello modalità appropriata per il progetto.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Se si usa Eclipse toocreate un progetto Web dinamico o Maven...
Hello utilizzare [Application Insights SDK per Java plug-in][eclipse].

#### <a name="if-youre-using-maven"></a>Se si usa Maven...
Se il progetto è già impostato toouse Maven per la compilazione, di tipo merge seguenti codice tooyour pom.xml file hello.

Quindi, file binari di hello tooget dipendenze progetto hello aggiornamento scaricato.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *Errori di convalida checksum o compilazione?* Provare a usare una versione specifica, ad esempio `<version>1.0.n</version>`. È disponibile la versione più recente di hello in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) o nel nostro [elementi Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Necessario tooupdate tooa nuovo SDK?* Aggiornare le dipendenze del progetto.

#### <a name="if-youre-using-gradle"></a>Se si usa Gradle...
Se il progetto è già impostato toouse Gradle per la compilazione, unire hello seguenti file di codice tooyour gradle.

File binari di hello tooget dipendenze progetto hello aggiornamento scaricati.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Errori di convalida checksum o compilazione? Provare a usare una versione specifica, come* `version:'1.0.n'`. *È disponibile la versione più recente di hello in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa nuovo SDK*
  * Aggiornare le dipendenze del progetto.

#### <a name="otherwise-"></a>In caso contrario...
Aggiungere manualmente hello SDK:

1. Scaricare hello [Application Insights SDK per Java](https://aka.ms/aijavasdk).
2. Estrarre i file binari hello da file zip hello e aggiungerli tooyour progetto.

### <a name="questions"></a>Domande...
* *Qual è la relazione hello tra hello `-core` e `-web` componenti ZIP hello?*

  * `applicationinsights-core`consente che Hello bare API. Questo componente sarà sempre necessario.
  * `applicationinsights-web` fornisce le metriche che consentono di tenere traccia del numero e dei tempi di risposta delle richieste HTTP. Questo componente può essere omesso se non si vuole che questi dati di telemetria vengano raccolti automaticamente. Ad esempio, se si desidera toowrite personalizzati.
* *hello tooupdate SDK di quando si pubblicano le modifiche*

  * Download più recenti hello [Application Insights SDK per Java](https://aka.ms/qqkaq6) e sostituire hello quelle meno recenti.
  * Le modifiche sono descritte in hello [note sulla versione di SDK](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Aggiungere un file XML di Application Insights
Aggiungere una cartella di risorse toohello ApplicationInsights.xml nel progetto o assicurarsi che viene aggiunto un percorso di classe di distribuzione del progetto tooyour. Copiare hello seguente XML al suo interno.

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
* Correlazione di eventi è un componente di richiesta di aggiunta toohello HTTP. Assegna una richiesta di tooeach identificatore ricevuta dal server hello e aggiunge questo identificatore come un elemento di dati di telemetria tooevery delle proprietà come proprietà hello 'Operation.Id'. Consente di telemetria hello toocorrelate associata a ogni richiesta impostando un filtro [ricerca diagnostica][diagnostic].
* chiave di Application Insights Hello può essere passato in modo dinamico da hello portale di Azure come una proprietà di sistema (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Se non è presente una proprietà definita, viene verificata la presenza della variabile di ambiente (APPLICATION_INSIGHTS_IKEY) nelle impostazioni dell'app Azure. Se entrambe le proprietà hello sono definite, viene usato il predefinito di hello manualmente InstrumentationKey da ApplicationInsights.xml. Questa sequenza consente di toomanage InstrumentationKeys diversi per diversi ambienti in modo dinamico.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Chiave di strumentazione di metodi alternativi tooset hello
Application Insights SDK cerca i chiave hello in questo ordine:

1. Proprietà di sistema: -DAPPLICATION_INSIGHTS_IKEY=ikey
2. Variabile di ambiente: APPLICATION_INSIGHTS_IKEY
3. File di configurazione: ApplicationInsights.xml

È anche possibile eseguirne l' [impostazione nel codice](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Aggiungere un filtro HTTP
ultimo passaggio di configurazione Hello consente hello HTTP richiesta componente toolog ogni richiesta web. (Non obbligatorio se si desidera hello bare API).

Individuare e aprire i file Web. XML hello nel progetto e hello merge seguente codice nel nodo di app web hello, dove sono stati configurati i filtri di applicazione.

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Se si usa Spring Web MVC 3.1 o versione successiva
Modificare questi elementi in *-pacchetto di Application Insights servlet.xml tooinclude hello:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Se si usa Struts 2
Aggiungere questo file di configurazione di elementi toohello strutture (in genere denominata struts.xml o strutture default.xml):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Se si dispone di intercettori definiti in uno stack predefinita, l'intercettore hello semplicemente aggiungere stack toothat.)

## <a name="5-run-your-application"></a>5. Eseguire l'applicazione
Eseguirlo in modalità di debug nel computer di sviluppo oppure tooyour server di pubblicazione.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Visualizzare i dati di telemetria in Application Insights
Restituzione della risorsa di Application Insights tooyour in [portale Microsoft Azure](https://portal.azure.com).

Dati di richieste HTTP vengono visualizzati nel pannello della panoramica hello. Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.

![dati di esempio](./media/app-insights-java-get-started/5-results.png)

[Altre informazioni sulle metriche.][metrics]

Click-through toosee qualsiasi grafico più dettagliate aggregate le metriche.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights si presuppone il formato di hello di richieste HTTP per le applicazioni MVC: `VERB controller/action`. Ad esempio, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` e `GET Home/Product/sdf96vws` vengono raggruppati in `GET Home/Product`. Questo raggruppamento consente aggregazioni significative delle richieste, come il numero di richieste e il tempo medio di esecuzione per le richieste.
>
>

### <a name="instance-data"></a>Dati dell'istanza
Fare clic su tramite una richiesta specifica digitare toosee singole istanze.

In Application Insights vengono visualizzati due tipi di dati, ovvero i dati aggregati, archiviati e visualizzati come medie, conteggi e somme, e i dati di istanza, ovvero singoli report di richieste HTTP, eccezioni, visualizzazioni di pagina o eventi personalizzati.

Quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analytics: linguaggio di query avanzato
Come si accumulano più dati, è possibile eseguire query entrambi tooaggregate dati e toofind le singole istanze.  [Analisi](app-insights-analytics.md) è uno strumento avanzato per ottenere informazioni sulle prestazioni e sull'utilizzo e ai fini della diagnostica.

![Esempio di Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Installare l'applicazione nel server hello
Pubblicare il server toohello app, consentire alle persone che usano e guardare telemetria hello visualizzati nel portale di hello.

* Verificare che il firewall consenta le porte di telemetria toothese toosend l'applicazione:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Se il traffico in uscita deve essere instradato attraverso un firewall, definire le proprietà di sistema `http.proxyHost` e `http.proxyPort`.

* Nei server Windows installare:

  * [Microsoft Visual C++ Redistributable Package](http://www.microsoft.com/download/details.aspx?id=40784)

    Questo componente abilita i contatori delle prestazioni.


## <a name="exceptions-and-request-failures"></a>Eccezioni e richieste non eseguite
Vengono raccolte automaticamente le eccezioni non gestite:

![Aprire Impostazioni e quindi Errori](./media/app-insights-java-get-started/21-exceptions.png)

dati toocollect su altre eccezioni, sono disponibili due opzioni:

* [Inserire le chiamate nel codice tootrackException()][apiexceptions].
* [Installare hello Java agente nel server](app-insights-java-agent.md). Specificare i metodi di hello da toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorare le chiamate al metodo e le dipendenze esterne
[Installare l'agente APM Java hello](app-insights-java-agent.md) toolog specificato metodi interni e le chiamate effettuate tramite JDBC, con dati di intervallo.

## <a name="performance-counters"></a>Contatori delle prestazioni
Aprire **impostazioni**, **server**, toosee un intervallo di contatori delle prestazioni.

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Personalizzare la raccolta del contatore delle prestazioni
toodisable raccolta di set di contatori delle prestazioni, standard di hello aggiungere hello seguente codice sotto il nodo radice hello del file ApplicationInsights.xml hello:

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Raccogliere dei contatori di prestazioni aggiuntive
È possibile specificare toobe i contatori delle prestazioni raccolti.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Contatori JMX (esposti da hello Java Virtual Machine)

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– nome hello visualizzato nel portale Application Insights hello.
* `objectName`– nome dell'oggetto JMX hello.
* `attribute`: attributo hello di hello JMX oggetto nome toofetch
* `type`(facoltativo): tipo di attributo dell'oggetto JMX hello:
  * Impostazione predefinita: un tipo semplice come int o long.
  * `composite`: i dati dei contatori delle prestazioni hello sono nel formato 'Attribute.Data' hello
  * `tabular`: i dati dei contatori delle prestazioni hello sono nel formato hello di una riga di tabella

#### <a name="windows-performance-counters"></a>Contatori delle prestazioni di Windows
Ogni [contatore delle prestazioni Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) è un membro di una categoria (in hello allo stesso modo che un campo è un membro di una classe). Le categorie possono essere globali o possono disporre di istanze numerate o denominate.

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName: nome hello visualizzato nel portale Application Insights hello.
* categoryName: hello categoria contatori delle prestazioni (oggetto prestazioni) a cui è associato questo contatore delle prestazioni.
* counterName – nome hello hello del contatore delle prestazioni.
* instanceName-nome hello dell'istanza di categoria del contatore delle prestazioni hello o una stringa vuota (""), se la categoria hello contiene una sola istanza. Se categoryName hello è processo e si desidera toocollect contatore delle prestazioni hello è dal processo JVM corrente hello in cui è in esecuzione l'app, specificare `"__SELF__"`.

I contatori delle prestazioni sono visibili come metriche personalizzate in [Esplora metriche][metrics].

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contatori delle prestazioni Unix
* [Installare collectd con plug-in Application Insights hello](app-insights-java-collectd.md) tooget un'ampia gamma di dati di sistema e di rete.

## <a name="get-user-and-session-data"></a>Ottenere i dati relativi a utenti e sessioni
I dati di telemetria vengono normalmente inviati dal server Web. Ora tooget hello 360 gradi di visualizzazione dell'applicazione, è possibile aggiungere più monitoraggio:

* [Aggiungere le pagine web di telemetria tooyour] [ usage] toomonitor pagina viste e le metriche di utente.
* [Configurare i test web] [ availability] toomake che l'applicazione rimane in tempo reale e reattiva.

## <a name="capture-log-traces"></a>Acquisire le tracce dei log
È possibile utilizzare Application Insights tooslice e ripartiscono registri Log4J o Logback altri framework di registrazione. È possibile correlare i registri di hello con richieste HTTP e altri dati di telemetria. [Informazioni][javalogs].

## <a name="send-your-own-telemetry"></a>Inviare i propri dati di telemetria
Ora che è stato installato hello SDK, è possibile utilizzare hello API toosend propri dati di telemetria.

* [Tenere traccia di eventi personalizzati e le metriche] [ api] toolearn gli utenti che eseguono l'applicazione.
* [Ricerca di eventi e log] [ diagnostic] toohelp diagnosticare i problemi.

## <a name="availability-web-tests"></a>Test Web di disponibilità
Application Insights è possibile testare il sito Web all'indirizzo toocheck a intervalli regolari che è attivo e risponde correttamente. [tooset backup][availability], fare clic su test Web.

![Fare clic su Test Web e quindi su Aggiungi test Web](./media/app-insights-java-get-started/31-config-web-test.png)

Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.

![Esempio di test Web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Altre informazioni sui test Web di disponibilità.][availability]

## <a name="questions-problems"></a>Domande? Problemi?
[Risoluzione dei problemi Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi
* [Monitorare chiamate alle dipendenze](app-insights-java-agent.md)
* [Monitorare contatori delle prestazioni Unix](app-insights-java-collectd.md)
* Aggiungere [monitoraggio le pagine web tooyour](app-insights-javascript.md) tempi di caricamento pagina toomonitor, le chiamate AJAX, le eccezioni del browser.
* Scrivere [telemetria personalizzata](app-insights-api-custom-events-metrics.md) tootrack utilizzo in hello browser o nel server di hello.
* Creare [dashboard](app-insights-dashboards.md) toobring grafici con chiave hello insieme per il monitoraggio del sistema.
* Usare [Analytics](app-insights-analytics.md) per eseguire query avanzate sui dati di telemetria dall'app
* Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
