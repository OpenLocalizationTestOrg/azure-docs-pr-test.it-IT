---
title: Ricerca in Azure Application Insights aaaUsing | Documenti Microsoft
description: Ricercare e filtrare elementi di telemetria non elaborata inviata da App Web.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Utilizzo della funzionalità Ricerca in Application Insights
Ricerca è una funzionalità di [Application Insights](app-insights-overview.md) utilizzare toofind e di esplorare gli elementi di telemetria singole, ad esempio le visualizzazioni di pagina, le eccezioni o di richieste web. È possibile visualizzare le tracce del log e gli eventi codificati.

Per le query più complesse sui dati, utilizzare [Analytics](app-insights-analytics-tour.md).

## <a name="where-do-you-see-search"></a>Dove si trova Ricerca?
### <a name="in-hello-azure-portal"></a>Nel portale di Azure hello
È possibile aprire una ricerca di diagnostica in modo esplicito dal Pannello di Application Insights Overview hello dell'applicazione:

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Viene anche aperta quando si fa clic su alcuni grafici ed elementi della griglia. In questo caso, i filtri pre-sono toofocus tipo hello dell'elemento selezionato. 

Ad esempio, nel pannello della panoramica hello, vi è un grafico a barre di richieste classificati in base al tempo di risposta. Fare clic su un toosee intervallo prestazioni un elenco delle singole richieste in tale intervallo di tempo di risposta:

![Fare clic sulle prestazioni della richiesta](./media/app-insights-diagnostic-search/07-open-from-filters.png)

Hello corpo principale della diagnostica di ricerca è un elenco di elementi di dati di telemetria - richieste di server, pagina viste, eventi personalizzati che è stato codificato e così via. Inizio dell'elenco di hello hello è un grafico di riepilogo che mostra i conteggi di eventi nel tempo.

Fare clic su Aggiorna tooget nuovi eventi.

### <a name="in-visual-studio"></a>In Visual Studio

In Visual Studio è inoltre disponibile una finestra Ricerca di Application Insights. È particolarmente utile per la visualizzazione di eventi di telemetria generati da un'applicazione hello che si esegue il debug. Tuttavia, inoltre possibile visualizzare gli eventi di hello raccolti dall'app pubblicate nel portale di Azure hello.

Aprire la finestra di ricerca hello in Visual Studio:

![Funzionalità di ricerca di Application Insights aperta in Visual Studio](./media/app-insights-diagnostic-search/32.png)

finestra di ricerca Hello dispone di funzionalità simile toohello web portale:

![Finestra di ricerca di Application Insights in Visual Studio](./media/app-insights-diagnostic-search/34.png)

scheda di operazione di rilevamento Hello è disponibile quando si apre una richiesta o una visualizzazione di pagina. Un ' operazione ' è una sequenza di eventi che è associata a tooa singola richiesta o pagina di visualizzazione. Ad esempio, chiamate di dipendenza, eccezioni, log di traccia ed eventi personalizzati potrebbero far parte di una singola operazione. Mostra scheda operazione di rilevamento di Hello hello graficamente intervallo e la durata di questi eventi nella relazione di toohello richiesta o la pagina di visualizzazione. 

## <a name="inspect-individual-items"></a>Controllare i singoli elementi
Selezionare tutti i campi chiave di dati di telemetria elemento toosee ed elementi correlati. Set completo di hello toosee dei campi, fare clic su "…". 

