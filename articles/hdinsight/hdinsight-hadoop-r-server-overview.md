---
title: aaaIntroduction tooR Server in Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse R Server per HDInsight toocreate applicazioni per l'analisi di dati.
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Introduzione tooR Server e le funzionalità di R open source in HDInsight

Microsoft R Server è disponibile come opzione di implementazione quando si creano cluster HDInsight in Azure. Questa nuova funzionalità offre gli esperti di dati statistici e ai programmatori di R con tooscalable accesso su richiesta, metodi distribuiti di analitica in HDInsight.

I cluster possono essere configurato in maniera appropriata toohello progetti e attività e quindi eliminata quando essi sono più necessari. Perché sono parte di Azure HDInsight, questi cluster includono il supporto di 24/7 a livello aziendale, un contratto di servizio del 99,9% tempo di attività e hello toointegrate possibilità con altri componenti di hello ecosistema di Azure.

R Server in HDInsight offre funzionalità più recente di hello per analitica basato su R nel set di dati di qualsiasi dimensione, caricato tooeither spazio di archiviazione Blob di Azure o Data Lake. Poiché R Server si basa su R open source, hello basato su R delle applicazioni possono sfruttare pacchetti hello 8000 + R open source. routine di Hello in ScaleR, pacchetto analitica di dati di Microsoft incluso R Server, sono anche disponibili.

nodo di Hello del bordo di un cluster fornisce una posizione comoda tooconnect toohello cluster e toorun gli script R. Con un nodo del bordo, si dispone di funzioni di opzione di esecuzione hello parallelizzato distributed hello di ScaleR tra core hello del server di nodo perimetrale hello. È possibile anche eseguirli tra i nodi del cluster hello hello utilizzando del ScaleR Hadoop MapReduce o Spark contesti di calcolo.

