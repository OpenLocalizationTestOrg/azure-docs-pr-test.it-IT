---
title: aaaGet avviato con Application Insights di Azure con Java in Eclipse | Documenti Microsoft
description: Utilizzare hello prestazioni tooadd plug-in Eclipse e utilizzo di monitoraggio del sito Web Java tooyour con Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Introduzione ad Application Insights con Java in Eclipse
Hello Application Insights SDK invia dati di telemetria dall'applicazione web Java, in modo che è possibile analizzare l'utilizzo e le prestazioni. plug-in per Application Insights Eclipse Hello installa automaticamente hello SDK nel progetto in modo che perdano la telemetria casella hello, oltre a un'API che è possibile utilizzare i dati di telemetria personalizzati toowrite.   

## <a name="prerequisites"></a>Prerequisiti
Attualmente hello plug-in funziona per i progetti Maven e i progetti Web dinamica in Eclipse.
([Progetto Java tipi tooother Aggiungi Application Insights][java].)

Sono necessari gli elementi seguenti:

* Oracle JRE 1.6 o versione successiva
* Una sottoscrizione troppo[Microsoft Azure](https://azure.microsoft.com/).
* [Eclipse IDE per sviluppatori Java EE](http://www.eclipse.org/downloads/), Indigo o versioni successive.
* Windows 7 o versioni successive o Windows Server 2008 o versioni successive

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Installare SDK hello in Eclipse (una volta)
È sufficiente toodo questo una volta per ogni computer. Questo passaggio vengono installati un toolkit che può quindi aggiungere hello SDK tooeach progetto Web dinamico.

1. Dal menu Help di Eclipse scegliere Install New Software.

    ![Guida in linea, Installa nuovo Software](./media/app-insights-java-eclipse/0-plugin.png)
2. Hello SDK è http://dl.microsoft.com/eclipse, in Azure Toolkit.
3. Deselezionare l'opzione **Contatta tutti i siti di aggiornamento...**

    ![Per Application Insights SDK deselezionare tutti i siti di aggiornamento Contatta tutti](./media/app-insights-java-eclipse/1-plugin.png)

Seguire i rimanenti passaggi per ogni progetto Java hello.

## <a name="create-an-application-insights-resource-in-azure"></a>Creare una risorsa di Application Insights in Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Creare una nuova risorsa di Application Insights. Impostare hello tipo tooJava applicazione web.  

    ![Fare clic su + e scegliere Application Insights](./media/app-insights-java-eclipse/01-create.png)  

4. Trovare la chiave di strumentazione hello della nuova risorsa hello. È necessario toopaste nel progetto di codice a breve.  

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Aggiungere il progetto tooyour Application Insights
1. Aggiungi Application Insights dal menu di scelta rapida hello del progetto web Java.

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/02-context-menu.png)
2. Incollare una chiave di strumentazione hello recuperato dal portale di Azure hello.

    ![Nella panoramica delle risorse hello nuovo, fare clic su proprietà e copiare hello chiave di strumentazione](./media/app-insights-java-eclipse/03-ikey.png)

chiave Hello viene inviata insieme a tutti gli elementi di dati di telemetria e indica toodisplay Application Insights nella risorsa.

## <a name="run-hello-application-and-see-metrics"></a>Eseguire un'applicazione hello e visualizzare le metriche
Eseguire l'applicazione.

Restituisce la risorsa di Application Insights tooyour in Microsoft Azure.

Dati di richieste HTTP verranno visualizzati nel pannello della panoramica hello. Se non sono visualizzati, attendere alcuni secondi e quindi fare clic su Aggiorna.

![Risposta del server, conteggi delle richieste ed errori ](./media/app-insights-java-eclipse/5-results.png)

Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate.

![Numero di richieste per nome](./media/app-insights-java-eclipse/6-barchart.png)

[Altre informazioni sulle metriche.][metrics]

E, quando si visualizzano le proprietà di hello di una richiesta, è possibile visualizzare gli eventi di telemetria hello associati, ad esempio le richieste e le eccezioni.

![Tutte le tracce per questa richiesta](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Telemetria sul lato client
Pannello avvio rapido di hello, fare clic su Get codice toomonitor le pagine web:

![Nel pannello della panoramica app, scegliere l'avvio rapido, ottenere codice toomonitor le pagine web. Copiare lo script hello.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Inserire il frammento di codice hello in head hello dei file HTML.

#### <a name="view-client-side-data"></a>Visualizzare i dati lato client
Aprire le pagine Web aggiornate e usarle. Attendere qualche minuto, quindi tornare tooApplication approfondimenti e blade utilizzo hello aperto. (Dal pannello della panoramica hello, scorrere verso il basso e fare clic su utilizzo)

Le metriche di visualizzazione, utente e della sessione di pagina verranno visualizzate nel Pannello di utilizzo di hello:

![Sessioni, utenti e visualizzazioni pagina](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Altre informazioni sulla configurazione della telemetria sul lato client.][usage]

## <a name="publish-your-application"></a>Pubblicare l'applicazione
Pubblicare il server toohello app, consentire alle persone che usano e guardare telemetria hello visualizzati nel portale di hello.

* Verificare che il firewall consenta le porte di telemetria toothese toosend l'applicazione:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Nei server Windows installare:

  * [Microsoft Visual C++ Redistributable Package](http://www.microsoft.com/download/details.aspx?id=40784)

    (Ciò abilita i contatori delle prestazioni).

## <a name="exceptions-and-request-failures"></a>Eccezioni e richieste non eseguite
Vengono raccolte automaticamente le eccezioni non gestite:

![](./media/app-insights-java-eclipse/21-exceptions.png)

dati toocollect su altre eccezioni, sono disponibili due opzioni:

* [Inserire le chiamate nel codice tooTrackException](app-insights-api-custom-events-metrics.md#trackexception).
* [Installare hello Java agente nel server](app-insights-java-agent.md). Specificare i metodi di hello da toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Monitorare le chiamate al metodo e le dipendenze esterne
[Installare l'agente APM Java hello](app-insights-java-agent.md) toolog specificato metodi interni e le chiamate effettuate tramite JDBC, con dati di intervallo.

## <a name="performance-counters"></a>Contatori delle prestazioni
Nel pannello della panoramica, scorrere verso il basso e fare clic su hello **server** riquadro. Verrà visualizzato un intervallo di contatori delle prestazioni.

![Scorrere verso il basso riquadro server di hello tooclick](./media/app-insights-java-eclipse/11-perf-counters.png)

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

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Contatori delle prestazioni Unix
* [Installare collectd con plug-in Application Insights hello](app-insights-java-collectd.md) tooget un'ampia gamma di dati di sistema e di rete.

## <a name="availability-web-tests"></a>Test Web di disponibilità
Application Insights è possibile testare il sito Web all'indirizzo toocheck a intervalli regolari che è attivo e risponde correttamente. [tooset backup][availability], scorrere verso il basso tooclick disponibilità.

![Scorrere verso il basso, fare clic su Disponibilità, quindi su Aggiungi test Web](./media/app-insights-java-eclipse/31-config-web-test.png)

Se il sito è inattivo, si otterranno grafici dei tempi di risposta, nonché notifiche di posta elettronica.

![Esempio di test Web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Altre informazioni sui test Web di disponibilità.][availability]

## <a name="diagnostic-logs"></a>Log di diagnostica
Se si usa Log4J o Logback (versione 1.2 o 2.0) per la traccia, è possibile utilizzare i log di traccia inviati automaticamente tooApplication informazioni dettagliate in cui è possibile esplorare e ricerche.

[Altre informazioni sui log di diagnostica][javalogs]

## <a name="custom-telemetry"></a>Telemetria personalizzata
Inserire alcune righe di codice nel toofind di applicazione web Java le operazioni con gli utenti o toohelp diagnosticare i problemi.

Nella pagina web JavaScript e Java di hello sul lato server, è possibile inserire codice.

[Informazioni sulla telemetria personalizzata][track]

## <a name="next-steps"></a>Passaggi successivi
#### <a name="detect-and-diagnose-issues"></a>Rilevare e diagnosticare i problemi
* [Aggiungi telemetria di client web] [ usage] telemetria relativi alle prestazioni tooget dal client web hello.
* [Configurare i test web] [ availability] toomake che l'applicazione rimane in tempo reale e reattiva.
* [Ricerca di eventi e log] [ diagnostic] toohelp diagnosticare i problemi.
* [Acquisire le tracce di Log4J o Logback][javalogs]

#### <a name="track-usage"></a>Tenere traccia dell'utilizzo
* [Aggiungi telemetria di client web] [ usage] toomonitor pagina viste e le metriche di utente di base.
* [Tenere traccia di eventi personalizzati e le metriche](app-insights-web-track-usage.md) toolearn sulle modalità di utilizzo dell'applicazione, sia nel client hello e nel server di hello.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
