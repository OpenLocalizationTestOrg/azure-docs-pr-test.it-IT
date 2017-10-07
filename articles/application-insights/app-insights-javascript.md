---
title: le app web aaaAzure Application Insights per JavaScript | Documenti Microsoft
description: Ottenere i conteggi delle visualizzazioni pagina e delle sessioni, i dati client Web e la traccia dei modelli di utilizzo. Rilevare le eccezioni e i problemi di prestazioni nelle pagine Web JavaScript.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights per pagine Web
Informazioni sulle prestazioni di hello e l'utilizzo di una pagina web o dell'app. Se si aggiungono [Application Insights](app-insights-overview.md) tooyour lo script della pagina, si ottiene gli intervalli di tempo di caricamento pagina e le chiamate AJAX, conteggi e i dettagli delle eccezioni del browser e gli errori di AJAX, nonché gli utenti e i conteggi di sessione. Tutti questi elementi possono essere segmentati per pagina, sistema operativo client e versione del browser, posizione geografica e altre dimensioni. È possibile impostare avvisi relativi al numero di errori o rallentare il caricamento delle pagine. E inserendo le chiamate di traccia nel codice JavaScript, è possibile monitorare le modalità di utilizzo delle diverse funzionalità di hello dell'applicazione a pagina web.

Application Insights è compatibile con tutte le pagine Web, con una minima aggiunta di codice JavaScript. Se il servizio Web è [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), è possibile integrare i dati di telemetria dal server e dai client.

