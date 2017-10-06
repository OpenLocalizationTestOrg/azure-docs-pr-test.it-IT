---
title: il monitoraggio delle prestazioni dell'applicazione sul aaaWeb - Azure Application Insights | Documenti Microsoft
description: Inserimento in hello devOps ciclo di Application Insights
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Diagnostica completa per servizi e app Web con Application Insights
## <a name="why-do-i-need-application-insights"></a>Funzione di Application Insights
Application Insights consente di monitorare l'app Web in esecuzione, segnalando errori e problemi di prestazioni e aiutando ad analizzare l'utilizzo dell'app da parte dei clienti. Funzionamento delle App in esecuzione su più piattaforme (ASP.NET, J2EE, Node.js,...) ed è ospitato in hello Cloud o locale. 

![Aspetti di complessità hello di offrire le app web](./media/app-insights-devops/010.png)

È essenziale toomonitor una moderna applicazione mentre è in esecuzione. In particolare, si desidera toodetect errori prima di eseguire la maggior parte dei clienti. Inoltre, desidera toodiscover e risolvere i problemi di prestazioni che, mentre non è irreversibile, ad esempio rallentano oppure alcuni inconvenienti tooyour utenti. E se il sistema hello esegue tooyour soddisfazione, si desidera tooknow degli utenti a cui hello eseguono con esso: sono funzionalità più recenti hello? e se stanno traendo vantaggio dal programma.

Applicazioni web moderne vengono sviluppate in un ciclo di recapito continuo: rilasciata una nuova funzionalità o miglioramento osservare l'accuratezza funziona per gli utenti di hello; pianificare successivo incremento di hello di sviluppo in base a tali informazioni. Una parte fondamentale del ciclo è fase di osservazione hello. Application Insights fornisce hello strumenti toomonitor un'applicazione web per l'utilizzo e delle prestazioni.

Hello più importante di questo processo è diagnosi e diagnostica. Se un'applicazione hello ha esito negativo, quindi business viene persa. ricevere notifiche immediatamente, toopresent che con informazioni hello necessari problema hello toodiagnose Hello ruolo principale di un framework di monitoraggio è pertanto toodetect errori in modo affidabile. Application Insights permette di fare esattamente questo.

### <a name="where-do-bugs-come-from"></a>Da dove provengono i bug?
Gli errori nei sistemi Web sono in genere causati da problemi di configurazione o difetti nell'interazione fra i numerosi componenti. Hello prima attività quando un evento imprevisto del sito in tempo reale di affrontare è pertanto luogo hello tooidentify del problema hello: il componente o una relazione è causa di hello?

I professionisti di più lunga data ricorderanno quando ogni programma informatico veniva eseguito in un solo computer. gli sviluppatori di Hello sarebbero testarla accuratamente prima di distribuirlo; e con fornito, sarebbe raramente vedere o riprovare su di esso. gli utenti di Hello avrebbe tooput bug residuo hello molti anni. 

Ora è cambiato tutto. L'applicazione ha moltissime toorun dispositivi diversi, e può essere difficile tooguarantee hello stesso comportamento su ciascuna di esse. Hosting di App nel cloud hello significa quali possono essere corretti veloce, ma anche continua la concorrenza e hello previsione delle nuove funzionalità a intervalli frequenti. 

In queste condizioni, hello solo modo tookeep di che un controllo confermato il numero di bug hello viene automatizzato unit test. Sarebbe toomanually verificare nuovamente tutti gli elementi in ogni recapito. Unit test è ora il processo di compilazione di una parte comune di hello. Strumenti, ad esempio hello Xamarin Test Cloud aiutano fornendo automatizzati dell'interfaccia utente test su più versioni di browser. Questi test teorici consentono toohope frequenza hello di bug trovati all'interno di un'app è possibile mantenere tooa minimo.

