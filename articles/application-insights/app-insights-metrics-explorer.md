---
title: aaaExploring metriche in Azure Application Insights | Documenti Microsoft
description: Come Esplora metrica dai grafici toointerpret e come toocustomize pannelli di Esplora metriche.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Esaminare le metriche in Application Insights
Le metriche in [Application Insights][start] sono valori e conteggi di eventi misurati, inviati nei dati di telemetria dall'applicazione. Consentono di rilevare problemi di prestazioni e osservare le tendenze nella modalità di uso dell'applicazione. Esiste una vasta gamma di metriche standard ed è anche possibile creare metriche ed eventi personalizzati.

Il conteggio delle metriche e degli eventi viene visualizzato nei grafici dei valori aggregati, ad esempio somme, medie o conteggi.

Ecco un esempio di set di grafici:

![](./media/app-insights-metrics-explorer/01-overview.png)

Disponibili ovunque grafici delle metriche nel portale Application Insights hello. Nella maggior parte dei casi, possono essere personalizzate ed è possibile aggiungere ulteriori pannello toohello di grafici. Dal pannello della panoramica hello, fare clic sulle toomore dettagliate grafici (che dispone di titoli, ad esempio "Server"), oppure fare clic su **Esplora metriche** tooopen un nuovo pannello in cui è possibile creare grafici personalizzati.

## <a name="time-range"></a>Intervallo di tempo
È possibile modificare l'intervallo di tempo coperto da grafici hello o griglie in qualsiasi pannello hello.

