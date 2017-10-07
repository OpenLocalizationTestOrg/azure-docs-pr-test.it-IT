---
title: prestazioni dell'applicazione web Java su Linux - Azure aaaMonitor | Documenti Microsoft
description: Estendere l'applicazione monitoraggio delle prestazioni del sito Web Java con hello CollectD plug-in per Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: metriche delle prestazioni Linux in Application Insights


tooexplore le metriche delle prestazioni di sistema di Linux in [Application Insights](app-insights-overview.md), installare [collectd](http://collectd.org/), insieme con il plug-in Application Insights. Questa soluzione open source raccoglie diverse che relative al sistema e alla rete.

In genere, si usa collectd se è già stato [instrumentato il servizio Web Java con Application Insights][java]. Consente di definire ulteriori dati toohelp si tooenhance le prestazioni dell'app o diagnosticare problemi. 

![Grafici di esempio](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>Ottenere la chiave di strumentazione
In hello [portale Microsoft Azure](https://portal.azure.com)aprire hello [Application Insights](app-insights-overview.md) risorsa in cui si desidera tooappear dati hello. In alternativa, [creare una nuova risorsa](app-insights-create-new-resource.md).

Eseguire una copia della chiave di strumentazione hello, che identifica una risorsa hello.

![Sfoglia tutto, aprire la risorsa e quindi nell'elenco a discesa Essentials hello, selezionare e copiare hello chiave di strumentazione](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Installare collectd e hello plug-in
Nei computer server Linux:

1. Installare [collectd](http://collectd.org/) versione 5.4.0 o successive.
2. Scaricare hello [plug-in Application Insights collectd writer](https://aka.ms/aijavasdk). Si noti il numero di versione di hello.
3. Copiare i plug-in di hello JAR in `/usr/share/collectd/java`.
4. Modificare `/etc/collectd/collectd.conf`:
   * Verificare che [hello plug-in Java](https://collectd.org/wiki/index.php/Plugin:Java) è abilitata.
   * Aggiornare hello JVMArg per hello di tooinclude java.class.path hello JAR seguenti. Aggiornare hello versione numero toomatch hello che uno è stato scaricato:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * Aggiungere questo frammento di codice, con chiave di strumentazione di hello dalla risorsa:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Di seguito è riportata una parte di un file di configurazione di esempio:

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Configurare altri [plug-in collectd](https://collectd.org/wiki/index.php/Table_of_Plugins), che possono raccogliere diversi dati da origini diverse.

Riavviare in base tooits collectd [manuale](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Visualizzare i dati di hello in Application Insights
Nella risorsa di Application Insights, aprire [Esplora metriche e aggiungere grafici][metrics], selezione metriche hello da toosee dalla categoria personalizzata hello.

![](./media/app-insights-java-collectd/result.png)

Per impostazione predefinita, le metriche hello vengono aggregate in tutti i computer host da cui sono state raccolte le metriche di hello. le metriche di hello tooview per ogni host, nel pannello dettagli grafico di hello, attivare il raggruppamento e quindi scegliere toogroup CollectD host.

## <a name="tooexclude-upload-of-specific-statistics"></a>caricamento di tooexclude di statistiche specifiche
Per impostazione predefinita, i plug-in Application Insights hello invia tutti i dati di hello raccolti da tutti hello abilitato collectd 'read' plug-in. 

tooexclude dati da origini dati o i plug-in specifici:

* Modificare il file di configurazione di hello. 
* In `<Plugin ApplicationInsightsWriter>`aggiungere righe di direttive analoghe alle seguenti:

| Direttiva | Effetto |
| --- | --- |
| `Exclude disk` |Escludere tutti i dati raccolti da hello `disk` plug-in |
| `Exclude disk:read,write` |Esclusione di origini di hello denominate `read` e `write` da hello `disk` plug-in. |

Separare le direttive con un valore NewLine.

## <a name="problems"></a>Problemi?
*Non è possibile visualizzare dati nel portale di hello*

* Aprire [ricerca] [ diagnostic] toosee se sono arrivato eventi non elaborati hello. In alcuni casi hanno più tooappear in Esplora metriche.
* Potrebbe essere troppo[impostare le eccezioni del firewall per i dati in uscita](app-insights-ip-addresses.md)
* Abilitare la traccia nel plug-in Application Insights hello. Aggiungere questa riga in `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Aprire un terminale e avviare collectd in modalità dettagliata, toosee eventuali problemi che sta inviando report:
  * `sudo collectd -f`

## <a name="known-issue"></a>Problema noto

Hello Application Insights scrivere plug-in non è compatibile con alcuni plug-in lettura. Alcuni plug-in di trasmissione talvolta "NaN" a cui i plug-in Application Insights hello prevede un numero a virgola mobile.

Sintomo: log collectd hello Mostra gli errori che includono "AI:... SyntaxError: N token non previsto".

Soluzione alternativa: Escludere i dati raccolti dai plug-in di hello problema scrittura. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


