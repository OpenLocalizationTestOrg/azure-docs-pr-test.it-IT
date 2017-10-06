---
title: Rilevamento - anomalie aaaSmart | Documenti Microsoft
description: "Application Insights esegue un'analisi intelligente dei dati di telemetria dell'app e segnala potenziali problemi. Questa funzionalità non richiede alcuna configurazione."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Rilevamento intelligente - anomalie nelle prestazioni

[Application Insights](app-insights-overview.md) automaticamente consente di analizzare hello prestazioni dell'applicazione web e visualizza un avviso su potenziali problemi. È possibile che questo messaggio venga letto perché si è ricevuta una delle nostre notifiche di rilevamento intelligente.

Questa funzionalità non richiede alcuna configurazione speciale, ma solo la configurazione dell'app per Application Insights, ovvero in [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md) o [Node.js](app-insights-nodejs.md) e nel [codice della pagina Web](app-insights-javascript.md). È attiva quando l'applicazione genera un numero sufficiente di dati di telemetria.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Ricezione di una notifica di rilevamento intelligente

Application Insights ha rilevato che si sono ridotte hello delle prestazioni dell'applicazione in uno dei modi seguenti:

* **Riduzione di tempo di risposta** -avviata risponde toorequests più lento rispetto a viene utilizzato per l'app. modifica di Hello potrebbe essere state rapida, ad esempio perché si è verificato nella distribuzione più recente una regressione. Oppure potrebbe essere stata graduale, probabilmente causata da una perdita di memoria. 
* **Riduzione di durata dipendenza** -app effettua chiamate API REST di tooa, database o altre dipendenze. dipendenza Hello risponde più lento rispetto a in passato.
* **Modello di riduzione delle prestazioni** -l'app viene visualizzata toohave delle prestazioni problema interessa solo alcune richieste. Ad esempio, le pagine si caricano molto più lentamente su un tipo di browser rispetto ad altri oppure le richieste vengono eseguite molto più lentamente da un server specifico. Attualmente, gli algoritmi esaminano i tempi di caricamento delle pagine, i tempi di risposta delle richieste e i tempi di risposta delle dipendenze.  

Rilevamento intelligente richiede almeno 8 giorni di dati di telemetria relativi a un volume utilizzabile in ordine tooestablish una linea di base di prestazioni normali. Pertanto, dopo l'esecuzione dell'applicazione per tale periodo, qualsiasi problema significativo comporterà una notifica.


## <a name="does-my-app-definitely-have-a-problem"></a>Verifica di eventuali problemi dell'app

Una notifica non significa che l'app ha sicuramente un problema. È semplicemente un suggerimento su un elemento che potrebbe essere necessario toolook in più da vicino.

## <a name="how-do-i-fix-it"></a>Risoluzione

le notifiche di Hello includono informazioni di diagnostica. Ad esempio:


