---
title: Flusso di metrica con metriche personalizzate e di diagnostica in Azure Application Insights aaaLive | Documenti Microsoft
description: Monitorare l'app Web in tempo reale, con metriche personalizzate e diagnosticare problemi con un feed live di errori, tracce ed eventi.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Live Metrics Stream: monitorare e diagnosticare con una latenza di 1 secondo 

Probe cuore heartbeat hello dell'applicazione web in tempo reale, in produzione utilizzando il flusso di metriche in tempo reale da [Application Insights](app-insights-overview.md). Selezionare e filtrare le metriche e le prestazioni toowatch contatori in tempo reale, senza alcun servizio tooyour disturbi. Esaminare le analisi dello stack da richieste ed eccezioni di esempio non riuscite. Insieme al [Profiler](app-insights-profiler.md), al [debugger di snapshot](app-insights-snapshot-debugger.md) e [al test delle prestazioni](app-insights-monitor-web-app-availability.md#performance-tests), Live Metrics Stream offre uno strumento di diagnostica non invasivo e potente per il sito Web live.

Con Live Metrics Stream, è possibile:

* Convalidare una correzione durante il rilasciato, osservando i contatori delle prestazioni e degli errori.
* Guardare effetto hello del test di carico e diagnosticare i problemi in tempo reale. 
* Concentrarsi sulle sessioni di test specifico o filtrare le problemi noti, selezione e filtro metriche hello da toowatch.
* Ottenere le eccezioni delle tracce in tempo reale.
* Provare varie combinazioni di filtri toofind hello KPI più rilevanti.
* Monitorare ogni contatore delle prestazioni di Windows live.
* Identificare un server che si verificano problemi e facilmente filtrare tutti hello KPI/live toojust feed che il server.

