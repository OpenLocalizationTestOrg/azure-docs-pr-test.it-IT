---
title: aaaOverview di Azure Application Insights per DevOps | Documenti Microsoft
description: Informazioni su come toouse Application Insights in un ambiente di sviluppo Ops.
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Panoramica di Application Insights per DevOps

Con [Application Insights](app-insights-overview.md) è possibile capire velocemente le prestazioni dell'app e come viene usata quando è attiva. Se si verifica un problema, è possibile conoscere, consente di valutare l'impatto di hello e consente di determinare la causa hello.

Ecco un account da un team che sviluppa applicazioni web:

* *"Un paio di giorni fa, è stato distribuito un 'piccolo' aggiornamento rapido. È Impossibile eseguire passi del test ampie, ma purtroppo alcune modifiche imprevisto sono state unite nel payload hello, causando l'incompatibilità tra hello estremità anteriore e posteriore. Immediatamente, viene generato l'avviso sono aumentate di eccezioni di server, e ci siamo a conoscenza di situazione hello. Pochi clic lontano nel portale Application Insights hello, abbiamo informazioni sufficienti da toonarrow stack di chiamate di eccezione del problema hello. Abbiamo rollback immediatamente e hello danni limitati. Application Insights ha reso questa parte della devops hello ciclo molto semplice e utilizzabili."*

In questo articolo si seguirà un team di Fabrikam Bank che sviluppa hello online banking online toosee di sistema (OBS) il relativo utilizzo tooquickly Application Insights rispondere toocustomers e apportare aggiornamenti.  

viene eseguita dal team di Hello in un ciclo DevOps illustrato nella seguente figura hello:

