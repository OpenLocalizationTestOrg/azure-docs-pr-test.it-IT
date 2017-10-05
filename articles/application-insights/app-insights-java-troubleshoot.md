---
title: Risoluzione dei problemi di Application Insights in un progetto Web Java
description: Guida per la risoluzione dei problemi - monitoraggio di app Java live con Application Insights.
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Risoluzione dei problemi e domande e risposte relative ad Application Insights per Java
Domande o problemi relativi ad [Azure Application Insights in Java][java]? Ecco alcuni suggerimenti.

## <a name="build-errors"></a>Errori di compilazione
**Quando si aggiunge Application Insights SDK in Eclipse tramite Maven o Gradle, vengono visualizzati errori di convalida relativi a compilazione o checksum.**

* Se l'elemento di dipendenza <version> usa un criterio di ricerca con caratteri jolly, ad esempio (Maven) `<version>[1.0,)</version>` o (Gradle) `version:'1.0.+'`, provare a indicare una versione specifica, come `1.0.2`. Vedere le [note sulla versione](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) per la versione più recente.

## <a name="no-data"></a>Dati non presenti
**Dopo avere aggiunto Application Insights correttamente ed avere eseguito l'app, nel portale non vengono visualizzati dati.**

* Attendere un minuto, quindi fare clic su Aggiorna. I grafici si aggiornano autonomamente periodicamente, ma è anche possibile aggiornare manualmente. L'intervallo di aggiornamento dipende dall'intervallo di tempo del grafico.
* Verificare di disporre di una chiave di strumentazione definita nel file ApplicationInsights.xml (presente nella cartella resources del progetto).
* Verificare che non vi siano nodi `<DisableTelemetry>true</DisableTelemetry>` nel file XML.
* Nel firewall, potrebbe essere necessario aprire le porte TCP 80 e 443 per il traffico in uscita verso dc.services.visualstudio.com. Vedere l' [elenco completo delle eccezioni del firewall](app-insights-ip-addresses.md)
* Nella schermata iniziale di Microsoft Azure osservare la mappa dello stato dei servizi. Se ci sono indicazioni di avviso, attendere che tornino alla normalità, quindi chiudere e riaprire il pannello dell'applicazione di Application Insights.
* Attivare la registrazione nella finestra della console IDE aggiungendo un elemento `<SDKLogger />` sotto il nodo radice nel file ApplicationInsights.xml (nella cartella resources del progetto) e verificare la presenza di voci con prefisso [Error].
* Per verificare che Java SDK abbia caricato il file ApplicationInsights.xml corretto, esaminare i messaggi di output della console e cercare il messaggio "Configuration file has been successfully found".
* Se il file di configurazione non è stato trovato, verificare i percorsi di ricerca di questo file nei messaggi di output e assicurarsi che il file ApplicationInsights.xml sia memorizzato in uno di tali percorsi. In linea di massima, il file di configurazione può essere salvato accanto ai file JAR di Application Insights SDK. In Tomcat, ad esempio, questo percorso corrisponde alla cartella WEB-INF/lib.

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>Non vengono più visualizzati i dati disponibili in precedenza
* Controllare il [blog sullo stato](http://blogs.msdn.com/b/applicationinsights-status/).
* È stata raggiunta la quota mensile relativa ai punti dati? Per saperlo, aprire Impostazioni/Quota e Prezzi. Se la quota è stata raggiunta, è possibile aggiornare il piano oppure pagare per disporre di ulteriore capacità. Vedere lo [schema dei prezzi](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-the-data-im-expecting"></a>Non sono presenti tutti i dati previsti
* Aprire il pannello Quota + prezzi e verificare se il [campionamento](app-insights-sampling.md) è abilitato. La trasmissione al 100% indica che il campionamento non è abilitato. È possibile impostare il servizio Application Insights in modo che vengano accettati soltanto i dati di telemetria provenienti dall'app. Ciò permette di evitare il superamento della quota mensile. 

## <a name="no-usage-data"></a>Dati di utilizzo non presenti
**I dati relativi a richieste e tempi di risposta vengono visualizzati, ma non sono presenti dati relativi alla visualizzazione di pagine, ai browser o dati relativi agli utenti.**

L'app è stata correttamente configurata per inviare dati di telemetria dal server. Il passaggio successivo consiste nel [configurare le pagine Web per inviare dati di telemetria dal Web browser][usage].

In alternativa, se il client è un'app in un [telefono o altro dispositivo][platforms], è possibile inviare i dati di telemetria da tali dispositivi. 

Usare la chiave di strumentazione per impostare la telemetria sia sul client che sul server. I dati verranno visualizzati nella stessa risorsa di Application Insights e sarà possibile correlare eventi dal client e dal server.


## <a name="disabling-telemetry"></a>Disabilitazione della telemetria
**In che modo è possibile disabilitare la raccolta di dati di telemetria?**

Nel codice:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Oppure** 

Aggiornare ApplicationInsights.xml (nella cartella resources del progetto). Aggiungere la riga seguente sotto il nodo radice:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Usando il metodo XML, dopo la modifica di questo valore sarà necessario riavviare l'applicazione.

## <a name="changing-the-target"></a>Modifica della destinazione
**In che modo è possibile modificare la risorsa di Azure che riceve i dati del progetto?**

* [Ottenere la chiave di strumentazione della nuova risorsa][java].
* Se si è aggiunto Application Insights al progetto usando Azure Toolkit for Eclipse, fare clic con il pulsante destro del mouse sul progetto Web, selezionare **Azure**, **Configura Application Insights**, quindi modificare la chiave.
* Oppure, aggiornare la chiave nel file ApplicationInsights.xml presente nella cartella resources del progetto.

## <a name="debug-data-from-the-sdk"></a>Debug dei dati dall'SDK

**Come ottenere informazioni sulle attività dell'SDK**

Per ottenere altre informazioni su quello che accade nell'API, aggiungere `<SDKLogger/>` sotto il nodo radice del file di configurazione ApplicationInsights.xml.

È anche possibile impostare il logger perché fornisca un file di output:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

I file si trovano in `%temp%\javasdklogs` o `java.io.tmpdir` nel caso di un server Tomcat.


## <a name="the-azure-start-screen"></a>Schermata iniziale di Azure
**Guardando nel [portale di Azure](https://portal.azure.com). la mappa contiene informazioni sull'app?**

No, la mappa visualizza lo stato di integrità dei server Azure nelle varie parti del mondo.

*Dalla schermata iniziale (home) di Azure, in che modo è possibile trovare i dati relativi all'app?*

Supponendo che [l'app sia stata impostata per Application Insights][java], fare clic su Esplora, selezionare Application Insights, quindi selezionare la risorsa dell'app creata per l'app specifica. Per raggiungere questa area più velocemente in futuro, è possibile aggiungere l'app alla schermata iniziale.

## <a name="intranet-servers"></a>Server Intranet
**È possibile monitorare un server nella Intranet?**

Sì, purché il server possa inviare dati di telemetria al portale di Application Insights tramite la rete Internet pubblica. 

Nel firewall, potrebbe essere necessario aprire le porte TCP 80 e 443 per il traffico in uscita verso dc.services.visualstudio.com e f5.services.visualstudio.com.

## <a name="data-retention"></a>Conservazione dei dati
**Per quanto tempo vengono conservati i dati nel portale? Tale conservazione è sicura?**

Vedere [Conservazione dei dati e privacy][data].

## <a name="next-steps"></a>Passaggi successivi
**Application Insights è stato correttamente impostato per l'app server Java. Cos'altro è possibile fare?**

* [Monitorare la disponibilità delle pagine Web][availability]
* [Monitorare l'utilizzo delle pagine Web][usage]
* [Tenere traccia dell'utilizzo delle app per dispositivi e diagnosticarne i problemi][platforms]
* [Scrivere codice per tenere traccia dell'utilizzo dell'app][track]
* [Acquisire i log di diagnostica][javalogs]

## <a name="get-help"></a>Ottenere aiuto
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

