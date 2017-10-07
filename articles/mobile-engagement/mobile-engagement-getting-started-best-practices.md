---
title: aaaAzure Mobile Engagement Guida introduttiva alle procedure consigliate
description: Guida introduttiva ad Azure Mobile Engagement e alle procedure consigliate per il caricamento
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - Guida introduttiva con procedure consigliate
## <a name="overview"></a>Panoramica
**schermata di dispositivi mobili Hello è uno spazio molto talmente:** 2013, uno studio di trova In dispositivi mobili medio hello era 27 applicazioni installate. Gli utenti in genere hanno dedicato alle app 30 ore al mese, la maggior parte delle quali al social networking e ai giochi (circa 20 ore). Da 2014, hello mercato Android era circa 1,5 milioni di applicazioni per gli utenti toochoose da. store di Apple Hello contenuti circa 1,2 milioni di App. L'uso di app per dispositivi mobili continua ad aumentare grazie alla competizione tra gli sviluppatori in questo mercato in crescita. 

utenti mobili medio Hello verranno installati e disinstallare App con frequenza elevata a seconda della modifica interessi e si verifica nell'applicazione. Successo hello toodetermine di ordine di un'app diventa fondamentale tooknow più solo il numero di utenti di installare l'applicazione. È importante tooknow come utile l'app è e se la tendenza di utilizzo in fase di modifica. Hello seguenti domande diventano importante:

* Gli utenti inizia toofind app obsoleto o non interessanti? 
* Quanti utenti hanno smesso del tutto di usare l'app? 
* La tendenza agli acquisti in-app sta salendo o scendendo?
* Gli utenti falliscono toocomplete flussi di lavoro a causa di problemi con l'applicazione hello o mancanza di interesse? 
* Impossibile mantenere l'app utili e pertinenti trasferendo base utente tooyour contenuto aggiornato? 
* Questo contenuto aggiornato sarebbe hello lo stesso per tutti gli utenti o con lo stato attivo su segmenti utente basati sul comportamento dell'App? 

Risposte tooquestions simile toothese potrebbe prolungare la durata hello e dei ricavi dall'app. oltre che per definire e conservare la base utenti. 

Le applicazioni tendono toohave relative ai supporti alcuni periodo di conservazione di massimo hello tra gli utenti. Uno dei motivi per l'oggetto è che costantemente vengono fornite toousers contenuto aggiornato. L'adozione anticipata di notifiche push utile indirizzato segmento utente tooa tende toohave un elevato impatto sulla memorizzazione di app. 

il programma di Azure Mobile Engagement Hello è progettato toohelp si estende vita hello e conservazione delle informazioni dell'app, fornendo un metodo toogather e analizzare le informazioni dettagliate sull'utilizzo di hello dell'app. Consentono di classificare la base di utenti in base toobehavior e creare campagne con stato attivo per il recapito delle notifiche push e i messaggi in-app segmenti utente tooidentified. Gli indicatori di prestazioni chiave (KPI) misurano il livello di attività degli utenti nei diversi ambiti dell'app. Azure Mobile Engagement fornisce i metodi di hello è necessario toodetermine questi indicatori KPI. Consente di aumentare hello ritorno sugli investimenti (ROI) fornendo infrastruttura hello occorre tooincrease engagement con app mobile. 