![Fare clic su nuovo elemento di lavoro, modificare i campi di hello e quindi fare clic su OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>I tipi di eventi sono i seguenti:
Aprire Pannello filtro hello e scegliere i tipi di evento hello si desidera toosee. (Se, successivamente, si desidera filtri hello toorestore con cui è stato aperto il pannello hello, fare clic su Reimposta).

![Scegliere il filtro e selezionare i tipi di telemetria](./media/app-insights-diagnostic-search/02-filter-req.png)

tipi di evento Hello sono:

* **Traccia**:  - [log di diagnostica](app-insights-asp-net-trace-logs.md) con chiamate TrackTrace, log4Net, NLog e System.Diagnostic.Trace.
* **Richiesta**: richieste HTTP ricevute dall'applicazione server, tra cui pagine, script, immagini, file di stile e dati. Questi eventi sono grafici Cenni preliminari sulla richiesta e risposta utilizzati toocreate hello.
* **Visualizzazione della pagina** - [telemetria inviati dal client web hello](app-insights-javascript.md), utilizzato toocreate pagina Visualizza report. 
* **Evento personalizzato** : se è stato inserito tooTrackEvent() chiamate in ordine troppo[monitorare l'utilizzo](app-insights-api-custom-events-metrics.md), è possibile cercare di seguito.
* **Eccezione** - non rilevata [eccezioni nel server di hello](app-insights-asp-net-exceptions.md)e quelle che si accede tramite trackexception () effettuate.
* **Dipendenza** - [chiamate dall'applicazione server](app-insights-asp-net-dependencies.md) tooother servizi, ad esempio le API REST o i database e chiamate AJAX dal [codice client](app-insights-javascript.md).
* **Disponibilità**: risultati dei [test di disponibilità](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filtrare in base ai valori delle proprietà
È possibile filtrare gli eventi ai valori hello delle relative proprietà. proprietà di Hello disponibili dipendono dai tipi di evento hello selezionato. 

Ad esempio, selezionare le richieste con un codice di risposta specifico. 

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/03-response500.png)

Non scelta di alcun valore di una determinata proprietà ha lo stesso effetto delle scelta tutti i valori hello. Viene disattivata l'applicazione dei filtri per quella proprietà.

### <a name="narrow-your-search"></a>Limitare la ricerca
Si noti che hello conta toohello a destra dei valori di filtro hello mostrare il numero di occorrenze sono set filtrato di hello corrente. 

In questo esempio è chiaro che la richiesta ' Rpt/Employees' hello risultati nella maggior parte degli errori di hello '500':

![Espandere una proprietà e scegliere un valore](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Trovare gli eventi con hello stessa proprietà
Trova hello tutti gli elementi con hello stesso valore della proprietà:

![Fare clic con il pulsante destro del mouse su una proprietà](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>La ricerca di dati hello

> [!NOTE]
> toowrite query più complesse, aprire [ **Analitica** ](app-insights-analytics-tour.md) dalla parte superiore di hello del Pannello di ricerca hello.
> 

È possibile cercare i termini in uno dei valori di proprietà hello. Ciò è particolarmente utile se sono stati scritti [eventi personalizzati](app-insights-api-custom-events-metrics.md) con i valori della proprietà. 

È possibile tooset un intervallo di tempo, come le ricerche di un intervallo più breve è più veloce. 

![Aprire la ricerca diagnostica](./media/app-insights-diagnostic-search/appinsights-311search.png)

Cercare parole complete, non sottostringhe. Utilizzare i caratteri speciali tooenclose tra virgolette.

| string | *non* si trova con | ma si trova con |
| --- | --- | --- |
| ControllerHome.Info |home<br/>controller<br/>fo | controllerhome<br/>info<br/>"homecontroller.info"|
|Stati Uniti|Uni<br/>ti|uniti<br/>stati<br/>uniti AND stati<br/>"stati uniti"

Di seguito sono espressioni di ricerca hello che è possibile utilizzare:

| Query di esempio | Effetto |
| --- | --- |
| `apple` |Trova tutti gli eventi nell'intervallo di tempo hello i cui campi includono la parola hello "apple" |
| `apple AND banana` |Individuazione di eventi che contengono entrambe le parole. Usare "AND" in lettere maiuscole, non "and". |
| `apple OR banana`<br/>`apple banana` |Individuazione degli eventi che contengono una delle parole. Usare "OR", non "or".<br/>Forma breve. |
| `apple NOT banana` |Individuare gli eventi che contengono una parola, ma non hello altri. |



## <a name="sampling"></a>campionamento
Se l'applicazione genera un grande quantità di dati di telemetria (e si sta utilizzando ASP.NET SDK versione 2.0.0-beta3 hello o versione successiva), il modulo di campionamento adattivo hello riduce automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi. Tuttavia, gli eventi che sono correlato toohello stessa richiesta vengono selezionate o deselezionate come gruppo, in modo che è possibile spostarsi tra gli eventi correlati. 

[Informazioni sul campionamento](app-insights-sampling.md).



## <a name="create-work-item"></a>Creare un elemento di lavoro
È possibile creare un bug in GitHub o Visual Studio Team Services con i dettagli di hello da qualsiasi elemento di dati di telemetria. 

![Fare clic su nuovo elemento di lavoro, modificare i campi di hello e quindi fare clic su OK.](./media/app-insights-diagnostic-search/42.png)

Hello prima volta, viene chiesto tooconfigure tooyour un collegamento Team Services account e del progetto.

![Immettere l'URL hello del server di Team Services e il nome di progetto hello, quindi fare clic su autorizza](./media/app-insights-diagnostic-search/41.png)

(È inoltre possibile configurare il collegamento hello nel Pannello di elementi di lavoro hello.)

## <a name="save-your-search"></a>Salvare la ricerca
Dopo avere impostato tutti i filtri di hello desiderato, è possibile salvare la ricerca hello come preferito. Se si utilizza un account aziendale, è possibile scegliere se tooshare con altri membri del team.

![Fare clic su preferito, impostare il nome di hello e fare clic su Salva](./media/app-insights-diagnostic-search/08-favorite-save.png)

ricerca di hello toosee nuovamente, **pannello della panoramica passare toohello** e aprire Preferiti:

![Sezione Preferiti](./media/app-insights-diagnostic-search/09-favorite-get.png)

Se è stato salvato con l'intervallo di tempo relativo, dati più recenti hello pannello riaperto hello. Se è stato salvato con l'intervallo di tempo assoluto, vedrai hello stessi dati ogni volta. (Se 'Relative' non è disponibile quando si desidera toosave Preferiti, fare clic su intervallo di tempo nell'intestazione hello e impostare un intervallo di tempo che non è un intervallo personalizzato.)

## <a name="send-more-telemetry-tooapplication-insights"></a>Inviare ulteriori dati di telemetria tooApplication Insights
In aggiunta toohello di dialogo dati di telemetria inviato da Application Insights SDK, è possibile:

* Acquisire le tracce del log dal framework di registrazione preferito in [.NET](app-insights-asp-net-trace-logs.md) o [Java](app-insights-java-trace-logs.md). Ciò significa che è possibile cercare le tracce del log e metterle in correlazione con le visualizzazioni pagina, le eccezioni e altri eventi. 
* [Scrivere codice](app-insights-api-custom-events-metrics.md) toosend eventi personalizzati, le visualizzazioni di pagina e le eccezioni. 

[Informazioni su come toosend log e dati di telemetria personalizzati tooApplication Insights](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>Domande e risposte
### <a name="limits"></a>Quanti dati vengono conservati?

Vedere hello [riepilogo limiti](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Come è possibile visualizzare dati POST nelle richieste server?
È non registra i dati POST hello automaticamente, ma è possibile utilizzare [chiamate a TrackTrace o log](app-insights-asp-net-trace-logs.md). Inserire i dati POST hello nel parametro messaggio hello. Non è possibile filtrare il messaggio hello in hello stesso modo è possibile filtrare le proprietà, ma il limite di dimensioni di hello è più lungo.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Passaggi successivi
* [Scrivere query complesse in Analytics](app-insights-analytics-tour.md)
* [Inviare i log e dati di telemetria personalizzati tooApplication Insights](app-insights-asp-net-trace-logs.md)
* [Configurare i test di disponibilità e velocità di risposta](app-insights-monitor-web-app-availability.md)
* [Risoluzione dei problemi](app-insights-troubleshoot-faq.md)
