---
title: aaaData conservazione e archiviazione in Azure Application Insights | Documenti Microsoft
description: Informativa sulla conservazione e sulla privacy
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Raccolta, conservazione e archiviazione di dati in Application Insights


Quando si installa [Azure Application Insights] [ start] SDK nell'applicazione, invia dati di telemetria sul toohello app Cloud. Naturalmente, gli sviluppatori responsabili desiderino tooknow esattamente quali dati vengono inviati, cosa accade toohello dati e come è possibile mantenere il controllo. In particolare, devono sapere se possono essere inviati dati sensibili, dove vengono archiviati e quale livello di sicurezza viene applicato. 

Prima di tutto, risposta breve hello:

* i moduli standard telemetria Hello eseguite "hello" sono servizio toohello di toosend improbabile che i dati sensibili. dati di telemetria Hello si occupa di carico, le metriche delle prestazioni e utilizzo, i report di eccezione e altri dati di diagnostica. dati utente principale di Hello visibili nei report di diagnostica hello sono URL; ma l'app in ogni caso non deve inserire i dati riservati in testo normale in un URL.
* È possibile scrivere codice che invia dati di telemetria personalizzati aggiuntivi toohelp durante la diagnostica e utilizzo di monitoraggio. Questa flessibilità è un'eccellente funzionalità di Application Insights. Sarebbe possibile, per errore, questo codice in modo che includa personale toowrite e altri dati sensibili. Se l'applicazione funziona con tali dati, è necessario applicare un codice di hello tooall processi di analisi accurata che scritto.
* Durante lo sviluppo e test dell'app, è facile tooinspect ciò che viene inviato da hello SDK. Hello dati visualizzati in hello debug la finestra di output di hello IDE e del browser. 
* dati Hello viene mantenuti nella [Microsoft Azure](http://azure.com) server USA hello o Europa. L'app può essere eseguita ovunque. Azure offre [processi di sicurezza efficaci e soddisfa una vasta gamma di standard di conformità](https://azure.microsoft.com/support/trust-center/). Solo utente e il team designato sono tooyour accedere ai dati. Lo staff Microsoft possa avere limitato accesso tooit solo in determinate circostanze limitati con la conoscenza. La crittografia in transito, ma non in server hello.

rest Hello di questo articolo vengono illustrate meglio queste risposte. Si è progettato toobe indipendenti, in modo che è possibile visualizzarlo toocolleagues che non fanno parte del proprio team.

## <a name="what-is-application-insights"></a>Informazioni su Azure Application Insights
[Azure Application Insights] [ start] è un servizio fornito da Microsoft che consente di migliorare le prestazioni di hello e facilità di utilizzo dell'applicazione in tempo reale. Esegue il monitoraggio dell'applicazione è in esecuzione, sia durante il test e dopo aver pubblicato o distribuito, tutto il tempo hello. Application Insights consente di creare grafici e tabelle cui viene illustrato, ad esempio, le ore del giorno, la maggior parte degli utenti, come app reattiva hello è e come servita da qualsiasi esterno anche i servizi dipende. Se sono presenti arresti anomali del sistema, errori o problemi di prestazioni, è possibile cercare tra i dati di telemetria hello causa hello toodiagnose di dettaglio. E servizio hello invierà messaggi di posta elettronica se sono state apportate modifiche nella disponibilità hello e le prestazioni dell'app.

In ordine tooget questa funzionalità, si installa un Application Insights SDK nell'applicazione, che diventa parte del codice. Quando l'app è in esecuzione, hello SDK consente di monitorare il funzionamento e invia dati di telemetria toohello Application Insights servizio. Si tratta di un servizio cloud ospitato da [Microsoft Azure](http://azure.com). Application Insights funziona tuttavia per tutte le applicazioni, non solo quelle ospitate in Azure.

![Hello SDK nell'applicazione invia dati di telemetria toohello servizio Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

servizio di Application Insights Hello archivia e analizza i dati di telemetria hello. analisi di hello toosee o eseguire una ricerca nei hello archiviati dati di telemetria, accedi tooyour account Azure e la risorsa di Application Insights hello aperto per l'applicazione. È inoltre possibile accedere ai dati toohello della condivisione con altri membri del team o con i sottoscrittori di Azure specificati.

È possibile disporre i dati esportati da hello servizio Application Insights, ad esempio tooa database o tooexternal strumenti. Ogni strumento è fornire con un tasto speciale che ottengono dal servizio hello. Se necessario, è possibile revocare la chiave Hello. 

Application Insights SDK sono disponibili per una gamma di tipi di applicazioni: servizi web ospitati nei propri server J2EE o ASP.NET o in Azure; client Web - e hello codice in esecuzione in una pagina web. applicazioni desktop e servizi. App per dispositivi, ad esempio Windows Phone, iOS e Android. Inviano dati di telemetria toohello stesso servizio.

## <a name="what-data-does-it-collect"></a>Quali dati raccoglie?
### <a name="how-is-hello-data-is-collected"></a>Come è dati hello viene raccolto?
Esistono tre origini dati:

* Hello SDK, che si integra con l'app sia [in fase di sviluppo](app-insights-asp-net.md) o [in fase di esecuzione](app-insights-monitor-performance-live-website-now.md). Sono disponibili diversi SDK per diversi tipi di applicazione. È inoltre disponibile un [SDK per le pagine web](app-insights-javascript.md), che carica in hello-browser dell'utente finale con la pagina hello.
  
  * Ogni SDK include un numero di [moduli](app-insights-configuration-with-applicationinsights-config.md), che utilizzano tecniche diverse toocollect diversi tipi di dati di telemetria.
  * Se si installa il SDK di hello in fase di sviluppo, è possibile utilizzare il toosend API propri dati di telemetria, nei moduli standard toohello di addizione. Questi dati di telemetria personalizzati possono includere gli eventuali dati da toosend.
* In alcuni server web, sono disponibili anche agenti che eseguono insieme app hello e inviare dati di telemetria sulla CPU, memoria e occupazione di rete. Ad esempio, macchine virtuali di Azure, host Docker e [server J2EE](app-insights-java-agent.md) possono disporre di tali agenti.
* [Test disponibilità](app-insights-monitor-web-app-availability.md) processi eseguiti da Microsoft che inviano richieste tooyour web app a intervalli regolari. risultati di Hello vengono inviati toohello servizio di Application Insights.

### <a name="what-kinds-of-data-are-collected"></a>Quali tipi di dati vengono raccolti?
categorie principali di Hello sono:

* [Dati di telemetria del server Web](app-insights-asp-net.md): richieste HTTP,  URI richiesta di tempo impiegato tooprocess hello, codice di risposta, indirizzo IP del client. ID sessione.
* [Pagine Web](app-insights-javascript.md): numero di pagine, utenti e sessioni, tempo di caricamento della pagina, eccezioni, chiamate AJAX.
* Contatori delle prestazioni: memoria, CPU, IO, occupazione della rete.
* Contesto client e server: sistema operativo, impostazioni locali, tipo di dispositivo, browser, risoluzione dello schermo.
* [Eccezioni](app-insights-asp-net-exceptions.md) e arresti anomali: **dump dello stack**, ID compilazione, tipo di CPU. 
* [Dipendenze](app-insights-asp-net-dependencies.md) -chiama tooexternal servizi, ad esempio REST, SQL, AJAX. URI o stringa di connessione, durata, esito positivo, comando.
* [Test di disponibilità](app-insights-monitor-web-app-availability.md) : durata del test e passaggi, risposte.
* [Log di traccia](app-insights-asp-net-trace-logs.md) e [telemetria personalizzata](app-insights-api-custom-events-metrics.md) - **tutto ciò che viene codificato nei log o nella telemetria**.

[Maggiori dettagli](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Come è possibile verificare cosa viene raccolto?
Se si sta sviluppando hello app con Visual Studio, eseguire l'applicazione hello in modalità di debug (F5). dati di telemetria Hello viene visualizzato nella finestra di Output di hello. Da qui, è possibile copiarli e formattarli come JSON per semplificare l'ispezione. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Nella finestra di diagnostica hello è inoltre disponibile una visualizzazione più leggibile.

Per le pagine Web, aprire la finestra di debug del browser.

![Premere F12 e aprire la scheda di rete hello.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>È possibile scrivere dati di telemetria hello toofilter codice prima che venga inviata?
Questo sarebbe possibile scrivendo un [plug-in del processore di telemetria](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Quanto tempo sono dati hello conservati?
Punti dati non elaborati (vale a dire, gli elementi che è possibile eseguire una query in Analitica e controllare nella ricerca) vengono conservati per impostare i giorni too90. Se è necessario tookeep dati più lungo, è possibile utilizzare [l'esportazione continua](app-insights-export-telemetry.md) toocopy è tooa account di archiviazione.

I dati aggregati, ovvero conteggi, medie e altri dati statistici visualizzati in Esplora metriche, vengono conservati con livello di dettaglio di 1 minuto per 90 giorni.

## <a name="who-can-access-hello-data"></a>Chi può accedere a dati hello?
dati Hello sono visibile tooyou e, se si dispone di un account aziendale, i membri del team. 

Possono essere esportato da utenti e i membri del team e può essere copiato tooother percorsi e passate tooother persone.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Operazioni eseguite Microsoft fare con informazioni hello l'applicazione invia tooApplication Insights?
Microsoft utilizza i dati di hello solo in ordine tooprovide hello servizio tooyou.

## <a name="where-is-hello-data-held"></a>In cui viene mantenuti dati hello?
* USA hello o Europa. Quando si crea una nuova risorsa di Application Insights, è possibile selezionare il percorso di hello. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Significa che l'applicazione ha toobe ospitati in hello USA o Europa?
* No. L'applicazione può eseguire in qualsiasi posizione, nel proprio host locale o nel Cloud hello.

## <a name="how-secure-is-my-data"></a>Quanto sono sicuri i dati?
Application Insights è un servizio di Azure. Criteri di sicurezza descritti in hello [white paper Azure sicurezza, Privacy e conformità](http://go.microsoft.com/fwlink/?linkid=392408).

Hello dati vengono archiviati nel server di Microsoft Azure. Per gli account nel portale di Azure hello, le restrizioni di account sono descritti in hello [documento Azure sicurezza, Privacy e conformità](http://go.microsoft.com/fwlink/?linkid=392408).

Accesso ai dati tooyour da personale Microsoft è limitato. È accedere ai dati solo con l'autorizzazione e se è necessario toosupport l'utilizzo di Application Insights. 

Dati di aggregazione di tutte le applicazioni di tutti i nostri clienti (ad esempio velocità dei dati e le dimensioni medie delle tracce) sono utilizzati tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>È possibile che i dati di telemetria di altri utenti interferiscano con i dati di Application Insights?
Impossibile inviano account tooyour telemetria aggiuntive utilizzando la chiave di strumentazione hello, che può essere trovata nel codice hello delle pagine web. Con una quantità sufficiente di dati aggiuntivi, è possibile che le metriche dell'utente non rappresentino correttamente le prestazioni e l'utilizzo dell'app.

Condividere codice con altri progetti, ricordare tooremove della chiave di strumentazione.

## <a name="is-hello-data-encrypted"></a>Dati hello è crittografati?
Non in server hello al momento.

Tutti i dati vengono crittografati durante lo spostamento tra data center.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Dati hello sono crittografati in transito verso il server di applicazioni tooApplication Insights?
Sì, utilizziamo portale toohello di https toosend dati da quasi tutti gli SDK, tra cui server web, dispositivi e le pagine web HTTPS. Hello unica eccezione è dati inviati dal normale le pagine web HTTP. 

## <a name="personally-identifiable-information"></a>Informazioni personali
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>È possibile informazioni identificabili personalmente (PII) inviare tooApplication Insights?
Sì, è possibile. 

Indicazioni generali:

* La maggior parte dei dati di telemetria standard, ovvero i dati di telemetria inviati senza scrittura di codice da parte dell'utente, non include informazioni personali esplicite. Tuttavia, potrebbe essere possibile tooidentify individui dall'inferenza da una raccolta di eventi.
* I messaggi di eccezione e di traccia potrebbero contenere informazioni personali
* Dati di telemetria personalizzati - chiamate, ad esempio TrackEvent scritto nel codice utilizzando le tracce di API o log hello - può contenere dati che scelto.

tabella Hello alla fine di hello di questo documento contiene una descrizione più dettagliata di hello dati raccolti.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Si è tenuto a rispettarlo leggi e normative di considerare tooPII?
Sì. È la responsabilità tooensure hello raccolta e utilizzo dei dati hello conforme a leggi e normative e alle condizioni di hello Microsoft Online Services.

È necessario notificare ai clienti in modo appropriato l'applicazione consente di raccogliere dati di hello e modalità di utilizzo dati hello.

#### <a name="can-my-users-turn-off-application-insights"></a>Gli utenti possono disattivare Application Insights?
Non direttamente. Non è disponibile un parametro che gli utenti possono operare tooturn off Application Insights.

È tuttavia possibile implementare una funzionalità di questo tipo nell'applicazione. Hello tutti gli SDK includono un'impostazione di API che consente di disattivare la raccolta dati di telemetria. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>L'applicazione raccoglie involontariamente informazioni riservate. Application Insights può eliminare questi dati in modo che non vengano conservati?
Application Insights non filtra o elimina i dati. Si deve gestire dati hello in modo appropriato ed evitare l'invio di tali tooApplication dati Insights.

## <a name="data-sent-by-application-insights"></a>Dati inviati da Application Insights
SDK Hello variano tra le piattaforme e sono presenti numerosi componenti che è possibile installare. (Vedere troppo[Application Insights - Panoramica][start].) Ogni componente invia dati diversi.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Classi di dati inviati nei diversi scenari
| Azione | Classi di dati raccolte (vedere la tabella seguente) |
| --- | --- |
| [Aggiungi progetto web di Application Insights SDK tooa .NET][greenbrown] |ServerContext<br/>Inferred<br/>Perf counters<br/>Requests<br/>**Eccezioni**<br/>Session<br/>users |
| [Installare Status Monitor in IIS][redfield] |Dipendenze<br/>ServerContext<br/>Inferred<br/>Perf counters |
| [Aggiungere app web di Application Insights SDK tooa Java][java] |ServerContext<br/>Inferred<br/>Richiesta<br/>Sessione<br/>users |
| [Aggiungi pagina tooweb SDK per JavaScript][client] |ClientContext  <br/>Inferred<br/>Page<br/>ClientPerf<br/>Ajax |
| [Definire le proprietà predefinite][apiproperties] |**Properties** in tutti gli eventi standard e personalizzati |
| [Chiamare TrackMetric][api] |Valori numerici<br/>**Proprietà** |
| [Chiamare Track*][api] |Nome evento<br/>**Proprietà** |
| [Chiamare TrackException][api] |**Eccezioni**<br/>Dump dello stack<br/>**Proprietà** |
| SDK non riesce a raccogliere dati. Ad esempio: <br/> - non riesce ad accedere ai contatori delle prestazioni<br/> - si è verificata un'eccezione nell'inizializzatore della telemetria |Diagnostica di SDK |

Per informazioni sugli [SDK per altre piattaforme][platforms], vedere i relativi documenti.

#### <a name="hello-classes-of-collected-data"></a>classi di Hello dei dati raccolti
| Classe di dati raccolti | Include (elenco non completo) |
| --- | --- |
| **Properties** |**Qualsiasi dato, in base al codice** |
| DeviceContext |ID, IP, impostazioni locali, modello dispositivo, rete, tipo di rete, nome OEM, risoluzione dello schermo, istanza del ruolo, nome ruolo, tipo di dispositivo. |
| ClientContext  |Sistema operativo, impostazioni locali, lingua, rete, risoluzione della finestra. |
| Session |ID sessione |
| ServerContext |Nome computer, impostazioni locali, sistema operativo, dispositivo, sessione utente, contesto utente, operazione. |
| Inferred |Area geografica in base a indirizzo IP, timestamp, sistema operativo, browser. |
| Metrica |Nome e valore della metrica. |
| Eventi |Nome e valore dell'evento. |
| PageViews |URL e nome della pagina o della schermata. |
| Client perf |URL/nome pagina, tempo di caricamento del browser. |
| Ajax |Chiamate HTTP da una pagina web tooserver |
| Requests |URL, durata, codice di risposta. |
| Dependencies |Tipo (SQL, HTTP, ...), stringa di connessione o URI, sincrono/asincrono, durata, esito positivo, istruzione SQL (con Monitoraggio stato) |
| **Eccezioni** |Tipo, **messaggio**, stack di chiamate, file di origine e numero di riga, ID thread. |
| Crashes |ID processo, ID processo padre, ID thread di arresto anomalo, patch applicazione, ID, compilazione, tipo di eccezione, indirizzo, motivo, simboli e registri offuscati, indirizzi di inizio e fine binari, nome e percorso binario, tipo di CPU |
| Trace |**Messaggio** e livello di gravità. |
| Perf counters |Tempo processore, memoria disponibile, frequenza di richieste, frequenza di eccezioni, byte privati del processo, velocità di I/O, durata richiesta, lunghezza coda richiesta. |
| Disponibilità |Codice di risposta del test Web, durata di ogni passo del test, nome del test, timestamp, esito positivo, tempo di risposta, posizione del test |
| Diagnostica di SDK |Messaggio di traccia o eccezione |

È possibile [disattivare alcuni dati hello modificando Applicationinsights][config]

## <a name="credits"></a>Credits
Questo prodotto include dati GeoLite2 creati da MaxMind, disponibile nel sito [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