In hello tooget di ordine massimo da Azure Mobile Engagement, è necessario toostart con un piano di engagement ben progettata. Il piano consentirà di identificare i dati di hello granulari sarà necessario toosegment in grado di toobe utente base. a partire dal comportamento e dalle esperienze in-app. Affinché il toobe piano ha esito positivo, è una migliore tooclearly pratica definire hello indicatore KPI che è necessario misurare gli obiettivi di hello dell'app. Con gli indicatori di prestazioni definiti, è possibile incorporare la logica necessaria hello facilmente app toocollect correttamente con granularità fine dati di cui sarà possibile utilizzare tooanalyze e valutare gli indicatori KPI. In questo argomento è una Guida alle procedure consigliate per la definizione di indicatori KPI hello da utilizzare con il piano del progetto. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Passaggio 1: Definire il modello di elemento hello toofit gli indicatori KPI
Definire correttamente gli indicatori KPI può essere toocomplete un'attività complessa. Le app progettate per settori diversi hanno le proprie specifiche e i propri obiettivi Ciò tende tooconfuse l'approccio. toohelp evitare questo problema, gli obiettivi e indicatori KPI devono essere classificati in tre categorie principali: **Business**, **Engagement**, e **tecniche**. Questo è ciò che viene definito hello **modello maggiore rilevanza**.

Una corretta pianificazione verrà in genere hanno obiettivi con gli indicatori KPI hello che misurano successi hello in ognuna delle seguenti categorie di modello di elemento hello hello.

#### <a name="business-kpis"></a>KPI per il business
Gli indicatori KPI business devono essere toobuild parte più semplice hello. Probabilmente sono già stati in qualche modo definiti quando si è pianificata l'app per dispositivi mobili. Questi KPI di solito consentono di misurare i ricavi e il rendimento del capitale investito per l'app. Hello elenco seguente include alcuni esempi di KPI aziendali che possono aiutare a istruzioni durante la definizione del indicatori di prestazioni:

* KPI per il business relativi a elementi multimediali
  * Numero di annunci su cui si è fatto clic
  * Numero di visite di pagina per utente
  * Numero di sottoscrizioni correnti
* KPI per il business relativi a giochi
  * Numero di acquisti in-app
  * Ricavi medi per utente
  * Tempo dedicato a ogni sessione
  * Giorni di gioco e livello attuale raggiunto nel gioco
* KPI per il business relativi all'e-commerce
  * Giorni di utilizzo dell'app
  * Ricavi medi per utente
  * Quantità media nel carrello durante il completamento della transazione
  * Categoria prodotto per la maggior parte delle visualizzazioni e degli acquisti
* KPI per il business relativi a banche e assicurazioni
  * Numero di conti
  * Funzionalità attivate
  * Pagine di offerte visitate
  * Avvisi selezionati o attivati       

#### <a name="engagement-kpis"></a>KPI per l'interesse
Un indicatore KPI Engagement è un impegno di hello toomeasure indicatore delle prestazioni degli utenti. Le tendenze in questa area consentono di determinare la memorizzazione hello dell'app. Ecco alcuni indicatori delle prestazioni di esempio per questo tipo di KPI:

* Utenti attivi in hello ultimi 7 giorni
* Numero di utenti inattivi per hello ultimi 7 giorni
* Numero di utenti che non hanno usato app hello in 30 giorni  

Alcuni ovvi fattori esterni possono influenzare gli indicatori in quest'area. Ad esempio, è possibile considerare toobe un dispositivo mobile con un utente in qualsiasi momento. Questo può essere vero o meno. Un'app di gioco potrebbe tendono toohave utilizzo più elevato per le festività quando un giocatore potrebbe essere riprodotto più durante il lavoro o all'esterno dell'istituto di istruzione.   

Definire gli indicatori KPI in questa categoria consentono di misurare la relazione hello tra l'app e i clienti.

#### <a name="technical-kpis"></a>KPI tecnici
Gli indicatori di prestazioni in questa categoria consentono di determinare se l'app funziona correttamente, si blocca o si arresta in modo anomalo. Questi indicatori possono misurare hello integrità dell'applicazione e determinare problemi di usabilità che potrebbero impedire agli utenti di usare app hello. Le informazioni raccolte per questa categoria potrebbe inoltre contenere informazioni sulle prestazioni che sarebbero rilevante toomarketing team. dati Hello potrebbero essere utili anche per la risoluzione dei problemi IT e toohelp i team di supporto per identificare gli errori riportati. 

Ecco alcuni esempi di KPI tecnici:

