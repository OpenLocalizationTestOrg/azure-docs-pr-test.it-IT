---
title: durata del processo di analisi scientifica dei dati di Team aaaAzure | Documenti Microsoft
description: Passaggi necessari tooexecute i progetti di analisi scientifica dei dati.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Ciclo di vita del processo di analisi scientifica dei dati per i team

Hello Team Data Science processo (TDSP) fornisce un ciclo di vita consigliata che è possibile utilizzare toostructure i progetti di analisi scientifica dei dati. ciclo di vita Hello descrive i passaggi di hello, dall'inizio toofinish, i progetti seguenti in genere quando vengono eseguiti. Se si utilizza un altro del ciclo di analisi scientifica dei dati, ad esempio [metodologia](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) o un processo personalizzato dell'organizzazione, è comunque possibile usare hello TDSP basato su attività con i cicli di vita di sviluppo. 

Questo ciclo di vita è stato progettato per i progetti di analisi scientifica dei dati che sono previsti tooship come parte di applicazioni intelligenti. Queste applicazioni distribuiscono modelli di Machine Learning o intelligenza artificiale per l'analisi predittiva. Anche i progetti di data science esplorativi e i progetti analitici ad hoc possono trarre vantaggio dall'utilizzo di questo processo. Ma in questi casi alcuni dei passaggi descritti possono non essere necessari.    

Ecco una rappresentazione visiva di hello **ciclo di vita del processo di analisi scientifica dei dati di Team**. 

