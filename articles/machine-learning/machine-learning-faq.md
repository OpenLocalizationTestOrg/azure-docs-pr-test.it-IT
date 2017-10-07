---
title: domande frequenti (FAQ) di Machine Learning aaaAzure | Documenti Microsoft
description: "Introduzione ad Azure Machine Learning; domande frequenti su fatturazione, funzionalità e limitazioni di un servizio cloud per la modellazione predittiva semplificata."
keywords: "introduzione al machine learning, modellazione predittiva, cos’è il machine learning"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Domande frequenti su Azure Machine Learning: fatturazione, funzionalità, limitazioni e supporto
Di seguito sono riportate alcune domande frequenti e le corrispondenti risposte su Azure Machine Learning, un servizio cloud che consente di sviluppare modelli predittivi e rendere operative le soluzioni tramite servizi Web. Queste domande frequenti forniscono domande su come toouse hello servizio, che include hello modello, funzionalità, limitazioni e supporto di fatturazione.

**Non è possibile trovare la risposta a una domanda?**

Azure Machine Learning è un forum MSDN in cui i membri della community di analisi scientifica dei dati hello possono porre domande su Azure Machine Learning. il team di Azure Machine Learning Hello monitora forum hello. Passare toohello [Forum di Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch per risposte o toopost una nuova domanda personalizzata.

## <a name="general-questions"></a>Domande generali
**Cos'è Azure Machine Learning?**

Azure Machine Learning è un servizio completamente gestito che è possibile utilizzare toocreate, test, operare e gestire soluzioni di analisi predittive nel cloud hello. Con un semplice browser è possibile accedere, caricare i dati e avviare immediatamente esperimenti di Machine Learning. La modellazione predittiva con trascinamento della selezione, un'ampia gamma di moduli e una libreria di modelli iniziali consentono di eseguire le attività comuni di Machine Learning in modo semplice e rapido. Per ulteriori informazioni, vedere hello [Cenni preliminari sul servizio di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/). Per l'apprendimento di toomachine un'introduzione che illustra i concetti e terminologia, vedere [tooAzure introduzione Machine Learning](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Cos'è Machine Learning Studio?**

Machine Learning Studio è un ambiente workbench accessibile con un Web browser. Machine Learning Studio ospita una tavolozza di moduli in un'interfaccia di composizione visiva che consente di compilare un end-to-end, flusso di lavoro scienza dei dati sotto forma di hello di un esperimento.

Per altre informazioni su Machine Learning Studio, vedere [Cos'è Machine Learning Studio?](machine-learning-what-is-ml-studio.md)

**Che cos'è il servizio di Machine Learning API hello?**

Hello servizio API di Machine Learning consente modelli predittivi toodeploy, come quelli che vengono compilati in Machine Learning Studio, come servizi web scalabili e a tolleranza di errore. i servizi web Hello creati dal servizio API di Machine Learning hello sono le API REST che forniscono un'interfaccia per la comunicazione tra applicazioni esterne e i modelli predittivi analitica.

Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

**Dove sono elencati i servizi Web classici? Dove sono elencati i nuovi servizi Web basati su Azure Resource Manager?**

I servizi Web creati tramite hello Classic web e il modello di servizi di distribuzione creati tramite hello Azure Resource Manager nuovo modello di distribuzione sono elencati in hello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net/) portale.

Sono elencati anche i servizi web classico [Machine Learning Studio](http://studio.azureml.net) su hello **servizi Web** scheda.

## <a name="azure-machine-learning-questions"></a>Domande su Azure Machine Learning
**Che cosa sono i servizi Web di Azure Machine Learning?**

I servizi Web di Machine Learning offrono un'interfaccia tra un'applicazione e un modello di assegnazione dei punteggi del flusso di lavoro di Machine Learning. Un'applicazione esterna è possibile utilizzare Azure Machine Learning toocommunicate con un modello del flusso di lavoro di Machine Learning assegnazione dei punteggi in tempo reale. Un servizio web Machine Learning di tooa chiamata restituisce applicazione esterna tooan risultati di stima. un servizio web di chiamata tooa toomake, passare una chiave API che è stata creata al momento della distribuzione del servizio web di hello. Un servizio Web di Machine Learning è basato su REST, un'opzione di architettura diffusa per progetti di programmazione Web.

Azure Machine Learning offre due tipi di servizi Web.

* Servizio di richiesta-risposta (RR): Una bassa latenza e servizio altamente scalabile che offre un'interfaccia toohello modelli senza stati creato e distribuito tramite Machine Learning Studio.
* Servizio esecuzione batch (BES): un servizio asincrono per l'assegnazione di punteggi a un batch di record di dati.

Esistono diversi modi tooconsume hello API REST e accesso hello servizio web. Ad esempio, è possibile scrivere un'applicazione in c#, R o Python con codice di esempio hello che viene generato al momento della distribuzione del servizio web di hello.

codice di esempio Hello è disponibile in:
- pagina di consumare Hello per il servizio web hello nel portale di servizi Web di Azure Machine Learning hello
- Hello pagina della Guida API nel dashboard del servizio web hello in Machine Learning Studio

È inoltre possibile utilizzare lavoro di Microsoft Excel di esempio hello che viene creato ed è disponibile nel dashboard del servizio web hello in Machine Learning Studio.

**Quali sono gli aggiornamenti principali di hello tooAzure Machine Learning?**

Per gli aggiornamenti più recenti di hello, vedere [novità in Azure Machine Learning](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Domande su Machine Learning Studio
### <a name="import-and-export-data-for-machine-learning"></a>Importare ed esportare dati per Machine Learning
**Quali origini dati sono supportate da Machine Learning?**

È possibile scaricare dati tooa esperimento di Machine Learning Studio in tre modi:

- Caricare un file locale come set di dati
- Utilizzare un modulo tooimport dati da servizi dati basati su cloud
- Importare un set di dati salvato da un altro esperimento

toolearn ulteriori informazioni sui formati di file supportati, vedere [importare i dati di training in Machine Learning Studio](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Le dimensioni hello set di dati possibile per my i moduli?
Moduli di Machine Learning Studio supportano i set di dati di backup too10 GB di dati numerici ad alta densità per casi di utilizzo comuni. Se un modulo accetta più input, hello valore di 10 GB è hello totale delle dimensioni di tutti gli input. È anche possibile campionare set di dati di dimensioni maggiori con query di Hive o del database SQL di Azure oppure usare la pre-elaborazione di Learning by Counts (Apprendimento in base a conteggi) prima dell'inserimento.  

Hello seguenti tipi di dati possono espandere toolarger i set di dati durante la normalizzazione di funzionalità e sono tooless limitata a 10 GB:

* Sparse
* Categorical
* Stringhe
* Dati binari

Hello seguenti moduli è limitate toodatasets minore di 10 GB:

* Moduli di raccomandazione
* Modulo SMOTE (Synthetic Minority Oversampling Technique)
* Moduli di script: R, Python, SQL
* I moduli in cui l'output di hello dimensioni dei dati possono essere più grandi delle dimensioni di dati di input, ad esempio Join o Feature Hashing
* La convalida incrociata, ottimizzare modello Iperparametri, Ordinal Regression e One-vs-All Multiclass, quando il numero di hello di iterazioni è molto grande

#### <a id="UploadLimit"></a>Quali sono i limiti di hello per dati carica?
Per i set di dati che superano un paio GB, caricare dati tooAzure archiviazione o Database SQL di Azure o usare Azure HDInsight anziché caricare direttamente da un file locale.

**È possibile leggere i dati da Amazon S3?**

Se si dispone di una piccola quantità di dati e si desidera tooexpose tramite un URL HTTP, sarà possibile utilizzare hello [l'importazione dei dati] [ import-data] modulo. Per maggiori quantità di dati, trasferirla tooAzure archiviazione prima e quindi utilizzare hello [l'importazione dei dati] [ import-data] toobring modulo nell'esperimento.
<!--

<SEE CLOUD DS PROCESS>
-->

**Esiste una capacità di input dell'immagine predefinita?**

Per informazioni sulle funzionalità di input di immagine in hello [le immagini importate] [ image-reader] riferimento.

### <a name="modules"></a>Moduli
**algoritmo di Hello, origine dati, il formato di dati o operazione di trasformazione dati che si sta cercando non è in Azure Machine Learning Studio. Quali sono le opzioni disponibili?**

È possibile passare toohello [forum sul feedback su utente](http://go.microsoft.com/fwlink/?LinkId=404231) toosee funzionalità richiede che si sta verificando. Aggiungere la richiesta di voto tooa se è già stata richiesta una funzionalità che si sta cercando. Se non esiste possibilità hello che si sta cercando, creare una nuova richiesta. È possibile visualizzare lo stato di hello della richiesta del forum, troppo. Si traccia questo elenco e aggiornare lo stato di hello della disponibilità delle funzionalità di frequente. Inoltre, è possibile utilizzare il supporto incorporato di hello per R e Python toocreate trasformazioni personalizzate quando necessario.

**È possibile trasferire un proprio codice esistente in Machine Learning Studio?**

Sì, è possibile inserire il codice R o Python esistente in Machine Learning Studio, eseguirlo nella hello stesso sperimentare con strumenti di apprendimento in Azure Machine Learning e distribuire soluzioni hello come un servizio web tramite Azure Machine Learning. Per altre informazioni, vedere [Estendere l'esperimento con R](machine-learning-extend-your-experiment-with-r.md) ed [Eseguire gli script di apprendimento automatico di Python in Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).

**È possibile toouse qualcosa di simile a [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine un modello?**

No. Il linguaggio PMML (Predictive Model Markup Language) non è supportato. È possibile usare R personalizzato e toodefine un modulo di codice Python.

**Quanti moduli è possibile eseguire in parallelo nell'esperimento?**  

È possibile eseguire i moduli di toofour in parallelo in un esperimento.

### <a name="data-processing"></a>Elaborazione dei dati
**Si è verificato un dati toovisualize possibilità (oltre a visualizzazioni R) in modo interattivo in esperimento hello?**

Fare clic su output di hello un toovisualize hello dei dati del modulo e ottenere le statistiche.

**Quando si visualizza in anteprima i risultati o i dati in un browser, il numero di hello di righe e colonne è limitato. Perché?**

Poiché è possibile inviare tooa browser grandi quantità di dati, dimensioni dei dati sono limitato tooprevent rallentare Machine Learning Studio. toovisualize tutti hello/risultati dei dati, la migliore toodownload hello dati e usare Excel o un altro strumento.

### <a name="algorithms"></a>Algoritmi
**Quali algoritmi esistenti sono supportati in Machine Learning Studio?**

Machine Learning Studio offre algoritmi all'avanguardia, ad esempio gli alberi delle decisioni con boosting scalabili, i sistemi di raccomandazione bayesiani, le reti neurali basate su Machine Deep Learning e le giungle delle decisioni sviluppati da Microsoft Research. Sono inclusi anche pacchetti open source scalabili di apprendimento automatico come Vowpal Wabbit. Machine Learning Studio supporta gli algoritmi di Machine Learning per la classificazione multiclasse e binaria, la regressione e il clustering. Vedere l'elenco completo di hello di [moduli di Machine Learning][machine-learning-modules].

**Si suggerisce automaticamente hello destra Machine Learning algoritmo toouse per i dati?**

No, ma Machine Learning Studio offre vari modi in cui risultati hello toocompare di toodetermine ogni algoritmo hello più appropriato per il problema.

**Si dispone di tutte le istruzioni in un algoritmo di prelievo rispetto a un altro per gli algoritmi fornito hello?**

Vedere [come toochoose un algoritmo](machine-learning-algorithm-choice.md).

**Gli algoritmi fornito hello scritte in R o Python?**

No, questi algoritmi vengono scritti per lo più un miglioramento delle prestazioni tooprovide lingue compilato.

**Sono i dettagli degli algoritmi hello forniti?**

Hello documentazione vengono fornite alcune informazioni sugli algoritmi hello e i parametri per l'ottimizzazione sono algoritmo hello toooptimize descritto per l'uso.  

**È previsto il supporto per l'apprendimento online?**

No. Attualmente è supportata solo la ripetizione del training a livello di codice.

**È visualizzare i livelli di hello di un modello di rete neurale tramite il modulo predefinito di hello?**

No.

**È possibile creare dei moduli personalizzati in C# o in altri linguaggi?**

Attualmente, è possibile utilizzare solo i moduli personalizzati di R toocreate nuovo.

### <a name="r-module"></a>Modulo R
**Quali pacchetti R sono disponibili in Machine Learning Studio?**

Machine Learning Studio supporta più di 400 dei pacchetti CRAN R oggi, di seguito è hello [elenco corrente](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) di tutti i pacchetti inclusi. Vedere anche [estendere l'esperimento con R](machine-learning-extend-your-experiment-with-r.md) toolearn come tooretrieve questo elenco se stessi. Se il pacchetto hello desiderato non è presente nell'elenco, specificare il nome di hello del pacchetto hello hello [forum sul feedback su utente](http://go.microsoft.com/fwlink/?LinkId=404231).

**È possibile toobuild un R personalizzato modulo?**

Sì. Per altre informazioni, vedere [Creare moduli R personalizzati in Azure Machine Learning](machine-learning-custom-r-modules.md).

**Esiste un ambiente REPL per R?**

No, vi è alcun ambiente Read-Eval-Print-Loop (REPL) per R in studio hello.

### <a name="python-module"></a>Modulo Python
**È possibile toobuild un modulo di Python personalizzato?**

Non attualmente, ma è possibile utilizzare uno o più [Execute Python Script] [ python] tooget moduli hello stesso risultato.

**Esiste un ambiente REPL per Python?**

È possibile utilizzare i notebook Jupyter hello in Machine Learning Studio. Per altre informazioni, vedere [Introducing Jupyter Notebooks in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)(Introduzione di Jupyter Notebook in Azure Machine Learning Studio).

## <a name="web-service"></a>Servizio Web
### <a name="retrain"></a>Ripetere il training
**Come è possibile ripetere il training dei modelli di Azure Machine Learning a livello di codice?**

Utilizzare le API di ripetizione di training hello. Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](machine-learning-retrain-models-programmatically.md). Codice di esempio è disponibile anche in hello [ripetizione di training Demo di Microsoft Azure Machine Learning](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Create
**È possibile distribuire il modello di hello localmente o in un'applicazione che non dispone di una connessione a Internet?**

No.

**Esiste una latenza di base prevista per tutti i servizi Web?**

Vedere hello [limiti della sottoscrizione Azure](../azure-subscription-service-limits.md).

### <a name="use"></a>Uso
**Quando è necessario toorun il modello predittivo come servizio esecuzione Batch rispetto a un servizio di risposta richiesta?**

Hello (RR) del servizio di risposta richiesta è bassa latenza, i modelli di servizio web su vasta scala che viene utilizzato tooprovide toostateless un'interfaccia che vengono creati e distribuiti nell'ambiente di sperimentazione hello. Hello servizio esecuzione Batch (BES) è un servizio che assegna un punteggio in modo asincrono un batch di record di dati. Hello di input per BES è, ad esempio dati di input che utilizza record di risorse. Hello differenza principale è che BES legge un blocco di record da una varietà di origini, ad esempio l'archiviazione Blob di Azure, archiviazione tabelle di Azure, Database SQL di Azure, HDInsight (query hive) e origini HTTP. Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

**Come aggiornare il modello di hello per il servizio web distribuito hello?**

tooupdate un modello di stima per un servizio già distribuito, modificare e rieseguire l'esperimento hello utilizzato tooauthor e Salva modello con training hello. Dopo aver creato una nuova versione del modello con training hello disponibile, Machine Learning Studio chiede se si desidera tooupdate il servizio web. Per informazioni dettagliate su come tooupdate un servizio web distribuito, vedere [distribuire un servizio web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

È inoltre possibile utilizzare hello Retraining API.
Per altre informazioni, vedere [Ripetere il training dei modelli di Machine Learning a livello di codice](machine-learning-retrain-models-programmatically.md). Codice di esempio è disponibile anche in hello [ripetizione di training Demo di Microsoft Azure Machine Learning](https://azuremlretrain.codeplex.com/).

**Come monitorare il servizio Web distribuito in produzione?**

Dopo aver distribuito un modello di stima, è possibile monitorare da hello Azure classico portale (solo servizi web classica) o il portale di servizi Web di Azure Machine Learning hello. Ogni servizio distribuito ha un proprio dashboard, in cui è possibile visualizzare le informazioni di monitoraggio per il servizio. Per ulteriori informazioni su come toomanage i servizi web distribuite, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md) e [gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md).

**È una posizione in cui è possibile visualizzare l'output di hello del mio RR/BES?**

Per record di risorse, risposta del servizio web hello è in genere consente di visualizzare il risultato di hello. È possibile anche scrivere la tooAzure nell'archiviazione Blob. BES, output di hello è scritta tooa blob per impostazione predefinita. È anche possibile scrivere hello output tooa database o una tabella utilizzando hello [Esporta dati] [ export-data] modulo.

**È possibile creare servizi Web solo da modelli creati in Machine Learning Studio?**

No. È anche possibile creare servizi Web direttamente con Jupyter Notebook e RStudio.

**Dove è possibile trovare informazioni sui codici di errore?**

Per un elenco dei codici di errore e delle relative descrizioni, vedere [Codici di errore dei moduli di Machine Learning](https://msdn.microsoft.com/library/azure/dn905910.aspx) .

## <a name="scalability"></a>Scalabilità
**Che cos'è la scalabilità di hello del servizio web hello?**

Attualmente, endpoint predefinito hello viene eseguito il provisioning con 20 richieste simultanee, record di risorse per ogni endpoint. È possibile scalare questa too200 di richieste simultanee per ogni endpoint, e che è possibile ridimensionare ogni too10 del servizio web, 000 endpoint al servizio web come descritto in [scalabilità di un servizio Web](machine-learning-scaling-webservice.md). Per BES, ogni endpoint può elaborare 40 richieste alla volta e le richieste aggiuntive oltre 40 vengono messe in coda. Queste richieste in coda eseguiti automaticamente come hello coda scarichi.

**I processi R sono distribuiti in più nodi?**

No.  

**Quanti dati è possibile usare per il training?**

Moduli di Machine Learning Studio supportano i set di dati di backup too10 GB di dati numerici ad alta densità per casi di utilizzo comuni. Se un modulo accetta hello input, più di un totale per tutti gli input sono 10 GB. È anche possibile campionare set di dati di dimensioni maggiori tramite query di Hive o del database SQL di Azure oppure tramite la pre-elaborazione con moduli [Learning with Counts][counts] (Apprendimento in base a conteggi) prima dell'inserimento.  

Hello seguenti tipi di dati possono espandere toolarger i set di dati durante la normalizzazione di funzionalità e sono tooless limitata a 10 GB:

* Sparse
* Categorical
* Stringhe
* Dati binari

Hello seguenti moduli è limitate toodatasets minore di 10 GB:

* Moduli di raccomandazione
* Modulo SMOTE (Synthetic Minority Oversampling Technique)
* Moduli di script: R, Python, SQL
* I moduli in cui l'output di hello dimensioni dei dati possono essere più grandi delle dimensioni di dati di input, ad esempio Join o Feature Hashing
* Convalida incrociata, ottimizzazione degli iperparametri del modello, regressione ordinale e multiclasse uno-tutti, quando il numero di iterazioni è molto elevato

Per i set di dati superiori a qualche GB, caricare dati tooAzure archiviazione o Database SQL di Azure o usare HDInsight anziché caricare direttamente da un file locale.

**Esistono limitazioni per la dimensione dei vettori?**

Le righe e colonne sono ogni limitazione .NET toohello limitato di Max Int: 2,147,483,647.

**È possibile regolare dimensioni hello della macchina virtuale hello che esegue il servizio web di hello?**

No.  

## <a name="security-and-availability"></a>Sicurezza e disponibilità
**Per impostazione predefinita, chi può accedere endpoint http hello per il servizio web hello? Come limita l'accesso toohello endpoint?**

Dopo avere distribuito un servizio Web, viene creato un endpoint predefinito per tale servizio. endpoint di Hello predefinito può essere chiamato utilizzando la propria chiave API. È possibile aggiungere che più endpoint con le rispettive chiavi dal portale di Azure classico hello o a livello di programmazione tramite le API di Gestione servizio Web di hello. Le chiavi di accesso sono chiamate necessarie toomake toohello del servizio web. Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

**Cosa succede se non viene trovato l'account di archiviazione di Azure?**

Machine Learning Studio si basa su dati intermedi toosave account di archiviazione di Azure fornito dall'utente durante l'esecuzione del flusso di lavoro di hello. Questo account di archiviazione viene fornito tooMachine Learning Studio quando viene creata un'area di lavoro. Dopo aver hello dell'area di lavoro viene creato, se account di archiviazione hello viene eliminato e non sono più disponibili, dell'area di lavoro hello smetterà di funzionare e tutte esperimenti in quanto l'area di lavoro avrà esito negativo.

Se l'account di archiviazione hello è stato eliminato accidentalmente, ricreare l'account di archiviazione hello con stesso nome in hello hello stessa area hello eliminato l'account di archiviazione. Successivamente, risincronizzare il tasto di scelta rapida hello.

**Cosa succede se la chiave di accesso dell'account di archiviazione non è sincronizzata?**

Machine Learning Studio si basa su dati intermedi toostore account di archiviazione di Azure fornito dall'utente durante l'esecuzione del flusso di lavoro di hello. Questo account di archiviazione fornito tooMachine Learning Studio quando viene creata un'area di lavoro e le chiavi di accesso hello sono associate a tale area di lavoro. Se le chiavi di accesso hello vengono modificate dopo la creazione dell'area di lavoro di hello, dell'area di lavoro hello non accedere non è più account di archiviazione hello. L'area di lavoro non funzionerà più e tutti gli esperimenti al suo interno avranno esito negativo.

Se si modifica chiavi di accesso di account di archiviazione, risincronizzare hello i tasti di scelta nell'area di lavoro hello utilizzando hello portale di Azure classico.  

## <a name="support-and-training"></a>Supporto e training
**Dove si trovano i training per Azure Machine Learning?**

Hello [Centro documentazione di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) ospita come tooguides ed esercitazioni video. Queste guide dettagliate introducono servizi hello e spiegano ciclo di vita dell'analisi scientifica dei dati hello di importazione di dati, pulizia dei dati, la creazione di modelli predittivi e distribuirli nell'ambiente di produzione con Azure Machine Learning.

Aggiungiamo toohello materiale nuovo centro di Machine Learning in maniera continuativa. È possibile inviare le richieste per il materiale di apprendimento aggiuntive nel centro di Machine Learning in hello [forum sul feedback su utente](https://windowsazure.uservoice.com/forums/257792-machine-learning).

È disponibile formazione anche in [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**Come si ottiene il supporto per Azure Machine Learning?**

il supporto tecnico per Azure Machine Learning, tooget andare troppo[Azure supporta](/support/options/)e selezionare **Machine Learning**.

È anche disponibile un forum della community di Azure Machine Learning su MSDN, in cui è possibile porre domande su Azure Machine Learning. il team di Azure Machine Learning Hello monitora forum hello. Andare troppo[Forum di Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Domande sulla fatturazione
**Come funziona la fatturazione di Machine Learning?**

Azure Machine Learning include due componenti: Machine Learning Studio e i servizi Web di Machine Learning.

Mentre si sta valutando Machine Learning Studio, è possibile utilizzare il livello di fatturazione gratuito di hello. livello gratuito Hello consente inoltre di distribuire un servizio web classica con capacità limitate.

Se si decide che Azure Machine Learning soddisfa le proprie esigenze, è possibile iscriversi a hello livello Standard. toosign backup, è necessario disporre di una sottoscrizione di Microsoft Azure.

Nel livello Standard hello, verrà addebitato ogni mese per ogni area di lavoro definiti in Machine Learning Studio. Quando si esegue un esperimento in studio hello, vengono fatturati per risorse di calcolo quando si esegue un esperimento. Quando si distribuisce un servizio web classica, transazioni e le ore vengono fatturate in base al consumo retribuzione hello di calcolo.

I nuovi servizi Web basati su Resource Manager introducono piani di fatturazione che consentono una maggiore prevedibilità dei costi. A più livelli di prezzi offre tariffe scontate toocustomers che necessitano di una grande quantità di capacità.

Quando si crea un piano, si esegue il commit tooa costi fornita con una quantità inclusa di ore di calcolo API e le transazioni di API fissato. Se è necessario più quantità incluse, è possibile aggiungere istanze tooyour piano. Se sono necessarie molte quantità incluse aggiuntive, è possibile scegliere un livello superiore che offre un numero di quantità incluse notevolmente maggiore e un tariffa scontata migliore.

Dopo hello quantità incluse nelle istanze esistenti vengono utilizzate, utilizzo aggiuntivo viene addebitato con frequenza eccedenza hello associata a livello di piano di fatturazione hello.

> [!NOTE]
Quantità incluse vengono riallocate ogni 30 giorni e quantitativi inclusi non passano toohello periodo successivo.

Per altre informazioni sulla fatturazione e sui prezzi, vedere [Prezzi di Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).

**Machine Learning offre una versione di valutazione gratuita?**

 Azure Machine Learning offre un'opzione di sottoscrizione gratuita, illustrata in [Prezzi di Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/). Machine Learning Studio è una versione di valutazione di otto ore rapida valutazione che è disponibile quando si accede troppo[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).

 Quando ci si iscrive a una versione di valutazione gratuita di Azure, è inoltre possibile provare tutti i servizi Azure per un mese. toolearn ulteriori informazioni su hello Azure versione di valutazione gratuita, visitare [Azure domande frequenti sulla versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial-faq/).

**Che cos'è una transazione?**

Una transazione rappresenta una chiamata API a cui Azure Machine Learning risponde. Le transazioni di chiamate al servizio richiesta risposta (RRS) e al servizio esecuzione batch (BES) vengono aggregate e addebitate nel piano di fatturazione.

**È possibile utilizzare quantità transazione hello incluso in un piano per le transazioni di record di risorse sia BES?**

Sì. Le transazioni dei servizi RRS e BES vengono aggregate e addebitate nel piano di fatturazione.

**Che cos'è un'ora di calcolo API?**

Un'ora di calcolo API è l'unità di fatturazione hello per volta hello le risorse di calcolo API chiamate accettano toorun tramite Machine Learning. Ai fini della fatturazione, tutte le chiamate vengono aggregate.

**Quanto tempo è necessario in genere per una tipica chiamata API di produzione?**

Tempi di chiamata delle API di produzione possono variare in modo significativo, in genere compreso tra centinaia di millisecondi tooa alcuni secondi. Alcune chiamate API potrebbero richiedere minuti a seconda della complessità hello del modello di machine learning e l'elaborazione dati hello. Hello migliore modo tooestimate API di produzione chiamata volte è un modello di servizio Machine Learning hello toobenchmark.

**Che cos'è un'ora di calcolo di Studio?**

Le ore di calcolo Studio sono l'unità di fatturazione hello per hello tempi di risoluzione che gli esperimenti usare risorse di calcolo in studio.

**In nuovi servizi web (basato su Azure Resource Manager), il livello di sviluppo/Test hello scopo per?**

Servizi web basati su Gestione risorse di forniscono più livelli che è possibile utilizzare tooprovision del piano di fatturazione. Hello tariffario sviluppo/Test fornisce quantità limitate, inclusa che consentono di tootest l'esperimento come servizio web senza incorrere in costi. È necessario hello opportunità toosee funzionamento.

**Sono previsti addebiti distinti per l'archiviazione?**

livello gratuito di Machine Learning Hello non richiede o consentire l'archiviazione separata. livello Standard di Machine Learning Hello richiede agli utenti toohave un account di archiviazione di Azure. L'archiviazione di Azure [viene fatturata separatamente](https://azure.microsoft.com/pricing/details/storage/).

**Machine Learning supporta la disponibilità elevata?**

Sì. Per informazioni dettagliate, vedere [Machine Learning prezzi](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) per una descrizione di hello contratto di servizio (SLA).

**In quale tipologia specifica di risorse di calcolo verranno eseguite le chiamate API di produzione?**

Hello servizio Machine Learning è un servizio multi-tenant. Risorse di calcolo effettivi utilizzati nel back-end hello variano e ottimizzate per le prestazioni e la prevedibilità.

### <a name="management-of-new-resource-manager-based-web-services"></a>Gestione dei nuovi servizi Web basati su Resource Manager
**Cosa succede se si elimina il proprio piano?**

Hello piano viene rimosso dalla sottoscrizione e vengono fatturati in uso.

> [!NOTE]
Un piano usato da un servizio Web non può essere eliminato. piano hello toodelete, è necessario assegnare un nuovo piano di servizio web toohello o eliminare il servizio web hello.

**Che cos'è un'istanza del piano?**

Un'istanza del piano è un'unità di quantità incluse che è possibile aggiungere tooyour piano di fatturazione. Quando si seleziona un livello per il piano di fatturazione, questo include un'istanza. Se è necessario più quantità incluse, è possibile aggiungere istanze di hello fatturazione livello tooyour piano selezionato.

**Quante istanze del piano possono essere aggiunte?**

È possibile disporre di un'istanza del piano tariffario sviluppo/Test hello in una sottoscrizione.

Per i livelli S1 Standard, S2 Standard e S3 Standard è possibile aggiungere tutte le istanze necessarie.

> [!NOTE]
A seconda dell'uso previsto, esso potrebbe essere più conveniente livello tooa tooupgrade che è più incluso quantità anziché aggiungere livello corrente di istanze toohello.

**Cosa succede quando si cambiano i livelli del piano (per aggiornamento o downgrade)?**

piano precedente Hello viene eliminato e viene fatturato utilizzo corrente di hello proporzionalmente. Per rest hello del periodo di hello viene creato un nuovo piano con hello completo incluso quantitativi aggiornato o il downgrade del livello di hello.

> [!NOTE]
Le quantità incluse vengono allocate per periodo e le quantità inutilizzate non vengono rinnovate.

**Cosa accade quando aumentano le istanze di hello in un piano?**

Quantità sono inclusi proporzionalmente e potrebbero richiedere efficace toobe 24 ore.

**Cosa succede quando si elimina un'istanza di un piano?**

istanza Hello viene rimosso dalla sottoscrizione e vengono fatturati ripartito utilizzo.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Iscriversi ai nuovi servizi Web basati su Resource Manager
**Come ci si iscrive a un piano?**

Si dispone di due piani di fatturazione toocreate modi.

Quando si distribuisce per la prima volta un servizio Web basato su Resource Manager, si può scegliere un piano esistente o crearne uno nuovo.

I piani creati in questo modo sono nel proprio paese predefinito e il servizio web verrà distribuito toothat area.

Se si desidera toodeploy servizi tooregions diverso dal proprio paese predefinito, è consigliabile toodefine i piani di fatturazione prima di distribuire il servizio.

In tal caso, è possibile accedere al portale di servizi Web di Azure Machine Learning toohello e passare toohello pagina dei piani. In questa pagina è possibile aggiungere ed eliminare piani, nonché modificare i piani esistenti.

**Il piano è consigliabile scegliere toostart off con?**

È consigliabile che viene avviato con hello S1 Standard di livello e monitorare il servizio per l'utilizzo. Se si ritiene che si sta utilizzando la quantità incluse rapidamente, è possibile aggiungere istanze o spostare tooa di livello superiore e ottenere prestazioni migliori tariffe scontate. Il piano di fatturazione può essere modificato in base alle esigenze nell'intero ciclo di fatturazione.

**Le aree sono disponibili in nuovi piani di hello?**

sono disponibili nuovi piani di fatturazione Hello hello tre regioni di produzione in cui è supportato nuovi servizi web di hello:

* Stati Uniti centro-meridionali
* Europa occidentale
* Asia sudorientale

**Se si hanno servizi Web in più aree, è necessario un piano per ogni area?**

Sì. I prezzi dei piani variano in base all'area. Quando si distribuisce un'area tooanother del servizio web, è necessario tooassign it un piano che è l'area toothat specifico. Per altre informazioni, vedere [Prodotti disponibili in base all'area]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Nuovi servizi Web: eccedenze
**Come si controlla se si è superato l'utilizzo del servizio Web?**

È possibile visualizzare l'utilizzo di hello in tutti i piani nella pagina dei piani hello nel portale di servizi Web di Azure Machine Learning hello. Accedi al portale toohello e quindi fare clic su hello **piani** opzione di menu.

In hello **transazioni** e **calcolo** le colonne di tabella hello, è possibile visualizzare le quantità hello incluso del piano di hello e percentuale di hello utilizzata.

**Cosa accade quando si utilizzano backup hello includono quantità piano tariffario sviluppo/Test hello?**

Servizi che hanno un prezzo toothem livello assegnato di sviluppo e Test vengono arrestati finché hello periodo successivo o fino a quando non vengono spostati livello tooa a pagamento.

**Per i servizi Web classici e le eccedenze dei nuovi servizi Web basati su Resource Manager, come vengono calcolati i prezzi per i carichi di lavoro richiesta-risposta (RRS) e batch (BES)?**

Per un carico di lavoro di record di risorse, vengono addebitati per ogni chiamata di transazioni di API che si apporta e hello tempo di calcolo associato a tali richieste. I costi di transazione API di produzione RR vengono calcolati come hello Totale chiamate API effettuate moltiplicato per il prezzo di hello per 1.000 transazioni (ripartito per singole transazioni). I costi di ora RR API calcolo API di produzione vengono calcolati come quantità hello di tempo necessaria per ogni toorun chiamata API, moltiplicato per hello il numero totale di transazioni di API, moltiplicato per il prezzo di hello per ore di calcolo API di produzione.

Ad esempio, per eccedenza S1 Standard, 1.000.000 transazioni di API che accettano secondi 0,72 ogni toorun comporterebbe (1.000.000 * $0,50 / 1K transazioni API) in $500 dei costi delle transazioni di API di produzione e (1.000.000 * 0.72 sec * $2 / h) $400 nel calcolo delle API di produzione ore, per un totale di $900.

Per un carico di lavoro BES, vengono addebitati in hello stesso modo. Tuttavia, i costi di transazione API hello rappresentano hello diverse procedure batch inviato e i costi di calcolo hello rappresentano tempo di calcolo hello associata a tali processi batch. I costi di transazione API di produzione BES vengono calcolati come numero totale di hello dei processi inviati moltiplicato per il prezzo di hello per 1.000 transazioni (ripartito per singole transazioni). I costi di ora BES API calcolo API di produzione vengono calcolati come quantità hello di tempo necessaria per ogni riga del processo di toorun moltiplicato per hello il numero totale di righe nel processo moltiplicato per hello il numero totale di processi moltiplicato per il prezzo di hello per API di produzione ore di calcolo. Quando si utilizza hello Calcolatrice di Machine Learning, hello transazione misuratore rappresenta hello numero di processi che si prevede di toosubmit e il campo di tempo per transazione hello rappresenta hello combinata ora è sufficiente per tutte le righe toorun ogni processo.

Con l'eccedenza in S1 Standard, ad esempio, si supponga di inviare 100 processi al giorno ognuno dei quali è costituito da 500 righe che impiegano 0,72 secondi ciascuna. I costi di eccedenza mensili equivarranno a $ 1,55 (100 processi al giorno = 3.100 processi/mese * $ 0,50/1.000 transazioni API) come costo delle transazioni dell'API di produzione e a $ 620 (500 righe * 0,72 secondi * 3.100 processi * $ 2/ora) per le ore di calcolo dell'API di produzione, per un totale di $ 621,55.

### <a name="azure-machine-learning-classic-web-services"></a>Servizi Web classici di Azure Machine Learning
**È ancora disponibile il pagamento in base al consumo?**

Sì. In Azure Machine Learning sono ancora disponibili i servizi Web classici.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Livello Gratuito e Standard di Azure Machine Learning
**Cosa è incluso nel livello gratuito di Azure Machine Learning hello?**

livello gratuito di Azure Machine Learning Hello è previsto tooprovide un toohello introduzione approfondita Azure Machine Learning Studio. Tutto il necessario è un toosign account Microsoft. livello gratuito Hello include area di lavoro di libero accesso tooone Azure Machine Learning Studio per [account Microsoft](https://www.microsoft.com/account/default.aspx). In questo livello, è possibile utilizzare too10 GB di spazio di archiviazione e utilizzare i modelli come API di gestione temporanea. I carichi di lavoro del livello Gratuito non sono coperti da un contratto di servizio e sono destinati esclusivamente allo sviluppo e all'uso personale. 

Le aree di lavoro di livello gratuito hanno hello limitazioni seguenti:

* I carichi di lavoro non è possibile accedere ai dati dalla connessione server locale tooan che esegue SQL Server.
* Non è possibile distribuire nuovi servizi Web basati su Resource Manager.


**Cosa è incluso nei piani e a livello di Azure Machine Learning Standard hello?**

livello Standard di Azure Machine Learning Hello è una versione di produzione a pagamento di Azure Machine Learning Studio. tariffa mensile viene fatturata in Azure Machine Learning Studio Hello una per ogni area di lavoro per ogni mese e ripartito per mesi parziali. Le ore di sperimentazione in Azure Machine Learning Studio vengono fatturate per ora di calcolo per sperimentazione attiva. La fatturazione è ripartita per ore parziali.  

il servizio API di Azure Machine Learning Hello viene fatturato a seconda se è un servizio web classica o un nuovo servizio web (Gestione risorse di base).

Hello seguendo gli addebiti viene aggregato per ogni area di lavoro per la sottoscrizione.

* Sottoscrizione dell'area di lavoro di Machine Learning: hello sottoscrizione dell'area di lavoro di Machine Learning è una tariffa mensile che fornisce l'area di lavoro Machine Learning Studio tooa access. sottoscrizione di Hello è obbligatorio toorun esperimenti in hello studio tooutilize hello produzione e le API.
* Ore sperimentazione in Studio: questa modalità di calcolo aggrega tutti i costi di calcolo che vengono accumulati eseguendo esperimenti in Machine Learning Studio e chiamate all'API di produzione in esecuzione nell'ambiente di gestione temporanea hello.
* Accesso ai dati dalla connessione server locale tooan che esegue SQL Server nei modelli per il training e assegnazione dei punteggi.
* Per i servizi Web classici:
  * Ore di calcolo dell'API di produzione. Questa misurazione include i costi di calcolo accumulati dai servizi Web eseguiti nell'ambiente di produzione.
  * Transazioni dell'API di produzione (in 1000s): questa modalità di calcolo include costi vengono accumulati per ogni chiamata tooyour servizio web di produzione.

Oltre a hello precedono le spese, in caso di hello del servizio web basato su Gestione risorse, gli addebiti sono aggregate toohello al piano selezionato:

* Standard S1/S2 o S3 API pianificare (unità): Questa modalità di calcolo rappresenta il tipo di hello dell'istanza selezionata per servizi web basati su Gestione risorse.
* Standard S1/S2 o S3 eccedenza ore di calcolo API: Questa modalità di calcolo include addebiti di calcolo che vengono accumulati dai servizi web basati su Gestione risorse eseguiti nell'ambiente di produzione dopo le quantità hello incluso nelle istanze esistenti vengono utilizzate. utilizzo di Hello aggiuntivo viene addebitato ai hello overate frequenza con cui è associata a livello di piano S1/S2 o S3.
* Transazioni di API eccedenza S1/S2 o S3 standard (in 1,000s): questa modalità di calcolo include costi vengono accumulati per ogni chiamata tooyour produzione backup vengono utilizzati i servizi web basati su Gestione risorse dopo l'inclusione di hello quantitativi in istanze esistenti. Hello utilizzo aggiuntivo viene addebitato ai hello overate frequenza associata a livello di piano S1/S2 o S3.
* Ore di calcolo API quantità inclusa: Con i servizi web basati su Gestione risorse di questo calcolo rappresenta quantità hello inclusa di ore di calcolo API.
* Della quantità di transazioni API (1,000s): servizi web basati su Gestione risorse, questo calcolo rappresenta quantità hello inclusa di transazioni API.

**Come ci si iscrive al livello Gratuito di Azure Machine Learning?**

È sufficiente un account Microsoft. Andare troppo[home page di Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), quindi fare clic su **Avvia ora**. Accedere con l'account Microsoft. Verrà automaticamente creata un'area di lavoro nel livello Gratuito. È possibile iniziare tooexplore e creare i seguenti esperimenti di Machine Learning immediatamente.

**Come ci si iscrive al livello Standard di Azure Machine Learning?**

È innanzitutto necessario accesso tooan sottoscrizione di Azure toocreate un'area di lavoro Standard Machine Learning. È possibile iscriversi per una sottoscrizione di Azure versione di valutazione gratuita 30 giorni e sottoscrizione di Azure a pagamento di tooa aggiornamento successive oppure è possibile acquistare una sottoscrizione a pagamento di Azure definitiva. È quindi possibile creare un'area di lavoro di Machine Learning dal portale classico di Microsoft Azure hello una volta ottenuto l'accesso toohello sottoscrizione. Hello vista [dettagliate](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

In alternativa, possono essere invitati dall'area di lavoro un Standard Machine Learning dell'area di lavoro proprietario tooaccess hello del proprietario.

**È possibile specificare personale toouse di account di archiviazione Blob di Azure con livello gratuito hello?**

No, livello Standard hello è equivalente toohello versione di hello servizio Machine Learning che era disponibile prima di hello livelli sono state introdotte.

**È possibile distribuire il modelli di machine learning come API livello gratuito hello?**

Sì, è possibile utilizzare l'apprendimento di modelli di toostaging API services come parte del livello gratuito hello. tooput hello servizio API di gestione temporanea nell'ambiente di produzione e ottenere un endpoint di produzione per il servizio di hello operativi, è necessario utilizzare livello Standard hello.

**Qual è la differenza hello tra Azure versione di valutazione gratuita e livello gratuito di Azure Machine Learning?**

Hello [versione di valutazione gratuita di Microsoft Azure](https://azure.microsoft.com/free/) offre crediti che è possibile applicare tooany Azure del servizio per un mese. Hello Azure Machine Learning Free livello offerte continua accedere in modo specifico tooAzure Machine Learning per carichi di lavoro non di produzione.

**Come spostare un esperimento dal livello Standard toohello livello gratuito di hello?**

toocopy gli esperimenti di livello Standard toohello livello gratuito di hello:

1. Accedi tooAzure Machine Learning Studio e assicurarsi che è possibile visualizzare l'area di lavoro gratuita hello sia hello Standard dell'area di lavoro nel selettore di area di lavoro hello nella barra di spostamento superiore hello.
2. Se si è nell'area di lavoro Standard di hello, passare tooFree dell'area di lavoro.
3. Nella visualizzazione elenco di hello esperimento, selezionare un esperimento che come toocopy e quindi fare clic su hello **copia** pulsante di comando.
4. Selezionare l'area di lavoro Standard di hello da hello finestra di dialogo che consente di aprire e quindi fare clic su hello **copia** pulsante.
   Tutti hello set di dati associati, il modello con training, e così via vengono copiati insieme esperimento hello nell'area di lavoro Standard di hello.
5. È necessario toorerun hello sperimentazione e ripubblicare il servizio web nell'area di lavoro Standard di hello.

### <a name="studio-workspace"></a>Area di lavoro di Studio
**Saranno emesse diverse fatture per le diverse aree di lavoro?**

Gli addebiti delle aree di lavoro vengono suddivisi separatamente per ogni misurazione applicabile in una singola fattura.

**In quale tipologia specifica di risorse di calcolo verranno eseguiti gli esperimenti?**

Hello servizio Machine Learning è un servizio multi-tenant. Risorse di calcolo effettivi utilizzati nel back-end hello variano e ottimizzate per le prestazioni e la prevedibilità.

### <a name="guest-access"></a>Accesso guest
**Che cos'è l'accesso Guest tooAzure Machine Learning Studio?**

L'accesso guest è un'esperienza di valutazione limitata. È possibile creare ed eseguire esperimenti in Azure Machine Learning Studio gratuitamente e senza autenticazione. Le sessioni Guest non sono permanenti (non salvata) e limitato tooeight ore. Le altre restrizioni includono la mancanza di supporto per R e Python, l'assenza di API di staging e dimensioni dei set di dati e capacità di archiviazione limitate. In confronto, gli utenti che scelgono toosign con un account Microsoft hanno livello gratuito di accesso completo a toohello di Machine Learning Studio descritto in precedenza, che include un'area di lavoro persistente e le funzionalità più completa. toochoose verificano la versione gratuita di Machine Learning, fare clic su **iniziare** in [https://studio.azureml.net](https://studio.azureml.net), quindi selezionare **indovinare accesso** o accedere con un database di Microsoft account.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