* Informazioni e conteggio di eccezioni non gestite e gestite 
* Timestamp per l'ultimo arresto anomalo
* Ultimo pulsante selezionato o ultima pagina visitata
* Utilizzo della memoria delle app hello
* Frequenza dei fotogrammi dell'app
* Versione del sistema operativo che hello app è in esecuzione in
* Versione dell'app

Definire le prestazioni dell'applicazione misura toohelp gli indicatori KPI e identificare potenziali errori. Questo indicatori consentono di ridurre il tempo di hello che necessario toodeliver una correzione per i clienti. oltre che a definire un segmento di utenti che ha riscontrato un particolare problema. È possibile utilizzare che le notifiche utente segmentazione toocreate campagne toodeliver relative disponibili correzioni e potenziali toohelp promozioni, ripristinare la soddisfazione dei clienti. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Esercizio di strategia 1: Creare il dashboard KPI
Quando si definisce la strategia di marketing, gli indicatori KPI dovrebbero offrire una panoramica di ogni obiettivo principale. Dovrebbero essere i punti di dati definito chiaramente che consentono di toocollect informazioni essenziali toomonitor il comportamento di app e hello dell'utente finale di hello.

Creare un dashboard KPI contenente hello sotto informazioni

1. Quali sono hello gli indicatori KPI per l'applicazione hello?
2. I dati che fa riferimento verranno utilizzare toorepresent ogni indicatore KPI?
3. Dove si trovano questi dati per l'applicazione (ad esempio, schermo, impostazioni, sistema)?
4. È possibile riprodurre una sequenza di interesse per questo KPI?

È possibile utilizzare hello **KPI generatore** foglio di lavoro in nostro [modello Playbook Media] [ Media Playbook link] per esempi e informazioni aggiuntive.

## <a name="step-2-your-engagement-program"></a>Passaggio 2: Programma di interesse
Un buon programma di engagement mobile dovrebbe essere considerato un componente chiave dell'app Assolutamente deve includere un ottimo programma iniziale che viene eseguito per un utente durante hello giorni prima dell'utilizzo dell'app. Questa impostazione tende toohave un effetto molto positivo sulla conservazione dell'app e impegno. Alcuni studi hanno dimostrato che maggioranza hello di arrestare gli utenti utilizzando un hello app primi giorni dopo l'installazione. Si desidera toostrive toomeet o supera interesse determinante previsione di cliente tempestivamente quando utente hello è ancora attivo si trova nella tua app. Verificare che si presentano clienti tooyour valore di chiave hello e vantaggi dell'app. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Notifiche push sono hello migliore approccio tooearly appuntamenti con gli utenti dei dispositivi mobili. Si deve tuttavia prestare molta attenzione quando si segmentano gli utenti per le notifiche push. Infatti, se l'utente ha la sensazione di ricevere posta indesiderata o notifiche non interessanti, le conseguenze possono essere gravi. In pochi clic, l'utente può eliminare l'applicazione tooreturn mai. utente Hello dovrebbe ricevere valore nell'applicazione personalizzata anziché generica posta indesiderata.

Una volta che gli utenti siano attivamente impegnati, il programma di engagement consente unità altri aspetti dell'applicazione hello.

Ad esempio, è Impossibile configurare una campagna che richiede il toorate utenti attivi app. Poiché questo segmento utente è più attivo hello e abbia hello la maggior parte delle esperienza con l'app, che ci si aspetta li toogive hello classificazione più accurati. Dopo aver creato un livello elevato di app, può essere utile unità di download di organici hello dell'app, nonché ridurre i costi di acquisizione nuovo cliente.

#### <a name="engagement-sequence"></a>Sequenza di interesse
Un programma di interesse completo include diverse sequenze di interesse. Ogni sequenza mira tooreach obiettivi diversi.