Le applicazioni Web tipiche includono molti componenti live. Aggiunta toohello client (in un'applicazione browser o nel dispositivo) e il server web hello, prevede l'elaborazione back-end sostanziale toobe probabile. Ad esempio back-end hello è una pipeline di componenti o una raccolta di parti di collaborare più blando. Molti di questi non saranno sotto controllo dell'utente, ma servizi esterni da cui dipende tutto.

Nelle configurazioni simili, può essere difficile e uneconomical tootest, o prevede, tutte le modalità di errore possibili, diverso da hello in tempo reale sistema stesso. 

### <a name="questions-"></a>Domande...
Alcune domande da chiedersi durante lo sviluppo di un sistema Web:

* L'app si arresta in modo anomalo? 
* Cosa succede esattamente? -Se non è riuscito di una richiesta, si desidera tooknow come ha ricevuto non esiste. Serve una traccia degli eventi...
* L'app è abbastanza veloce? Quanto tempo occorre toorespond tootypical richieste?
* Carica hello di handle server hello? Quando si aumenta la frequenza hello delle richieste, il tempo di risposta hello ferma?
* Tempi di risposta sono my dipendenze - hello le API REST, i database e altri componenti che chiama l'applicazione. In particolare, se il sistema hello è lento, è il componente o si ottiene una risposta lenta da un altro utente?
* L'app è attiva o bloccata? Possibile può essere visualizzato dal mondo hello? È utile sapere se si arresta...
* Che cos'è una causa principale di hello? Stato errore hello il componente o una dipendenza? Si tratta di un problema di comunicazione?
* Quanti sono gli utenti interessati? Se si hanno più di un problema tootackle, che è più importante hello?

## <a name="what-is-application-insights"></a>Informazioni su Azure Application Insights
![Flusso di lavoro di base di Application Insights](./media/app-insights-devops/020.png)

1. Application Insights Instrumenta app e invia i dati di telemetria su di esso durante l'esecuzione di app hello. È possibile compilare hello Application Insights SDK in app hello oppure è possibile applicare la strumentazione in fase di esecuzione. Hello primo metodo è più flessibile, come è possibile aggiungere i propri moduli normali toohello di telemetria.
2. dati di telemetria Hello viene inviato portale Application Insights toohello, in cui sono stati archiviato ed elaborato. (Pur essendo ospitato in Microsoft Azure, Application Insights consente di monitorare tutte le app Web e non solo le app di Azure.)
3. dati di telemetria Hello viene presentato tooyou in forma di hello di grafici e tabelle di eventi.

Esistono due tipi principali di telemetria: istanze non elaborate e istanze aggregate. 

* I dati delle istanze includono, ad esempio, il report di una richiesta ricevuta da un'app Web. È possibile cercare e controllare i dettagli di hello di una richiesta usando lo strumento di ricerca hello portale Application Insights hello. istanza di Hello potrebbe includere dati, ad esempio per quanto tempo l'app ha impiegato toorespond toohello richiesta, nonché hello URL richiesto, la posizione approssimativa del client hello e altri dati.
* Dati aggregati includono i conteggi di eventi per unità di tempo, in modo che sia possibile confrontare frequenza hello delle richieste con tempi di risposta hello. È inoltre inclusa la media di metriche quali i tempi di risposta alle richieste.

Hello categorie principali di dati sono:

* Richieste tooyour app (in genere richieste HTTP), con i dati su URL, il tempo di risposta e l'esito positivo o negativo.
* Le dipendenze, ovvero le chiamate REST e SQL effettuate dall'app, complete di URI, tempi di risposta ed esiti.
* Le eccezioni, incluse le analisi dello stack.
* Dati della visualizzazione pagina, che provengono da browser degli utenti hello.
* Metriche come i contatori delle prestazioni, nonché metriche scritte manualmente. 
* Eventi personalizzati che è possibile utilizzare gli eventi di business tootrack
* Tracce del log a scopo di debug.

## <a name="case-study-real-madrid-fc"></a>Case study: Real Madrid C.F.
servizio web di Hello [reale Madrid Football Club](http://www.realmadrid.com/) serve circa 450 milioni ventole tutto il mondo hello. Ventole diritti di accesso sia tramite web browser e hello App per dispositivi mobili dell'associazione. non solo per prenotare i biglietti, ma anche per consultare informazioni e guardare clip video sui risultati, i giocatori e le partite in programma. I tifosi possono eseguire ricerche applicando filtri come, ad esempio, il numero di goal segnati. Sono inoltre supporto toosocial collegamenti. esperienza utente Hello altamente personalizzato ed è progettato come le ventole tooengage una comunicazione bidirezionale.

Hello soluzione [è un sistema di servizi e applicazioni in Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). La scalabilità è un requisito essenziale: il traffico è variabile e può raggiungere volumi molto elevati prima, dopo e durante le partite.

Di Madrid, è le prestazioni del sistema hello toomonitor fondamentale. Azure Application Insights offre una visualizzazione completa sistema hello, garantire un livello superiore e affidabile di servizio. 

Hello Club ottiene anche una conoscenza approfondita dei relativi ventole: dove sono (solo 3% sono Spagna), quali interesse hanno lettori, risultati e giochi e la modalità di risposta toomatch risultati.

La maggior parte dei dati di telemetria raccolti automaticamente senza codice aggiunto, semplificato soluzione hello e ridotta complessità operativa.  Per il Real Madrid, Application Insights gestisce ogni mese 3,8 miliardi di punti di telemetria.

Madrid reale Usa hello Power BI modulo tooview i dati di telemetria.

![Visualizzazione di Power BI per Application Insights Telemetry](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Rilevamento intelligente
La [diagnostica proattiva](app-insights-proactive-diagnostics.md) è una funzionalità recente. Senza richiedere configurazioni particolari da parte dell'utente, Application Insights rileva automaticamente gli aumenti atipici nella frequenza degli errori dell'app e fornisce avvisi a tale riguardo. È abbastanza tooignore uno sfondo di guasti occasionali, e anche maggiore che sono semplicemente proporzionale tooa aumento delle richieste. Ad esempio, se si verifica un errore in uno dei servizi di hello che si dipende o se hello nuova build appena distribuito non funziona bene, quindi si saprà su di esso, non appena si osserva la posta elettronica. Saranno inoltre disponibili webhook che consentiranno di attivare altre app.

Un altro aspetto di questa funzionalità consente di eseguire un'analisi approfondita giornaliera dei dati di telemetria, cercando modelli insoliti delle prestazioni disco toodiscover. come un rallentamento delle prestazioni associato a una particolare area geografica oppure a una determinata versione di un browser.

In entrambi i casi, hello avviso indica non soltanto si hello sintomi viene individuato, ma anche fornisce i dati necessari toohelp diagnosi hello problema, ad esempio report eccezioni rilevanti.

![Messaggio di posta dalla diagnostica proattiva](./media/app-insights-devops/030.png)

Ricorda il cliente Samtec: "Ultimamente, durante una migrazione completa delle funzionalità, abbiamo scoperto che un database sottodimensionato stava raggiungendo i limiti di risorse e provocava timeout. È stato trasmesso tramite gli avvisi di rilevamento proattivo letteralmente è durante la valutazione problema hello, molto quasi in tempo reale come annunciato. Questo avviso insieme con gli avvisi di piattaforma Azure hello ci ha consentito di quasi istantaneamente risolvere il problema di hello. Tempo di inattività totale: neanche 10 minuti."

## <a name="live-metrics-stream"></a>Flusso di metriche live
Distribuzione di build più recente di hello può essere un'esperienza pronti. Se sono presenti eventuali problemi, si desidera tooknow su di essi immediatamente, in modo che, se necessario, è possibile annullare. Flusso metriche attive offre le metriche essenziali con una latenza di circa un secondo.

![Metriche attive](./media/app-insights-devops/040.png)

E consente di analizzare immediatamente un campione di errori o eccezioni.

![Eventi di errore live](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Mappa delle applicazioni
Mappa delle applicazioni individua automaticamente la topologia dell'applicazione, layout di informazioni sulle prestazioni di hello in primo luogo, toolet per identificare facilmente i colli di bottiglia delle prestazioni e i flussi problematici in tutto l'ambiente distribuito. Consente le dipendenze dell'applicazione toodiscover nei servizi di Azure. È possibile valutare problema hello da capire se è correlato al codice o dipendenze relative e da un'unica posizione analizza diagnostica correlata esperienza. Ad esempio, l'applicazione potrebbe essersi verificati a causa di una riduzione delle tooperformance livello SQL. Con il mapping di applicazioni, è possibile verificarlo immediatamente e analizzare hello SQL Index Advisor o informazioni dettagliate Query esperienza.

![Mappa delle applicazioni](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Analytics in Application Insights
Con [Analytics](app-insights-analytics.md)è possibile scrivere query arbitrarie in un efficace linguaggio simile a SQL.  La diagnosi nello stack intera app hello diventa semplice come connessione diverse prospettive che è possibile richiedere hello domande corrette toocorrelate le prestazioni del servizio con le metriche di Business e analisi utilizzo software. 

È possibile eseguire una query tutte le metrici dati non elaborati memorizzati nel portale di hello e dell'istanza di dati di telemetria. linguaggio di Hello include filtri, join, aggregazione e altre operazioni. È possibile calcolare i campi ed eseguire analisi statistiche e sono disponibili visualizzazioni grafiche e tabulari.

![Query di Analisi e grafico dei risultati](./media/app-insights-devops/025.png)

Ad esempio, è facile:

* Segmentare i dati sulle prestazioni dal cliente livelli toounderstand l'esperienza di richiesta dell'applicazione.
* Cercare specifici codici di errore o nomi di eventi personalizzati durante l'analisi dei siti attivi.
* Il drill-down nell'utilizzo delle app hello di clienti specifici toounderstand come funzionalità vengono acquisite e adottate.
* Tenere traccia delle sessioni e tempi di risposta per il supporto per tooenable utenti specifici e operazioni team tooprovide cliente immediata.
* Determinare le app usati di frequente funzionalità tooanswer funzionalità priorità domande.

Cliente DNN dichiara: "Application Insights ci ha fornito hello manchi una parte dell'equazione hello per essere in grado di toocombine, ordinamento, query e filtrare i dati in base alle esigenze. Consentendo toouse il nostro team propri toofind un certo livello di esperienza di dati con un linguaggio di query potenti ha consentito toofind approfondimenti e di risolvere i problemi che sapevamo anche si è verificato. Molte delle risposte interessanti provengono da domande hello a partire da *' I computer se... '.*"

## <a name="development-tools-integration"></a>Integrazione di strumenti di sviluppo
### <a name="configuring-application-insights"></a>Configurazione di Application Insights
Visual Studio ed Eclipse dispongono di strumenti tooconfigure hello corretto SDK pacchetti per il progetto hello che si sta sviluppando. Non vi è un tooadd di comando di menu Application Insights.

Se si è verificata tramite un framework di registrazione di traccia, ad esempio Trace, NLog o Log4N toobe, si otterranno hello opzione toosend hello registri tooApplication Insights insieme hello altri dati di telemetria, in modo che è facilmente possibile correlare le tracce di hello con le richieste , chiamate a dipendenze e le eccezioni.

### <a name="search-telemetry-in-visual-studio"></a>Ricercare i dati di telemetria in Visual Studio
Durante lo sviluppo e debug di una funzionalità, è possibile visualizzare e cercare hello telemetria direttamente in Visual Studio, usando hello stesso ricerca strutture come nel portale web hello.

E quando Application Insights si connette un'eccezione, è possibile visualizzare punto dati hello in Visual Studio e passare toohello retta rilevante codice.

![Ricerca di Visual Studio](./media/app-insights-devops/060.png)

Durante il debug, sono disponibili dati di telemetria hello tookeep opzione hello computer di sviluppo, visualizzarlo in Visual Studio, ma senza inviarlo toohello portale. Con l'opzione locale si evita di mischiare il debug e la telemetria della produzione.

### <a name="build-annotations"></a>Annotazioni sulla compilazione
Se si utilizza Visual Studio Team Services toobuild e distribuire l'app, annotazioni distribuzione visualizzati nei grafici nel portale di hello. Se la versione più recente ha alcun effetto sulle metriche di hello, diventa evidente.

![Annotazioni sulla compilazione](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Elementi di lavoro
Quando viene generato un avviso, Application Insights può creare automaticamente un elemento di lavoro nel sistema di tracciamento delle attività.

## <a name="but-what-about"></a>Altri aspetti
* [Privacy e archiviazione](app-insights-data-retention-privacy.md): i dati di telemetria vengono conservati nei server sicuri di Azure.
* Prestazioni - impatto hello è molto basso. I dati di telemetria sono organizzati in batch.
* [Prezzi](app-insights-pricing.md): il servizio è gratuito finché i volumi sono ridotti.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi
Iniziare a usare Application Insights è semplice. opzioni di Hello principali sono:

* Instrumentare un'app Web già in esecuzione, In questo modo tutti i dati di telemetria hello prestazioni predefiniti. Questa opzione è disponibile per [Java](app-insights-java-live.md) e [server IIS](app-insights-monitor-performance-live-website-now.md), nonché per le [App Web di Azure](app-insights-azure.md).
* Instrumentare il progetto in fase di sviluppo, cosa possibile per le app [ASP.NET](app-insights-asp-net.md) o [Java](app-insights-java-get-started.md), nonché per [Node. js](app-insights-nodejs.md) e una serie di [altri tipi](app-insights-platforms.md). 
* Instrumentare [qualsiasi pagina Web](app-insights-javascript.md) aggiungendo un breve frammento di codice.

