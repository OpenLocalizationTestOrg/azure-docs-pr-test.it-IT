---
title: aaaCortana Playbook modello di soluzione di Business Intelligence per la previsione della domanda di energia | Documenti Microsoft
description: Modello di soluzione di Microsoft Cortana Intelligence utile per la previsione della domanda di energia per un'azienda di pubblici servizi.
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Studio del modello di soluzione Cortana Intelligence per la previsione della domanda di energia
## <a name="executive-summary"></a>Sunto
In hello oltre anni, Internet delle cose (IoT), rinnovabili alternativo e dati sono uniti toocreate opportunità di grande utilità hello e dominio di energia. In hello contemporaneamente, utilità hello e settore energetico intera hello è visto prima consumo appiattimento con consumer complesse toocontrol modi migliori l'uso di energia. Di conseguenza, hello utilità e griglia smart società in tooinnovate bisogno e rinnovare autonomamente. Inoltre, molti griglie di alimentazione e utilità diventano obsoleti e molto costoso toomaintain e gestire. Durante l'ultimo anno hello, team hello ha lavorato su un numero di appuntamenti all'interno di dominio di energia hello. Durante questi appuntamenti, si sono verificato molti casi in cui hello utilità o fornitori di software indipendenti (fornitori di Software indipendenti) interessare in previsione della domanda di energia futuri per. Queste previsioni svolgono un ruolo importante nella propria azienda attuali e futura e sono diventati foundation hello per diversi casi di utilizzo. come previsioni del carico elettrico a breve e lungo termine, commercializzazione, bilanciamento del carico, ottimizzazione delle reti e così via. Dati di grandi dimensioni e i metodi di Advanced Analitica (AA), ad esempio Machine Learning (ML) sono particolarmente importanti hello per produrre le previsioni accurate e affidabile.  

In questo playbook, abbiamo business hello e analitiche linee guida necessarie per lo sviluppo di un esito positivo e a previsione la distribuzione della domanda di energia soluzione. Le linee guida qui proposte consentono ad aziende di pubblici servizi, data scientist e data engineer di creare soluzioni per la previsione della domanda completamente operative e basate sul cloud. Per le aziende che hanno i relativi dati e viaggio analitica avanzate, una soluzione di questo tipo può rappresentare hello iniziale il valore di inizializzazione strategia a lungo termine smart griglia.

> [!TIP]
> toodownload diagramma in cui viene fornita una panoramica dell'architettura del modello, vedere [architettura Cortana modello di soluzione di Business Intelligence per la previsione della domanda di energia](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Panoramica
Questo documento descrive hello business, dati e gli aspetti tecnici dell'utilizzo di Cortana Intelligence e in particolare Azure Machine Learning AML () per l'implementazione di hello e distribuzione delle soluzioni di previsione di energia. documento Hello è costituito da tre parti principali:  

1. Informazioni commerciali  
2. Informazioni sui dati  
3. Implementazione tecnica

Hello **comprensione delle esigenze aziendali** profili delle parti hello uno toounderstand esigenze di business aspetto e prendere in considerazione una decisione di investimento toomaking precedente. Viene spiegato come tooqualify hello problema aziendale a mano tooensure analitica predittiva e machine learning siano davvero efficace e applicabile. documento Hello ulteriormente vengono illustrati concetti fondamentali di hello di machine learning e come viene utilizzato tooaddress previsione energia problemi. Vengono descritti i prerequisiti di hello e criteri di hello qualifica di un caso d'uso. Fornisce anche alcuni casi d'uso di esempio e scenari di casi aziendali.

Dati sono l'elemento principale di hello per qualsiasi di machine learning soluzione. Hello **informazioni sui dati** parte di questo documento vengono illustrati alcuni aspetti importanti dei dati di hello. Vengono descritti il tipo di hello di dati necessari per le previsioni di energia, i requisiti di qualità dei dati e quali origini dati in genere esistono. Viene descritto anche come dati non elaborati hello sono funzioni di unità effettivamente hello parte di modellazione dati tooprepare utilizzato.

Hello terza parte hello documento copre hello **implementazione tecnica** aspetto di una soluzione. Feature team di progettazione e modellazione sono alla base di hello del processo di analisi scientifica dei dati hello e sono pertanto vengono trattate in modo dettagliato. Viene illustrato il concetto di hello di servizi web, ovvero un veicolo importanti per la distribuzione di cloud di soluzioni analitica predittiva. Descrive anche una tipica architettura di soluzione end-to-end operativa

Documento hello include inoltre materiale di riferimento che è possibile utilizzare toogain ulteriormente la comprensione della tecnologia e del dominio hello.

È importante toonote che non si intende toocover in questa documento hello più approfondita dei dati dell'analisi scientifica dei processo gli aspetti matematici e tecnici. Tali informazioni dettagliate sono reperibili nella [documentazione di Azure ML](http://azure.microsoft.com/services/machine-learning/) e nei [blog](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Destinatari
destinatari Hello per questo documento sono aziendali e del personale tecnico che desiderano knowledge toogain e comprensione di Machine Learning basato su come questi vengono utilizzati in modo specifico all'interno di dominio di previsione energia hello e soluzioni.

Gli esperti di dati possono essere utile anche di leggere questo toogain documento una migliore comprensione del processo di livello elevato di hello che unità hello distribuzione dell'energia previsione soluzione. In questo contesto può essere anche usato tooestablish una buona base di riferimento e punto di partenza per ulteriori informazioni dettagliate e avanzate materiale.

### <a name="industry-trends"></a>Tendenze del settore
In hello alcuni anni passati, IoT rinnovabili alternativo e dati sono uniti toocreate opportunità di grande utilità hello e spazio di energia. In hello contemporaneamente, l'utilità hello e settori energetico intera hello sono visto prima consumo appiattimento con consumer complesse toocontrol modi migliori l'uso di energia.

Molte utilità e aziende del settore energetico smart sono stati pioniera a nell'hello [griglia smart](https://en.wikipedia.org/wiki/Smart_grid) distribuendo un numero di utilizzare casi che rendono utilizzano dati hello generate dalla griglia di hello. Molti casi di utilizzo riguardano caratteristiche intrinseche di hello di produzione di elettricità: non possono essere accumulato né archiviato presi in considerazione come inventario. L'energia prodotta deve essere usata. Utilità che desidera toobecome più efficiente necessario consumo di energia elettrica tooforecast semplicemente perché in questo modo le maggiori capacità troppo**bilanciare domanda e offerta**, evitando lo scarto di energia, **ridurre greenhouse emissione di gas**e controllare i costi.

In tema di costi, un altro aspetto importante è quello del prezzo. Nuovo power tootrade di funzionalità tra le utilità hanno portato il bisogno troppo**previsioni sulla domanda futura e prezzo future dell'energia elettrica**. Questo può aiutare le aziende a determinare i volumi di produzione.