![Ciclo di vita TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

ciclo di vita TDSP Hello è costituito da cinque fasi principali che vengono eseguite in modo iterativo. incluse le seguenti:

* **Informazioni commerciali**
* **Acquisizione e comprensione dei dati**
* **Modellazione**
* **Distribuzione**
* **Accettazione del cliente**

Per ogni fase, forniamo hello le seguenti informazioni:

* **Obiettivi**: hello obiettivi specifici.
* **Modalità toodo è**: hello attività specifiche descritte e informazioni aggiuntive fornite al loro completamento.
* **Elementi**: i risultati finali hello e hello il supporto per la produzione.


## <a name="1-business-understanding"></a>1. Informazioni commerciali

### <a name="goals"></a>Obiettivi
* Hello **chiave variabili** sono specificate che sono tooserve come hello **modello destinazioni** e vengono utilizzate i cui metriche correlate determinare hello riuscita per il progetto hello.
* Hello rilevante **origini dati** vengono identificati che disponga di accesso tooor esigenze tooobtain business hello.

### <a name="how-toodo-it"></a>Come toodo,
Questa fase comprende due attività principali: 

* **Definizione degli obiettivi**: collaborare con il cliente e toounderstand altre parti interessate e identificare i problemi di business hello. Formulare domande che definiscono gli obiettivi aziendali hello e che le tecniche di analisi scientifica dei dati possono essere destinati.
* **Identificare le origini dati**: ricerca hello dati rilevanti che consentono di rispondono alle domande di hello che definiscono gli obiettivi di hello del progetto hello.

#### <a name="11-define-objectives"></a>1.1 Definire gli obiettivi

1. Un obiettivo centrale di questo passaggio è chiave hello tooidentify **variabili aziendali** che analysis hello deve toopredict. Queste variabili sono hello cui tooas **modello destinazioni** e metriche hello associate vengono utilizzati toodetermine hello successo del progetto hello. Due esempi di tali destinazioni sono probabilità di previsione o hello delle vendite di un ordine di frode.

2. Definire hello **gli obiettivi del progetto** da cui viene richiesto e il perfezionamento "sharp" questioni rilevanti e specifiche e non ambiguo. Analisi scientifica dei dati è il processo di hello di utilizzo di nomi e numeri tooanswer tali domande. Per ulteriori informazioni sulle domande acuto, vedere [come toodo analisi scientifica dei dati](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blog. Analisi scientifica dei dati / machine learning è in genere utilizzate tooanswer cinque tipi di domande:
 
   * In che quantità o in che numero? (regressione)
   * Quale categoria? (classificazione)
   * Quale gruppo? (clustering)
   * È strano? (rilevamento anomalie)
   * Quale opzione scegliere? (suggerimento)

    Determinare quali di queste domande si sta ponendo e come rispondendo ad esse sia possibile conseguire gli obiettivi aziendali.

3. Definire hello **progetto team** specificando hello ruoli e responsabilità dei relativi membri. Sviluppare un piano di alto livello da ripetere man mano che la quantità di informazioni acquisite aumenta.  

4. **Definire le metrica di riuscita**. Ad esempio: ottenere l'accuratezza della stima della varianza del cliente di 0x % dall'entità finale di questo progetto di 3 mesi, hello in modo che possiamo offrire promozioni tooreduce varianza. devono essere metriche Hello **SMART**: 
   * **S**pecific: specifiche 
   * **M**easurable: misurabili
   * **A**chievable: conseguibili 
   * **R**elevant: rilevanti 
   * **T**ime-bound: con associazione temporale 

#### <a name="12-identify-data-sources"></a>1.2 Identificare le origini dei dati
Identificare le origini dati che contengono esempi di domande acuto tooyour di risposte. Cercare hello dati seguenti:

* I dati **relativo** toohello domanda. Sono presenti misure di destinazione hello e le funzionalità correlate toohello destinazione?
* Dati che sono un **misure Accurate** delle funzionalità del modello hello e di destinazione di interesse.

Non è insolito, ad esempio, toofind che i sistemi esistenti devono toocollect e registrare altri tipi di dati tooaddress hello problema e ottenere gli obiettivi del progetto hello. In questo caso, è possibile utilizzare toolook per origini dati esterne o aggiornare i dati di nuovo toocollect sistemi.

### <a name="artifacts"></a>Elementi
Ecco i risultati finali hello in questa fase:

* [**Noleggiare documento**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): un modello standard viene fornito nella definizione della struttura progetto TDSP hello. Si tratta di un documento che viene aggiornato in tutto il progetto di hello quando vengono effettuate nuove scoperte e come business cambiano i requisiti in evoluzione. chiave di Hello è tooiterate su questo documento, l'aggiunta di ulteriori dettagli, come è stato di avanzamento tramite il processo di individuazione hello. Keep hello cliente e altre parti interessate coinvolte effettuare modifiche hello e chiaro motivi hello toothem modifiche hello.  
* [**Origini dati**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): si tratta di hello **origini dati non elaborati** sezione di hello **le definizioni dei dati** report presenti nel progetto TDSP hello **Report dei dati**  cartella. Specifica hello originale e percorsi di destinazione per i dati non elaborati hello. In un secondo momento, è inserire ulteriori dettagli, ad esempio gli script toomove hello tooyour dati analitici ambiente.  
* [**I dizionari di dati**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): questo documento fornisce le descrizioni dei dati di hello fornito dal client hello. Queste descrizioni includono informazioni sullo schema hello (tipi di dati, informazioni sulle regole di convalida, se presente) e hello diagrammi di entità e relazioni, se disponibile.


## <a name="2-data-acquisition-and-understanding"></a>2. Acquisizione e comprensione dei dati

### <a name="goals"></a>Obiettivi
* Pulizia di alta qualità set di dati vengono riconosciute le variabili di destinazione i cui toohello relazioni che si trovano in ambiente di hello analitica appropriato toomodel pronto.
* Un'architettura della soluzione di hello dati pipeline toorefresh e punteggio dati regolarmente sviluppati.

### <a name="how-toodo-it"></a>Come toodo,
Questa fase comprende tre attività principali:

* **Inserimento dati hello** nell'ambiente di hello destinazione analitico.
* **Esplorare i dati di hello** toodetermine se la qualità dei dati hello è domanda hello tooanswer adeguate. 
* **Configurare una pipeline di dati** tooscore new o regolarmente l'aggiornamento dati.

#### <a name="21-ingest-hello-data"></a>2.1 inserimento dati hello
Imposta i dati di hello hello processo toomove da percorsi di origine toohello i percorsi di destinazione in cui operazioni di analitica come training e le stime sono toobe eseguita. Per informazioni tecniche e le opzioni su toodo con vari servizi di dati di Azure, vedere [caricare i dati in ambienti di archiviazione per analitica](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 esplorare dati hello
Prima di eseguire il training dei modelli, è necessario conoscere a fondo i dati di hello toodevelop. I set di dati reali sono spesso fastidiosi, mancano di valori, sono numerosi o presentano altre discrepanze. Visualizzazione e riepilogo dei dati sono utilizzati tooaudit hello qualità dei dati e fornire informazioni hello necessari tooprocess hello dati prima che sia pronto per la modellazione. Spesso, questo processo è iterativo.

TDSP fornisce un'utilità automatica denominata [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp visualizzare i dati di hello e preparare i report di riepilogo dei dati. È consigliabile iniziare con IDEAR prima tooexplore hello dati toohelp sviluppare comprensione iniziale dei dati in modo interattivo con alcun codice e quindi scrivere codice personalizzato per la visualizzazione ed esplorazione dei dati. Per ulteriori informazioni sulla pulizia dei dati di hello, vedere [tooprepare dati per l'apprendimento automatico migliorato attività](machine-learning-data-science-prepare-data.md).  

Dopo avere effettuato con una qualità dei dati pulito hello hello, hello sarà toobetter comprendere i modelli di hello che vengono svolte in dati hello che consentono di scelgono e sviluppano un modello predittivo appropriato per la destinazione. Cercare le prove per l'accuratezza dei dati connessi hello sono toohello destinazione e se è sufficiente toomove dati avanti con passaggi modellazione hello. Anche questo processo è iterativo. Potrebbe essere necessario toofind nuove origini dati con più accurato o più pertinente tooaugment hello set di dati identificato nella fase precedente hello.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 Impostare una pipeline di dati
Inoltre inserimento iniziale toohello e pulizia di hello dati, in genere necessario tooset di un processo tooscore nuovi dati o di un aggiornamento dei dati hello regolarmente come parte di un processo di apprendimento in corso. Per ottenere questo risultato, è possibile configurare una pipeline di dati o un flusso di lavoro. Ecco un [esempio](machine-learning-data-science-move-sql-azure-adf.md) come tooset di una pipeline con [Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

Un'architettura della soluzione della pipeline di dati hello è stata sviluppata in questa fase. pipeline Hello inoltre viene sviluppata in parallelo con hello seguenti fasi di progetto di analisi scientifica dei dati hello. pipeline Hello può essere basata su batch o di flusso/reale-tempo o una configurazione ibrida a seconda dell'azienda deve e hello vincoli dei sistemi esistenti in cui questa soluzione integrata. 

### <a name="artifacts"></a>Elementi
di seguito Hello sono i risultati finali hello in questa fase.

* [**Il Report qualità di dati**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): il report contiene i riepiloghi dei dati, le relazioni tra ogni attributo e destinazione, variabile classificazione hello e così via [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) strumento fornito come parte di TDSP è possibile generare rapidamente Questo report per qualsiasi set di dati tabulare, ad esempio un file CSV o una tabella relazionale. 
* **Architettura della soluzione**: può trattarsi di un diagramma o la descrizione del punteggio di dati utilizzata pipeline toorun o stime sui nuovi dati dopo aver creato un modello. Contiene inoltre hello pipeline tooretrain il modello basato su nuovi dati. documento Hello viene archiviato in hello [progetto](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) directory quando si utilizza modello di struttura di directory TDSP hello.
* **Decisione di Checkpoint**: prima di iniziare la progettazione di funzionalità completo e la compilazione del modello, è possibile riesaminare hello progetto toodetermine se è previsto un valore hello è sufficiente toocontinue auspicabile. Si potrebbe, ad esempio, essere tooproceed pronto, è necessario toocollect più dati o abbandonare progetto hello come dati hello inesistente domanda hello tooanswer.


## <a name="3-modeling"></a>3. Modellazione

### <a name="goals"></a>Obiettivi
* Funzionalità ottimale dei dati per il modello di apprendimento automatico hello.
* Modello informativo di ML che stima destinazione hello in modo più accurato.
* Un modello ML adatto per la produzione.

### <a name="how-toodo-it"></a>Come toodo,
Questa fase comprende tre attività principali:

* **Funzionalità di progettazione**: creare funzionalità dati di training del modello toofacilitate hello dati non elaborati.
* **Training del modello**: trovare il modello di hello domanda risposte hello in modo più accurato confrontando le metriche di successo.
* Stabilire se il modello è **adatto alla produzione**.

#### <a name="31-feature-engineering"></a>3.1 Progettazione delle funzioni
Progettazione funzionalità comporta l'inclusione, aggregazione e trasformazione di variabili non elaborato toocreate hello funzionalità utilizzate nell'analisi hello. Se si desidera approfondite fattori da un modello, è necessario toounderstand come funzionalità sono correlati tooeach altri e come algoritmi di machine learning hello sono toouse tali funzionalità. Questo passaggio richiede una combinazione di competenze e approfondimenti ottenute nel passaggio di esplorazione dati hello creativa. Si tratta di un compromesso di ricerca e inclusione di variabili informative evitando troppe variabili non correlate. Variabili di tipo informative migliorare il risultato. le variabili non correlate introducono inutili nel modello hello. È inoltre necessario toogenerate queste funzionalità per tutti i nuovi dati ottenuti durante l'assegnazione dei punteggi. Pertanto generazione hello di queste funzionalità possa solo dipendono dai dati che sono disponibili in fase di hello dell'assegnazione di punteggi. Per informazioni tecniche nella progettazione di funzionalità con varie tecnologie di dati di Azure, vedere [funzionalità engineering nel processo di analisi scientifica dei dati hello](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 Training dei modelli
A seconda del tipo di domanda a cui si sta tentando di rispondere, sono disponibili numerosi algoritmi di modellazione. Per ulteriori informazioni sulla scelta di algoritmi di hello, vedere [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md). Sebbene in questo articolo è scritto per Azure Machine Learning, hello è utile per qualsiasi di machine learning progetti fornisce indicazioni. 

il processo di Hello per il training del modello include hello alla procedura seguente: 

* **Dati di input hello Split** in modo casuale per la modellazione in un set di dati di training e un set di dati di test.
* **Compilazione di modelli di hello** utilizzano set di dati di training hello.
* **Valutare** (dataset di training e di test) una serie di competizione algoritmi di machine learning insieme hello vari ottimizzazioni parametri associati (noti come sweep di parametri) che sono pensati per rispondere alle domande hello di interesse con hello dati correnti.
* **Determinare la soluzione "migliore" di hello** domanda hello tooanswer confrontando la metrica di successo hello tra metodi alternativi.

> [!NOTE]
> **Evitare la perdita di**: perdita di dati può essere causato da inclusione hello dei dati dall'esterno hello training set di dati che consente a un modello o un algoritmo di apprendimento automatico toomake eccessivamente buone stime. Perdita è una causa comune perché gli esperti di dati visualizzato nervoso quando ricevono risultati predittivi che sembrano troppo buona toobe true. Queste dipendenze possono essere toodetect disco rigido. perdita tooavoid richiede spesso l'iterazione tra la creazione di un set di dati di analisi, creazione di un modello e valutare l'accuratezza di hello. 
> 
> 

Vengono forniti un [dello strumento di creazione rapporti e modellazione automatizzata](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) con TDSP che è in grado di toorun tramite più algoritmi e parametro sweep tooproduce un modello di linea di base. Lo strumento produce anche un report di base sulla modellazione che riepiloga le prestazioni di ogni combinazione di modello e parametro, inclusa l'importanza della variabile. Anche questo processo è iterativo poiché potrebbe risultare in una nuova progettazione di funzionalità. 

### <a name="artifacts"></a>Elementi
gli elementi di Hello prodotti in questa fase includono:

* [**Set di funzionalità**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): hello funzionalità sviluppate per la modellazione hello sono descritte hello **set di funzionalità** sezione di hello **definizione dati** report. Contiene le funzioni hello toogenerate di puntatori toohello codice e descrizione sul modo in cui è stato generato funzionalità hello.
* [**Report dei modelli**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): per ogni modello provato viene generato un report standard basato su modelli che fornisce dettagli su ogni esperimento.
* **Decisione di Checkpoint**: valutare se il modello di hello esegue anche sufficiente toodeploy il sistema di produzione tooa. Tooask alcune domande chiave sono:
  * Domanda di hello modello risposte hello con sufficiente sicurezza dispone dei dati di test hello? 
  * È necessario provare soluzioni alternative, come raccogliere dati aggiuntivi, eseguire nuova progettazione di funzionalità o provare con altri algoritmi?


## <a name="4-deployment"></a>4. Distribuzione

### <a name="goal"></a>Obiettivo
* I modelli con una pipeline di dati sono distribuiti tooa produzione o ambiente di produzione per l'accettazione di un utente finale. 

### <a name="how-toodo-it"></a>Come toodo,
attività principali Hello trattati in questa fase:

* **Rendere operativo il modello di hello**: distribuzione di produzione tooa modello e la pipeline di hello o ambiente di produzione per l'utilizzo dell'applicazione.

#### <a name="41-operationalize-a-model"></a>4.1 Rendere operativo il modello
Dopo aver creato un set di modelli che funzionino correttamente, è possibile operationalized per tooconsume altre applicazioni. A seconda dei requisiti di business hello, stime eseguite in tempo reale o in un singolo batch. toobe operativi, i modelli di hello hanno toobe esposta con un'interfaccia API aprire facilmente utilizzato da varie applicazioni, ad esempio siti Web in linea, fogli di calcolo, i dashboard o business e back-end applicazioni line-of. Per esempi su come rendere operativi i modelli con un servizio Web di Azure Machine Learning, vedere [Pubblicare un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md). È inoltre una migliore telemetria toobuild pratica e monitoraggio in hello modello di produzione e hello toohelp di pipeline distribuita di dati con stato successive del sistema reporting e risoluzione dei problemi.  

### <a name="artifacts"></a>Elementi
* Dashboard di stato sull'integrità del sistema e metriche principali.
* Report di modellazione finale con informazioni dettagliate sulla distribuzione.
* Documento finale sull'architettura della soluzione.

## <a name="5-customer-acceptance"></a>5. Accettazione del cliente

### <a name="goal"></a>Obiettivo
* **Completare i risultati finali progetto hello**: verificare che la pipeline hello, hello modello e la distribuzione in un ambiente di produzione siano soddisfacente obiettivi del cliente.

### <a name="how-toodo-it"></a>Come toodo,
Questa fase comprende due attività principali:

* **La convalida del sistema**: confermare modello hello distribuito e pipeline soddisfino le esigenze dei clienti.
* **Progetto**: entità toohello toorun hello sistema nell'ambiente di produzione.

cliente Hello deve convalidare che il sistema hello soddisfa le proprie esigenze di business e risposte hello hello domande con precisione toodeploy hello sistema tooproduction da utilizzare per le applicazioni client. Tutta la documentazione di hello viene finalizzata e verificata. Viene completata una consegna di entità di toohello progetto hello responsabile per le operazioni. Questa entità può essere, ad esempio, un IT o team di analisi scientifica dei dati cliente o un agente del cliente hello che è responsabile dell'esecuzione del sistema hello nell'ambiente di produzione. 

### <a name="artifacts"></a>Elementi
elemento principale di Hello prodotto in questa fase finale è hello **uscita Report del progetto per il cliente**. Si tratta di rapporto tecnico di hello contenente tutti i dettagli di progetto hello che toolearn utili sulle e operare sistema hello. TDSP fornisce un modello di [report di uscita](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) da usare così com'è o da personalizzare secondo le esigenze specifiche del cliente. 

## <a name="summary"></a>Riepilogo
Hello [ciclo di vita del processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess) viene modellata in base alle esigenze di una sequenza di passaggi iterati che vengono fornite indicazioni sulle attività hello toouse di modelli predittivi. Questi modelli possono essere distribuiti in un ambiente toobe sfruttate toobuild intelligenti le applicazioni di produzione. obiettivo di Hello di questo ciclo di vita del processo è toocontinue toomove un dati progetto scientifico in avanti verso un punto di fine engagement deselezionare. Mentre è vero che analisi scientifica dei dati è un esercizio di ricerca e comunicare l'individuazione, viene tooclearly in grado di questi team tooyour attività e i clienti usando un set ben definito di elementi che consentono di modelli standard dipendenti evitare malinteso e aumentare la probabilità di hello di esito positivo di un progetto di analisi scientifica dei dati complessi.

## <a name="next-steps"></a>Passaggi successivi
Procedure dettagliate end-to-end che illustrano il processo di hello per tutti i passaggi di hello completo **scenari specifici** vengono anche forniti. Vengono elencati e collegati con le descrizioni di anteprima in hello [procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md) argomento.