![Di seguito è riportato un esempio di rilevamento della riduzione del tempo di risposta del server](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Valutazione**. notifica Hello Mostra il numero di utenti o quante operazioni sono interessate. Ciò consente di assegnare un problema di toohello priorità.
2. **Ambito**. Problema di hello interessa tutto il traffico o solo alcune pagine? È it limitato tooparticular browser o le posizioni? Queste informazioni possono essere ottenute dalla notifica hello.
3. **Diagnosi**. Spesso, le informazioni di diagnostica hello nella notifica hello suggerirà natura hello del problema in hello. Ad esempio, se il tempo di risposta diminuisce quando la frequenza delle richieste è elevata, questo suggerisce che il server o le dipendenze sono sovraccariche. 

    In caso contrario, aprire Pannello prestazioni hello in Application Insights. Qui sono contenuti i dati del [Profiler](app-insights-profiler.md). Se vengono generate eccezioni, è anche possibile provare hello [debugger snapshot](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>Configurare le notifiche tramite posta elettronica

Smart notifiche rilevamento siano abilitate per impostazione predefinita e inviate toothose che dispongono di [i proprietari, collaboratori e lettori di accedere a risorsa di Application Insights toohello](app-insights-resources-roles-access-control.md). toochange questa operazione, fare clic su **configura** in hello notifica tramite posta elettronica o le impostazioni di rilevamento Smart in Application Insights. 
  
  ![Impostazioni di rilevamento intelligente](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * È possibile utilizzare hello **annullare la sottoscrizione** collegamento hello rilevamento intelligente posta elettronica toostop la ricezione di notifiche di posta elettronica hello.

Messaggi di posta elettronica su anomalie rilevamenti Smart sono limitate tooone posta elettronica al giorno per ogni risorsa di Application Insights. messaggio di posta elettronica Hello verrà inviato solo se è presente almeno un nuovo problema rilevato in tale giorno. senza alcuna ripetizione dello stesso messaggio. 

## <a name="faq"></a>domande frequenti

* *Il servizio implica l'accesso manuale ai dati da parte di Microsoft?*
  * No. servizio Hello è completamente automatico. Solo ricevere le notifiche di hello. ma i dati restano [privati](app-insights-data-retention-privacy.md).
* *Si analizza tutti i dati di hello raccolti da Application Insights?*
  * Attualmente no. Al momento vengono analizzati il tempo di risposta alla richiesta, il tempo di risposta della dipendenza e il tempo di caricamento della pagina. L'analisi delle metriche aggiuntive si trova nel backlog futuro.

* Per quali tipi di applicazione funziona?
  * Questi cali vengono rilevati in qualsiasi applicazione che genera i dati di telemetria hello appropriato. Se Application Insights è stata installata nell'app Web, le richieste e le dipendenze vengono rilevate automaticamente. Ma in servizi back-end o altre App, se è stata inserita chiamate troppo[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) o [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), rilevamento intelligente funzionerà in hello stesso modo.

* *Si possono creare regole personalizzate di rilevamento delle anomalie o personalizzare le regole esistenti?*

  * Non ancora, ma è possibile:
    * [Impostare avvisi](app-insights-alerts.md) per essere informati quando una determinata metrica supera una soglia.
    * [Esportare i dati di telemetria](app-insights-export-telemetry.md) tooa [database](app-insights-code-sample-export-sql-stream-analytics.md) o [tooPowerBI](app-insights-export-power-bi.md), in cui è possibile analizzarli manualmente.
* *La frequenza con cui viene eseguita l'analisi di hello?*

  * È hello analisi eseguita quotidianamente sui dati di telemetria hello da hello giorno precedente (giorno completo nel fuso orario UTC).
* *Ciò sostituisce [gli avvisi delle metriche](app-insights-alerts.md)?*
  * No.  È non impegnare toodetecting ogni comportamento da prendere in considerazione anomala.


* *Se non eseguire alcuna operazione nella risposta tooa notifica, viene visualizzato un promemoria?*
  * No, il messaggio relativo a un singolo problema viene ricevuto una sola volta. Se il problema hello persiste verrà aggiornato in hello che rilevamento intelligente feed pannello.
* *Ho perso la posta elettronica hello. Dove trovare le notifiche di hello nel portale di hello?*
  * In panoramica di Application Insights hello dell'app, fare clic su hello **rilevamento Smart** riquadro. Vi sarà toofind in grado di che eseguire il backup di tutte le notifiche di too90 giorni.

## <a name="how-can-i-improve-performance"></a>In che modo è possibile migliorare le prestazioni?
Le risposte lente e sono una delle proprie frustrazioni principali hello per gli utenti del sito web, come descritto in precedenza la propria esperienza. In tal caso, è importante tooaddress hello problemi.

### <a name="triage"></a>Valutazione
Occorre prima di tutto stabilire l'impatto del problema. Se una pagina è sempre tooload lento, ma solo l'1% di utenti del sito dovesse toolook la, forse toothink aspetti più importanti è disponibile su. In hello invece se solo aprire % 1 di utenti, ma genera eccezioni ogni volta, il che potrebbe essere utile esaminare.

Utilizzare l'istruzione di impatto hello, gli utenti interessati o % del traffico, come guida generale, ma tenere presente che non si tratta tutto hello. Raccogliere altri tooconfirm evidenza.

Prendere in considerazione i parametri di hello del problema hello. Se dipende dall'area geografica, configurare [test di disponibilità](app-insights-monitor-web-app-availability.md) che includono quell'area: è possibile che si stiano semplicemente verificando problemi di rete nell'area specifica.

### <a name="diagnose-slow-page-loads"></a>Diagnosi dei caricamenti lenti delle pagine
Dove è il problema di hello? È hello server lenta toorespond, pagina hello molto lunghi o browser hello ha toodo una grande quantità di lavoro toodisplay è?

Aprire Pannello metriche di hello browser. Hello segmentata visualizzazione del browser pagina carico ora viene visualizzato in cui si sta ora hello. 

* Se **Invia ora richiesta** è elevato, uno dei due server hello risponde lentamente o richiesta di hello è una richiesta post con una grande quantità di dati. Esaminare hello [le metriche delle prestazioni](app-insights-web-monitor-performance.md#metrics) tooinvestigate tempi di risposta.
* Impostare [tenere traccia delle dipendenze](app-insights-asp-net-dependencies.md) toosee se ciò hello è scadenza tooexternal servizi o il database.
* Se il valore **Tempo per la ricezione della risposta** è predominante, la pagina e le relative parti dipendenti, ovvero JavaScript, CSS, immagini e così via (ma non i dati caricati in modo asincrono) sono molto lunghe. Impostare un [test disponibilità](app-insights-monitor-web-app-availability.md), e che tooset hello opzione tooload parti. Quando si ottengono alcuni risultati, aprire dettagli hello di un risultato ed espanderlo hello toosee tempi di diversi file di caricamento.
* Un valore elevato per **Tempo di elaborazione client** indica che l'esecuzione degli script è lenta. Se non è ovvio motivo hello, considerare l'aggiunta di codice di temporizzazione e inviare volte hello nelle chiamate a trackMetric.

### <a name="improve-slow-pages"></a>Migliorare le pagine lente
È un sito web completo dei suggerimenti su come migliorare le risposte del server e i tempi di caricamento pagina, in modo non verrà tentato toorepeat tutti qui. Di seguito sono riportati alcuni suggerimenti che è probabilmente già conoscere, tooget solo si pensa:

* Lenta durante il caricamento a causa di file di grandi dimensioni: hello script e altre parti di carico in modo asincrono. Usare la creazione di bundle di script. Interruzione di pagina principale di hello in widget che carica i relativi dati separatamente. Non inviare HTML precedente semplice per le tabelle lungo: utilizzare un script toorequest hello dati come JSON o un altro formato compact, quindi compilare la tabella hello sul posto. Esistono toohelp Framework grande tutte. Per semplificare queste operazioni, sono disponibili utili framework, che ovviamente includono script di grandi dimensioni.
* Rallentamento delle dipendenze del server: considerare hello posizioni geografiche dei componenti. Ad esempio, se si usa Azure, assicurarsi hello web e database di hello risiedono in hello stessa area. Le query recuperano una quantità di informazioni superiore al necessario? La memorizzazione nella cache o l'invio in batch possono essere utili?
* Problemi di capacità: esaminare le metriche server hello dei tempi di risposta e i conteggi delle richieste. Se i picchi dei tempi di risposta non sono proporzionati ai picchi del numero di richieste, è probabile che le capacità dei server siano insufficienti.


## <a name="server-response-time-degradation"></a>Riduzione del tempo di risposta del server

notifica degradazione tempo di risposta Hello indica:

* tempo di risposta Hello confrontati toonormal tempo di risposta per questa operazione.
* Il numero di utenti interessati.
* Tempo medio di risposta e tempi di risposta 90 ° percentile per l'operazione nel giorno hello di rilevamento hello e sette giorni prima. 
* Numero di richieste di questa operazione giorno hello di rilevamento hello e sette giorni prima.
* La correlazione tra la riduzione in questa operazione e le riduzioni nelle relative dipendenze. 
* Consente di diagnosticare il problema di hello toohelp di collegamenti.
  * Profiler tracce toohelp è visualizzare dove viene impiegato il tempo di funzionamento (collegamento hello è disponibile se sono stati raccolti gli esempi di traccia di Profiler per questa operazione durante il periodo di rilevamento hello). 
  * I report di prestazioni in Metric Explorer (Esplora metriche), in cui è possibile suddividere e ripartire filtri/intervalli di tempo per questa operazione.
  * Ricerca per questo chiama tooview proprietà chiamate specifiche.
  * Segnala un errore, se count > 1, questo significa che si sono verificati errori in questa operazione che potrebbe aver contribuito tooperformance riduzione.

## <a name="dependency-duration-degradation"></a>Riduzione della durata delle dipendenze

Un'applicazione moderna adottare più approccio di progettazione di servizi micro, ottenendo in molti casi l'affidabilità tooheavy i servizi esterni. Ad esempio, se l'applicazione si basa sulla piattaforma alcuni dati o anche se si crea la propria bot service è probabilmente inoltrerà su alcuni tooenable di provider di servizi cognitivi il toointeract Bot in modi più risorse umani e alcuni dati di servizio per hello toopull bot archiviano risposte da.  

Esempio di notifica di riduzione delle dipendenze:

![Di seguito è riportato un esempio di rilevamento della riduzione della durata delle dipendenze](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Le informazioni fornite includono:

* durata Hello confrontati toonormal tempo di risposta per questa operazione
* Il numero di utenti interessati
* Durata media e durata a 90 percentile per questa dipendenza nel giorno hello del rilevamento hello e sette giorni prima
* Numero di dipendenze chiamate giorno hello del rilevamento hello e sette giorni prima
* Consente di diagnosticare il problema di hello toohelp di collegamenti
  * I report delle prestazioni in Metric Explorer (Esplora metriche) per questa dipendenza
  * Ricerca di questa dipendenza chiama tooview proprietà chiamate
  * I rapporti errore - se count > 1, questo significa che non vi sono la dipendenza viene chiamato durante il rilevamento di hello periodo che potrà aver contribuito tooduration riduzione. 
  * Aprire l'Analisi con le query che consentono di calcolare la durata e il numero delle dipendenze  

## <a name="smart-detection-of-slow-performing-patterns"></a>Rilevamento intelligente dei modelli di esecuzione lenta 

Application Insights rileva i problemi di prestazioni che potrebbero riguardare solo alcuni utenti o che riguardano gli utenti solo in alcuni casi. Ad esempio, le notifiche relative al caricamento più lento delle pagine su un tipo di browser rispetto ad altri o se le richieste vengono eseguite più lentamente da un server specifico. È anche possibile rilevare problemi legati alle combinazioni di proprietà, ad esempio caricamenti lenti della pagine in un'area geografica per clienti che usano un particolare sistema operativo.  

Anomalie questi sono molto difficile toodetect semplicemente esaminando i dati di hello, ma sono più comuni di si potrebbe pensare. Spesso emergono solo quando i clienti si lamentano. Da quel momento, è troppo tardi: gli utenti interessato hello già passa concorrenti tooyour!

Attualmente, il nostro algoritmi osservare tempi di caricamento pagina, tempi di risposta richiesta server hello e tempi di risposta delle dipendenze.  

Non dispone di una o più soglie tooset o configurare le regole. Machine learning e algoritmi di data mining sono modelli anomali toodetect utilizzato.

![Avviso di posta elettronica hello, fare clic su hello collegamento tooopen hello report di diagnostica in Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Quando** Mostra è stato rilevato hello ora hello problema.
* In **Informazioni approfondite** vengono visualizzate le informazioni seguenti:

  * problema di Hello che è stato rilevato;
  * caratteristiche di Hello di hello set di eventi che è stato trovato il comportamento di problema hello visualizzato.
* tabella Hello Confronta set scarse hello con hello Media di tutti gli altri eventi.

Scegliere report rilevanti, filtrati su tempo hello e proprietà di hello lenta esecuzione set hello collegamenti tooopen Explorer metrica e la ricerca.

Modificare hello ora intervallo e i filtri tooexplore hello telemetria.

## <a name="next-steps"></a>Passaggi successivi
Questi strumenti di diagnostica consentono di controllare la telemetria hello dall'app:

* [Profiler](app-insights-profiler.md) 
* [Debugger di snapshot](app-insights-snapshot-debugger.md)
* [Analisi](app-insights-analytics-tour.md)
* [Diagnostica intelligenti di Analisi](app-insights-analytics-diagnostics.md)

Gli avvisi di rilevamento intelligente sono completamente automatici, Ma forse si vogliono tooset di alcune ulteriori avvisi?

* [Configurare manualmente gli avvisi relativi alle metriche](app-insights-alerts.md)
* [Test Web di disponibilità](app-insights-monitor-web-app-availability.md)