###### <a name="life-push-sequence"></a>Sequenza di push del ciclo di vita
gli obiettivi di Hello per una sequenza di push vita sono diversi a seconda del ciclo di vita di hello coinvolgimento dell'utente hello app hello. Un particolare utente può essere nuovo, inattivo o molto attivo. In diverse fasi di un ciclo di vita, gli utenti potrebbero trarre vantaggio dal nuovo contenuto sotto forma di hello di toodocumentation suggerimenti o collegamenti. 

Ad esempio un nuovo utente potrebbe aiutare recupero tooan orientato alle app o trarre vantaggio da un nuovo utente incentivi simile toohello seguente hello prima volta che si avvia applicazione hello...

*"Toohave lieti nell'onboarding. Ricordare toologin tooget il 1 ° mese gratuito! "*

###### <a name="behavioral-push-sequence"></a>Sequenza di push comportamentale
sequenza di push comportamentali Hello mira utilizzo tooincrease basato sul comportamento degli utenti raccolto per l'applicazione hello.  

Un utente di un'app di fantascienza football molto attivo, ad esempio, può risultare vantaggioso viene occupato con hello previa notifica push...

*"Gianni, sei un vero appassionato di calcio! Nella sezione NFL tooour di log e win libero accesso toohello SuperBowl".*

###### <a name="alerting-push-sequence"></a>Sequenza di push di avviso
Gli utenti apprezzeranno le notizie rilevanti per i propri interessi. Una sequenza di push di avviso accresce l'interesse inviando avvisi basati sulle preferenze chiaramente dimostrate da un utente. È possibile esplicita quando un utente seleziona i propri interessi in app hello. È stato inoltre determinare in modo implicito in base ai dati raccolti durante l'interazione dell'utente con l'applicazione hello.

Ad esempio, utente hello di un'app di E-Commerce può regolarmente acquistare una marca di caffè che è stato acquisito con un indicatore KPI business specifica. Hello seguente avviso è possibile migliorare il coinvolgimento dell'utente con l'applicazione hello.

*"Hi Wes, uno dei Preferiti marchi di caffè verrà eseguite su vendita 25% hello prima settimana del mese di settembre 2015. Ti ringraziamo come un cliente e voleva che toomake sapendo".*

###### <a name="rentention-push-sequence"></a>Sequenza di push di fidelizzazione
Gli utenti di tooretain obiettivi questo sequenza usando un toohelp campagne di notifica push ricorrenti unità regolare abitudine di impegno con app hello. Questo può contribuire ad aumentare memorizzazione app se utente hello goda interazioni hello. 

Ad esempio, l'utente hello di un'app correlati sportivi potrebbe ricevere hello notifica push settimanale in base a Preferiti team dell'utente hello seguente:

*"Per una probabilità toowin 200 punti, Vai voto se hello New York Yankees avrà la precedenza di un gioco questa settimana rispetto a Roma blu Jays!"*

#### <a name="hello-3w-approach"></a>approccio espressione 3s Hello
Crea una copia master delle sequenze di push diversi hello consente di contattare gli utenti finali. Tuttavia, è comunque necessario approccio di espressione 3s toouse hello per le notifiche di personalizzazione. Hello approccio espressione 3s deve prendere in considerazione che cosa e quando per ogni notifica. Se si risponde correttamente a queste tre domande, le notifiche dovrebbero risultare mirate al coinvolgimento degli utenti.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Chi: hello segmento utente che riceverà i messaggi
Gli utenti tooyour le notifiche push deve essere considerato un canale di comunicazione molto sensibili. Assicurarsi che le notifiche di hello che è puntare segmento di toosend tooa utente sono interessi toohello anche con ambito di tale segmento di utente. Una notifica indirizzata in modo non corretto è molto probabile toohave un effetto negativo per un utente. È consigliabile posta indesiderata iniziali tooyour app da disinstallare. 

Usare una combinazione di criteri tecnici e comportamentale specifici quando si definiscono i segmenti di utenti che riceveranno le notifiche. Un esempio semplice che definisce un segmento utente potrebbe essere simile toohello istruzione:

