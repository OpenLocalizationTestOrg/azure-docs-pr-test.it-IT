---
title: "aaaWhat è processo di analisi scientifica dei dati del Team?  | Microsoft Docs"
description: "Hello processo di analisi scientifica dei dati di Team è un metodo sistematico per la compilazione di applicazioni intelligenti che sfruttano analitica avanzate."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Che cos'è hello Team Data Science processo (TDSP)?
Hello [Team Data Science processo (TDSP)](data-science-process-overview.md) fornisce un approccio sistematico toobuilding le applicazioni intelligenti che consente ai team di toocollaborate gli esperti di dati in modo efficace hello ciclo di vita completo di attività necessarie tooturn queste applicazioni nei prodotti. Hello TDSP descrive una sequenza di passaggi che forniscono **indicazioni** su come problema hello toodefine, configurare gli strumenti di hello e l'ambiente necessario, analizzare i dati rilevanti, compilare e valutare i modelli predittivi e quindi distribuire tali modelli in applicazioni aziendali. 

Ecco i passaggi di hello in **processo di analisi scientifica dei dati di Team**:  

![Flusso di lavoro CAP](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

il processo di Hello **iterativo**: hello comprensione di nuovo ed esistente o perfezionamenti nel modello hello si evolve e richiede la rielaborazione delle operazioni completate in precedenza nella sequenza di hello. Sviluppo azienda esistente e i processi di pianificazione dei progetti sono **adattato facilmente** toowork con hello definito TDSP sequenza di passaggi. 

Hello passaggi di processo hello illustrata nel diagramma sono collegati in hello [il percorso di apprendimento TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e descritto di seguito.  

## <a name="preparation-steps"></a>Passaggi preliminari
## <a name="p1-plan-hello-analytics-project"></a>P1. Pianificare il progetto di analitica hello
Avviare un progetto di analisi definendo gli obiettivi aziendali e i problemi, specificandoli in termini di **requisiti aziendali**. Un obiettivo centrale di questo passaggio è tooidentify hello chiave business variabili (sales previsione o hello probabilità di un ordine essere contraffatto, ad esempio) hello toosatisfy toopredict esigenze di analisi di questi requisiti. Ulteriori informazioni sulla pianificazione è quindi essenziale in genere toodevelop la comprensione di hello **origini dati** necessari tooaddress hello obiettivi del progetto hello dal punto di vista analitica. Non è insolito, ad esempio, toofind che i sistemi esistenti devono toocollect e registrare altri tipi di dati tooaddress hello problema e ottenere gli obiettivi del progetto hello. Per istruzioni, vedere [pianificazione dell'ambiente per processo di analisi scientifica dei dati di Team hello](machine-learning-data-science-plan-your-environment.md) e [scenari per analitica avanzate in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Configurare l'ambiente di analisi
Un ambiente analitica per processo di analisi scientifica dei dati di Team hello include diversi componenti: 

* **aree di lavoro dati** in cui i dati di hello sono preconfigurati per l'analisi e modellazione, 
* un **infrastruttura di elaborazione** per pre-elaborazione, esplorazione e modellazione dei dati hello
* un **l'infrastruttura di runtime** toooperationalize hello modelli analitici ed eseguire le applicazioni client intelligenti hello che utilizzano modelli hello.  

infrastruttura analitica Hello che richiede l'installazione di toobe è spesso parte di un ambiente che è separato da sistemi operativi di base. Ma in genere dati da più sistemi all'interno dell'organizzazione hello oltre che da una società esterna toohello origini. infrastruttura di Hello analitica può essere basata esclusivamente sul cloud, o un'installazione locale o una combinazione di hello due. Per le opzioni, vedere [configurare gli ambienti di analisi scientifica dei dati da utilizzare nel processo di analisi scientifica dei dati di Team hello](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Passaggi di analisi:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Inserimento di dati nell'ambiente analitici hello
primo passaggio Hello è dati rilevanti di hello toobring da vari origini, un altro all'interno o dall'organizzazione hello esterno, un analitiche gli ambienti in cui possono essere elaborati i dati hello. Hello **formato** di hello dati di origine può essere diverso dal formato hello richiesto dalla destinazione hello. Pertanto, alcune trasformazioni di dati possono inoltre essere toobe scopo, gli strumenti di acquisizione hello. Per le opzioni, vedere [Caricare i dati in ambienti di archiviazione per l'analisi](machine-learning-data-science-ingest-data.md)

In inserimento iniziale toohello di aggiunta di dati, molte applicazioni intelligenti sono necessari toorefresh hello dati regolarmente come parte di un processo di apprendimento in corso. Per ottenere questo risultato, è possibile configurare una **pipeline di dati** o un flusso di lavoro. Questo fa parte della parte di iterativo hello del processo di hello che include la ricompilazione e valutare nuovamente modelli analitici di hello utilizzati da un'applicazione hello intelligente distribuzione soluzione hello. Ad esempio, vedere [spostare i dati da un tooSQL di server SQL Azure con Azure Data Factory locale](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Esplorare e pre-elaborare i dati
passaggio successivo Hello è tooobtain una comprensione più approfondita dei dati hello in base all'esame relativo **le statistiche di riepilogo** , relazioni e l'utilizzo di tali tecniche **visualizzazione**. In questa fase vengono anche gestiti i problemi relativi alla **qualità dei dati** e all'integrità, ad esempio valori mancanti, mancate corrispondenze tra tipi di dati e relazioni non coerenti tra i dati. Trasformazioni pre-elaborazione vengono utilizzati tooclean dei dati non elaborati di hello prima ulteriore analitica ed è possibile eseguire la modellazione. Per una descrizione, vedere [tooprepare dati per l'apprendimento automatico migliorato attività](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Sviluppare funzionalità
Gli esperti di dati, in collaborazione con gli esperti di dominio, è necessario identificare le funzionalità di hello che acquisizione hello salienti di proprietà del set di dati hello e che può essere più variabili di chiave business hello toopredict utilizzati identificate durante la pianificazione. Queste nuove funzionalità possono essere derivate da dati esistenti o richiedere dati aggiuntivi toobe raccolti. Questo processo è noto come **funzionalità engineering** e fa parte di hello passaggi chiave per la creazione di un sistema efficace analitica predittiva. Questo passaggio richiede una combinazione di informazioni dettagliate di competenze e hello dominio ottenuta nel passaggio di esplorazione dati hello creativa. Per istruzioni, vedere [funzionalità engineering nel processo di analisi scientifica dei dati di Team hello](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Creare modelli produttivi
Gli esperti di dati compilare modelli analitici variabili chiave hello toopredict identificate dai requisiti di business hello definiti in hello pianificazione passaggio tramite i dati che sono stati puliti e trasformato. Sistemi di Machine learning supportano più **modellazione algoritmi** che sono applicabili tooa vasta gamma di casi. Per istruzioni, vedere [come toochoose algoritmi per il Team di Azure Machine Learning](machine-learning-algorithm-choice.md).

Gli esperti di dati è necessario scegliere il modello più appropriato di hello per le attività di stima e non è insolito che i risultati di più modelli necessario toobe combinati tooobtain hello ottenere risultati ottimali. Hello dati di input per la modellazione sono generalmente suddivisa in modo casuale in tre parti:

* Set di dati di training 
* Set di dati di convalida 
* Set di dati di test 

i modelli di Hello vengono compilati mediante hello **set di dati di training**. Hello combinazione ottimale di modelli (con parametri ottimizzati) è selezionata, eseguire modelli hello e misurare gli errori di stima hello per hello **set di dati di convalida**. Infine hello **set di dati di test** tooevaluate utilizzati hello prestazioni del modello scelto hello sui dati indipendenti che non è stato utilizzato tootrain o convalidare hello modello.  Per le procedure, vedere [tooevaluate come modello di prestazioni in Azure Machine Learning](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Distribuire e utilizzare i modelli
Una volta che un set di modelli che funzionino correttamente, possono essere **operativi** per tooconsume altre applicazioni. A seconda dei requisiti di business hello, stime eseguite in **in tempo reale** o scegliere un **batch** base. toobe operativi, i modelli di hello hanno toobe esposta con un' **aprire l'interfaccia API** che è facilmente utilizzati da varie applicazioni tale sito Web online, fogli di calcolo, i dashboard o business e back-end applicazioni line-of. Vedere, [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Riepilogo e passaggi successivi
Hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) viene modellato come una sequenza di passaggi iterati che **forniscono materiale sussidiario** attività hello toouse necessari analitica toobuild un intelligente applicazioni avanzate. Ogni passaggio fornisce inoltre informazioni dettagliate su come toouse varie attività di hello toocomplete di tecnologie Microsoft descritto. 

Mentre TDSP prescrivono tipi specifici di **documentazione** elementi, è una pratica toodocument hello ottimale di esplorazione dei dati di hello, modellazione e la valutazione e toosave hello codice pertinenti in modo che hello analysis può iterata quando necessario. Ciò consente anche di riutilizzo di hello analitica di lavoro quando si lavora in altre applicazioni che includono dati simili e attività di stima.

Procedure dettagliate end-to-end che illustrano il processo di hello per tutti i passaggi di hello completo **scenari specifici** vengono anche forniti. Per esempi, vedere:

* [Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo dei cluster HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Analisi scientifica dei dati con Spark in Azure HD.mdnsight](machine-learning-data-science-spark-overview.md)
* [Analisi scientifica dei dati scalabile in Azure Data Lake: procedura dettagliata end-to-end](machine-learning-data-science-process-data-lake-walkthrough.md)