Quando si usa word hello 'intelligente', si riferiscono griglia tooa informazioni e quindi eseguire stime. Può prevedere le variazioni stagionali del consumo energetico nonché **situazioni di sovraccarico temporaneo ed eseguire automaticamente le regolazioni necessarie**. Definendo il consumo (con l'aiuto di hello di questi controlli sono smart) in modalità remota, overload localizzata situazioni possono essere gestiti. **Stima di prima e quindi agisce**, griglia hello rende più intelligenti nel tempo.

Per rest hello di questo documento si concentra su un gruppo specifico di casi d'uso che coprono le previsioni del futuro, a breve termine e a lungo termine domanda di energia. Si sta in queste aree per alcuni mesi e già acquisite alcune conoscenze e competenze che consentono di risultati di livello di settore tooproduce. Verranno descritta anche altri casi di utilizzo nel documento hello hello prossimo futuro.

## <a name="business-understanding"></a>Informazioni commerciali
### <a name="business-goals"></a>Obiettivi commerciali
Hello **energia Demo** obiettivo è un tipico analitica predittiva toodemonstrate e machine learning soluzione che può essere distribuita in un intervallo di tempo molto breve. In particolare, l'obiettivo attuale è l'abilitazione di soluzioni di previsione della domanda di energia per valutarne e sfruttarne rapidamente il valore commerciale. informazioni di Hello in questo playbook possono aiutare i clienti di hello il completamento di hello gli obiettivi seguenti:

* Soluzione basata su toovalue breve periodo di tempo di machine learning
* Capacità tooexpand un tooother case utilizzare pilota casi di utilizzo o un ambito più ampio tooa in base alle esigenze aziendali
* Apprendere rapidamente l'uso della suite Cortana Intelligence.

Tenendo presenti questi obiettivi, questo playbook intende fornire business hello e competenze tecniche utili per ottenere questi obiettivi.

### <a name="power-load-and-demand-forecasting"></a>Previsione della domanda e del carico elettrico
All'interno del settore energetico hello, potrebbe essere molti modi in cui richiesta previsione consentono di risolvere problemi aziendali critici. In effetti, la previsione richiesta può essere considerata foundation hello per molti casi di utilizzo di core nel settore hello. In generale, vengono presi in considerazione due tipi di previsione della domanda di energia: a breve termine e a lungo termine. Ognuno di essi può avere uno scopo diverso e usare un approccio differente. Hello differenza principale tra hello due è hello orizzonte, vale a dire hello intervallo di tempo in futuro hello per cui è necessario prevedere la previsione.

#### <a name="short-term-load-forecasting"></a>Previsione di carico a breve termine
Nel contesto di hello della domanda di energia, breve termine caricare previsione (STLF) è definito come carico di aggregati di hello che viene prevista in hello prossimo futuro in varie parti dell'hello (o una griglia hello nel suo complesso). In questo contesto, a breve termine è il limite di tempo toobe definito intervallo hello di ore too24 1 ora. In alcuni casi è anche possibile avere un orizzonte di 48 ore. Pertanto, STLF è molto comune in un caso d'uso operativa della griglia hello. Di seguito sono riportati alcuni esempi di casi d'uso basati sulla previsione di carico a breve termine:

* Bilanciamento della domanda e dell'offerta.
* Supporto alla commercializzazione dell'energia.
* Market making e determinazione del prezzo dell'energia.
* Ottimizzazione operativa della rete.
* [Risposta alla domanda](https://en.wikipedia.org/wiki/Demand_response)
* Previsione dei picchi nella domanda.
* Gestione sul lato della domanda.
* Bilanciamento del carico e prevenzione del sovraccarico.
* Previsione di carico a lungo termine.
* Rilevamento di guasti e anomalie.
* Riduzione e livellamento dei picchi. 

Modello STLF dipendono principalmente hello quasi oltre (ultimo giorno o settimana) i dati di utilizzo e di utilizzo previsti temperatura come un importante fattore di stima. Recupero accurata temperatura previsione per hello un'ora e le ore too24 è sempre minore di una richiesta di verifica giorni ora. Questi modelli sono meno sensibili tooseasonal modelli o le tendenze di utilizzo a lungo termine.

Soluzioni SLTF sono anche probabile toogenerate volume elevato di chiamate di stima (richieste di servizio) poiché viene richiamati su base oraria e in alcuni casi anche con una frequenza maggiore. È inoltre molto comune impianto toosee in cui ogni sottostazione singoli o transformer è rappresentata come un modello autonomo e pertanto volume hello di richieste di stima sono ancora maggiore.

#### <a name="long-term-load-forecasting"></a>Previsione di carico a lungo termine.
obiettivo di Hello di lungo termine carico previsione (LTLF) è richiesta power tooforecast con un limite di tempo che vanno da mesi toomultiple 1 settimana (e in alcuni casi per un numero di anni). Questo orizzonte di previsione si applica principalmente a casi d'uso di pianificazione e investimento.

Per gli scenari a lungo termine, si tratta di dati di alta qualità toohave importante che copre un intervallo di anni più (minimi 3 anni). Questi modelli verranno in genere estrarre dei modelli di stagionalità dai dati cronologici hello e avvalersi della predicators esterna ad come modelli meteo e clima.

È importante tooclarify che hello hello più previsione orizzonte, potrebbe essere hello meno accurate hello previsione. È pertanto importante tooproduce previsione alcuni intervalli di confidenza insieme hello effettivo che permetterebbero comprensibile la possibile variazione hello toofactor nel processo di pianificazione.

Poiché uno scenario di consumo hello per LTLF è principalmente la pianificazione, è possibile previsto molto inferiore volumi stima (come confrontati tooSTLF). È in genere necessario visualizzate queste stime incorporate in strumenti di visualizzazione, ad esempio Excel o Power BI e richiamare manualmente dall'utente hello.

### <a name="short-term-vs-long-term-prediction"></a>Confronto tra la previsione a breve termine e la previsione a lungo termine
Hello nella tabella seguente vengono confrontate STLF e LTLF negli attributi più importanti di riguardo toohello:

| Attributo | Previsione di carico a breve termine | Previsione di carico a lungo termine |
| --- | --- | --- |
| Orizzonte di previsione |Dalle ore too48 1 ora |Da mesi 1 too6 o più |
| Granularità dei dati |Oraria |Oraria o giornaliera |
| Casi d'uso tipici |<ul><li>Bilanciamento di domanda/offerta</li><li>Previsione delle ore di picco</li><li>Risposta alla domanda</li></ul> |<ul><li>Pianificazione a lungo termine</li><li>Pianificazione degli asset della rete</li><li>Pianificazione delle risorse</li></ul> |
| Predittori tipici |<ul><li>Giorno o settimana</li><li>Ora del giorno</li><li>Temperatura oraria</li></ul> |<ul><li>Mese dell'anno</li><li>Giorno del mese</li><li>Condizioni climatiche e temperatura a lungo termine</li></ul> |
| Intervallo di dati storici |Dati relativi a due anni toothree |Dati relativi a cinque anni too10 |
| Precisione tipica |MAPE* pari al 5% o inferiore |MAPE* pari al 25% o inferiore |
| Frequenza di previsione |Ogni ora oppure ogni 24 ore |Mensile, trimestrale o annuale |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error): errore medio assoluto percentuale.

Come si può notare da questa tabella, è molto importante toodistinguish tra hello breve e a lungo termine hello previsione scenari come questi rappresentano le esigenze aziendali diverse e si potrebbe disporre di distribuzione diversi e modelli di utilizzo.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Caso d'uso di esempio 1: eSmart Systems - Ottimizzazione del sovraccarico
Un ruolo importante di un [griglia smart](https://en.wikipedia.org/wiki/Smart_grid) è toodynamically costantemente ottimizzare e regolare per la modifica di modelli di consumo hello. Il consumo energetico può essere influenzato da cambiamenti a breve termine causati principalmente da variazioni della temperatura. *Ad esempio*, i maggiori consumi dovuti all'uso del riscaldamento o dell'aria condizionata. AT hello stesso tempo, alimentazione consumo dipende anche dalla tendenze a lungo termine. Sono inclusi, ad esempio, effetti stagionali, festività nazionali, aumento del consumo a lungo termine e persino fattori economici come l'indice al consumo, il prezzo del greggio e il PIL.

In questo caso, utilizzare [eSmart](http://www.esmartsystems.com/) soluzione toodeploy basato su cloud che consente di tendenza hello stima di una situazione di sovraccarico in qualsiasi dato sottostazione della griglia hello. In particolare, eSmart voleva sottostazioni tooidentify che sono probabilmente toooverload all'interno di hello ora successiva, in modo che un'azione immediata possono essere eseguite tooavoid o risolvere questa situazione.

Una previsione rapida e accurata richiede l'implementazione di tre modelli predittivi:

* Che consente di previsione di consumo di energia elettrica su ogni sottostazione durante hello settimane o mesi successivi alcuni lungo termine modello
* Modello a breve termine che consente di stima della situazione di sovraccarico in un determinato sottostazione durante hello ora successiva
* Modello di temperatura, che consente di prevedere le temperature future in più scenari.

obiettivo di Hello del modello a lungo termine hello è sottostazioni hello toorank da loro toooverload tendenza (assegnato loro capacità di energia elettrica trasmissione) durante hello prossima settimana o mese. Ciò consente di creare hello un breve elenco di sottostazioni utilizzati come input per la stima a breve termine hello. Come temperatura è un fattore di stima importante per il modello a lungo termine hello, non c'è una temperatura di multi-scenario producono tooconstantly necessità previsioni e li feed come input nel modello a lungo termine toohello. a breve termine Hello previsione viene quindi richiamata toopredict quali sottostazione è probabilmente toooverload su hello ora successiva.

i modelli di Hello a breve termine e a lungo termine vengono distribuiti singolarmente per ogni sottostazione. Esecuzione pratiche di hello di questi modelli è pertanto necessario orchestrazione completo. dedicato per ogni ora del giorno hello toogain maggiore accuratezza della stima in hello a breve termine, un modello più granulare. Tutti questi modelli vengono eseguiti ogni ora e terminata l'esecuzione entro pochi minuti tooallow sufficiente tempo toorespond per e intraprendere azioni preventive, se necessario. Questa raccolta di modelli è mantenuta aggiornata tramite periodica ripetizione di training con dati più recenti di hello.

Altre informazioni su questo caso d'uso sono disponibili [qui](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Criteri di qualificazione dei casi d'uso - Prerequisiti
forza principale Hello Intelligence Cortana è il possibilità potente toodeploy e scala machine learning basato su soluzioni. È progettato toosupport migliaia di stime che vengono eseguiti contemporaneamente. È possibile scalare automaticamente toomeet un modello di utilizzo di modifica. La soluzione è quindi incentrata sulla precisione e sulle prestazioni di calcolo. Ad esempio, una società di utilità è interessata alla produzione di domanda di energia accurate previsioni per hello un'ora e per ogni ora del giorno hello. In hello invece, si intende meno rispondere hello domanda del motivo per cui non è richiesta hello toobe stimato perché è (modello hello stesso si occuperà di tale).

È pertanto importante toorealize che non tutti i casi di utilizzo e problemi aziendali possono essere risolto in modo efficace tramite l'apprendimento.

Cortana Intelligence e machine learning può essere estremamente efficiente per risolvere un problema aziendale specifico quando viene soddisfatte hello seguenti criteri:

* è Hello problema aziendale in mano **predittiva** in natura. Un esempio di utilizzo predittiva case è una società di utilità che desidera toopredict power carico su un determinato sottostazione durante hello ora successiva. In hello invece, l'analisi e la classificazione dei driver di richiesta cronologico sarebbe **descrittivo** natura e pertanto meno applicabile.
* È chiaro **percorso dell'azione** toobe una volta eseguita la stima hello è disponibile. Stima di un overload in una sottostazione durante hello ora successiva, ad esempio, può attivare un'azione attiva di ridurre il carico che è associato a tale sottostazione e impedendo potenzialmente un overload.
* rappresenta il caso di utilizzo di Hello un **tipico tipo di problema** in modo che quando è stato risolto può pave hello modo toosolving altri casi di utilizzo simili.
* Imposta cliente Hello **obiettivi quantitativi e qualitativi** toodemonstrate un'implementazione della soluzione corretta. Ad esempio, un obiettivo quantitativo valido per la previsione della domanda di energia sarebbe soglia di accuratezza richiesto hello (*ad esempio*, backup too5 è consentito % errore) o per la stima di overload sottostazione quindi precisione hello (tasso di veri positivi) e richiamo (estensione di veri positivi) deve essere superiore al limite specificato. Questi obiettivi dovrebbero essere derivati da agli obiettivi aziendali del cliente hello.
* È chiaro **lo scenario di integrazione** con flusso di lavoro aziendale della società hello. Ad esempio, hello sottostazione carico previsione può essere integrati in attività di prevenzione di hello griglia controllo center tooallow overload.
* cliente Hello è pronto toouse **dati con una qualità sufficiente** toosupport hello caso d'uso (ulteriori informazioni nella sezione successiva hello, **Data Quality**, di questo playbook).
* architettura incentrate sui dati del cliente abbracci cloud Hello o **apprendimento basato su cloud**, tra cui Azure ML e altri componenti di Cortana Intelligence Suite.
* cliente Hello è tooestablish disposti **un flusso di dati end tooend** che strutture hello la distribuzione di dati nel cloud hello in maniera continuativa e disposti troppo**rendere operative le** hello soluzione.
* cliente Hello è pronto troppo**dedicare risorse** che sarà possibile attivamente durante l'implementazione pilota iniziale hello in modo che può essere Knowledge Base e la proprietà di soluzione hello trasferiti toohello cliente all'esito positivo completamento.
* Hello cliente risorsa deve essere un **professional esperto di dati**, preferibilmente un esperto di dati.

Qualifica di un caso d'uso in base a hello criteri precedenti notevolmente può migliorare le percentuali di successo hello di un caso d'uso e stabilire un buon beachhead per l'implementazione di hello di casi d'uso futuro.

### <a name="cloud-based-solutions"></a>Soluzioni basate sul cloud
Suite di Business Intelligence di Cortana in Azure è un ambiente integrato che si trova nel cloud hello. distribuzione di Hello di una soluzione analitica avanzate in un ambiente cloud contiene notevoli vantaggi per le aziende e in hello contemporaneamente può significare modifica grande per le aziende che comunque usare locali soluzioni IT. All'interno del settore energetico hello, sussiste una tendenza chiara della migrazione graduale delle operazioni in cloud hello. Questa tendenza va paralleli insieme sviluppo hello della griglia smart hello come descritto in precedenza, **le tendenze del settore**. Poiché questo playbook stato attivo si trova in una soluzione basata su cloud in dominio energia hello, è importante tooexplain hello vantaggi e altre considerazioni di distribuzione di una soluzione basata su cloud.

Ad esempio hello principale vantaggio di una soluzione basata su cloud è hello costo. Dal momento che la soluzione fa uso di componenti distribuiti nel cloud, non c'è una componente COGS (costo del venduto) o costi iniziali associati. Ciò significa che non vi è alcun tooinvest necessità di hardware, software e la manutenzione IT ed è pertanto una riduzione notevole il rischio di business.

Un altro vantaggio importante è hello costo consumo struttura di soluzioni basate su cloud. I server basati sul cloud destinati al calcolo o all'archiviazione possono essere distribuiti e ridimensionati in base alle necessità. Questo rappresenta hello costo efficienza sfruttare una soluzione basata su cloud.

Infine, non è necessario per gli investimenti in manutenzione IT o per lo sviluppo futuro di infrastruttura perché tutte queste non fa parte dell'offerta di hello basato su cloud. extent toothat, Cortana Intelligence Suite include hello meglio in servizi di classe e la mappa stradale continua evoluzione. Nuove funzionalità e nuovi componenti vengono introdotti e sviluppati continuamente.

Per una società che è stata appena avviata la transizione allo cloud hello, viene elevata consigliata tootake un approccio graduale implementando una carta stradale migrazione cloud. Riteniamo che per le aziende nel dominio di energia hello e utilità, casi d'uso hello che sono descritti in questo playbook rappresentano un'eccellente opportunità per la distribuzione pilota soluzioni analitica predittiva nel cloud hello.

#### <a name="business-case-justification-considerations"></a>Considerazioni per la motivazione dei casi aziendali
In molti casi, il cliente hello potrebbe essere interessato effettua una motivazione aziendale per un caso di utilizzo specifico in cui una soluzione basata su cloud e Machine Learning sono componenti importanti. A differenza di una soluzione locale, nel caso di hello di una soluzione basata su cloud, il componente di costo iniziale hello è minimo e la maggior parte degli elementi di costo hello sono associata a utilizzo effettivo. Per quanto riguarda toodeploying energia previsione soluzione su Cortana Intelligence Suite, più servizi possono essere integrati con una singola struttura comune di costo. Ad esempio, i database (*ad esempio*, SQL Azure) può essere utilizzato toostore dati non elaborati di hello e quindi per hello effettivo previsioni di Azure ML è usato toohost hello previsione servizi. In questo esempio, la struttura dei costi hello può includere componenti transazionali e archiviazione.

In hello invece uno deve avere una buona conoscenza del valore aziendale hello di operativo di una richiesta di energia previsione (breve o lungo termine). È in realtà, valore di business hello toorealize importante di ogni operazione di previsione. Ad esempio, in modo accurato previsione carico power per hello 24 ore successive possono impedire overproduction o possono aiutare a evitare gli overload nella griglia hello e questo è possibile quantificare in termini di risparmio finanziario su base giornaliera.

Una formula di base per il calcolo entrate hello della domanda di previsione soluzione sarebbe: ![formula di base per il calcolo entrate hello della domanda di previsione soluzione](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Poiché Cortana Intelligence Suite fornisce un modello di determinazione dei prezzi di pagamento a consumo, non è necessario per incorrere in una formula di toothis componente costi fissi. La formula può essere calcolata su base giornaliera, mensile o annuale.

I piani tariffari correnti della suite Cortana Intelligence e di Azure ML sono disponibili [qui](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Processo di sviluppo di soluzioni
ciclo di sviluppo Hello di una richiesta di energia previsione soluzione prevede in genere 4 fasi, in ognuno dei quali si rende l'utilizzo delle tecnologie basate su cloud e servizi all'interno di hello Cortana Intelligence Suite.

Questo comportamento è illustrato nel seguente diagramma hello:

![Ciclo della smart grid](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Hello paragrafo seguente descrive questo processo di 4 passaggio:

1. **Raccolta dei dati**: qualsiasi soluzione basata sull'analisi avanzata si fonda sui dati. Vedere in proposito la sezione **Informazioni sui dati**. In particolare, per quanto riguarda toopredictive analitica e le previsioni, ci si basano su in corso, dinamico e di flusso di dati. In caso di hello della previsione della domanda di energia, questi dati possono derivare direttamente da smart metri o già essere aggregati in un database locale. È possibile basarsi anche su altre origini dati esterne, ad esempio le condizioni meteorologiche e la temperatura. Questo flusso di dati continuo deve essere orchestrato, pianificato e archiviato. [Azure Data Factory](http://azure.microsoft.com/services/data-factory/) è lo strumento principale per eseguire questa attività.
2. **Modellazione** : per le previsioni di energia accurato e affidabile, uno necessario sviluppare (Training) e mantenere un modello ideale che rende la dei dati cronologici hello ed estrae hello significativo e modelli predittivi in hello dati. area Hello di Machine Learning (ML) crescendo rapidamente con gli algoritmi più avanzati in fase di sviluppo regolarmente. Azure ML Studio fornisce un'esperienza utente ottimale che consente di utilizzare hello più avanzate algoritmi di Machine Learning in un flusso di lavoro di completamento. Il flusso di lavoro è illustrata in un diagramma di flusso intuitivo e include la preparazione dei dati hello, estrazione di funzioni, modellazione e valutazione del modello. è possibile includere utente Hello centinaia di vari modelli inclusi in questo ambiente. Per il termine hello di questa fase un esperto di dati disporrà di un modello di lavoro che è completamente valutate e pronto per la distribuzione.
   
   Hello seguente diagramma viene illustrato un tipico flusso di lavoro:
   
   ![Flusso di lavoro di modellazione](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Distribuzione** : con un modello di lavoro a disposizione, hello è la distribuzione. Di seguito modello hello viene convertito in un servizio web che espone un'API RESTful che può essere richiamata contemporaneamente su hello Internet dai vari client consumo. Azure ML fornisce un modo semplice di distribuzione di un modello direttamente dal hello Azure ML Studio con un solo clic di un pulsante. il processo di distribuzione intera Hello avviene quinte hello. Questa soluzione è possibile scalare automaticamente il consumo di hello necessario toomeet.
4. **Consumo** : In questa fase, si rende effettivamente utilizzare hello stime tooproduce modello di previsione. consumo Hello può essere determinato da un'applicazione utente (*ad esempio*, dashboard) oppure direttamente da un sistema operativo, ad esempio richiesta/fornitura bilanciamento del carico di sistema o una soluzione di ottimizzazione della griglia. Più casi d'uso possono essere determinati da un unico modello.

## <a name="data-understanding"></a>Informazioni sui dati
Dopo aver fattori aziendali hello (vedere **comprensione delle esigenze aziendali**) di una richiesta di energia previsione soluzione, è ora sono pronti toodiscuss hello parte di dati. Qualsiasi soluzione di analisi predittiva si basa su dati affidabili. Per la previsione della domanda di energia ci si basa su dati storici relativi al consumo con vari livelli di granularità. I dati cronologici viene utilizzati come hello materie prime. Che verrà sottoposto ad un'analisi accurata nelle quali hello esperto di dati identificata predittori (anche le funzionalità di cui viene fatto riferimento tooas) che possono essere inseriti in un modello che genererà infine previsioni hello necessario.

Nel resto hello di questa sezione verranno descritti hello diversi passaggi e considerazioni per la comprensione dei dati hello e come toobring è tooa utilizzabile.

### <a name="hello-model-development-cycle"></a>Modello di ciclo di sviluppo Hello
Per generare un buon modello di previsione è necessario eseguire un'attenta preparazione e pianificazione. Suddivisione hello in più passaggi di processo di modellazione e concentrarsi su un unico passaggio alla volta può migliorare notevolmente risultato hello dell'intero processo hello.

Hello diagramma seguente illustra come processo di modellazione hello può essere suddivisa in più passaggi:

![Ciclo di sviluppo del modello](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Come mostrato hello ciclo è costituito da sei passaggi:

* Formulazione del problema.
* Inserimento ed esplorazione dei dati.
* Preparazione dei dati e progettazione di funzionalità.
* Modellazione
* Valutazione del modello.
* Sviluppo.

Nel resto di hello di questa sezione si descrive singoli passaggi hello e tooconsider gli elementi in ogni fase.

### <a name="problem-formulation"></a>Formulazione del problema.
È possibile prendere in considerazione formulazione problema hello esigenze hello più importante passaggio uno tooimplementing precedente tootake qualsiasi soluzione analitica predittiva. Qui si trasforma hello problema aziendale e scomporre il toospecific elementi che possono essere risolto utilizzando i dati e le tecniche di modellazione. Si tratta di un problema di hello tooformulate buona norma come una serie di domande desideriamo tooanswer. Di seguito sono riportate alcune domande possibili che possono essere applicati all'interno di ambito hello della previsione della domanda di energia:

* Che cos'è il carico hello previsto in un singolo sottostazione in hello ora o giorno successivo?
* L'ora del giorno hello della griglia, si verificherà picco?
* Qual è la probabilità il carico di picco griglia toosustain hello previsto?
* Quanta capacità durante ogni ora del giorno hello generare stazione power hello?

La formulazione di queste domande consentirà toofocus sul recupero di dati di destra hello e implementare una soluzione completamente allineato al problema aziendale di hello in questione. Inoltre, è quindi possibile impostare alcune metriche chiave che consentono di prestazioni di hello tooevaluate del modello di hello. Ad esempio, il livello di accuratezza deve hello prevedere essere e qual è l'intervallo di hello di errore che è comunque accettabile da business hello?

### <a name="data-sources"></a>Origini dati
griglia smart moderna Hello raccoglie i dati da varie parti e i componenti della griglia hello. Questi dati rappresentano i vari aspetti dell'operazione hello e l'utilizzo di hello della griglia power hello. Nell'ambito di hello di previsione della domanda di energia hello, stiamo limitare il discussione hello su origini dati che riflettono il consumo di hello richiesta effettiva. Un'origine dati importante per il consumo energetico è costituita dai contatori intelligenti. Utilità del mondo hello sono distribuisce rapidamente metri intelligenti per utenti. Smart metri registrano il consumo di energia effettivo hello e costantemente società dati toohello back-utilità di inoltro. Dati raccolti e inviati nuovamente a intervalli fissi, comprese tra ogni ora too1 5 minuti. Metri smart più avanzati possono essere programmati in modalità remota toocontrol e saldo hello consumo effettivo all'interno di una famiglia. I dati forniti dai contatori intelligenti sono relativamente affidabili e includono un timestamp. Questo li rende un elemento importante per la previsione della domanda. Dati misuratore possono essere aggregati (riepilogati) a vari livelli all'interno della topologia di griglia hello: transformer sottostazione, regione, *via*. È quindi possibile selezionare toobuild livello di aggregazione hello richiesto un modello di previsione per tale. Ad esempio, se l'azienda hello come tooforecast future carica in ognuno dei relativi sottostazioni griglia dati di tutti i controlli possono quindi essere aggregati per ogni singolo sottostazione e utilizzati come input per hello modello di previsione. Facciamo riferimento toosmart metri come un'origine dati interna.

Perché una previsione della domanda di energia sia affidabile è necessario avere a disposizione anche origini dati esterne. Un importante fattore che influisce su consumo di energia elettrica è weather hello o più precisamente hello temperatura. I dati storici mostrano una stretta correlazione tra temperatura esterna e consumo energetico. Giorni estate a caldo, rendere i consumer utilizzano della loro condizionatori e durante l'accensione inverno hello in sistemi di riscaldamento. Un'origine affidabile delle temperature cronologiche nella posizione della griglia hello è pertanto chiave. Una previsione accurata delle temperature è un altro predittore del consumo energetico.

Anche altre origini dati esterne possono contribuire alla compilazione di modelli di previsione della domanda di energia. Sono inclusi,*ad esempio*, i cambiamenti climatici a lungo termine, gli indici economici come il PIL e così via. In questo documento non vengono trattate le altre origini dati.

### <a name="data-structure"></a>Struttura dei dati
Dopo l'identificazione di hello necessario origini dati, si potrebbe come tooensure che dati non elaborati che sono stati raccolti includano hello correggere le funzionalità di data. modello di previsione toobuild una richiesta affidabile, è necessario tooensure che i dati raccolti hello include elementi di dati che consentono di stimare la domanda futura hello. Ecco alcuni requisiti di base relativi hello dati struttura (schema) dei dati non elaborati hello.

dati non elaborati Hello è costituito da righe e colonne. Ogni misurazione è rappresentata come una singola riga di dati. Ogni riga di dati include più colonne (anche le funzionalità di cui viene fatto riferimento tooas o campi).

1. **Timestamp** : campo timestamp hello rappresenta il tempo effettivo di hello quando è stato registrato misura hello. Deve essere conformi a uno dei formati di data/ora comuni hello. Devono essere incluse sia la data che l'ora. Nella maggior parte dei casi, non è necessario per hello ora toobe registrate fino a: hello secondo livello di granularità. È importante toospecify hello fuso orario nel quale vengono registrati dati hello.
2. **Controllare l'ID** -questo campo identifica misuratore hello o un dispositivo di misurazione hello. È una variabile di categoria e può essere una combinazione di numeri e lettere.
3. **Il valore di consumo** : si tratta di utilizzo effettivo della hello in una data/ora specificata. consumo Hello può essere misurato in kWh (kilowatt-hour) o qualsiasi altro preferibile unità. È importante toonote che hello unità di misura deve rimanere coerente in tutte le misurazioni nei dati hello. In alcuni casi il consumo può essere fornito in tre fasi di alimentazione. In questo caso è necessario toocollect tutte le fasi di consumo indipendenti hello.
4. **Temperatura** – temperatura hello in genere verrà raccolti da un'origine indipendente. Tuttavia, devono essere compatibile con i dati di utilizzo di hello. Deve includere un timestamp, come descritto in precedenza che ne consentono toobe sincronizzati con i dati di utilizzo effettivo hello. il valore di temperatura Hello può essere specificato in gradi Celsius o gradi Fahrenheit, ma dovrebbe essere sempre coerenza in tutte le misurazioni.
5. **Ubicazione:** campo percorso hello è in genere associato a sul posto di hello in cui sono stati raccolti dati di temperatura hello. Può essere rappresentata come codice di avviamento postale o sotto forma di latitudine/longitudine.

Hello le tabelle seguenti vengono illustrati esempi di un formato di dati di utilizzo e temperatura valido:

| **Data** | **Ora** | **ID contatore** | **Fase 1** | **Fase 2** | **Fase 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Data** | **Ora** | **Posizione** | **Temperatura** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

Come illustrato sopra, questo esempio include tre valori diversi per il consumo associati a tre fasi di alimentazione. Si noti inoltre che i campi di data e ora hello sono separati, tuttavia possono anche essere combinati in una singola colonna. Colonna percorso hello in questo caso è rappresentato in un formato di 5 cifre CAP e temperatura hello in un formato gradi Celsius.

### <a name="data-format"></a>Formato dati
Cortana Intelligence Suite può supportare formati di dati più comuni di hello come CSV, TSV, JSON, *via*. È importante che il formato dati hello rimanga coerenza per hello intero ciclo di vita del progetto hello.

### <a name="data-ingestion"></a>Inserimento di dati
Poiché la previsione della domanda di energia è costantemente e spesso stimata, è necessario assicurarsi che i dati non elaborati hello vengono trasmessi tramite un processo di inserimento dati affidabile e solido. il processo di acquisizione Hello deve garantire che i dati non elaborati hello sono disponibili per hello previsione processo in fase di hello necessario. Questa situazione implica che la frequenza di inserimento dati hello deve essere maggiore di hello previsione frequenza.

Ad esempio: se la richiesta di previsione soluzione genera una nuova previsione alle ore 8:00 su base giornaliera, è necessario tooensure che tutti i dati raccolti durante hello hello ultima 24 ore è completamente caricamento fino a quel punto e tooeven includono hello ultima ora di dati.

In ordine tooaccomplish, Cortana Intelligence Suite offre vari modi toosupport un processo di acquisizione affidabile dei dati. Questo verrà discussa ulteriormente in hello **distribuzione** sezione di questo documento.

### <a name="data-quality"></a>Qualità dei dati
origine dati non elaborati Hello che è necessaria per eseguire la previsione richiesta affidabile e accurato deve soddisfare i criteri di qualità alcuni dati di base. Anche se i metodi statistici avanzati possono essere utilizzato toocompensate per un problema di qualità di dati, è comunque necessario tooensure che ci stiamo che attraversano una soglia di qualità di dati di base durante l'inserimento di nuovi dati. Di seguito sono riportate alcune considerazioni sulla qualità dei dati non elaborati:

* **Valore mancante** -si riferisce toohello situazione quando non è stato raccolto misura specifica. Hello requisito di base qui è che hello manca il tasso di valore non deve essere superiore al 10% per un periodo di tempo specificato. Un singolo valore mancante dovrà essere indicato usando un valore predefinito, ad esempio "9999", e non "0" che può essere una misurazione valida.
* **Accuratezza di misurazione** : hello effettivo valore consumo o temperatura deve essere registrato in modo accurato. Misurazioni poco accurate generano previsioni imprecise. Errore di misurazione hello in genere, deve essere inferiore al valore di % 1 relativo toohello true.
* **Tempo di misurazione** : è necessario tale timestamp effettivo hello di hello dati raccolti verranno deviare non più di 10 secondi relativo toohello true ora di misurazione effettiva hello.
* **Sincronizzazione** : quando si usano più origini dati,*ad esempio*il consumo e la temperatura, è necessario assicurarsi che non presentino problemi di sincronizzazione. Ciò significa che ora hello differenza tra il timestamp di hello raccolti da qualsiasi origine dati indipendenti due non deve superare più di 10 secondi.
* **Latenza**: come illustrato nella sezione **Inserimento di dati**, un flusso di dati affidabile e il processo di inserimento sono componenti fondamentali. toocontrol che è necessario assicurarsi che controllo di latenza dei dati hello. Questo valore è specificato come differenza di tempo hello tra l'ora di hello hello effettivo misurazione e l'ora di hello in corrispondenza del quale è stato caricato in archiviazione di Cortana Intelligence Suite hello e pronto per essere utilizzato. Per il carico a breve termine latenza totale di previsione hello non deve essere maggiore di 30 minuti. Per il carico a lungo termine latenza totale di previsione hello non deve essere maggiore di 1 giorno.

### <a name="data-preparation-and-feature-engineering"></a>Preparazione dei dati e progettazione di funzionalità.
Una volta che sono stata caricamento dati non elaborati hello (vedere **inserimento di dati**) ed è stato in modo sicuro archiviati, è pronto toobe elaborati. Hello fase di preparazione dei dati è fondamentalmente richiede dati non elaborati hello e conversione (trasformazione, modificare la forma) in un formato per la fase di modellazione hello. Che può includere operazioni semplici come l'utilizzo di colonna di dati non elaborati hello è con relativo effettivo valore misurato, standard di valori, le operazioni più complesse, ad esempio [tempo di ritardo](https://en.wikipedia.org/wiki/Lag_operator)e altri. colonne di dati Hello appena creato sono funzionalità dati di cui viene fatto riferimento tooas e processo hello di generazione di questi è engineering funzionalità tooas cui viene fatto riferimento. Dall'entità finale di questo processo hello abbiamo un nuovo set di dati che è stato derivato da dati non elaborati hello e può essere utilizzato per la modellazione. In fase di preparazione dei dati hello inoltre, è necessario tootake cure valori mancanti (vedere **Data Quality**) e li compensare. In alcuni casi, è anche necessario toonormalize hello dati tooensure che tutti i valori sono rappresentati in hello stessa scala.

In questa sezione che verranno descritte alcune delle funzionalità di dati comuni hello inclusi in energia hello i modelli di previsione della domanda.

**Ora funzionalità basate su:** queste funzionalità sono derivate dai dati di date o timestamp hello. Tali dati vengono estratti e convertiti in funzionalità categoriche quali:

* Ora del giorno: si tratta di hello ora hello che acquisisce i valori 0 too23
* Giorno della settimana: questo rappresenta hello giorno della settimana hello e acquisisce i valori 1 (domenica) too7 (sabato)
* Giorno del mese: ciò rappresenta la data effettiva di hello e può accettare valori da 1 too31
* Mese dell'anno: ciò rappresenta il mese di hello e acquisisce i valori 1 (gennaio) too12 (dicembre)
* Fine settimana-questa è una funzionalità a valore binario che accetta valori hello pari a 0 per giorni della settimana o 1 per i fine settimana
* Giorno festivo - questa è una funzionalità a valore binario che accetta valori hello pari a 0 per un giorno regolare o 1 per un giorno festivo
* Termini Fourier: hello Fourier termini sono pesi che derivano da timestamp hello e vengono utilizzati toocapture hello stagionalità (cicli) nei dati hello. Dato che nei dati sono presenti più stagioni, possono essere necessari più termini di Fourier. Ad esempio, se i valori della domanda hanno stagioni/cicli annuali, settimanali e giornalieri saranno necessari tre termini di Fourier.

**Funzionalità di misurazione indipendenti:** hello indipendente comprende tutti gli elementi di dati hello che si desidera utilizzare toouse come variabili predittive nel modello in esame. Qui sono esclusi i funzionalità dipendente hello che sarà necessaria toopredict.

* La funzione Lag: sono ora spostato i valori della richiesta effettiva hello. Ad esempio, lag 1 funzionalità conterrà il valore di richiesta di hello in timestamp corrente relativo toohello ora precedente (presupponendo che i dati ogni orari) di hello. Allo stesso modo, è possibile aggiungere ritardo 2, 3, di ritardo *via*. combinazione effettivo di hello di funzionalità di ritardo che vengono utilizzati vengono determinati durante la fase di modellazione hello dalla valutazione di risultati del modello hello.
* A lungo termine tendenza: questa funzionalità rappresenta hello lineare aumento della domanda tra gli anni.

**Funzionalità dipendente:** funzionalità dipendente hello è colonna di dati hello cui desideriamo toopredict il modello. Con [l'apprendimento supervisionato](https://en.wikipedia.org/wiki/Supervised_learning), è necessario innanzitutto eseguire il training modello di hello utilizzando le funzionalità dipendenti hello (che è anche le etichette di cui viene fatto riferimento tooas). In questo modo i dati di hello associati alla funzionalità dipendente hello hello modello toolearn hello dei modelli. In previsione della domanda di energia è in genere consigliabile toopredict domanda effettiva di hello e pertanto è necessario usarla come funzionalità dipendente hello.

**La gestione dei valori mancanti:** durante la fase di preparazione dati hello, dobbiamo toodetermine hello migliore strategia toohandle valori mancanti. Questa funzionalità è particolarmente utilizzando hello varie statistiche [i metodi di imputazione dati](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). In caso di hello della domanda di energia di previsione, in genere è necessario attribuire valori mancanti usando Media mobile dai punti di dati disponibili precedente.

**Normalizzazione dei dati:** normalizzazione dei dati è un altro tipo di trasformazione che viene utilizzato toobring tutti i dati numerici, ad esempio la domanda di previsione in una scala simile. Ciò in genere consente di migliorare la precisione e accuratezza del modello hello. È in genere questa operazione viene effettuata dividendo valore effettivo di hello per intervallo hello di dati di hello.
Valore originale di hello verranno ridimensionate verso il basso in un intervallo più piccolo, in genere compreso tra -1 e 1.

## <a name="modeling"></a>Modellazione
fase di modellazione Hello è in cui la conversione di hello dei dati hello in un modello viene eseguita. In hello core di questo processo vi sono avanzati algoritmi di analisi dati cronologici hello (dati di training), estrarre modelli e compilare un modello. Tale modello può essere in seguito utilizzati toopredict sui nuovi dati non sono stato modello hello toobuild utilizzato.

Una volta ottenuto un utilizzo affidabile modello per poterlo quindi utilizzare tooscore nuovi dati strutturati tooinclude hello richiesta funzionalità (X). processo di classificazione Hello renderà del modello persistente hello (oggetto dalla fase di training hello) e variabile di destinazione hello è identificata da Ŷ di stima.

### <a name="demand-forecasting-modeling-techniques"></a>Tecniche di modellazione della previsione della domanda
Nel caso di hello di previsione rendiamo richiesta utilizzare i dati cronologici che viene ordinati in base al tempo. Si riferiscono in genere toodata che include una dimensione temporale hello come [ora serie](https://en.wikipedia.org/wiki/Time_series). obiettivo di Hello modellizzazione della serie è ora toofind relative tendenze, stagionalità, auto-correlazione (correlazione nel tempo) e formulare tali file in un modello.

Negli ultimi anni algoritmi avanzati sono state sviluppate tooaccommodate ora serie previsione e tooimprove previsione accuratezza. Alcuni di questi vengono illustrati brevemente in questa sezione,

> [!NOTE]
> In questa sezione non è previsto toobe utilizzato come una macchina di apprendimento e le previsioni Panoramica ma piuttosto come un sondaggio tecniche di uso comune per la richiesta di previsione di modellazione. Per ulteriori informazioni e la documentazione sulle previsioni serie di tempo, si consiglia di libri online hello [Forecasting: principi e procedure consigliate](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**Media mobile**](https://www.otexts.org/fpp/6/2)
Media mobile è uno dei hello prima le tecniche di analisi che è stato utilizzato per la previsione delle serie di tempo ed è ancora una delle tecniche di hello più comunemente usato a partire da oggi. È inoltre foundation hello per più avanzate tecniche di previsione. Con la media mobile è stiamo previsione punto dati successivo hello, calcolando la media su hello K dati più recenti, dove K indica l'ordine di hello di hello Media mobile.

tecnica di Media mobile Hello ha effetto hello anti-aliasing hello previsione e pertanto non può gestire la volatilità e grandi dimensioni nei dati hello.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**Smorzamento esponenziale**](https://www.otexts.org/fpp/7/5)
Anti-aliasing esponenziale (ETS) è una famiglia di diversi metodi che usano Media ponderata dei punti dati recenti nell'ordine toopredict hello Avanti dato. idea Hello è pesi superiori tooassign valori recenti toomore e ridurre gradualmente il peso per valori misurati precedenti. Esistono diversi modi con questa famiglia, alcuni di essi includono, ad esempio, la gestione della stagionalità nei dati hello [metodo stagionali Holt Winters](https://www.otexts.org/fpp/7/5).

Alcuni di questi metodi anche scomporre in stagionalità hello dei dati di hello.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**Modello autoregressivo integrato a media mobile (ARIMA)**](https://www.otexts.org/fpp/8)
Il modello autoregressivo integrato a media mobile (ARIMA) raggruppa un'altra famiglia di metodi comunemente usati per la previsione basata sulle serie storiche. Unisce i metodi autoregressivi alla media mobile. Metodi di regressione di automatica utilizzano i modelli di regressione creando precedente serie i valori in ordine toocompute hello successivo data punto. Metodi ARIMA si applicano anche differenze i metodi che includono il calcolo hello differenza tra i punti dati e con quelli anziché valore misurato originale hello. Infine, ARIMA si avvale anche di hello spostamento medie tecniche che vengono discussi in precedenza. combinazione di Hello di tutti questi metodi in vari modi è quali costrutti hello famiglia di metodi ARIMA.

ARIMA e smorzamento esponenziale sono ampiamente usati per la previsione della domanda di energia e per molti altri problemi di previsione. In molti casi queste sono combinate insieme toodeliver molto precisa.

**Regressione più generale** i modelli di regressione potrebbe essere l'approccio di modellazione più importante di hello all'interno di dominio hello di machine learning e statistiche. Nel contesto di hello di serie temporale utilizziamo valori futuri di regressione toopredict hello (*ad esempio*, di richiesta). Nella regressione è eseguire una combinazione lineare di variabili predittive hello e informazioni pesi hello (anche i coefficienti di cui viene fatto riferimento tooas) di tali variabili predittive durante il processo di training hello. obiettivo di Hello è tooproduce una retta di regressione che verrà prevedere il valore stimato. Metodi di regressione sono adatti quando la variabile di destinazione hello è numerica e pertanto anche adatta previsione serie di tempo. La vasta gamma dei metodi regressivi esistenti include modelli regressivi molto semplici, come la [regressione lineare](https://en.wikipedia.org/wiki/Linear_regression), e altri più avanzati, come gli alberi di decisione, le [foreste casuali](https://en.wikipedia.org/wiki/Random_forest), le [reti neurali](https://en.wikipedia.org/wiki/Artificial_neural_network) e gli alberi di decisione con boosting.

Costruzione di richiesta di energia di previsione di un problema di regressione offre una notevole flessibilità nella selezione delle funzionalità dei dati che possono essere combinate da fattori esterni, ad esempio temperatura e di dati della serie temporale hello richiesta effettiva. Ulteriori informazioni sulle funzionalità di hello selezionato vengono discussi in hello Engineering funzionalità (vedere **preparazione dei dati e funzionalità Engineering**) sezione di questo playbook.

Dall'esperienza acquisita con l'implementazione e distribuzione del progetto pilota previsioni della domanda di energia, è stato rilevato che i modelli di regressione avanzate disponibili in Azure Machine Learning hello tendono tooproduce ottenere risultati ottimali hello e rendiamo loro utilizzo.

## <a name="model-evaluation"></a>Valutazione del modello.
Valutazione del modello ha un ruolo fondamentale all'interno di hello **ciclo di sviluppo modello**. In questo passaggio vengono esaminati convalida modello hello e le prestazioni con dati reali. Durante il passaggio di modellazione hello utilizziamo una parte dei dati di hello disponibili per il training del modello di hello. Durante la fase di valutazione hello Adotteremo resto hello hello tootest hello di modello di data. In pratica significa che ci stiamo alimentazione hello modello nuovi dati che sono stati rinnovati e contiene hello stesse caratteristiche disponibili come hello training set. Tuttavia, durante il processo di convalida hello, si usa variabile di destinazione di hello modello toopredict hello anziché specificare la variabile di destinazione disponibili hello. Spesso, ci si riferisce toothis processo come modello di punteggio. È quindi verranno utilizzati i valori di destinazione true hello e confronto con hello stimato quelle. obiettivo Hello è toomeasure e ridurre al minimo di errore di stima hello, vale a dire hello differenza stime hello e il valore true hello. Quantifica di misurazione errore hello è chiave poiché si desideri modello hello toofine ottimizzare e verificare se l'errore hello effettivamente diminuisce. Modello di ottimizzazione hello può essere eseguita modificando i parametri di modello che controllano il processo di apprendimento hello, o aggiungendo o rimuovendo le funzionalità di data (cui tooas [durante lo sweep di parametri](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). In pratica, ciò significa che è possibile che vengano tooiterate tra Progettazione funzionalità hello, modellazione, è necessario e le fasi di valutazione del modello più volte fino a quando non si sono in grado di tooreduce hello errore toohello richiesto livello.

È importante tooemphasis che errore stima hello non potranno mai essere pari al numero zero non è mai un modello che è possibile stimare perfettamente ogni risultato. Tuttavia, è di grandezza di errore che è accettabile per il business hello. Durante il processo di convalida hello, desideriamo tooensure che l'errore di stima del modello è in hello livello o di prestazioni migliori rispetto a tolleranza di business hello. È pertanto importante livello hello tooset di errore di tollerabile hello all'inizio di hello di hello ciclo durante hello **formulazione problema** fase.

### <a name="typical-evaluation-techniques"></a>Tecniche di valutazione tipiche
L'errore di previsione può essere misurato e quantificato in vari modi. In questa sezione esamineremo discussione hello per le serie tootime rilevanti tecniche di valutazione e in specifico per la previsione della domanda di energia.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE è l'acronimo di Mean Absolute Percentage Error, errore medio assoluto percentuale. Con MAPE ci stiamo calcolo differenza di hello tra ogni punto previsto e il valore effettivo di hello di tale punto. È quindi quantificano errore hello per ogni punto calcolando la proporzione di hello del valore effettivo di hello differenza toohello relativo. L'ultimo passaggio consiste nel calcolare la media di questi valori. formula matematica di Hello utilizzata per MAPE può essere seguito hello:

![Formula MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*in cui A<sub>t</sub> è hello valore effettivo, F<sub>t</sub> hello valore stimato e n è hello orizzonte di previsione.*

## <a name="deployment"></a>Distribuzione
Una volta abbiamo enorme hello fase di modellazione e convalidare le prestazioni del modello hello siamo toogo pronto in fase di distribuzione hello. In questo contesto, distribuzione indica l'abilitazione di cliente hello tooconsume hello modello eseguendo stime effettive su di esso su vasta scala. il concetto di Hello di distribuzione è chiave in Azure Machine Learning perché l'obiettivo principale è tooconstantly richiamare stime come toojust anziché ottenere una visione hello dai dati hello. fase di distribuzione Hello è parte di hello in cui si abilita hello modello toobe utilizzati in larga scala.

Nel contesto di hello di previsione della domanda di energia, il nostro obiettivo è tooinvoke continua e periodica previsioni assicurando che dati aggiornati sono disponibili per il modello di hello che hello ha pianificato l'invio dei dati back-toohello dispendiosa in termini di client.

### <a name="web-services-deployment"></a>Distribuzione di servizi Web
Hello principale distribuibile blocco predefinito in Azure Machine Learning è servizio web hello. Si tratta di hello più efficace modo tooenable utilizzo di un modello predittivo in cloud hello. servizio Web Hello incapsula modello hello e conclude con un [RESTful](http://www.restapitutorial.com/) API (Application Programming Interface). Hello API utilizzabile come parte del codice client, come illustrato nel seguente diagramma hello.

![Distribuzione del servizio e consumo](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Come si può notare, servizio web hello viene distribuito nel cloud Cortana Intelligence Suite hello e può essere richiamata su endpoint API REST esposta. Un tipo diverso di client tra domini diversi è possibile richiamare servizio hello tramite hello API Web contemporaneamente. servizio web Hello consentendogli di supportare migliaia di chiamate simultanee.

### <a name="a-typical-solution-architecture"></a>Esempio di architettura della soluzione tipica
Quando si distribuisce una richiesta di energia previsione soluzione, siamo interessati all'implementazione di una soluzione di tooend end che va oltre al servizio web di stima hello e facilita il flusso di dati intero hello. In fase di hello che è richiamare una nuova previsione, dobbiamo toomake che tale modello hello verrà immesse con le funzionalità di dati aggiornati. Questa situazione implica che hello appena raccolti i dati non elaborati sono costantemente caricamento, elaborati e trasformati in set su cui è stato compilato il modello di cui hello di funzionalità richiesto hello. AT hello stesso tempo, si desidera toomake hello previsti sono disponibili dati per hello terminano dispendiosa in termini di client. Un esempio dati ciclo flusso (o dati pipeline) viene illustrata nel diagramma hello riportato di seguito:

![TooEnd fine del flusso di dati di previsione della domanda di energia](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Questi passaggi hello che si verificano come parte del ciclo di previsione di hello energia richiesta:

1. Milioni di contatori di dati distribuiti generano continuamente dati sul consumo energetico in tempo reale.
2. I dati vengono raccolti e caricati in un repository cloud,*ad esempio*BLOB di Azure.
3. Prima di essere elaborato, dati non elaborati hello sono sottostazione tooa aggregati o a livello regionale definito dal business hello.
4. l'elaborazione di Hello funzionalità (vedere **preparazione dei dati e funzionalità di elaborazione**) quindi viene eseguita e produce hello i dati necessari per modellare training o la valutazione: hello funzionalità set vengono memorizzati in un database (*, ad esempio*, SQL Azure).
5. viene richiamato Hello riesecuzione del training servizio hello toore train previsione – modello di versione aggiornata del modello di hello è persistente in modo che può essere utilizzato dal servizio web di punteggio hello.
6. servizio web di punteggio Hello viene richiamato in una pianificazione che si adatta a frequenza previsione hello necessario.
7. Hello previsti dati vengono archiviati in un database accessibile dal client di consumo fine hello.
8. Hello consumo client recupera le previsioni hello, viene applicato alla griglia hello e utilizza in base al caso d'uso hello necessario.

È importante toonote che l'intero ciclo di completamente automatizzato e viene eseguito in base a una pianificazione. può eseguire l'intera orchestrazione di Hello del ciclo dati tramite gli strumenti, ad esempio [Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Terminare tooEnd architettura di distribuzione
In ordine toopractically distribuire una soluzione di previsione di richiesta energia Cortana Intelligence, è necessario tooensure che i componenti necessario di hello sono stabiliti e configurati correttamente.

Hello seguente diagramma viene illustrata un'architettura tipica di Business Intelligence di Cortana in base che implementa e gestisce il ciclo di flusso di dati hello è descritto in precedenza:

![Terminare tooEnd architettura di distribuzione](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Per ulteriori informazioni su ognuno dei componenti di hello e hello intera architettura, vedere il modello di soluzione energia toohello.