"Tutti gli utenti che ha avviato un'applicazione per dispositivi mobili per hello prima volta 3 giorni fa hello e hanno visitato la pagina di accesso hello due volte senza completarla un account di accesso".

Tale istruzione consente di identificare i dati di hello sarebbe necessario toocollect toosupport uno scenario specifico.

###### <a name="what-hello-message-that-you-will-send"></a>Informazioni: il messaggio hello che verrà inviato
**Tono**

Negli impegni usare un tono appropriato per gli utenti segmentati. Questo è decisamente tooconnect un modo efficace con gli utenti finali e alzare di livello d'interesse di un utente nell'app. 

**Reindirizzamento**

Per aprire più di un'applicazione hello, è possibile utilizzare una notifica push. Se hello messaggio di notifica fornisce un contesto, ad esempio news broadcast o promozione di un prodotto, il collegamento diretto di maggio notifica direttamente toohello destra il contenuto all'interno di un'applicazione hello. toosupport, è necessario creare un URL di un'applicazione hello toolet schema gestire il reindirizzamento di hello. Questo è un importante passaggio da non dimenticare quando si usano le sequenze di interesse.

Il reindirizzamento può essere gestito anche per altri sistemi. Ad esempio, con un URL di azione è possibile tooredirect gli utenti finali toomany altri sistemi inclusi hello seguenti:

* Un sito Web
* Una cassetta postale con la posta elettronica già configurata
* Una casella SMS
* Un servizio di chiamata
* Direttamente toohello archivio dell'applicazione per la valutazione di un'applicazione hello. 

Fornisce molte opportunità gli utenti finali tooengage e creare le regole automatiche tooimprove prestazioni.

**Formato/Contenuto**

Formati di notifica push e tipi diversi:

