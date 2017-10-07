---
title: "aaaWhat è una macchina virtuale di analisi scientifica dei dati? | Microsoft Docs"
description: Come tooget iniziare a eseguire gli scenari chiave analitica con macchine virtuali di analisi scientifica dei dati.
keywords: strumenti di analisi scientifica dei dati, macchina virtuale per l'analisi scientifica dei dati, strumenti per l'analisi scientifica dei dati, analisi scientifica dei dati per Linux
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Introduzione toohello basato su cloud di macchina virtuale dell'analisi scientifica dei dati per Linux e Windows
Hello macchina virtuale di analisi scientifica dei dati (DSVM) è un'immagine di macchina virtuale personalizzata nel cloud di Microsoft Azure progettato specificamente per eseguire l'analisi scientifica dei dati. Ha molte analisi scientifica dei dati comuni e altri strumenti di pre-installato e pre-configurato compilazione di applicazioni intelligenti per analitica avanzate toojump-inizio. È disponibile in Windows Server e in Linux. L'edizione della DSVM per Windows è disponibile in Windows Server 2016 e Windows Server 2012. Offriamo edizione Linux di hello DSVM Ubuntu 16.04 LTS e le distribuzioni basate su OpenLogic 7.2 CentOS Linux. 

In questo argomento viene illustrato cosa si può fare con hello VM di analisi scientifica dei dati, vengono illustrati alcuni dei principali scenari di hello per l'utilizzo di hello VM, consente di definire diverse funzionalità chiave hello disponibile in Windows hello e nelle versioni di Linux e vengono fornite istruzioni su come tooget a usare i.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>Che cosa può fare con hello macchina virtuale di analisi scientifica dei dati
obiettivo di Hello di hello macchina virtuale di analisi scientifica dei dati è tooprovide professionisti di dati in tutti i livelli di competenza e i ruoli con un ambiente di analisi scientifica dei dati senza le forze di attrito. La VM consente di risparmiare una notevole quantità di tempo che sarebbe necessario se si volesse implementare un ambiente analogo in autonomia. Questa soluzione consente invece di avviare immediatamente il progetto di analisi scientifica dei dati in una nuova istanza di VM. 

Hello VM di analisi scientifica dei dati è progettato e configurato per l'utilizzo di scenari di utilizzo ampie. È possibile aumentare e ridurre le prestazioni dell'ambiente a seconda delle esigenze del progetto. Si è in grado di toouse le attività di analisi scientifica dei dati tooprogram lingua preferita. È possibile installare altri strumenti e personalizzare il sistema di hello per le proprie esigenze.

## <a name="key-scenarios"></a>Scenari chiave
Questa sezione viene suggerita alcuni scenari chiave per cui hello VM di analisi scientifica dei dati possono essere distribuiti.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Preconfigurato desktop analitica nel cloud hello
Hello VM di analisi scientifica dei dati fornisce una configurazione di base per i team di analisi scientifica dei dati ricerca tooreplace desktop locale con un desktop cloud gestito. Questa linea di base garantisce che tutti gli esperti di dati hello in un team Usa una configurazione coerenza con cui esperimenti tooverify e alzare di livello collaborazione. Riduce i costi, riducendo il carico di sysadmin hello e salvataggio puntualmente hello necessari tooevaluate, installare e gestire hello diversi pacchetti software necessari toodo avanzate analitica.  

### <a name="data-science-training-and-education"></a>Preparazione e formazione sull'analisi scientifica dei dati
Istruttori Enterprise e ai docenti spiega le classi di analisi scientifica dei dati in genere forniscono un tooensure immagine di macchina virtuale che gli studenti abbiano una configurazione coerenza e che gli esempi di hello funzionano in modo prevedibile. Hello VM di analisi scientifica dei dati crea un ambiente su richiesta con una configurazione coerenza che consente di semplificare i problemi di incompatibilità e supporto hello. Casi in cui questi ambienti necessitano toobe compilati frequentemente, in particolare per corsi di formazione più breve, trarranno.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Capacità elastica su richiesta per progetti su larga scala
Gli hackathon e i concorsi di analisi scientifica dei dati o la modellazione e l'esplorazione di dati su larga scala richiedono una maggiore capacità hardware, in genere per brevi periodi di tempo. Hello VM di analisi scientifica dei dati consente di replicare hello data science ambiente rapidamente su richiesta, nei server di scalabilità che consentono di esperimenti che richiedono molto potenti toobe risorse elaborazione eseguire.

