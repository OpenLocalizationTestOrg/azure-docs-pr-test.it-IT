---
title: opzioni del contesto aaaCompute per Server di R in HDInsight - Azure | Documenti Microsoft
description: Informazioni su hello calcolo differente contesto opzioni disponibile toousers con R Server in HDInsight
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Opzioni del contesto di calcolo per R Server su HDInsight (anteprima)

Microsoft R Server in Azure HDInsight controlla l'esecuzione delle chiamate dal contesto di calcolo hello impostazione. Questo articolo vengono illustrati le opzioni di hello che siano disponibili toospecify se e come viene eseguito in parallelo esecuzione tra core del nodo del bordo hello o del cluster HDInsight.

nodo di Hello del bordo di un cluster fornisce una posizione comoda tooconnect toohello cluster e toorun gli script R. Con un nodo del bordo, si dispone di funzioni di opzione di esecuzione hello parallelizzato distributed hello di ScaleR tra core hello del server di nodo perimetrale hello. È possibile anche eseguirli tra i nodi del cluster hello hello utilizzando del ScaleR Hadoop MapReduce o Spark contesti di calcolo.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server in Azure HDInsight
[Microsoft R Server in Azure HDInsight](hdinsight-hadoop-r-server-overview.md) fornisce funzionalità più recenti di hello per basato su R analitica. È possibile utilizzare i dati archiviati in un contenitore HDFS il [Blob di Azure](../storage/common/storage-introduction.md "archiviazione Blob di Azure") account di archiviazione, un archivio Data Lake o file system di hello locale Linux. Poiché R Server si basa su R open source, applicazioni basate su R hello che compili possono applicare uno qualsiasi dei pacchetti hello 8000 + R open source. È inoltre possibile utilizzare le routine di hello in [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), big data analitica pacchetto Microsoft incluso con R Server.  

## <a name="compute-contexts-for-an-edge-node"></a>Contesti di calcolo per un nodo perimetrale
In generale, uno script R che viene eseguito nel Server R sul nodo del bordo hello viene eseguito all'interno di interprete R hello in tale nodo. eccezioni di Hello sono i passaggi che chiama una funzione di ridimensionamento. le chiamate ScaleR Hello eseguite in un ambiente di calcolo che è determinato dal contesto di calcolo ScaleR hello all'impostazione.  Quando si esegue lo script R da un nodo del bordo, i valori possibili di hello hello calcolano contesto sono:

- sequenziale locale (*"local"*)
- parallelo locale (*"localpar"*)
- MapReduce
- Spark

Hello *'local'* e *'localpar'* opzioni differiscono solo come **rxExec** chiamate vengono eseguite. Entrambi eseguono altre chiamate di funzione rx in modo parallelo tra core tutti disponibili se non specificato diversamente mediante l'utilizzo di hello ScaleR **numCoresToUse** opzione, ad esempio `rxOptions(numCoresToUse=6)`. Le opzioni di esecuzione parallela offrono prestazioni ottimali.

Hello nella tabella seguente vengono riepilogate hello che vari tooset opzioni contesto esecuzione delle chiamate di calcolo:

| Contesto di calcolo  | Come tooset                      | Contesto di esecuzione                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Sequenziale locale | rxSetComputeContext('local')    | Parallelizzato esecuzione tra core hello di hello nodo server perimetrale tranne rxExec chiamate, che vengono eseguite in serie |
| Parallelo locale   | rxSetComputeContext('localpar') | Parallelizzato esecuzione tra core hello del server di nodo perimetrale hello |
| Spark            | RxSpark()                       | Parallelizzato esecuzione distribuita tramite Spark tra i nodi di hello del cluster HDI hello |
| MapReduce       | RxHadoopMR()                    | Parallelizzato esecuzione distribuita tramite MapReduce tra i nodi di hello del cluster HDI hello |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Linee guida per la scelta di un contesto di calcolo

Quali hello tre opzioni che consente l'esecuzione parallelizzato dipende dalla natura hello analitica, dimensioni hello ed eseguire il percorso di hello dei dati. Non sussiste alcuna formula semplice che indica quale toouse contesto di calcolo. Esistono tuttavia alcuni principi che consentono di effettuare la scelta giusta hello o, almeno, consentono di limitare le scelte effettuate prima di eseguire un benchmark. Ecco alcuni dei principi guida:

- file system di Hello locale Linux è più veloce rispetto a HDFS.
- Analisi ripetute sono più veloce se i dati di hello sono locali, e se è presente nel con estensione XDF.
- È preferibile toostream piccole quantità di dati da un'origine dati di testo. Se è più grande quantità di hello di data, convertirla tooXDF prima dell'analisi.
- sovraccarico Hello di copia o nodo di hello dati toohello del bordo per l'analisi di flusso diventa difficile da gestire per grandi quantità di dati.
- Spark è più veloce rispetto a Map Reduce per l'analisi in Hadoop.

Questi principi di base, hello nelle sezioni seguenti offrono alcune regole generali per la selezione di un contesto di calcolo.

### <a name="local"></a>Local
* Se la quantità di hello di tooanalyze dati sono limitate e non richiede analisi ripetute, quindi il flusso direttamente in hello analisi routine tramite *'local'* o *'localpar'*.
* Se quantità hello di tooanalyze dati è di piccole o medie dimensioni e richiede analisi ripetute, quindi copiarlo toohello file system locale, importarlo tooXDF e analizzarli tramite *'local'* o *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Se è grande quantità di hello di tooanalyze di dati, quindi importarlo tooa frame di dati di Spark usando **RxHiveData** o **RxParquetData**, tooXDF in HDFS o (a meno che l'archiviazione è un problema) e analizzarlo hello Spark contesto di calcolo.

### <a name="hadoop-map-reduce"></a>Hadoop MapReduce
* Utilizzare il contesto di calcolo MapReduce hello solo se si verifica un problema con il contesto di calcolo di hello Spark insormontabili perché è in genere più lento.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Guida in linea su rxSetComputeContext
Per ulteriori informazioni ed esempi di ScaleR contesti di calcolo, vedere la Guida in R sul metodo rxSetComputeContext hello, ad esempio hello inline:

    > ?rxSetComputeContext

È anche possibile fare riferimento toohello "[ScaleR Distributed Computing Guide](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" disponibile all'hello [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server su MSDN") libreria.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato sulle opzioni hello toospecify disponibili se e come l'esecuzione viene parallelizzata tra core del nodo del bordo hello o del cluster HDInsight. toolearn ulteriori informazioni su come i cluster toouse R Server con HDInsight, vedere hello seguenti argomenti:

* [Panoramica: R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-overview.md)
* [Introduzione all'uso di R Server su HDInsight (anteprima)](hdinsight-hadoop-r-server-get-started.md)
* [Aggiungere RStudio Server tooHDInsight (se non è aggiunto durante la creazione del cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opzioni di Archiviazione di Azure per R Server su HDInsight](hdinsight-hadoop-r-server-storage.md)

