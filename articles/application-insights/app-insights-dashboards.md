---
title: aaaDashboards e spostamento in hello Azure Application Insights | Documenti Microsoft
description: Creare visualizzazioni di query e grafici APM chiave.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Spostamento e i dashboard nel portale Application Insights hello
Dopo aver [configurare Application Insights al progetto](app-insights-overview.md), verranno visualizzati i dati di telemetria sull'utilizzo e delle prestazioni dell'app nella risorsa di Application Insights del progetto in hello [portale di Azure](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Trovare i dati di telemetria
Accedi toohello [portale di Azure](https://portal.azure.com) e passare a risorsa di Application Insights toohello creato per l'app.

![Fare clic su Sfoglia, selezionare Application Insights, quindi fare clic sull'app.](./media/app-insights-dashboards/00-start.png)

pannello della panoramica Hello (pagina) per l'app viene visualizzato un riepilogo delle metriche di diagnostica chiave hello dell'app ed è di altre funzionalità del portale hello toohello un gateway.

![I principali di dati di telemetria tooview route](./media/app-insights-dashboards/010-oview.png)

È possibile personalizzare le griglie e grafici hello e aggiungerli tooa dashboard. In questo modo, è possibile unire dati di telemetria chiave hello da diverse App in un dashboard centrale.

## <a name="dashboards"></a>Dashboard
Hello in primo luogo viene visualizzato dopo l'accesso toohello [portale Microsoft Azure](https://portal.azure.com) è un dashboard. Qui è possibile raggruppare i grafici di hello che sono più importanti tooyou tra tutte le risorse di Azure, inclusi i dati di telemetria da [Azure Application Insights](app-insights-overview.md).

![Un dashboard personalizzato.](./media/app-insights-dashboards/31.png)

1. **Passare alle risorse toospecific** , ad esempio l'app in Application Insights: barra sinistra hello di utilizzo.
2. **Dashboard corrente restituito toohello**, o cambiare vista recenti tooother: menu di scelta rapida utilizzare hello in alto a sinistra.
3. **Passare i dashboard**: menu di scelta rapida utilizzare hello nel titolo del dashboard hello
4. **Creare, modificare e condividere i dashboard** nella barra degli strumenti del dashboard hello.
5. **Modificare il dashboard di hello**: passare il mouse su un riquadro e quindi usare superiore barra toomove, personalizzare o rimuoverlo.

## <a name="add-tooa-dashboard"></a>Aggiungere dashboard tooa
Quando si cerca un pannello o un set di grafici che è particolarmente interessante, è possibile aggiungere una copia del dashboard toohello. Saranno visibili al successivo accesso.

![toopin un grafico, passare il mouse su di essa e quindi fare clic su "…" nell'intestazione di hello.](./media/app-insights-dashboards/33.png)

1. Aggiungi grafico toodashboard. Una copia di hello grafico viene visualizzato nel dashboard di hello.
2. PIN hello intero pannello toohello - visualizzato nel dashboard hello sotto forma di riquadro che è possibile fare clic.
3. Fare clic su dashboard corrente toohello di hello tooreturn nell'angolo superiore sinistro. È quindi possibile utilizzare visualizzazione corrente di hello dal menu a discesa tooreturn toohello.

Si noti che i grafici sono raggruppati in riquadri e che un riquadro può contenere più di un grafico. Si blocca hello intero riquadro toohello o un dashboard.

grafico Hello viene aggiornata automaticamente con una frequenza che dipende da intervallo di tempo del grafico hello:

* Intervallo di ore too1 di tempo: aggiornare ogni 5 minuti
* Intervallo di tempo da una a 24 ore: viene aggiornato ogni 15 minuti
* Intervallo di tempo superiore a 24 ore: (intervallo di tempo) / 60.

### <a name="pin-any-query-in-analytics"></a>Aggiungere query in Analisi
È anche possibile [aggiungere Analitica](app-insights-analytics-using.md#pin-to-dashboard) grafici tooa [condivisa](#share-dashboards-with-your-team) dashboard. In questo modo tooadd grafici delle query insieme a metriche standard hello arbitrario. 

I risultati vengono ricalcolati automaticamente ogni ora. Clic sull'icona di aggiornamento di hello in hello grafico toorecalculate immediatamente. (L'aggiornamento del browser non esegue il ricalcolo).

## <a name="adjust-a-tile-on-hello-dashboard"></a>Modificare un riquadro nel dashboard di hello
Una volta un riquadro nel dashboard di hello, è possibile modificare.

![Passare il mouse sopra un grafico in ordine tooedit.](./media/app-insights-dashboards/36.png)

1. Aggiungere un riquadro toohello grafico.
2. Impostare la metrica hello, group by dimensione e lo stile (tabella, grafico) di un grafico.
3. Trascina toozoom diagramma hello. Fare clic su hello annullamento pulsante tooreset hello timespan; impostare le proprietà di filtro per i grafici di hello sul riquadro hello.
4. Impostare il titolo del riquadro.

I riquadri aggiunti dai pannelli di Esplora metriche hanno più opzioni di modifica rispetto ai riquadri aggiunti da un pannello Panoramica.

riquadro Hello originale è stato aggiunto non è influenzato da tutte le modifiche.

## <a name="switch-between-dashboards"></a>Passare da un dashboard all'altro
È possibile salvare più dashboard e passare da un dashboard all'altro. Quando si aggiunge un grafico o un pannello, vengono aggiunte toohello dashboard corrente.

![tooswitch tra i dashboard, fare clic su Dashboard e selezionare un dashboard salvato. toocreate e salvare un nuovo dashboard, fare clic su nuovo. toorearrange, fare clic su Modifica.](./media/app-insights-dashboards/32.png)

Ad esempio, potrebbe essere un dashboard per la visualizzazione a schermo intero nella chat team hello e l'altra per lo sviluppo generale.

Nel dashboard di hello, viene visualizzato un pannello sotto forma di riquadro: selezionarlo toogo toohello blade. Un grafico consente di replicare il grafico hello nella posizione originale.

![Fare clic su un pannello di hello tooopen riquadro che rappresenta](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Condividere dashboard
Dopo aver creato un dashboard, è possibile condividerlo con altri utenti.

![Nell'intestazione di hello dashboard, fare clic su Condividi](./media/app-insights-dashboards/41.png)

Altre informazioni su [ruoli e controllo di accesso](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Esplorazione delle app
pannello della panoramica Hello è hello gateway toomore informazioni dell'app.

* **Qualsiasi riquadro o un grafico** : fare clic su qualsiasi riquadro o grafico toosee ulteriori dettagli sulla descrizione.

### <a name="overview-blade-buttons"></a>Pulsanti del pannello Panoramica
![Barra di spostamento superiore del pannello Panoramica](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Esplora metriche**](app-insights-metrics-explorer.md): consente di creare grafici su prestazioni e uso.
* [**Cerca**](app-insights-diagnostic-search.md): consente di analizzare istanze specifiche di eventi, ad esempio richieste, eccezioni o tracce di log.
* [**Analisi**](app-insights-analytics.md): consente di eseguire query avanzate con i dati di telemetria.
* **Intervallo di tempo** -modificare l'intervallo di hello visualizzato da tutti i grafici di hello nel pannello hello.
* **Eliminare** -eliminare la risorsa di Application Insights hello per questa applicazione. È necessario anche rimuovere pacchetti di Application Insights hello dal codice dell'app oppure modificare hello [chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key) nell'app toodirect telemetria tooa diversi risorsa di Application Insights.

### <a name="essentials-tab"></a>Scheda Informazioni di base
* [Chiave di strumentazione](app-insights-create-new-resource.md#copy-the-instrumentation-key): identifica la risorsa dell'app.
* Prezzi: rende disponibili le funzionalità e imposta i limiti per i volumi.

### <a name="app-navigation-bar"></a>Barra di spostamento delle app
![Barra di spostamento sinistra](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Panoramica** -pannello della panoramica app toohello restituito.
* **Log attività**: fornisce avvisi e informazioni su eventi amministrativi di Azure.
* [**Controllo di accesso** ](app-insights-resources-roles-access-control.md) -forniscono accesso a membri tooteam e altri.
* [**Tag** ](../azure-resource-manager/resource-group-using-tags.md) -utilizzare tag toogroup app con altri utenti.

RICERCA CAUSA

* [**Mappa delle applicazioni** ](app-insights-app-map.md) -Active mappa con i componenti di hello dell'applicazione, è derivato dalle informazioni di dipendenza hello.
* [**Rilevamento intelligente**](app-insights-proactive-diagnostics.md): consente di esaminare gli avvisi recenti sulle prestazioni.
* [**Flusso attivo**](app-insights-live-stream.md): un set fisso di metriche quasi istantanee, utile quando si distribuisce una nuova compilazione o si esegue il debug.
* [**Disponibilità / test Web** ](app-insights-monitor-web-app-availability.md) -invia richieste regolare tooyour app web da intorno mondo hello. *
* [**Gli errori, prestazioni** ](app-insights-web-monitor-performance.md) -eccezioni, guasti e una risposta volte per le richieste tooyour app e per le richieste dall'app troppo[dipendenze](app-insights-asp-net-dependencies.md).
* [**Performance**](app-insights-web-monitor-performance.md): tempo di risposta e tempi di risposta delle dipendenze.
* [Server](app-insights-web-monitor-performance.md) : contatori delle prestazioni. Disponibile se si [installa Status Monitor](app-insights-monitor-performance-live-website-now.md).
* **Browser** : prestazioni AJAX e di visualizzazione di pagine. Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).
* **Utilizzo** : numero di sessioni, utenti e visualizzazioni di pagine. Disponibile se si [instrumentano le pagine Web](app-insights-javascript.md).

CONFIGURA

* **Per iniziare** : esercitazione inline.
* **Proprietà** : chiave di strumentazione, sottoscrizione e ID risorsa.
* [Avvisi](app-insights-alerts.md) : configurazione degli avvisi sulle metriche.
* [L'esportazione continua](app-insights-export-telemetry.md) -configurare l'esportazione di archiviazione di dati di telemetria tooAzure.
* [Test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests) : impostazione di un carico sintetico nel sito Web.
* [Quota e prezzi](app-insights-pricing.md) e [campionamento per inserimento](app-insights-sampling.md).
* **L'accesso all'API** -creare [versione annotazioni](app-insights-annotations.md) e per hello API di accesso ai dati.
* [**Gli elementi di lavoro** ](app-insights-diagnostic-search.md#create-work-item) -connettersi in modo che è possibile creare bug durante l'analisi di dati di telemetria, sistema di verifica del lavoro tooa.

IMPOSTAZIONI

* [**Blocchi**](../azure-resource-manager/resource-group-lock-resources.md): bloccano le risorse di Azure.
* [**Script di automazione** ](app-insights-powershell.md) -esportare una definizione di risorsa di Azure hello in modo che è possibile utilizzarlo come un nuove risorse toocreate di modello.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi

|  |  |
| --- | --- |
| [Esplora metriche](app-insights-metrics-explorer.md)<br/>Consente di filtrare e segmentare le metriche |![Esempio di ricerca](./media/app-insights-dashboards/64.png) |
| [Ricerca diagnostica](app-insights-diagnostic-search.md)<br/>Consente di cercare e analizzare eventi ed eventi correlati e di creare bug |![Esempio di ricerca](./media/app-insights-dashboards/61.png) |
| [Analisi](app-insights-analytics.md)<br/>Linguaggio di query avanzato |![Esempio di ricerca](./media/app-insights-dashboards/63.png) |