### <a name="short-term-experimentation-and-evaluation"></a>Valutazione e sperimentazione a breve termine
Hello VM di analisi scientifica dei dati può essere utilizzato tooevaluate o informazioni su strumenti, ad esempio Microsoft R Server, SQL Server, strumenti di Visual Studio, Jupyter, deep learning / ML Toolkit e nuovi strumenti utilizzati di frequente nei hello community con uno sforzo minimo di installazione. Poiché hello VM di analisi scientifica dei dati può essere configurato rapidamente, può essere applicato in altri scenari di utilizzo a breve termine, ad esempio la replica esperimenti pubblicati, le demo, procedure dettagliate seguenti nelle sessioni online o esercitazioni conferenza in esecuzione.

### <a name="deep-learning"></a>Apprendimento avanzato
analisi scientifica dei dati Hello VM può essere utilizzato per training del modello utilizzando gli algoritmi di apprendimento completa su GPU hardware di base (unità di elaborazione grafica). Adotta VM scalabilità proprie capacità del cloud di Azure, DSVM consente di utilizzare hardware della GPU basato su cloud hello in base alle necessità. Una possibile passare tooa GPU basato su macchina virtuale durante il training di modelli di grandi dimensioni o necessitano calcoli ad alta velocità mantenendo hello stesso disco del sistema operativo.  edizione di Windows Server 2016 Hello di DSVM viene pre-installato con i driver GPU, Framework e la versione GPU di hello completa algoritmi di apprendimento. In hello Linux, deep learning GPU è abilitata solo nei hello [macchina virtuale di analisi scientifica dei dati per l'edizione di Linux (Ubuntu)](http://aka.ms/dsvm/ubuntu). È possibile distribuire l'edizione di Windows/Ubuntu-2016 hello di VM dell'analisi scientifica dei dati toonon GPU basato su macchina virtuale di Azure in questo caso tutti i framework di formazione hello verranno modalità toohello fallback della CPU. Per Windows Server 2012 è stato in precedenza pubblicato un [toolkit di apprendimento avanzato](http://aka.ms/dsvm/deeplearning), ma ora è consigliabile usare Windows Server 2016 per i carichi di lavoro di apprendimento avanzato basati su Windows. edizione basata su CentOS Linux Hello di hello DSVM contiene solo hello CPU build di alcune completa (CNTK, Tensorflow, MXNet) di strumenti di apprendimento hello ma non preinstallati con Framework e i driver GPU hello. 

## <a name="whats-included-in-hello-data-science-vm"></a>Cosa è incluso in hello VM di analisi scientifica dei dati?
Hello macchina virtuale di analisi scientifica dei dati ha molti analisi scientifica dei dati comuni e deep learning strumenti già installato e configurato. Include inoltre strumenti che consentono di facile toowork con vari prodotti analitica e di dati di Azure. Consente di esplorare e compilare modelli predittivi in set di dati su larga scala utilizzando hello Microsoft R Server o SQL Server 2016. Un host di altri strumenti dalla community open source hello e da Microsoft sono anche blocchi appunti e incluso, nonché esempi di codice. Hello nella tabella seguente vengono definiti e confronta i componenti principali di hello inclusi in Windows hello e le versioni di Linux di hello macchina virtuale di analisi scientifica dei dati.


| **Strumento**                                                           | **Edizione per Windows** | **Edizione per Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R Open](https://mran.microsoft.com/open/) con i pacchetti più diffusi pre-installati   |S                      | S             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition include <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) parallelo e framework R distribuito ad alte prestazioni<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction): nuovi algoritmi ML all'avanguardia da Microsoft <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [Operazionalizzazione R](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |S                      | S <br/> (MicrosoftML non ancora disponibile)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro-Plus con attivazione condivisa - Excel, Word e PowerPoint   |S                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 con i pacchetti più diffusi pre-installati    |S                      |S              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) con i pacchetti più diffusi pre-installati per il linguaggio di programmazione Julia                         |S                      |S              |
| Database relazionali                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Strumenti del database                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * driver di ODBC/JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (strumento di query), <br /> * bcp, sqlcmd <br /> * driver di ODBC/JDBC|
| Analisi database scalabile con SQL Server R services | S     |N              |
| **[Jupyter Notebook Server](http://jupyter.org/) con i kernel seguenti,**                                  | S     | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 & 3.5 | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | S | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | S |
|     &nbsp;&nbsp;&nbsp;&nbsp;*   [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (soltanto Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | S |
| JupyterHub (server notebook multiutente)| N | S |
| **Strumenti di sviluppo, editor di codice e IDE**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) &gt;con plug-in Git, Azure HDInsight (Hadoop), Data Lake, SQL Server Data Tools, [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs) e [R Tools per Visual Studio (RTVS)](http://microsoft.github.io/RTVS-docs/) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio Code](https://code.visualstudio.com/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Atom](https://atom.io/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (Julia IDE)](http://junolab.org/)| S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim ed Emacs | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git e GitBash | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* .Net Framework | S | N |
| PowerBI Desktop | S | N |
| SDK tooaccess Cortana Intelligence Suite di servizi e di Azure | S | S |
| **Strumenti di gestione e spostamento dati** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Storage Explorer | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy(Azure Data Lake Storage)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Strumento di migrazione dei dati DocDB](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Gateway di gestione dati di Microsoft](https://msdn.microsoft.com/library/dn879362.aspx): spostare i dati tra posizione locale e cloud | S | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Utilità della riga di comando Unix/Linux | S | S |
| [Apache Drill](http://drill.apache.org) per l'esplorazione dei dati | S | S |
| **Strumenti di Machine Learning** |||
| &nbsp;&nbsp;&nbsp;&nbsp;*- Integrazione con [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R, Python) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Xgboost](https://github.com/dmlc/xgboost) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rattle](http://rattle.togaware.com/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (soltanto Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [H2O](https://www.h2o.ai/h2o/) | N | Y (soltanto Ubuntu) |
| **Strumenti di apprendimento avanzato basati sulla GPU** |Edizione Windows Server 2016  |Edizione Ubuntu |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Tensorflow](https://www.tensorflow.org/) | S | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | S | S|
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Caffe &amp; Caffe2](https://github.com/caffe2/caffe2) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Driver Nvidia, CUDA, CUDNN](https://developer.nvidia.com/cuda-toolkit) | S | S |
| **Piattaforma Big Data (soltanto Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* [Spark](http://spark.apache.org/) locale indipendente | N | S |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Hadoop](http://hadoop.apache.org/) locale (HDFS, YARN) | N | S |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>La modalità di avvio con una macchina virtuale di analisi scientifica dei dati di Windows hello tooget
* Creare un'istanza dell'edizione di Windows DSVM hello desiderato, passare a
  * [DSVM basata su Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  oppure 
  * [DSVM basata su Windows Server 2012](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Fare clic su hello **ottenere IT ora** pulsante.
* Accedi toohello VM dal desktop remoto utilizzando le credenziali di hello specificato al momento della creazione hello macchina virtuale.
* toodiscover e avviare hello gli strumenti disponibili, fare clic su hello **avviare** menu.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Introduzione a hello VM Linux di analisi scientifica dei dati
* Creare un'istanza di hello desiderato edition Linux DSVM passando troppo
  * [DSVM basata su Ubuntu](http://aka.ms/dsvm/ubuntu)

  oppure

  * [DSVM basata su OpenLogic CentOS](http://aka.ms/dsvm/centos)

  
* Fare clic su hello **Scarica adesso** pulsante.
* Accedi toohello macchina virtuale da un client SSH, ad esempio Putty o comando SSH, utilizzando le credenziali di hello specificato al momento della creazione hello macchina virtuale.
* Nel prompt della shell hello, immettere informazioni di più dsvm.
* Per un computer desktop con interfaccia grafico, scaricare il client di hello X2Go per la piattaforma client [qui](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) e seguire le istruzioni di hello nel documento di analisi scientifica dei dati di Linux VM hello [hello provisioning macchina virtuale di analisi scientifica dei dati Linux](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Passaggi successivi
### <a name="for-hello-windows-data-science-vm"></a>Per la macchina virtuale di analisi scientifica dei dati di Windows hello
* Per ulteriori informazioni su come toorun specifici strumenti disponibile nella versione di Windows hello, vedere [hello effettuare il provisioning della macchina virtuale dell'analisi scientifica dei dati Microsoft](machine-learning-data-science-provision-vm.md) e
* Per ulteriori informazioni su come tooperform diverse attività necessarie per il progetto di analisi scientifica dei dati su hello macchina virtuale di Windows, vedere [dieci operazioni da eseguire su hello analisi scientifica dei dati macchina virtuale](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Per hello VM Linux di analisi scientifica dei dati
* Per ulteriori informazioni su come toorun specifici strumenti disponibile nella versione di hello Linux, vedere [hello provisioning macchina virtuale di analisi scientifica dei dati di Linux](machine-learning-data-science-linux-dsvm-intro.md).
* Per una procedura dettagliata che illustra come tooperform attività più comuni analisi scientifica dei dati con hello VM Linux, vedere [analisi scientifica dei dati nella macchina virtuale di analisi scientifica dei dati di Linux hello](machine-learning-data-science-linux-dsvm-walkthrough.md).