![Ciclo DevOps](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

I requisiti passano nel backlog di sviluppo (elenco attività). In breve, funzionano sprint, che offrono spesso un software di lavoro - in genere sotto forma di hello di miglioramenti ed estensioni toohello applicazione esistente. applicazione in tempo reale Hello viene aggiornato di frequente con nuove funzionalità. Mentre è in tempo reale, il team di hello esegue monitoraggio per le prestazioni e l'utilizzo con l'aiuto di hello di Application Insights. Questi dati APM riconducono al loro backlog di sviluppo.

team Hello utilizza l'applicazione web in tempo reale di Application Insights toomonitor hello strettamente per:

* Prestazioni. Desiderano toounderstand come tempi di risposta variano con numero di richieste; quanto più CPU, rete, disco e altre risorse in uso; e in cui sono colli di bottiglia hello.
* Errori. Se esistono eccezioni richieste non riuscite o se un contatore delle prestazioni viene portato non rientra nell'intervallo familiarità, hello team esigenze tooknow rapidamente in modo che è possibile eseguire azioni.
* Utilizzo. Ogni volta che viene rilasciata una nuova funzionalità, team hello desidera tooknow toowhat misura viene utilizzata e indica se gli utenti hanno difficoltà con esso.

Concentriamoci sulla parte di commenti e suggerimenti hello del ciclo di hello:

![Rilevare-Valutare-Diagnosticare](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Rilevare scarsa disponibilità
Marcela Markova è uno sviluppatore senior team OBS hello e accetta hello lead al monitoraggio delle prestazioni in linea. Imposta alcuni [test di disponibilità](app-insights-monitor-web-app-availability.md):

* Un test URL singolo per la pagina principale hello per le app di hello, http://fabrikambank.com/onlinebanking/. Imposta i criteri del codice HTTP 200 e il testo 'Benvenuto'. Se il test ha esito negativo, ci sono problemi gravi con rete hello o server hello o potrebbe essere un problema di distribuzione. (O un utente è stato modificato hello benvenuto! messaggio nella pagina di hello evitando proprio noti.)
* Un test più approfondito in più passaggi, che registra e ottiene un elenco di account corrente, che verifica alcuni dettagli chiave in ogni pagina. Questo test verifica che database di account toohello collegamento hello funziona. Usa un id cliente fittizio: alcuni vengono mantenuti a scopo di test.

Con questi test impostare Marcela è sicuro che Team hello conosceranno rapidamente qualsiasi interruzione.  

Gli errori visualizzati come punti rossi nel grafico del test web hello:

![Visualizzazione dei test web che hanno eseguito su hello precedente](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Ma soprattutto, un avviso per eventuali errori viene inviato tramite posta elettronica toohello team di sviluppo. In tal modo, sono preliminari su di esso quasi tutti i clienti di hello.

## <a name="monitor-performance"></a>Monitorare le prestazioni
Nella pagina Panoramica hello in Application Insights è un grafico che mostra una vasta gamma di [metriche chiave](app-insights-web-monitor-performance.md).

![Alcuni criteri di misurazione](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Il tempo di caricamento della pagina del browser deriva dai dati di telemetria inviati direttamente dalle pagine Web. Tempo di risposta server, il numero di richieste di server e il numero di richieste non riuscite vengono tutti misurate in server web hello e inviati tooApplication informazioni da lì.

Marcela è leggermente in questione con graph di risposta server hello. Questo grafico mostra il tempo medio di hello tra quando server hello riceve una richiesta HTTP da un browser, e restituisce quando la risposta hello. Non è insolito toosee una variazione in questo grafico, in base alla variazione carico sul sistema hello. Ma in questo caso, ci toobe una correlazione tra small maggiore hello numero di richieste e grande aumenta nel tempo di risposta hello. Che potrebbe indicare che il sistema hello opera solo limiti.

Apre i grafici hello server:

![Alcuni criteri di misurazione](./media/app-insights-detect-triage-diagnose/06.png)

Non ci toobe alcun segno di risorse insufficienti, in modo maybe hello salti nei grafici di risposta server hello sono solo una coincidenza.

## <a name="set-alerts-toomeet-goals"></a>Impostare gli avvisi toomeet obiettivi
Tuttavia, vuole tookeep sotto controllo per i tempi di risposta hello. Se si verificano troppo elevati, desiderate tooknow informazioni immediatamente.

Quindi imposta un [avviso](app-insights-metrics-explorer.md) se i tempi di risposta sono superiori alla soglia tipica. Questo le consentirà di conoscere la velocità dei tempi di risposta.

![Pannello Aggiungi avviso](./media/app-insights-detect-triage-diagnose/07-alerts.png)

È possibile impostare avvisi su svariate altre metriche. Ad esempio, è possibile ricevere messaggi di posta elettronica se la memoria disponibile hello diventa bassa o del numero di eccezioni hello diventa elevato o se è presente un picco nelle richieste del client.

## <a name="stay-informed-with-smart-detection-alerts"></a>Rimanere aggiornati con gli avvisi di rilevamento intelligente
Il giorno successivo arriva un avviso in posta elettronica da Application Insights. Ma quando si apre, trova che non è di avviso di tempo di risposta hello che lei impostata. Al contrario, indica che c'è stato un aumento improvviso delle richieste non riuscite, ovvero, delle richieste che hanno restituito 500 o più codici di errore.

Richieste non riuscite sono in cui gli utenti hanno rilevato un errore, in genere dopo un'eccezione generata nel codice hello. Forse viene visualizzato il messaggio "Sorry we couldn't update your details right now" (Non è possibile aggiornare i dettagli adesso). In alternativa, nel peggiore imbarazzante assoluto, un dump dello stack viene visualizzato sullo schermo dell'utente hello, gentilmente server web hello.

Questo avviso è una categoria Sorpresa, perché hello ora dell'ultimo utente esaminata, hello richieste non riuscite conteggio solidi insufficiente. Un numero ridotto di errori è toobe previsto in un server occupato.

Era inoltre un bit di una novità per suo conto perché e non è stato possibile tooconfigure questo avviso. Application Insights include il rilevamento intelligente. Modifica automaticamente modello errore consuete tooyour dell'app e gli errori "viene utilizzato per" in una pagina specifica o in un carico elevato o metriche tooother collegato. Genera un avviso di hello solo se è disponibile un aumento sopra l'oggetto a cui viene fornito tooexpect.

![messaggio di posta elettronica sulla diagnostica proattiva](./media/app-insights-detect-triage-diagnose/21.png)

Si tratta di un messaggio di posta elettronica molto utile. Non si limita a generare un avviso, Esegue una notevole quantità di valutazione hello e attività di diagnostica, troppo.

Mostra il numero di clienti coinvolti e le pagine Web o le operazioni. Marcela può decidere se è necessario tooget hello tutto il team lavorando su questo come un antincendio o se può essere ignorato fino a quando la settimana prossima.

messaggio di posta elettronica Hello Mostra anche che una particolare eccezione si è verificato e - ancora più interessante - errore hello è associata a chiamate non riuscite tooa particolare database. Questo spiega perché errore hello improvvisamente è presente anche se il team del Marcela non è stato distribuito recente eventuali aggiornamenti.

Guida di hello Marcella ping del team di database hello in base a questo messaggio di posta elettronica. Lei apprende che essi rilasciato un aggiornamento rapido in hello ultimi mezz'ora; e non potrebbe essere presente una modifica dello schema secondario...

Così il problema di hello è sul toobeing modo hello fissata, anche prima di analizzare i log ed entro 15 minuti di esso derivanti. Marcela fa clic sul collegamento di hello tooopen Application Insights. Si apre direttamente in una richiesta non riuscita e individuare il database non riuscito chiamare hello elenco di chiamate a dipendenze.

![richiesta non riuscita](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Rilevare le eccezioni
Con una minima del programma di installazione, [eccezioni](app-insights-asp-net-exceptions.md) vengono automaticamente segnalate tooApplication Insights. È possibile anche acquisito in modo esplicito mediante l'inserimento di chiamate troppo[trackexception () effettuate](app-insights-api-custom-events-metrics.md#trackexception) nel codice hello:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


il team di Fabrikam Bank Hello si è evoluto pratica hello di sempre l'invio di dati di telemetria di un'eccezione, a meno che non vi è un ripristino ovvio.  

In realtà, la strategia è ancora più ampia rispetto a quello: inviano i dati di telemetria in ogni caso in cui si sentono frustrati i dati cliente di hello volevano toodo, se corrisponde tooan eccezione nel codice hello o non. Ad esempio, se il sistema di trasferimento Inter-bank esterna hello restituisce un messaggio "Impossibile completare l'operazione" per ragioni operative (nessun errore di cliente hello) quindi consentono di tenere traccia dell'evento.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException infatti tooreport utilizzati eccezioni invia una copia dello stack hello. TrackEvent è tooreport utilizzati altri eventi. È possibile collegare le proprietà che potrebbero essere utili nella diagnosi.

Eccezioni e gli eventi visualizzati nella hello [ricerca diagnostica](app-insights-diagnostic-search.md) blade. È possibile analizzare le proprietà aggiuntive di toosee hello e traccia dello stack.

![Nella ricerca di diagnostica, utilizzare i filtri tooshow particolari tipi di dati](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Monitorare in modo proattivo
Marcela non resta ferma in attesa di avvisi. Dopo ogni ridistribuzione, prende in considerazione [tempi di risposta](app-insights-web-monitor-performance.md) - entrambi hello figura complessiva e conta tabella hello di richieste più lente, nonché l'eccezione.  

![Grafico dei tempi di risposta e griglia dei tempi di risposta del server.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

È possibile valutare effetto sulle prestazioni di hello di ogni distribuzione, in genere il confronto di ultima settimana con hello. Se è presente un improvviso aggravi, che lei genera con gli sviluppatori rilevanti hello.

## <a name="triage-issues"></a>Problemi di valutazione
La valutazione - valutazione gravità hello ed extent di un problema, è innanzitutto hello dopo il rilevamento. Dovremmo si richiamano team hello a mezzanotte? Oppure può essere lasciato fino al successivo gap pratico di hello nel backlog hello? Esistono alcune domande fondamentali nella valutazione.

La frequenza con cui è il problema? grafici di Hello nel pannello della panoramica hello assegnare problemi tooa prospettiva. Ad esempio, Fabrikam applicazione hello generati avvisi di test web quattro una notte. Osservando il grafico hello mattino hello, team hello visualizzare che non vi sono effettivamente alcuni punti rossi, se ancora la maggior parte dei test hello fosse verde. Drill-down grafico disponibilità hello, era chiaro che tutti questi problemi intermittenti erano dal percorso di un test. La situazione era ovviamente dovuta a un problema di rete che interessava solo una route e molto probabilmente si sarebbe risolta automaticamente da sola.  

Al contrario, un aumento significativo e stabile nel grafico hello del conteggio delle eccezioni o tempi di risposta è ovviamente toopanic su.

Una tattica di valutazione utile è fare una prova in prima persona. Se si verificano hello stesso problema, si saprà sia reale.

La frazione degli utenti sono interessati? tooobtain una risposta approssimativa, dividere il tasso di esiti negativi hello per il numero di sessioni di hello.

![Grafici delle sessioni e richieste non riuscite](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Quando sono presenti una risposta lenta, è possibile confrontare tabella hello di richieste più lente risponde con una frequenza di utilizzo di hello di ogni pagina.

Il livello di importanza è uno scenario di hello bloccato? Se si tratta di un problema funzionale che blocca una storia utente specifica, chiedersi quanto è importante. Se i clienti non possono pagare le fatture, si tratta di un problema grave. Se non è possibile modificare le preferenze di colore dello schermo, è un problema non urgente. salve dettagli dell'evento hello o dell'eccezione o identità hello della pagina lento hello, indica dove i clienti riscontrano problemi.

## <a name="diagnose-issues"></a>Diagnosticare i problemi
Diagnosi non è abbastanza hello stesso modo del debug. Prima si avvia la traccia tramite codice hello, è necessario avere un'idea approssimativa dei motivi per cui, dove e quando si verifica il problema di hello.

**Quando può verificarsi?**  visualizzazione cronologici di hello fornita da grafici di evento e metrica hello rende facile toocorrelate effetti con le possibili cause. Se sono presenti picchi intermittenti nella velocità di risposta tempo o di un'eccezione, esaminare il numero di richieste di hello: se picco hello stesso tempo, quindi simile a un problema di risorse. È necessario tooassign più CPU o memoria? O è una dipendenza che non è possibile gestire il carico hello?

**Dipende da chi?**  Se si dispone di un calo improvviso delle prestazioni di un determinato tipo di richiesta - ad esempio quando hello cliente vuole raggiungere un estratto conto, quindi è possibile potrebbe essere un sottosistema esterno anziché all'applicazione web. In Esplora metriche, selezionare il numero di errori di dipendenza hello e di tariffe di durata delle dipendenze e confrontare le cronologie su hello oltre ad alcune ore o giorni con il database è stato rilevato un problema hello. Se vi sono correlazione delle modifiche, un sottosistema esterno potrebbe essere tooblame.  

![Grafici di errore di dipendenza e la durata delle chiamate toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Alcuni problemi di dipendenza lenta sono problemi di georilevazione. La banca Fabrikam usa macchine virtuali di Azure e ha scoperto che aveva inavvertitamente posizionato i server Web e di account in paesi diversi. Si è avuto un notevole miglioramento con la migrazione di uno dei server.

**Che cosa è successo?** Se non è presente una dipendenza toobe problema hello e se non è sempre presente, è probabilmente provocato da una modifica recente. Hello cronologico prospettiva fornita dai grafici di metrica ed evento hello rende facile toocorrelate eventuali modifiche improvvise con le distribuzioni. Che consente di limitare la ricerca hello per problema hello.

**Cosa sta succedendo?** Alcuni problemi si verificano solo raramente e possono essere difficile tootrack verso il basso eseguendo i test non in linea. È possibile eseguire questa operazione è bug di hello toocapture tootry quando si verifica in tempo reale. È possibile esaminare il dump dello stack hello nei report di eccezione. Inoltre, è possibile scrivere le chiamate di traccia, con il framework di registrazione preferito o con TrackTrace() o TrackEvent().  

Fabrikam ha un problema intermittente con i trasferimenti tra conti, ma solo con determinati tipi di conti. toounderstand migliori Qual era il problema, vengono inserite le chiamate a tracktrace () presenti in punti chiavi nel codice hello, associare il tipo di account hello come una chiamata di tooeach proprietà. Questo è stato facile toofilter out solo le tracce in ricerca di diagnostica. I nodi collegati anche i valori dei parametri come chiamate di traccia toohello proprietà e le misure.

## <a name="respond-toodiscovered-issues"></a>Rispondere toodiscovered problemi
Una volta che è stato: identificato problema hello, è possibile apportare toofix un piano è. Forse è necessario tooroll nuovamente una modifica recente oppure potrebbe essere possibile proseguiamo e correggerlo. Al termine, correzione hello Application Insights indica se ha avuto esito positivo.  

Il team di sviluppo della banca Fabrikam richiedere una misura tooperformance approccio più strutturata rispetto toobefore utilizzati Application Insights.

* Nella pagina Panoramica di Application Insights hello impostano obiettivi in termini di misure specifiche.
* Progettano le misurazioni di prestazioni in un'applicazione hello dall'inizio di hello, ad esempio le metriche di hello di misurano lo stato di avanzamento utente tramite 'grafici a imbuto.'  


## <a name="monitor-user-activity"></a>Monitorare l'attività dell'utente
Quando il tempo di risposta è valido in modo coerente e vi sono alcune eccezioni, è possibile spostare team di sviluppo hello in toousability. Si pensi come tooimprove hello esperienza degli utenti, e come tooencourage hello di tooachieve ulteriori utenti desiderato obiettivi.

Application Insights può essere anche usato toolearn degli utenti a cui si con un'applicazione. Una volta che viene eseguito senza problemi, team hello sarebbe tooknow quali funzionalità sono hello più diffuso, quali gli utenti come o avere problemi e la frequenza con cui tornare. Tali informazioni consentiranno di stabilire le priorità relative al lavoro imminente. E poter pianificare come parte del ciclo di sviluppo hello successo hello toomeasure di ogni funzionalità. 

Ad esempio, un proprio processo utente tipico tramite sito web hello ha un chiaro "a imbuto." Molti clienti considerano in base alle tariffe di tipi diversi di prestito hello. Un numero inferiore andare toofill nel modulo offerta hello. Di quelle che ottengono una citazione, alcuni proseguiamo e diamo out prestito hello.

![Numero di visualizzazioni della pagina](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Considerando in entrata hello un numero maggiore di clienti, business hello possibile scoprire come tooget più utenti tramite toohello fondo hello a imbuto. In alcuni casi, potrebbe esserci un errore dell'esperienza utente: ad esempio, il pulsante 'Avanti' hello è toofind disco rigido o istruzioni hello non sono evidenti. Più probabilmente, sono presenti più significativi motivi aziendali per drop-out: forse hello prestito rientrino troppo elevato.

Qualsiasi motivo, hello dati hello consentono hello team di risolvere svolte dagli utenti. Rilevamento di altre chiamate può essere inserito toowork ulteriori dettagli. Trackevent può essere utilizzato toocount tutte le azioni utente, da dettaglio hello di fa clic sul pulsante singoli, toosignificant obiettivi, ad esempio estinzione un prestito.

team Hello stanno toohaving utilizzato informazioni sulle attività degli utenti. Attualmente, quando progetta una nuova funzionalità, valuta in che modo potrà ricevere commenti e suggerimenti sull'utilizzo. Progettano chiamate di rilevamento nella funzionalità hello dall'inizio hello. Usano funzionalità hello tooimprove commenti e suggerimenti di hello in ogni ciclo di sviluppo.

[Altre informazioni sul monitoraggio dell'utilizzo](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Applicare il ciclo di DevOps hello
Si tratta come un team di usare Application Insights toofix non solo singoli problemi, ma tooimprove intero ciclo di vita di sviluppo. Si tratta di suggerimenti e idee su come Application Insights può aiutare a gestire le prestazioni delle proprie applicazioni.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi
È possibile iniziare in diversi modi, a seconda delle caratteristiche di hello dell'applicazione. Scegliere l'opzione più adatta:

* [Applicazione Web ASP.NET](app-insights-asp-net.md)
* [Applicazione Web Java](app-insights-java-get-started.md)
* [Applicazione Web Node.js](app-insights-nodejs.md)
* App già distribuite, ospitate in [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md) o [Azure](app-insights-azure.md).
* [Pagine Web](app-insights-javascript.md) -applicazione a pagina singola o pagina web comune - usare questo autonomamente o in aggiunta tooany hello opzioni del server.
* [Test disponibilità](app-insights-monitor-web-app-availability.md) tootest l'app da hello rete internet pubblica.