![Pannello della panoramica hello aperti dell'applicazione nel portale di Azure hello](./media/app-insights-metrics-explorer/03-range.png)

Se si è in attesa di alcuni dati non ancora visualizzati, fare clic su Aggiorna. Aggiornamento grafici a intervalli, ma sono più tempi per intervalli di tempo più ampi intervalli hello. Può richiedere un po' di tempo per dati toocome tramite pipeline di analisi hello in un grafico.

toozoom nella parte di un grafico, trascinare su di essa:

![Trascinare il puntatore su una parte di un grafico.](./media/app-insights-metrics-explorer/12-drag.png)

Fare clic su toorestore di pulsante Annulla Zoom hello è.

## <a name="granularity-and-point-values"></a>Granularità e valori dei punti
A questo punto, posiziona il mouse su valori hello toodisplay di hello del grafico delle metriche hello.

![Posizionare il mouse di hello su un grafico](./media/app-insights-metrics-explorer/02-focus.png)

valore di Hello della metrica hello in un particolare punto è aggregato in hello precedente intervallo di campionamento.

intervallo di campionamento Hello o "granularità" viene visualizzata nella parte superiore di hello del pannello hello.

![intestazione Hello di un pannello.](./media/app-insights-metrics-explorer/11-grain.png)

È possibile regolare la granularità hello nel Pannello di intervallo di tempo hello:

![intestazione Hello di un pannello.](./media/app-insights-metrics-explorer/grain.png)

granularità Hello disponibili dipendono dall'intervallo di tempo hello selezionato. granularità esplicita Hello sono alternative toohello la granularità "automatico" per l'intervallo di tempo hello.


## <a name="editing-charts-and-grids"></a>Modifica di grafici e griglie
tooadd un nuovo pannello toohello grafico:

![In Esplora metriche scegliere Aggiungi grafico](./media/app-insights-metrics-explorer/04-add.png)

Selezionare **modificare** in tooedit un grafico esistente o nuovo cosa viene illustrato:

![Selezionare una o più metriche](./media/app-insights-metrics-explorer/08-select.png)

È possibile visualizzare più di una metrica in un grafico, anche se sono presenti restrizioni sulle combinazioni di hello che possono essere visualizzate insieme. Non appena si sceglie una metrica, alcune delle hello che altri è disabilitata.

Se è stata codificata [metriche personalizzate] [ track] nell'app (chiamate tooTrackMetric e TrackEvent) questi verranno elencati di seguito.

## <a name="segment-your-data"></a>Segmentare i dati
È possibile dividere una metrica dalla proprietà, ad esempio, le visualizzazioni pagina toocompare nei client con sistemi operativi diversi.

Selezionare un diagramma o griglia, attivare il raggruppamento e scegliere un toogroup di proprietà da:

![Attivare il raggruppamento e poi selezionare una proprietà in Raggruppa per](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Quando si utilizza il raggruppamento, i tipi di Area e di grafico a barre hello forniscono una visualizzazione in pila. È adatto in cui il metodo di aggregazione hello è Sum. Tuttavia, in cui il tipo di aggregazione hello Media, scegliere tipi di visualizzazione di riga o una griglia hello.
>
>

Se è stata codificata [metriche personalizzate] [ track] nell'app e includono i valori delle proprietà, sarà in grado di tooselect proprietà hello nell'elenco di hello.

È troppo piccolo per i dati segmentati grafico hello? modificarne l'altezza:

![Regolare il dispositivo di scorrimento hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Tipi di aggregazione
legenda Hello sul lato di hello per impostazione predefinita in genere viene visualizzato il valore aggregato hello periodo hello del grafico hello. Se si passa il mouse sopra il grafico di hello, verrà visualizzato il valore di hello a questo punto.

Ogni punto dati nel grafico hello è un'aggregazione di valori di dati hello ricevuti nel precedente intervallo di campionamento "granularità" hello. viene visualizzata nella parte superiore di hello del pannello hello granularità Hello e varia in base alla hello complessiva della scala cronologica del grafico hello.

Le metriche possono essere aggregate in modi diversi:

* **Conteggio** è un numero di eventi di hello ricevuti nell'intervallo di campionamento hello. Viene utilizzato per gli eventi come le richieste. Variazioni del grafico hello altezza hello indica le variazioni nel numero hello che si verificano gli eventi di hello. Ma si noti che il valore numerico di hello cambia quando si modifica l'intervallo di campionamento hello.
* **Somma** aggiunge i valori hello di tutti i punti dati hello ricevuti tramite l'intervallo di campionamento hello o periodo hello del grafico hello.
* **Media** divide hello somma tramite un numero di punti dati ricevuti in intervallo hello hello.
* **Unica** : i conteggi vengono usati per contare gli utenti e gli account. Intervallo di campionamento hello o periodo hello del grafico hello, hello figura conteggio hello dei diversi utenti visualizzati in quel momento.
* **%** - le versioni in percentuale di ogni aggregazione vengono utilizzate solo con i grafici segmentati. Totale Hello aggiunge sempre % too100 grafico hello Mostra contributo relativo di hello dei diversi componenti di un totale.

    ![Aggregazione in percentuale](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Modificare il tipo di aggregazione hello

![Modificare il grafico hello e quindi selezionare aggregazione](./media/app-insights-metrics-explorer/05-aggregation.png)

il metodo predefinito Hello per ogni metrica viene visualizzato quando si crea un nuovo grafico o quando vengono deselezionate tutte le metriche:

![Deselezionare tutte le metriche toosee hello le impostazioni predefinite](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Bloccare l'asse Y 
Per impostazione predefinita un grafico mostra i valori dell'asse Y a partire da zero fino a: i valori massimi nell'intervallo di dati hello, toogive una rappresentazione visiva del quantum di valori hello. Ma in alcuni casi più quantum hello potrebbe essere interessante toovisually controllare piccole modifiche nei valori. Per le personalizzazioni come questo utilizzo hello asse y intervallo modifica funzionalità toopin hello valore dell'asse y minimo o massimo nella posizione desiderata.
Fare clic su "Impostazioni" casella di controllo toobring backup hello intervallo dell'asse y impostazioni

![Fare clic su Impostazioni avanzate, selezionare l'intervallo Personalizzato e specificare i valori minino e massimo](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filtrare i dati
metrica di toosee hello solo per un set di valori di proprietà selezionato:

![Fare clic su Filtro, espandere una proprietà e selezionare alcuni valori](./media/app-insights-metrics-explorer/19-filter.png)

Se non si seleziona tutti i valori per una particolare proprietà, dispone di hello stesso come selezionarle tutte: non sono presenti filtri su questa proprietà.

Hello notare i conteggi di eventi insieme a ogni valore della proprietà. Quando si selezionano i valori di una proprietà, hello conta insieme ad altre proprietà vengono modificati i valori.

I filtri vengono applicati i grafici di hello tooall in un pannello. Se si desidera grafici toodifferent filtri diversi, creare e salvare blade metriche. Se si desidera, è possibile aggiungere grafici dal dashboard toohello diversi pannelli, in modo che possano vederli uno accanto a altro.

### <a name="remove-bot-and-web-test-traffic"></a>Rimuovere il traffico di bot e test Web
Usa filtro hello **traffico reale o sintetico** e controllare **reale**.

È possibile anche filtrare in base a **Origine del traffico sintetico**.

### <a name="tooadd-properties-toohello-filter-list"></a>elenco di filtri tooadd proprietà toohello
Si desidera telemetria toofilter su una categoria di propria scelta. Ad esempio, è possibile che si dividano gli utenti in categorie diverse e si voglia segmentare i dati in base a queste categorie.

[Creare proprietà personalizzate](app-insights-api-custom-events-metrics.md#properties). Impostare la proprietà in un [telemetria inizializzatore](app-insights-api-custom-events-metrics.md#defaults) toohave appare in tutti i dati di telemetria, inclusi i dati di telemetria standard hello inviato da diversi moduli SDK.

## <a name="edit-hello-chart-type"></a>Modificare il tipo di grafico hello
Si noti che è possibile passare dalle griglie ai grafici e viceversa:

![Selezionare una griglia o un grafico e quindi scegliere un tipo di grafico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Salvare il pannello delle metriche
Dopo aver creato alcuni grafici, è possibile salvarli come preferiti. È possibile scegliere se tooshare con altri membri del team, se si utilizza un account aziendale.

![Scegliere Preferito](./media/app-insights-metrics-explorer/21-favorite-save.png)

nuovo pannello con hello toosee **pannello della panoramica passare toohello** e aprire Preferiti:

![Nel pannello della panoramica hello, scegliere Preferiti](./media/app-insights-metrics-explorer/22-favorite-get.png)

Se si sceglie l'intervallo di tempo relativo al momento del salvataggio, pannello hello verrà aggiornato con le metriche più recente di hello. Se si sceglie l'intervallo di tempo assoluto, verrà visualizzato hello stessi dati ogni volta.

## <a name="reset-hello-blade"></a>Reimpostazione hello pannello
Se si modifica un pannello ma quindi cui si desidera che i set di backup toohello originale salvato tooget, semplicemente fare clic su Reimposta.

![Nei pulsanti di hello nella parte superiore di hello di Esplora metriche](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Flusso metriche attive

Per una visualizzazione molto più immediata dei dati di telemetria, aprire [flusso live](app-insights-live-stream.md). La maggior parte delle metriche accettano pochi minuti tooappear, a causa del processo di hello di aggregazione. Al contrario, le metriche attive sono ottimizzate per bassa latenza. 

## <a name="set-alerts"></a>Impostazione di avvisi
toobe una notifica tramite posta elettronica di valori insoliti per le metriche, aggiungere un avviso. È possibile scegliere gli amministratori degli account toohello toosend hello posta elettronica o toospecific indirizzi di posta elettronica.

![In Esplora metriche scegliere Regole di avviso, Aggiungi avviso](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Altre informazioni sugli avvisi][alerts].


## <a name="continuous-export"></a>Esportazione continua
Se si vuole che i dati vengano esportati in modo continuo per poterli elaborare esternamente, considerare la possibilità di usare l' [esportazione continua](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Se si desidera arricchire la visualizzazione dei dati, è possibile [esportare tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analytics
[Analitica](app-insights-analytics.md) è un esempio di modalità più versatile tooanalyze dati di telemetria utilizzando un linguaggio di query avanzate. Usarlo se si desidera toocombine risultati di metriche di calcolo o eseguire un'analisi approfondita del prestazioni recente dell'app. 

In un grafico di metrica, è possibile scegliere hello Analitica icona tooget direttamente toohello Analitica query equivalente.

## <a name="troubleshooting"></a>Risoluzione dei problemi
*All'interno del grafico non vengono visualizzati dati.*

* I filtri vengono applicati i grafici di hello tooall nel pannello hello. Assicurarsi che, mentre sta porre l'attenzione su un grafico, non è stato impostato un filtro che escluda tutti i dati di hello in un altro.

    Se si desidera tooset filtri diversi nei grafici diversi, crearli in diversi pannelli, salvare i Preferiti come separate. Se si desidera, è possibile aggiungerli toohello dashboard in modo che possano vederli uno accanto a altro.
* Se si raggruppa un grafico da una proprietà che non è definita nella metrica hello, quindi verrà nulla sul grafico hello. Provare a lasciare il campo "Raggruppa in base a" vuoto o scegliere una proprietà di raggruppamento diversa.
* I dati sulle prestazioni (CPU, velocità di IO e così via) sono disponibili per servizi Web Java, app desktop di Windows, [app Web IIS se si installa Status Monitor](app-insights-monitor-performance-live-website-now.md) e [servizi cloud di Azure](app-insights-azure.md). I dati non sono disponibili per i siti Web di Azure.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi
* [Monitoraggio dell'utilizzo con Application Insights](app-insights-web-track-usage.md)
* [Uso di Ricerca diagnostica](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
