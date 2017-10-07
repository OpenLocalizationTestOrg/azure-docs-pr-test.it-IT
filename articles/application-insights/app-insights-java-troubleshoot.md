---
title: aaaTroubleshoot Application Insights in un progetto web Java
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Risoluzione dei problemi e domande e risposte relative ad Application Insights per Java
Domande o problemi relativi ad [Azure Application Insights in Java][java]? Ecco alcuni suggerimenti.

## <a name="build-errors"></a>Errori di compilazione
**In Eclipse, durante l'aggiunta di hello Application Insights SDK tramite Maven o Gradle, ottenere gli errori di convalida di checksum o di compilazione.**

* Se hello dipendenza <version> elemento viene usato un modello con caratteri jolly (ad esempio (Maven) `<version>[1.0,)</version>` (Gradle) o `version:'1.0.+'`), provare a specificare invece una versione specifica come `1.0.2`. Vedere hello [note sulla versione](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) per la versione più recente di hello.

## <a name="no-data"></a>Dati non presenti
**È stato aggiunto correttamente Application Insights ed è stata eseguita l'applicazione, ma non ho potuto osservare i dati nel portale di hello.**

* Attendere un minuto, quindi fare clic su Aggiorna. grafici di Hello Aggiorna periodicamente se stessi, ma è anche possibile aggiornare manualmente. intervallo di aggiornamento Hello dipende dall'intervallo di tempo hello del grafico hello.
* Verificare di disporre di una chiave di strumentazione definita nel file ApplicationInsights.xml hello (nella cartella delle risorse hello del progetto)
* Verificare che sia presente alcun `<DisableTelemetry>true</DisableTelemetry>` nodo nel file xml di hello.
* Nel firewall, potrebbe essere tooopen le porte TCP 80 e 443 per toodc.services.visualstudio.com il traffico in uscita. Vedere hello [elenco completo delle eccezioni del firewall](app-insights-ip-addresses.md)
* In Microsoft Azure hello avviare discussioni ed esaminare mappa lo stato del servizio hello. Se sono presenti alcune indicazioni relative all'avviso, attendere hanno restituito tooOK e quindi chiudere e riaprire il pannello di applicazioni di Application Insights.
* Attivare la registrazione di finestra della console toohello IDE, aggiungendo un `<SDKLogger />` elemento sotto il nodo radice hello nel file ApplicationInsights.xml hello (nella cartella delle risorse hello del progetto) e cercare voci preceduti da [errore].
* Verificare che tale hello corretto ApplicationInsights.xml file è stato caricato correttamente da hello SDK per Java, esaminando i messaggi di output della console hello per un'istruzione "file di configurazione è stato trovato".
* Se non viene trovato il file di configurazione di hello, hello toosee di messaggi di output in cui viene cercato il file di configurazione di hello per verificare e assicurarsi che tale hello che applicationinsights.XML si trova in uno di questi percorsi di ricerca. Come regola generale, è possibile inserire il file di configurazione hello quasi file JAR di hello Application Insights SDK. Ad esempio: in Tomcat, ciò significa hello cartella WEB-INF/lib.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Utilizzato toosee dati, ma è stato arrestato
* Controllare hello [stato blog](http://blogs.msdn.com/b/applicationinsights-status/).
* È stata raggiunta la quota mensile relativa ai punti dati? Aprire impostazioni/quote e prezzi toofind out. Se la quota è stata raggiunta, è possibile aggiornare il piano oppure pagare per disporre di ulteriore capacità. Vedere hello [prezzi schema](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Non ho tutti i dati di hello che consapevole previsto
* Aprire hello quote e prezzi blade e controllare se [campionamento](app-insights-sampling.md) è in esecuzione. (trasmissione 100% significa che il campionamento non è nell'operazione). Hello servizio Application Insights può essere set tooaccept solo una frazione di telemetria hello in arrivo dall'app. Ciò permette di evitare il superamento della quota mensile. 

## <a name="no-usage-data"></a>Dati di utilizzo non presenti
**I dati relativi a richieste e tempi di risposta vengono visualizzati, ma non sono presenti dati relativi alla visualizzazione di pagine, ai browser o dati relativi agli utenti.**

I dati di telemetria toosend app è stato configurato dal server hello. Dopo il passaggio successivo è troppo[impostare dati di telemetria toosend pagine web da browser hello][usage].

In alternativa, se il client è un'app in un [telefono o altro dispositivo][platforms], è possibile inviare i dati di telemetria da tali dispositivi. 

Utilizzare hello stesso tooset chiave di strumentazione di telemetria del client e server. dati Hello verranno visualizzata nella stessa risorsa di Application Insights hello e sarà in grado di toocorrelate eventi dal client e server.


## <a name="disabling-telemetry"></a>Disabilitazione della telemetria
**In che modo è possibile disabilitare la raccolta di dati di telemetria?**

Nel codice:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Oppure** 

Aggiornare ApplicationInsights.xml (nella cartella delle risorse hello del progetto). Aggiungere il seguente hello nel nodo radice hello:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Metodo XML hello è un'applicazione hello toorestart quando si modifica il valore di hello.

## <a name="changing-hello-target"></a>Modifica della destinazione di hello
**In che modo è possibile modificare la risorsa di Azure che riceve i dati del progetto?**

* [Ottenere la chiave di strumentazione hello della nuova risorsa hello.][java]
* Se è stato aggiunto il progetto di tooyour Application Insights usando hello Azure Toolkit per Eclipse, fare clic con il pulsante destro del progetto web, selezionare **Azure**, **Configura Application Insights**e modificare la chiave hello.
* In caso contrario, aggiornare la chiave hello ApplicationInsights.xml nella cartella risorse hello nel progetto.

## <a name="debug-data-from-hello-sdk"></a>Debug dei dati da hello SDK

**Come è possibile scoprire quali hello esegue SDK?**

aggiungere ulteriori informazioni su cosa avviene nel hello API, tooget `<SDKLogger/>` sotto il nodo radice hello hello ApplicationInsights.xml del file di configurazione.

È anche possibile indicare file tooa toooutput del logger di hello:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

file Hello sono reperibile nella `%temp%\javasdklogs` o `java.io.tmpdir` in caso di server Tomcat.


## <a name="hello-azure-start-screen"></a>schermata di avvio Azure Hello
**Osservando [hello Azure portal](https://portal.azure.com). Mappa hello indica un elemento mia applicazione?**

No, Mostra stato hello del server Azure tutto il mondo hello.

*Dalla scheda Azure inizio hello (schermata iniziale), come è possibile individuare dati mia applicazione?*

Presupponendo che sia [impostare l'app per Application Insights][java], fare clic su Sfoglia, selezionare Application Insights e selezionare hello app risorsa creata per l'app. tooget non esiste più velocemente in futuro, è possibile aggiungere la scheda avvio toohello di app.

## <a name="intranet-servers"></a>Server Intranet
**È possibile monitorare un server nella Intranet?**

Sì, purché il server può inviare portale Application Insights toohello di telemetria tramite hello rete internet pubblica. 

Nel firewall, potrebbe essere tooopen le porte TCP 80 e 443 per toodc.services.visualstudio.com il traffico in uscita e f5.services.visualstudio.com.

## <a name="data-retention"></a>Conservazione dei dati
**Quanto tempo i dati verranno mantenuti nel portale di hello? Tale conservazione è sicura?**

Vedere [Conservazione dei dati e privacy][data].

## <a name="next-steps"></a>Passaggi successivi
**Application Insights è stato correttamente impostato per l'app server Java. Cos'altro è possibile fare?**

* [Monitorare la disponibilità delle pagine Web][availability]
* [Monitorare l'utilizzo delle pagine Web][usage]
* [Tenere traccia dell'utilizzo delle app per dispositivi e diagnosticarne i problemi][platforms]
* [Scrivere tootrack utilizzo del codice dell'app][track]
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

