---
title: Data Lake archivio ottimizzazione linee guida sulle prestazioni aaaAzure | Documenti Microsoft
description: Linee guida per l'ottimizzazione delle prestazioni di Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Ottimizzazione delle prestazioni di Azure Data Lake Store

Data Lake Store supporta la velocità effettiva elevata per l'analisi con uso intensivo dell'I/O e lo spostamento dei dati.  In archivio Azure Data Lake utilizzando tutti disponibile velocità effettiva: quantità hello di dati che possono essere letti o scritti al secondo: è importante tooget ottenere prestazioni ottimali hello.  Questo risultato viene ottenuto eseguendo il numero massimo possibile di operazioni di lettura e scrittura in parallelo.

![Prestazioni di Data Lake Store](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Archivio Azure Data Lake adattabile tooprovide hello necessaria una velocità effettiva per scenario analitica tutti. Per impostazione predefinita, un account archivio Azure Data Lake fornisce automaticamente la velocità effettiva sufficiente esigenze hello toomeet di un'ampia categoria di casi di utilizzo. Per i casi in cui i clienti eseguire in limite predefinito di hello hello hello account ADLS può essere configurato tooprovide maggiore velocità effettiva contattando il supporto tecnico Microsoft.

## <a name="data-ingestion"></a>Inserimento di dati

Durante l'inserimento di dati da un tooADLS di sistema di origine, è importante tooconsider che hello tooADLS di connettività di rete, hardware di rete di origine e hardware di origine può essere collo di bottiglia hello.  

![Prestazioni di Data Lake Store](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

È importante tooensure che hello lo spostamento dei dati non è interessato da tali fattori.

### <a name="source-hardware"></a>Hardware di origine

Se si utilizza il computer locale o macchine virtuali in Azure, è necessario scegliere con attenzione hardware appropriato hello. Per l'Hardware del disco di origine, preferisce tooHDDs unità SSD e selezionare l'hardware del disco con dischi più veloci. Per l'Hardware di rete di origine, utilizzare le schede NIC tempi hello.  In Azure, si consiglia di macchine virtuali di Azure D14 disco in modo appropriato potente hello e hardware di rete.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Archivio tooAzure Data Lake di connettività di rete

connettività di rete Hello tra i dati di origine e l'archivio Azure Data Lake può talvolta essere collo di bottiglia hello. Quando i dati di origine sono in locale, valutare l'opportunità di usare un collegamento dedicato con [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/) . Se i dati di origine in Azure, hello prestazioni saranno migliori quando i dati di hello sono hello stessa area Azure hello archivio Data Lake.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Configurare gli strumenti di inserimento di dati per la massima parallelizzazione

Una volta siano risolti hardware origine hello e colli di bottiglia connettività precedente di rete, si è pronti tooconfigure gli strumenti di inserimento. Hello nella tabella seguente sono riepilogate le impostazioni di chiave hello di più strumenti comuni di inserimento e fornisce approfondita ottimizzazione delle prestazioni degli articoli per essi.  toolearn ulteriori informazioni su quale strumento toouse per lo scenario, visitare questo [articolo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Strumento               | Impostazioni     | Altre informazioni                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Collegamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Unità Azure Data Lake Analytics  |   [Collegamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (mapper)   | [Collegamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Data factory di Azure| parallelCopies    | [Collegamento](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size, -m (mapper)    |   [Collegamento](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Strutturare il set di dati

Quando i dati vengono archiviati in archivio Data Lake, dimensioni del file hello, numero di file e la struttura di cartelle attiva un impatto sulle prestazioni.  Hello nella sezione seguente vengono descritte le procedure consigliate in queste aree.  

### <a name="file-size"></a>Dimensioni complete

I motori di analisi come HDInsight e Azure Data Lake Analytics in genere gestiscono il sovraccarico a livello di singolo file.  Se quindi si archiviano i dati in molti file di piccole dimensioni, questo può influire negativamente sulle prestazioni.  

Per ottenere prestazioni migliori, è in genere opportuno organizzare i dati in file di dimensioni più grandi.  Come regola generale, organizzare i set di dati in file di 256 MB o di dimensione maggiore. In alcuni casi, ad esempio immagini e dati binari, non è possibile tooprocess usarle in parallelo.  In questi casi, è consigliabile tookeep singoli file meno di 2GB.

In alcuni casi, le pipeline di dati non dispongono di controllo sui dati non elaborati di hello che dispone di molti file di piccole dimensioni.  È consigliabile toohave processo "cooking" che genera l'errore maggiori file toouse per le applicazioni a valle.  

### <a name="organizing-time-series-data-in-folders"></a>Organizzazione dei dati di serie temporali in cartelle

Hive e ADLA carichi di lavoro, l'eliminazione di partizione dei dati della serie temporale consente di alcune query solo un subset di dati hello che migliora le prestazioni di lettura.    

Queste pipeline che inseriscono dati di serie temporali, posizionano spesso i file usando un sistema di denominazione molto strutturato per file e cartelle. Di seguito è riportato un esempio molto comune in cui i dati sono strutturati per data:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Si noti che le informazioni di data/ora hello viene visualizzato come cartelle e nel nome file hello.

Per data e ora, hello seguito è riportato un modello comune

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Nuovamente, scelta hello effettuata con l'organizzazione di file e cartelle hello necessario ottimizzare per hello dimensione dei file e un numero ragionevole di file in ogni cartella.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Ottimizzazione dei processi con uso intensivo dell'I/O nei carichi di lavoro Hadoop e Spark in HDInsight

I processi rientrano in uno dei seguenti tre categorie di hello:

* **Uso intensivo della CPU.**  Questi processi hanno tempi di elaborazione lunghi e tempi di I/O minimi,  come i processi di machine learning e quelli di elaborazione del linguaggio naturale.  
* **Uso intensivo della memoria.**  Questi processi usano grandi quantità di memoria,  come i processi di PageRank e quelli di analisi in tempo reale.  
* **Uso intensivo dell'I/O.**  Questi processi impiegano la maggior parte del tempo a eseguire operazioni di I/O.  Un esempio comune è rappresentato da un processo di copia che esegue solo operazioni di lettura e scrittura.  Altri esempi includono i processi preparazione dei dati letti una grande quantità di dati, esegue alcune trasformazioni di dati e quindi scrive hello archivio back-toohello dati.  

istruzioni disponibili Hello è solo applicabili tooI processi/O intensivo.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Considerazioni generali per un cluster HDInsight

* **Versioni di HDInsight.** Per prestazioni ottimali, utilizzare l'ultima versione di hello di HDInsight.
* **Aree.** Inserire l'archivio Data Lake di hello in hello cluster HDInsight hello stessa area.  

Un cluster HDInsight è composto da due nodi head e da alcuni nodi di ruolo di lavoro. Ogni nodo di lavoro fornisce un numero specifico di core e memoria, è determinata dal hello tipo di macchina virtuale.  Quando si esegue un processo, YARN è negoziatore risorse hello che alloca la memoria disponibile di hello e contenitori toocreate Core.  Ogni contenitore viene eseguito processo hello toocomplete necessarie attività di hello.  Contenitori vengono eseguiti in parallelo tooprocess attività rapidamente. È quindi possibile ottenere un miglioramento delle prestazioni eseguendo la quantità massima possibile di contenitori paralleli.

Esistono tre livelli all'interno di un cluster HDInsight che possono essere ottimizzate tooincrease hello numero di contenitori e usare la velocità effettiva tutti disponibile.  

* **Livello fisico**
* **Livello YARN**
* **Livello del carico di lavoro**

### <a name="physical-layer"></a>Livello fisico

**Eseguire il cluster con più nodi e/o macchine virtuali di dimensioni maggiori.**  Un cluster di dimensioni maggiore consentirà si toorun più contenitori di YARN, come illustrato nell'immagine di hello riportata di seguito.

![Prestazioni di Data Lake Store](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Usare macchine virtuali con maggiore larghezza di banda di rete.**  quantità di Hello di larghezza di banda di rete può essere un collo di bottiglia, se è meno larghezza di banda di rete di velocità effettiva di archivio Data Lake.  Macchine virtuali differenti avranno dimensioni variabili della larghezza di banda di rete.  Scegliere un tipo di macchina virtuale che dispone di hello più grande possibile larghezza di banda.

### <a name="yarn-layer"></a>Livello YARN

**Usare contenitori YARN di dimensioni inferiori.**  Ridurre le dimensioni di hello di ogni toocreate contenitore YARN più contenitori con hello stessa quantità di risorse.

![Prestazioni di Data Lake Store](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

A seconda del carico di lavoro, sarà sempre necessaria una dimensione minima per i contenitori YARN. Se si sceglie un contenitore troppo piccolo, si verificheranno problemi di memoria insufficiente per i processi. In genere, la dimensione dei contenitori YARN non deve essere inferiore a 1 GB. Si tratta di contenitori YARN 3GB toosee comuni. Per alcuni carichi di lavoro, possono essere necessari contenitori YARN più grandi.  

**Aumentare il numero di core per contenitore YARN.**  Aumentare il numero di hello di core allocati tooeach contenitore tooincrease hello numero di attività parallele in esecuzione in ogni contenitore.  Questa soluzione è valida per le applicazioni, come Spark, che eseguono più attività per contenitore.  Per le applicazioni, ad esempio Hive che eseguono un singolo thread in ogni contenitore, è meglio toohave più contenitori anziché più core per ogni contenitore.   

### <a name="workload-layer"></a>Livello del carico di lavoro

**Usare tutti i contenitori disponibili.**  Impostare il numero di hello di attività toobe uguale o maggiore del numero di hello di contenitori disponibili, in modo che tutte le risorse vengono utilizzate.

![Prestazioni di Data Lake Store](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Le attività che non vengono eseguite correttamente sono dispendiose.** Se ogni attività dispone di una grande quantità di dati tooprocess, errore di un'attività risultati in un nuovo tentativo di costoso.  Pertanto, è preferibile toocreate altre attività, ognuno dei quali elabora una piccola quantità di dati.

In aggiunta toohello linee guida generali sopra, ogni applicazione dispone di parametri diversi tootune disponibili per l'applicazione specifica. tabella Hello riportata di seguito sono elencate alcune hello parametri e i collegamenti tooget avviato con l'ottimizzazione delle prestazioni per ogni applicazione.

| Carico di lavoro               | Attività tooset parametro                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Spark in HDInisight](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Executor-memory</li><li>Executor-cores</li></ul> |
| [Hive in HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce in HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm in HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Numero di processi del ruolo di lavoro</li><li>Numero di istanze di spout executor</li><li>Numero di istanze di bolt executor </li><li>Numero di attività spout</li><li>Numero di attività bolt</li></ul>|

## <a name="see-also"></a>Vedere anche
* [Panoramica dell’Archivio Data Lake di Azure](data-lake-store-overview.md)
* [Introduzione all’analisi dei dati di Data Lake di Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