[![Video di Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Flusso di metriche in tempo reale è attualmente disponibile per le app di ASP.NET in esecuzione in locale o nel Cloud hello. 

## <a name="get-started"></a>Attività iniziali

1. Se [Application Insights](app-insights-asp-net.md) non è stato ancora installato nell'app Web ASP.NET o nell'[app del server Windows](app-insights-windows-services.md), è possibile farlo ora. 
2. **Versione più recente di aggiornamento toohello** del pacchetto di Application Insights hello. In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**. Aprire hello **aggiornamenti** scheda **Includi versione preliminare**e selezionare tutti i pacchetti hello Microsoft.ApplicationInsights.*.

    Ridistribuire l'app.

3. In hello [portale di Azure](https://portal.azure.com), aprire la risorsa di Application Insights hello per l'app e quindi aprire il flusso in tempo reale.

4. [Il canale di controllo sicura hello](#secure-the-control-channel) se è possibile utilizzare i dati sensibili, ad esempio i nomi dei clienti nei filtri.


![Nel pannello della panoramica hello, fare clic su un flusso in tempo reale](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Dati non visualizzati Controllare il firewall del server

Controllare hello [in uscita di porte per il flusso di metriche in tempo reale](app-insights-ip-addresses.md#outgoing-ports) aperte nel firewall hello del server. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Differenze tra Live Metrics Stream ed Esplora metriche e Analisi

| |Live Stream | Esplora metriche e Analisi |
|---|---|---|
|Latency|Dati visualizzati in un secondo|Aggregati in minuti|
|Nessuna conservazione|Dati persiste mentre nel grafico hello e viene eliminata|[Dati mantenuti per 90 giorni](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|On demand|I dati vengono trasmessi durante l'apertura di Live Metrics|I dati vengono inviati ogni volta che hello SDK viene installato e attivato|
|Free|Non sono previste spese per i dati di Live Stream|Oggetto troppo[prezzi](app-insights-pricing.md)
|campionamento|Tutte le metriche selezionate e i contatori vengono trasmessi. Gli errori e le analisi dello stack vengono usati come esempi. TelemetryProcessors non viene applicato.|Eventi potrebbero essere usati come [esempi](app-insights-api-filtering-sampling.md)|
|Canale di controllo|I segnali di filtro vengono inviati toohello SDK. È consigliabile [proteggere questo canale](#secure-channel).|La comunicazione è unidirezionale, toohello portale|


## <a name="select-and-filter-your-metrics"></a>Selezionare e filtrare le metriche

(Disponibile in versione classica App ASP.NET con hello SDK più recente.)

È possibile monitorare i KPI personalizzato in tempo reale applicando filtri arbitrari a qualsiasi telemetria di Application Insights dal portale hello. Fare clic su controllo filtro hello che mostra quando si del puntatore del mouse uno qualsiasi dei grafici hello. Hello seguente grafico viene tracciato un numero di richieste personalizzato KPI con filtri sugli attributi di URL e la durata. Convalidare i filtri con hello sezione di anteprima di flusso che mostra un feed in tempo reale di dati di telemetria che corrisponde ai criteri di hello che è stato specificato in qualsiasi punto nel tempo. 

![Indicatore KPI di richieste personalizzato](./media/app-insights-live-stream/live-stream-filteredMetric.png)

È possibile monitorare un valore diverso dal conteggio. opzioni di Hello dipendono dal tipo di hello del flusso, che può essere qualsiasi telemetria di Application Insights: le richieste, dipendenze, eccezioni, le tracce, eventi o metriche. Può essere la propria [misura personalizzata](app-insights-api-custom-events-metrics.md#properties):

![Opzioni del valore](./media/app-insights-live-stream/live-stream-valueoptions.png)

Inoltre tooApplication telemetria Insights, è anche possibile monitorare qualsiasi contatore delle prestazioni di Windows che selezionando una delle opzioni flusso hello e fornendo il nome di hello hello del contatore delle prestazioni.

Le metriche attive vengono aggregate in due punti: in locale su ciascun server e quindi su tutti i server. È possibile modificare l'impostazione predefinita hello in è possibile selezionare altre opzioni in hello rispettivi elenchi a discesa.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Telemetria di esempio: eventi di diagnostica live personalizzati
Per impostazione predefinita, il feed in tempo reale di hello degli eventi vengono mostrati esempi di richieste non riuscite e chiamate a dipendenze, eccezioni, eventi e tracce. Fare clic su hello icona toosee hello applicato criteri del filtro in qualsiasi punto nel tempo. 

![Feed live predefinito](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Come con le metriche, è possibile specificare qualsiasi tooany criteri arbitrari di tipi di dati di telemetria di Application Insights hello. In questo esempio, vengono selezionati eventi, tracce e richieste non riuscite specifiche. Vengono selezionate anche tutte le eccezioni e gli errori di dipendenza.

![Feed live personalizzati](./media/app-insights-live-stream/live-stream-events.png)

Nota: Attualmente, per i criteri basata su messaggi di eccezione, utilizzare il messaggio di eccezione più esterno hello. Nell'esempio sopra riportato, hello toofilter out eccezione grave di hello con messaggio di eccezione interna (segue hello "<-" delimitatore) "hello client si è disconnesso." usare un criterio che non contiene il messaggio "Errore durante la lettura del contenuto della richiesta".

Vedere i dettagli di hello di un elemento in hello live feed facendovi clic sopra. È possibile sospendere hello feed, fare clic su **sospendere** semplicemente scorrendo verso il basso o facendo clic su un elemento. Feed Live verrà ripresa dopo lo scorrimento indietro toohello top o facendo clic sul contatore hello degli elementi raccolti mentre era stato sospeso.

![Errori live campionati](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filtro per istanza di server

Se si desidera toomonitor un'istanza del ruolo server specifico, è possibile filtrare dal server.

![Errori live campionati](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Requisiti SDK
Live Metrics Stream personalizzato è disponibile con la versione 2.4.0-beta2 o più recente di [Application Insights SDK per il Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Memorizza l'opzione "Includi versione provvisoria" tooselect da Gestione pacchetti NuGet.

## <a name="secure-hello-control-channel"></a>Proteggere il canale di controllo di hello
Hello personalizzato i filtri i criteri specificati vengono inviati componente di metriche in tempo reale toohello indietro hello Application Insights SDK. i filtri di Hello potrebbero contenere informazioni riservate, ad esempio ID cliente. È possibile apportare canale hello protetta con una chiave segreta di API inoltre toohello chiave di strumentazione.
### <a name="create-an-api-key"></a>Creare una chiave API

![Creare una chiave API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Aggiungere tooConfiguration chiave API
Nel file applicationinsights config hello, aggiungere hello AuthenticationApiKey toohello QuickPulseTelemetryModule:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
O nel codice, impostare su hello QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Tuttavia, se e attendibile che tutti hello server collegati, è possibile provare i filtri personalizzati hello senza canale hello autenticato. Questa opzione è disponibile per sei mesi. Questa sostituzione è necessaria una volta per ogni nuova sessione oppure quando un nuovo server è online.

![Opzioni di autenticazione delle metriche attive](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>È consigliabile impostare canale hello autenticato prima di immettere informazioni potenzialmente riservate, ad esempio CustomerID in Criteri di filtro hello.
>

## <a name="generating-a-performance-test-load"></a>Generazione di un carico di test delle prestazioni

Se si desidera effetto hello toowatch di un carico aumenta, utilizzare hello Test delle prestazioni blade. Simula le richieste da un certo numero di utenti simultanei. È possibile eseguire entrambi "test manuale" (ping test) di un singolo URL o può essere eseguito un [test delle prestazioni web multipassaggio](app-insights-monitor-web-app-availability.md#multi-step-web-tests) caricare (in hello stesso modo come una disponibilità di test).

> [!TIP]
> Dopo aver creato i test delle prestazioni di hello, aprire test hello e hello pannello flusso Live in finestre distinte. È possibile vedere quando hello in coda Avvia test delle prestazioni e flusso in tempo reale di espressioni di controllo in hello contemporaneamente.
>


## <a name="troubleshooting"></a>Risoluzione dei problemi

Dati non visualizzati Se l'applicazione si trova in una rete protetta: Live Metrics Stream usa un indirizzo IP diverso dagli altri dati di Application Insights Telemetry. Assicurarsi che [tali indirizzi IP](app-insights-ip-addresses.md) siano aperti nel firewall.



## <a name="next-steps"></a>Passaggi successivi
* [Monitoraggio dell'utilizzo con Application Insights](app-insights-web-track-usage.md)
* [Uso di Ricerca diagnostica](app-insights-diagnostic-search.md)
* [Profiler](app-insights-profiler.md)
* [Debugger di snapshot](app-insights-snapshot-debugger.md)