![In portal.azure.com aprire la risorsa dell'app e fare clic su Browser](./media/app-insights-javascript/03.png)

È necessaria una sottoscrizione troppo[Microsoft Azure](https://azure.com). Se il team dispone di una sottoscrizione azienda, chiedere hello proprietario tooadd tooit l'Account Microsoft. Lo sviluppo e un uso su scala ridotta sono gratuiti.

## <a name="set-up-application-insights-for-your-web-page"></a>Installare Application Insights per la pagina Web
Aggiungere hello caricatore codice frammento tooyour pagine web, come indicato di seguito.

### <a name="open-or-create-application-insights-resource"></a>Aprire o creare una risorsa Application Insights
Hello risorsa di Application Insights è in cui vengono visualizzati i dati sulle prestazioni e sull'utilizzo della pagina. 

Accedere al [portale di Azure](https://portal.azure.com).

Se è già configurato il monitoraggio per il lato server hello dell'app, si dispone già di una risorsa:

![Scegliere Sfoglia, quindi Servizi per gli sviluppatori, Application Insights](./media/app-insights-javascript/01-find.png)

Se non si ha un account, crearlo:

![Scegliere Nuovo, quindi Servizi per gli sviluppatori, Application Insights.](./media/app-insights-javascript/01-create.png)

*Altre domande?* [Altre informazioni sulla creazione di una risorsa](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Aggiungere app tooyour di hello SDK script o pagine web
Durante l'avvio rapido, ottenere script hello per le pagine web:

![Nel pannello della panoramica app, scegliere l'avvio rapido, ottenere codice toomonitor le pagine web. Copiare lo script hello.](./media/app-insights-javascript/02-monitor-web-page.png)

Inserire uno script di hello prima hello `</head>` tag di ogni pagina desiderata tootrack. Se il sito Web dispone di una pagina master, è possibile inserire script hello non esiste. ad esempio:

* In un progetto ASP.NET MVC inserire lo script in `View\Shared\_Layout.cshtml`
* In un sito di SharePoint, nel Pannello di controllo hello, aprire [Impostazioni sito o pagina Master](app-insights-sharepoint.md).

script Hello contiene una chiave di strumentazione hello che indirizza una risorsa di Application Insights tooyour dati hello. 

([Script hello spiegazione più approfondita. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Se si usa un framework di pagine Web noto, cercare adattatori Application Insights. Ad esempio, [un modulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Configurazione dettagliata
Sono disponibili diversi [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) che è possibile impostare, anche se nella maggior parte dei casi non è necessario farlo. Ad esempio, è possibile disabilitare o limitare il numero di hello di chiamate Ajax segnalato per la visualizzazione di pagina (tooreduce traffico). Oppure è possibile impostare spostamento di dati di telemetria toohave modalità debug rapidamente tramite la pipeline hello senza essere eseguite in batch.

tooset questi parametri, cercare la seguente riga nel frammento di codice hello e aggiungere più elementi separati da virgola dopo di esso:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Hello [parametri disponibili](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) includono:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Eseguire l'app
Eseguire l'app web, usare un toogenerate telemetria e attendere qualche alcuni secondi. È possibile eseguire utilizzando hello **F5** chiave nel computer di sviluppo, o pubblicarla e consentire agli utenti di modificarlo nel modo desiderato.

Se si desidera telemetria hello toocheck che un'app web stia inviando informazioni tooApplication, utilizzare gli strumenti di debug del browser (**F12** in molti browser). Dati inviati toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Esplorare i dati sulle prestazioni del browser
Aprire hello Browser pannello tooshow aggregato i dati sulle prestazioni dal browser degli utenti.

![In portal.azure.com aprire la risorsa dell'app e fare clic su Impostazioni, Browser](./media/app-insights-javascript/03.png)

*Ancora nessun dato? Fare clic su **aggiornamento** nella parte superiore di hello della pagina hello. Ancora niente di fatto? Vedere [Risoluzione dei problemi](app-insights-troubleshoot-faq.md).*

pannello Browser Hello è un [pannello Esplora metriche](app-insights-metrics-explorer.md) con filtri predefiniti e le selezioni di grafico. È possibile modificare l'intervallo di tempo hello, filtri e configurazione del grafico se si desidera e salvare il risultato di hello come preferito. Fare clic su **Ripristina impostazioni predefinite** configurazione di blade tooget toohello indietro originale.

## <a name="page-load-performance"></a>Prestazioni di caricamento delle pagine
Hello superiore è un grafico segmentato dei tempi di caricamento pagina. altezza totale del Hello del grafico hello rappresenta pagine tooload e la visualizzazione del tempo medio hello dall'app nei browser degli utenti. tempo di Hello viene misurato dal momento browser hello invia una richiesta HTTP iniziale hello fino al carico sincrono tutti gli eventi sono stati elaborati, inclusi i layout e l'esecuzione di script. Non sono incluse le attività asincrone, ad esempio il caricamento di Web part da chiamate AJAX.

grafico Hello segmenti di tempo totale di caricamento hello in hello [gli intervalli di tempo standard definiti da W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Si noti che hello *la connessione di rete* ora è inferiore al previsto, spesso perché è una media su tutte le richieste dal server di toohello browser hello. Numero di richieste singoli più Connetti pari a 0 perché esiste già un server di toohello connessione attiva.

### <a name="slow-loading"></a>Caricamento lento
Il caricamento lento delle pagine è tra le principali cause di insoddisfazione per gli utenti. Se il grafico hello indica caricamento pagina lento, è facile toodo alcune ricerche di diagnostica.

grafico di Hello Mostra Media hello di tutti i caricamenti di pagina nell'app. toosee se il problema di hello è confinata tooparticular pagine, esaminare ulteriormente verso il basso il pannello hello, URL della pagina in cui è presente una griglia segmentata per:

![](./media/app-insights-javascript/09-page-perf.png)

Si noti il conteggio delle viste pagina hello e deviazione standard. Se il conteggio delle pagine hello è molto basso, quindi problema hello non è interessata utenti molto. La deviazione standard elevata (Media toohello confrontabili stesso) indica molte variazioni tra singole misure.

**Ingrandire un URL e una visualizzazione pagina.** Fare clic su qualsiasi toosee nome pagina un pannello del browser grafici filtrati toothat solo URL; e quindi in un'istanza di una visualizzazione di pagina.

![](./media/app-insights-javascript/35.png)

Fare clic su `...` per un elenco completo delle proprietà per tale evento, o di controllare le chiamate Ajax hello e gli eventi correlati. Chiamate Ajax lente interessano hello complessiva pagina tempo di caricamento, se sono sincroni. Gli eventi sono le richieste per hello server stesso URL (se impostati Application Insights sul server web).

**Prestazioni delle pagine nel tempo.** Tornare al pannello browser hello modificare griglia tempo di caricamento pagina visualizzazione hello in toosee di grafico a una riga se sono stati picchi in determinati momenti:

![Fare clic sull'intestazione della griglia hello hello e selezionare un nuovo tipo di grafico](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentare in base ad altre dimensioni.** Forse le pagine sono più lenti tooload in una località di browser, del sistema operativo client o utente specifica? Aggiungere un nuovo grafico e sperimentare hello **Group by** dimensione.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Prestazioni AJAX
Assicurarsi che le prestazioni di tutte le chiamate AJAX nelle pagine Web siano soddisfacenti. Sono spesso utilizzati toofill parti della pagina in modo asincrono. Sebbene hello pagina generale potrebbe caricare immediatamente, agli utenti potrebbero essere frustrati dai veniva visualizzata vuota web part, in attesa di tooappear di dati in essi contenuti.

Chiamate AJAX dalla pagina web vengono visualizzate nel pannello browser hello con dipendenze.

Sono disponibili grafici di riepilogo nella parte superiore di hello del pannello hello:

![](./media/app-insights-javascript/31.png)

e griglie dettagliate più in basso:

![](./media/app-insights-javascript/33.png)

Fare clic su una riga per visualizzare i dettagli specifici.

> [!NOTE]
> Se si elimina filtro browser hello nel Pannello di hello, in questi grafici sono inclusi sia i server e le dipendenze AJAX. Fare clic su Ripristina impostazioni predefinite tooreconfigure hello filtro.
> 
> 

**toodrill le chiamate Ajax non riuscite di** scorrere verso il basso della griglia di errori di toohello dipendenza e quindi fare clic su istanze specifiche di toosee una riga.

![](./media/app-insights-javascript/37.png)


Fare clic su `...` per dati di telemetria completo hello per una chiamata Ajax.

### <a name="no-ajax-calls-reported"></a>Nessuna chiamata AJAX segnalata
Chiamate AJAX includono chiamate HTTP/HTTPS eseguite dallo script hello della pagina web. Se non li segnalato, verificare il frammento di codice hello non imposta hello `disableAjaxTracking` o `maxAjaxCallsPerView` [parametri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Eccezioni del browser
Nel Pannello di browser hello, non vi è un grafico di riepilogo di eccezioni e una griglia dei tipi di eccezione ulteriormente verso il basso il pannello hello.

![](./media/app-insights-javascript/39.png)

Se le eccezioni del browser segnalate non viene visualizzata, verificare il frammento di codice hello non impostato hello `disableExceptionTracking` [parametro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Esaminare singoli eventi di visualizzazione pagina

In genere la telemetria delle visualizzazioni di pagina viene analizzata da Application Insights e vengono quindi visualizzati solo i report cumulativi, mediati su tutti gli utenti del sito. A scopo di debug, tuttavia, è possibile visualizzare anche singoli eventi di visualizzazione di pagina.

Nel pannello diagnostica ricerca hello, impostare i filtri tooPage visualizzazione.

![](./media/app-insights-javascript/12-search-pages.png)

Selezionare qualsiasi evento toosee maggiori dettagli. Nella pagina dettagli hello, fare clic su "…" toosee ancora più dettagliate.

> [!NOTE]
> Se si utilizza [ricerca](app-insights-diagnostic-search.md), si noti la presenza di parole intere toomatch: "Informazioni" e "ulteriori informazioni sul" non corrispondono a "About".
> 
> 

È inoltre possibile utilizzare hello potente [il linguaggio di query Log Analitica](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch visualizzazioni di pagina.

### <a name="page-view-properties"></a>Proprietà delle visualizzazioni di pagina
* **Durata della visualizzazione pagina** 
  
  * Per impostazione predefinita, hello tempo accetta tooload hello pagina, dal client richiesta toofull caricare (inclusi i file ausiliari ma escluse le attività asincrone, ad esempio le chiamate Ajax). 
  * Se si imposta `overridePageViewDuration` in hello [configurazione pagina](#detailed-configuration), hello innanzitutto l'intervallo tra i client richiesta tooexecution di hello `trackPageView`. Se è stato spostato trackPageView rispetto alla posizione normale dopo l'inizializzazione di hello dello script hello, riflette un valore diverso.
  * Se `overridePageViewDuration` viene impostato e una durata viene fornito l'argomento in hello `trackPageView()` chiamare, quindi viene utilizzato il valore di argomento hello. 

## <a name="custom-page-counts"></a>Conteggi di pagina personalizzati
Per impostazione predefinita, un conteggio delle pagine si verifica ogni volta che viene caricata una nuova pagina nel browser client hello.  Ma è possibile toocount visualizzazioni di pagina aggiuntiva. Ad esempio, una pagina potrebbe visualizzare il relativo contenuto in schede e si desidera toocount una pagina quando hello utente passa da schede. O codice JavaScript nella pagina hello potrebbe caricare nuovo contenuto senza modificare l'URL del browser hello.

Nel punto appropriato di hello nel codice client, inserire una chiamata di JavaScript simile al seguente:

    appInsights.trackPageView(myPageName);

nome della pagina Hello può contenere hello stesso caratteri sotto forma di URL, ma tutti gli elementi presenti dopo "#" o "?" viene ignorato.

## <a name="usage-tracking"></a>Monitoraggio dell'utilizzo
Desidera toofind le operazioni che gli utenti da eseguire con l'app?

* [Informazioni sul monitoraggio dell'utilizzo](app-insights-web-track-usage.md)
* [Altre informazioni sull'API per gli eventi e le metriche personalizzati](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Video


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Passaggi successivi
* [Tenere traccia dell'utilizzo](app-insights-web-track-usage.md)
* [Metriche ed eventi personalizzati](app-insights-api-custom-events-metrics.md)
* [Build-measure-learn](app-insights-web-track-usage.md)