i modelli di Hello o stime che è possibile scaricare i risultati di analisi per utilizzano in locale. o impiegate altrove in Azure, in particolare tramite il [servizio Web](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md) di [Azure Machine Learning Studio](http://studio.azureml.net).

## <a name="get-started-with-r-on-hdinsight"></a>Introduzione all'uso di R su HDInsight
tooinclude R Server in un cluster HDInsight, è necessario selezionare il tipo di cluster di Server R hello durante la creazione di un cluster HDInsight tramite hello portale di Azure. il tipo di cluster di Server R Hello include R Server ai nodi dati hello del cluster di hello e su un nodo di edge, che funge da una zona di destinazione per analitica basato su Server R. Vedere [Guida introduttiva di R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md) per una procedura dettagliata su come toocreate hello cluster.

## <a name="learn-about-data-storage-options"></a>Informazioni sulle opzioni di archiviazione dei dati
Spazio di archiviazione predefinito per hello HDFS file system del cluster HDInsight può essere associata a un account di archiviazione di Azure o un archivio Azure Data Lake. Questa associazione assicura che tutti i dati viene caricati toohello archiviazione del cluster durante l'analisi viene resa persistente. Sono disponibili vari strumenti per la gestione di hello trasferimento toohello opzione dell'archivio dati che si seleziona, incluse funzionalità di caricamento basate sul portale hello dell'account di archiviazione hello e hello [AzCopy](../storage/common/storage-use-azcopy.md) utilità.

È possibile hello aggiunta tooadditional accesso ai dati Blob e archivi lake durante il processo indipendentemente dall'opzione di archiviazione primaria hello in uso di provisioning del cluster di hello. Vedere [Guida introduttiva di R Server in HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) per informazioni sull'aggiunta di account di accesso tooadditional. Vedere hello supplementare [opzioni di archiviazione di Azure per R Server HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) toolearn articolo ulteriori informazioni sull'utilizzo di più account di archiviazione.

È inoltre possibile utilizzare [file di Azure](../storage/files/storage-how-to-use-files-linux.md) come opzione di archiviazione per l'utilizzo nel nodo edge hello. File di Azure consente toomount una condivisione file che è stata creata in archiviazione di Azure toohello sistema di file di Linux. Per altre informazioni su queste opzioni di archiviazione dei dati per R Server su cluster HDInsight, vedere [Azure Storage options for R Server on HDInsight clusters](hdinsight-hadoop-r-server-storage.md)(Opzioni di Archiviazione di Azure per R Server su cluster HDInsight).

## <a name="access-r-server-on-hello-cluster"></a>Accesso R Server nel cluster hello
È possibile connettersi tooR tooinclude RStudio Server scelta Server nel nodo edge hello utilizzando un browser, fornito durante il processo di provisioning hello. Se quest'ultimo non è stato installato al durante il provisioning di cluster hello, è possibile aggiungere in un secondo momento. Per informazioni sull'installazione di RStudio Server dopo la creazione di un cluster, vedere [Installing RStudio Server on HDInsight clusters](hdinsight-hadoop-r-server-install-r-studio.md) (Installazione di RStudio Server in cluster HDInsight). È inoltre possibile connettere toohello R Server mediante SSH/PuTTY tooaccess hello R console. 

## <a name="develop-and-run-r-scripts"></a>Sviluppare ed eseguire script R
creare ed eseguire gli script di Hello R è possono utilizzare uno qualsiasi dei hello 8000 + pacchetti R open source in aggiunta toohello parallelizzato e distribuiti routine disponibili nella libreria ScaleR hello. In generale, uno script che viene eseguito con R Server sul nodo del bordo hello viene eseguito con l'interprete R hello in tale nodo. eccezioni di Hello sono i passaggi necessari toocall una funzione ScaleR con un contesto di calcolo che viene impostato tooHadoop MapReduce (RxHadoopMR) o Spark (RxSpark). In questo caso, la funzione hello viene eseguito in modalità distribuita tra i nodi di dati (attività) del cluster hello che sono associati a dati hello a cui fa riferimento. Per ulteriori informazioni sulle opzioni di contesto di calcolo diversi hello, vedere [calcolo opzioni del contesto per il Server di R in HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Rendere operativo un modello
Una volta completata la modellazione dei dati, è possibile rendere operative le stime di toomake hello modello per i nuovi dati da Azure e locali. Questo processo è noto come assegnazione di punteggi. L'assegnazione dei punteggi può essere eseguita in HDInsight, in Azure Machine Learning o in locale.

### <a name="score-in-hdinsight"></a>Assegnare punteggi in HDInsight
tooscore in HDInsight, scrivere una funzione di R che chiama il modello toomake le stime per un nuovo file di dati che sono stati caricati tooyour account di archiviazione. Quindi salvare le stime hello toohello back-account di archiviazione. Nel nodo di edge hello del cluster o tramite un processo pianificato, è possibile eseguire hello routine su richiesta.  

### <a name="score-in-azure-machine-learning-aml"></a>Assegnare punteggi in Azure Machine Learning (AML)
utilizzando un servizio web AML, utilizzare hello tooscore apre il pacchetto di Azure Machine Learning R origine noto come [Azure ml](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish il modello come un servizio web di Azure. Per comodità, questo pacchetto è già installato nel nodo di hello del bordo. Successivamente, utilizzare funzioni hello in Machine Learning toocreate un'interfaccia utente per il servizio web hello e chiamare quindi il servizio web di hello in base alle esigenze per il punteggio.

Se si sceglie questa opzione, è necessario utilizzare qualsiasi ScaleR modello oggetti tooequivalent open source degli oggetti del modello con il servizio web hello tooconvert. Per tale conversione usare le funzioni di coercizione di ScaleR, come `as.randomForest()` per i modelli basati su insiemi.

### <a name="score-on-premises"></a>Assegnare punteggi in locale
tooscore locale dopo la creazione del modello, è possibile serializzare il modello di hello in R, download, deserializzazione e quindi utilizzarlo per il punteggio di nuovi dati. È possibile assegnare un punteggio nuovi dati con hello approccio descritto in precedenza nella [punteggio in HDInsight](#scoring-in-hdinsight) o utilizzando [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Gestire i cluster di hello
### <a name="install-and-maintain-r-packages"></a>Installare e gestire i pacchetti R
La maggior parte dei pacchetti hello R usati sono necessarie nel nodo del bordo hello poiché la maggior parte dei passaggi degli script R eseguiti. pacchetti R aggiuntivi tooinstall nel nodo di hello edge, è possibile utilizzare hello consueta `install.packages()` metodo in R.

Se si utilizza soltanto routine dalla libreria ScaleR hello cluster hello, non è in genere necessario tooinstall pacchetti R aggiuntivi ai nodi dati hello. Tuttavia, potrebbe essere necessario utilizzare hello toosupport di pacchetti aggiuntivi di **rxExec** o **RxDataStep** esecuzione ai nodi dati hello.

In questi casi, possono essere installati pacchetti aggiuntivi di hello con un'azione di script dopo aver creato il cluster hello. Per altre informazioni, vedere l'articolo relativo alla [creazione di un cluster HDInsight con R Server](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Modificare le impostazioni di memoria per Hadoop MapReduce
Un cluster può essere modificato toochange hello memoria che è disponibile tooR Server quando è in esecuzione un processo MapReduce. toomodify un cluster, utilizzare hello Apache Ambari dell'interfaccia utente disponibili tramite hello Azure-blade portale per il cluster. Per istruzioni su come tooaccess hello Ambari UI per il cluster, vedere [gestione dei cluster HDInsight tramite hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).

È inoltre possibile toochange hello memoria che è disponibile tooR Server utilizzando opzioni di Hadoop in chiamata hello troppo**RxHadoopMR** come indicato di seguito:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Applicare la scalabilità al cluster
Un cluster esistente può essere scalato verso l'alto o verso il basso attraverso il portale di hello. Scalando, è possibile ottenere una capacità aggiuntiva hello che potrebbe essere necessario per attività di elaborazione più grande oppure è possibile abbassare un cluster quando è inattivo. Per istruzioni su come tooscale un cluster, vedere [cluster HDInsight gestire](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Gestire il sistema hello
Altri aggiornamenti e patch del sistema operativo di tooapply manutenzione viene eseguita su hello sottostante macchine virtuali Linux in un cluster HDInsight l'orario di ufficio. In genere, la manutenzione viene eseguita alle 3:30:00 (in base all'ora locale hello hello VM) ogni lunedì e giovedì. Gli aggiornamenti vengono eseguiti in modo che queste non influiscono sulle più di un trimestre di cluster hello alla volta.  

Poiché i nodi head hello sono ridondanti e non tutti i nodi di dati sono interessati, tutti i processi in esecuzione durante questo tempo potrebbero rallentare. Deve essere ancora eseguito toocompletion, tuttavia. Gli eventuali software personalizzati o i dati locali di cui si dispone vengono preservati durante tutti questi eventi di manutenzione, a meno che si verifichi un errore catastrofico che richiede la ricompilazione del cluster.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Informazioni sulle opzioni IDE per R Server su un cluster HDInsight
nodo di Hello Linux del bordo di un cluster HDInsight è hello zona per l'analisi basata su R di destinazione. Le versioni recenti di HDInsight offrono un'opzione predefinita per l'installazione di versione della community di hello [RStudio Server](https://www.rstudio.com/products/rstudio-server/) nel nodo edge hello come un IDE basate su browser. Utilizzo di RStudio Server come un IDE per lo sviluppo di hello e l'esecuzione di script R può essere notevolmente più produttivi rispetto all'utilizzo solo di console hello R. Se si sceglie di non tooadd RStudio Server durante la creazione di cluster hello ma vogliono tooadd in un secondo momento, quindi vedere [installazione R Studio Server nei cluster HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Un'altra opzione IDE completa è tooinstall un IDE desktop e usarlo cluster hello tooaccess tramite l'utilizzo di un contesto di calcolo remoto MapReduce o Spark. Le opzioni includono [R Tools per Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS) Microsoft, RStudio e [StatET](http://www.walware.de/goto/statet) Walware basato su Eclipse.

Infine, è possibile accedere console di R Server hello sul nodo del bordo hello digitando **R** al prompt dei comandi di Linux hello dopo la connessione tramite SSH o PuTY. Quando si utilizza l'interfaccia della console hello, è utile toorun un editor di testo per lo sviluppo di script R in un'altra finestra e tagliare e incollare sezioni dello script nella console R hello in base alle esigenze.

## <a name="learn-about-pricing"></a>Informazioni sui prezzi
Hello addebiti associati a un cluster con R Server sono di HDInsight strutturato in modo analogo toohello tariffe per i cluster HDInsight standard hello. Sono basate su ridimensionamento hello di hello sottostante macchine virtuali tra nome hello, dati e i nodi di bordo, con aggiunta di hello di un sollevamento core ora. Per ulteriori informazioni sui prezzi di HDInsight e la disponibilità di hello di una versione di valutazione gratuita di 30 giorni, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su come i cluster toouse R Server con HDInsight, vedere hello seguenti argomenti:

* [Introduzione a R Server su HDInsight](hdinsight-hadoop-r-server-get-started.md)
* [Aggiungere RStudio Server tooHDInsight (se non è installato durante la creazione del cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opzioni di Archiviazione di Azure per R Server su HDInsight](hdinsight-hadoop-r-server-storage.md)