1. **Gli annunci** : consente di toosend pubblicità messaggi toousers in momenti diversi (all'esterno dell'app, nell'app o in qualsiasi momento).
2. **Esegue il polling** : abilitato si toogather informazioni degli utenti finali ponendo domande. Le risposte saranno disponibili durante la creazione di criteri agli utenti finali tootarget.
3. **Inserisce dati** : consente una binario base64 dati file tooupdate hello app o toosend. informazioni Hello contenute in un push di dati viene inviate l'esperienza degli utenti di tooyour applicazione toopersonalize hello nell'app. L'applicazione deve toobe progettato toosupport hello dati in un push di dati.
4. **Riquadri (solo Windows Phone)** : abilitato si toouse hello Microsoft Push Notification Service (MPNS) toosend notifica Push nativa che contiene dati XML (supportate dal SDK versione 0.9.0. payload finale di Hello per i riquadri non può superare i 32 KB.). messaggio Hello viene visualizzata direttamente nel riquadro della Lavagna.
5. **Visualizzazione Web** : Una visualizzazione Web è un popup con contenuto Web. Questo popup viene visualizzato quando l'utente finale di hello ha fatto clic su notifica push di hello. Una visualizzazione web consente toohave ulteriori interazione dell'utente finale di hello.

> [!NOTE]
> Assicurarsi che il contenuto di hello inviati come notifiche push sia conforme con la piattaforma del rispettivo hello (iOS, Android, Windows) linee guida per lo sviluppo di App e l'invio di notifiche push.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Quando: hello temporizzazione della campagna
Quando è hello migliore tempo tooactivate una campagna di attivazione di notifiche push? Dovrebbero essere manuali o automatiche? Dovrebbero essere ricorrenti? Determinazione hello destra ora o la frequenza è essenziale tooengage gli utenti con risultati ottimali hello. Per ogni sequenza di engagement e scenario, è necessario specificare quando saranno toosend tempo migliore hello notifiche push. Di seguito sono riportati alcuni possibili esempi:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Se si intende inviare molte notifiche ogni giorno, è necessario prendere in seria considerazione la possibilità che gli utenti percepiscano le comunicazioni come posta indesiderata. 

Azure Mobile Engagement fornisce due modalità toohelp evitare comunicazioni viene percepite come posta indesiderata. Innanzitutto, utilizzare tooensure segmentazione grana hello di destinazione non è eseguire agli stessi utenti. Azure Mobile Engagement fornisce anche una funzionalità di "quota" che può limitare le notifiche inviate per una campagna. Ad esempio, l'impostazione di un too5 di quota predefinito per ogni settimana garantisce che un utente incluso come parte del segmento di hello campagna utente riceve le notifiche non più di 5 per quella settimana.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Esercizio di strategia 2: Creare il programma di interesse
Dedicare del tempo di riepilogo gli obiettivi e la definizione di campagne hello si prevede che tooplay utilizzando sequenze specifiche. Assicurarsi di applicare le notifiche di hello espressione 3s approccio toohello in campagne. 

Hello utilizzare **Engagement programma** foglio di lavoro in hello [modello Playbook Media] [ Media Playbook link] per esempi e informazioni aggiuntive.

## <a name="step-3-app-integration"></a>Passaggio 3: Integrazione con l'app
#### <a name="create-a-tag-plan"></a>Creare un piano di tag
Azure Mobile Engagement toointegrate nell'app occorre toocreate un piano di tag. piano di tag Hello è fondamenta hello di un progetto di hello. Definisce la relazione hello tra specifiche marketing, il flusso di lavoro dell'applicazione hello hello e hello reale contrassegnare i dati raccolti in hello app toomeasure gli indicatori KPI. Indica quale analitica sarà possibile toosee nel portale di hello. Consente inoltre di definire i segmenti utente e inviare tooengage le notifiche push con stato attivo agli utenti finali. Dopo aver creato il piano di tag hello definito, l'aggiunta di toointegrate codice hello nell'app è semplice utilizzando hello Azure Mobile Engagement SDK.

Un piano di tag non dovrebbe contrassegnare qualsiasi elemento in un'applicazione, ma solo includere i dati dei tag che fanno parte della strategia di engagement mobile, che sarà probabilmente diversa a seconda dell'applicazione. Hello [modello Playbook Media] [ Media Playbook link] fornita da Azure Mobile Engagement consente compilare un piano di tag con un metodo specificato. Hello utilizzare **piano Tag** foglio di lavoro come una Guida di toobuilding il tag di pianificazione.

Quando si definisce una sezione di tag nel foglio di lavoro hello, essere molto specifico. Questo è molto importante tooavoid confusione. Descrivere in dettaglio ogni scenario previsto in cui verrà inviato ogni tag. Includere il nome di hello dell'attività hello in cui è incorporato in ciascun tag. Si devono tutti essere inclusi in hello **Informative** parte del foglio di lavoro hello. foglio di lavoro piano di Hello tag deve essere di riferimento principale di hello per la verifica del test. 

In hello **toocollect dati** sezione, il team di sviluppo deve trovare i tipi di hello, nomi, i valori e coppie chiave/valore aggiuntivo-info obbligatorio per ogni tag che verrà incorporato in un'applicazione hello.

Si consiglia di esaminare il piano di Tag hello con tutti i team associati hello progetto. Apportare le correzioni necessarie e verificare che sia tutto chiaro per i team del marketing e dello sviluppo.

Hello **rapporto di lavoro** foglio di lavoro può essere utilizzato toohelp Guida le persone coinvolte nel progetto hello.

#### <a name="data-types"></a>Tipi di dati
Si tratta di tipi di dati comuni supportati da Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Dispositivi e utenti
Azure Mobile Engagement identifica gli utenti generando un identificatore univoco per ogni dispositivo, Questo identificatore viene definito identificatore dispositivo hello (o deviceid). Viene generato in modo che tutte le applicazioni in esecuzione in tale condivisione dispositivo stesso hello stesso identificatore del dispositivo.

###### <a name="sessions-and-activities"></a>Sessioni e attività
Una sessione è un'istanza di applicazione hello eseguito da un utente. sessione Hello si estende dall'hello avvio utente hello app hello, finché termina.

Un'attività è un raggruppamento logico di un set di operazioni possono eseguire app hello durante una sessione. In genere è una particolare schermata nell'applicazione hello, ma può essere che qualsiasi elemento definito da hello logica dell'applicazione hello. Come minimo è consigliabile contrassegnare ogni schermata o attività per l'app. In questo modo si toounderstand hello utente-path.

###### <a name="events"></a>Events
Gli eventi sono l'interazione dell'utente utilizzato tooreport app hello. Possono essere azioni istantanee, come la condivisione di contenuto o l'avvio di un video. Tag di eventi sarà con le raccolte di dati che mostrano l'interazione degli utenti con app hello. 

###### <a name="jobs"></a>Processi
I processi sono utilizzati tooreport azioni hanno una durata. Di seguito sono riportati alcuni esempi:

* Esecuzione di chiamate API
* Tempo di visualizzazione degli annunci
* Durata delle attività in background 
* Durata dei processi di acquisto
* Visualizzazione di un video

###### <a name="errors"></a>Errors
Gli errori vengono riscontrati tooreport utilizzati dall'applicazione hello. ad esempio azioni utente non corrette o errori delle chiamate API.

###### <a name="application-information"></a>Informazioni sull'applicazione
Informazioni sull'applicazione (App-Info) viene utilizzati tootag dati correlati tooa l'esperienza utente con un'applicazione. Viene generato dall'interazione dell'utente con un'applicazione hello. 

Per una chiave specificata, app-info, Azure Mobile Engagement solo tiene traccia del valore più recente di hello (nessuno). App-info, viene visualizzato lo stato di hello dell'app o gli utenti finali. Ad esempio lo stato di log hello o gruppo di prodotto Preferiti dell'utente.

###### <a name="crash-data"></a>Dati sugli arresti anomali
Data di arresto anomalo del sistema vengono raccolti automaticamente da Mobile Engagement SDK hello errori dell'applicazione di report non è gestiti da un'applicazione hello. ad esempio un'eccezione non gestita.

###### <a name="extra-data"></a>Dati aggiuntivi
Eventi, errori, attività e processi possono essere migliorati con i parametri, Si tratta di uno sviluppatore può fornire come dati specifici di un'applicazione hello-informazioni extra. Si tratta di un aspetto importante per definire una segmentazione con granularità fine. 

Ad esempio, valore hello di un tag "articolo" consente agli utenti finali toosegment in base che visualizzare tale articolo particolare. Questo però potrebbe non bastare. È meglio se lo stesso tag "articolo" include anche informazioni aggiuntive, ad esempio "categoria_notizie" in un'attività. Sarebbe utile toodetermine hello in modo dinamico le categorie preferite per l'utente hello. 

Le informazioni aggiuntive vengono segnalate come coppia chiave/valore. Nell'esempio hello per l'applicazione supporti hello extra-informazioni per "news_category" sarebbe valore hello per tale categoria. Ad esempio, "sport", "economia" o "politica".

#### <a name="tag-and-sdk-integration"></a>Integrazione tag e SDK
Per istruzioni dettagliate per l'integrazione di hello Azure Mobile Engagement SDK nell'app, seguire hello [Engagement SDK integrazione](mobile-engagement-windows-store-integrate-engagement.md) documentazione nel sito Web Azure. Scegliere la piattaforma di destinazione dai collegamenti hello nella parte superiore di hello di tale pagina.

Si consiglia di creare i progetti per due app basate su Azure Mobile Engagement. Uno per lo sviluppo e gestione temporanea di test e altri per la gestione temporanea a produzione hello. Il team IT può quindi alzare di livello dal test tooproduction di gestione temporanea quando il test di accettazione utente hello ha esito positivo.

#### <a name="user-acceptance-testing-uat"></a>Test di accettazione utente
Il test di accettazione utente ha lo scopo di verificare che tutto funzioni come previsto. I flussi di lavoro possono essere completati e possono raccogliere tutti i dati necessari in base al piano di tag:

* Informazioni di tag devono essere disponibili in base a toodocumented concetti AZME
* Tutte le informazioni necessarie vengono raccolte (inclusi il valore Extra info e il valore App info)
* Nomenclatura corrisponde tooyout secondo piano Tag
* Non sono stati inviati tag duplicati

Testare accuratamente tutti i tipi di hello del comportamento di notifica che non è stato incorporato nell'app

* Annunci, sondaggi, push di dati al di fuori dell'app e in-app
* Visualizzazione Web/testo
* Aggiornamento di notifiche, categorie

#### <a name="setup"></a>Configurazione
Configurare Azure Mobile Engagement è molto semplice. Tutta la documentazione di hello correlati è disponibile nel sito Web di Azure Mobile Engagement hello, interfaccia utente toohello [come toonavigate hello interfaccia utente](mobile-engagement-user-interface-home.md).

È consigliabile iniziare impostando i ruoli appropriati hello e le appartenenze ai ruoli per gli utenti di hello del progetto. Ciò consente di gestire piattaforma toohello accesso appropriato per tutti gli utenti. I ruoli possono includere:

* Amministratori:
* Sviluppatori:
* Visualizzatori 

Successivamente:

* Registrare il tootest deviceID sul proprio dispositivo.
* Vai toohello impostazioni dell'account e impostare i grafici di toohave hello fuso orario e l'ora di recapito notifica impostato per il fuso orario.
* Vai toohello impostazioni dell'applicazione e registrare hello "App-info" è necessario tootarget per l'utente finale a portata di mano.

Per ulteriori informazioni su come toorun il primo push della campagna di notifica, revisione [come tooget all'utilizzo e gestione inserisce tooreach gli utenti finali tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusioni
I programmi di interesse sono iterativi e devono essere continuamente migliorati man mano che si determina cosa funziona meglio con l'app. 

Inizialmente, durante lo sviluppo di esperienza con engagement strategie non provare toobuild una strategia di engagement globale intero. Adottare un approccio graduale che identifica gli indicatori KPI e la modalità tooleverage li. La strategia di interesse sarà univoca per ogni app.

Dopo che è stato sviluppato esperienza che è possibile aggiungere le seguenti applicazioni engagement tooyour hello:

* Rilevamento: si acquisiscono utenti e probabilmente si definiscono le origini per la raccolta dati. Azure mobile Engagement possono essere origini di toodata-raccolta collegato. Consente prestazioni toomonitor di ogni origine. Queste informazioni sarà toomaximize interessante l'investimento di acquisizione. 
* Test A/B: è una parte essenziale del programma di interesse. Ogni app ha le proprie specifiche. Con il test A/B, è possibile migliorare il programma di interesse.
* Georilevazione: è una grande opportunità per i marchi. Funzionalità toothis grazie può raggiungere in esecuzione e posto giusto hello. Si consiglia di verifica per determinare se che sono stati raccolti i dati sul comportamento sufficiente per l'utente finale prima di avviare toouse posizione geografica.
* Push di dati: Il push di dati è un push invisibile. Il push di dati consente di personalizzare l'applicazione in base al comportamento degli utenti finali. Ad esempio, se un segmento utente consulta spesso prodotti high-tech, proprietario dell'applicazione hello possibile inviare un push di dati che verranno utilizzate la home page con il contenuto ad alta tecnologia.

## <a name="next-steps"></a>Passaggi successivi
* [Creare un account Azure Mobile Engagement](mobile-engagement-create.md).
* Visitare [definire la strategia di Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn ulteriori informazioni sulla definizione della strategia di Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
