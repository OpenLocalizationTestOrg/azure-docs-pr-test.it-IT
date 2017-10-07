---
title: tooSpark aaaIntroduction in Azure HDInsight | Documenti Microsoft
description: "Questo articolo fornisce un'introduzione tooSpark su HDInsight e hello diversi scenari in cui è possibile utilizzare cluster Spark in HDInsight."
keywords: "che cos'è spark apache, cluster spark, introduzione toospark, spark in hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Introduzione tooSpark in HDInsight

In questo articolo fornisce un'introduzione tooSpark in HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> è un framework di elaborazione parallela open source che supporta in memoria prestazioni di elaborazione tooboost hello delle applicazioni analitiche big data. Il cluster Spark in HDInsight è compatibile con Archiviazione di Azure (WASB) e con Azure Data Lake Store. È quindi possibile elaborare con facilità tramite un cluster Spark i dati esistenti archiviati in Azure.

Quando si crea un cluster Spark in HDInsight, si creano risorse di calcolo di Azure con Spark installato e configurato. È sufficiente cluster toocreate un Spark in HDInsight circa dieci minuti. Hello toobe di dati elaborati verrà archiviati in archiviazione di Azure o archivio Azure Data Lake. Vedere [Usare l'Archiviazione di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).

**cluster toocreate un Spark in HDInsight**, vedere [Guida introduttiva: creare un cluster Spark in HDInsight ed eseguire query interattivo utilizzando Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Informazioni su Apache Spark in Azure HDInsight
I cluster Spark in HDInsight offrono un servizio Spark completamente gestito. I vantaggi della creazione di un cluster Spark in HDInsight sono elencati qui.

| Funzionalità | Descrizione |
| --- | --- |
| Facilità di creazione dei cluster Spark |È possibile creare un nuovo cluster Spark in HDInsight in minuti con hello portale di Azure, Azure PowerShell o hello HDInsight .NET SDK. Vedere [Introduzione ai cluster Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Semplicità d'uso |Il cluster Spark in HDInsight include notebook di Jupyter e Zeppelin. È possibile usarli per la visualizzazione e l'elaborazione interattiva di dati.|
| API REST |I cluster Spark in HDInsight sono [inserire il](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), un Spark basate su API REST di processi server tooremotely invio e monitoraggio processi. |
| Supporto per Archivio Azure Data Lake | Il cluster Spark in HDInsight può essere configurato toouse archivio Azure Data Lake come un'ulteriore spazio di archiviazione, nonché l'archiviazione primaria (solo con i cluster HDInsight 3.5). Per altre informazioni su Archivio Data Lake, vedere [Panoramica di Archivio Azure Data Lake](../data-lake-store/data-lake-store-overview.md). |
| Integrazione con servizi di Azure |Il cluster Spark in HDInsight viene fornito con un tooAzure connettore hub eventi. Gli utenti possono creare lo streaming di applicazioni con gli hub di eventi di hello inoltre troppo[Kafka](http://kafka.apache.org/), che è già disponibile come parte di Spark. |
| Supporto per R Server | È possibile impostare un Server di R in HDInsight Spark cluster toorun distribuita calcoli R con velocità hello promessa con un cluster Spark. Per altre informazioni, vedere [Introduzione all'uso di R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md). |
| Integrazione con IDE di terze parti | HDInsight fornisce i plug-in per IDE come IntelliJ IDEA ed Eclipse, che è possibile utilizzare toocreate e inviare tooan applicazioni cluster HDInsight Spark. Per altre informazioni, vedere [Usare Azure Toolkit per IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md) e [Usare Azure Toolkit per Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Query simultanee |I cluster Spark in HDInsight supportano le query simultanee. In questo modo più query da un utente o di più query da diversi utenti e applicazioni tooshare hello stesse risorse di cluster. |
| La memorizzazione nella cache nelle unità SSD |È possibile scegliere toocache dati in memoria o in unità SSD allegato toohello i nodi del cluster. La memorizzazione nella cache in memoria offre migliori prestazioni di query hello ma può essere costoso; memorizzazione nella cache in unità SSD fornisce un'opzione utilissima per migliorare le prestazioni di query senza necessità di hello toocreate un cluster di dimensioni che sono necessario toofit hello intero set di dati in memoria. |
| Integrazione con strumenti di Business Intelligence |I cluster Spark in HDInsight offrono connettori per strumenti di Business Intelligence, come [Power BI](http://www.powerbi.com/) e [Tableau](http://www.tableau.com/products/desktop), per l'analisi dei dati. |
| Librerie Anaconda precaricate |I cluster Spark in HDInsight sono dotati di librerie Anaconda preinstallate [Anaconda](http://docs.continuum.io/anaconda/) fornisce librerie too200 chiusura per l'apprendimento, analisi dei dati, visualizzazione e così via. |
| Scalabilità |Sebbene sia possibile specificare il numero di hello di nodi del cluster durante la creazione, si desidera toogrow oppure ridurre il carico di lavoro di hello cluster toomatch. Tutti i cluster HDInsight consentono numero hello toochange di nodi nel cluster hello. Inoltre, i cluster Spark possono essere eliminati senza perdita di dati poiché tutti i dati di hello viene archiviata in archiviazione di Azure o archivio Data Lake. |
| Supporto 24/7 |I cluster Spark in HDInsight includono il supporto continuo a livello aziendale e un Contratto di servizio che garantisce tempi di attività pari al 99,9%. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Quali sono i casi di utilizzo hello per Spark in HDInsight?
Il cluster Spark in HDInsight Abilita hello seguendo gli scenari principali.

### <a name="interactive-data-analysis-and-bi"></a>Analisi dei dati interattivi e Business Intelligence
[Esaminare un'esercitazione](hdinsight-apache-spark-use-bi-tools.md)

Apache Spark in HDInsight archivia i dati nell'Archiviazione di Azure o in Azure Data Lake Store. Esperti aziendali e responsabili delle decisioni chiave possono analizzare e generare rapporti su dati e report interattivi di Microsoft Power BI toobuild dai dati hello analizzato. Gli analisti possono avviare dai dati non strutturati/semi strutturati nell'archiviazione cluster, definire uno schema per i dati di hello utilizzando blocchi appunti e quindi compilare modelli di dati con Microsoft Power BI. I cluster Spark in HDInsight supportano anche alcuni strumenti di BI di terze parti, ad esempio Tableau, e sono quindi una piattaforma ottimale per gli analisti di dati, gli esperti aziendali e i decision maker principali.

### <a name="spark-machine-learning"></a>Machine Learning in Spark
[Esaminare un'esercitazione: stima delle temperature di compilazione mediante i dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Esaminare un'esercitazione: stima dei risultati di ispezione del cibo](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark include [MLlib](http://spark.apache.org/mllib/), una libreria di Machine Learning basata su Spark, che è possibile usare da un cluster Spark in HDInsight. Il cluster Spark in HDInsight include inoltre Anaconda, una distribuzione di Python con un'ampia gamma di pacchetti per l'apprendimento automatico. Aggiungendo il supporto incorporato per notebook Jupyter e Zeppelin si otterrà un ambiente di qualità elevata per la creazione di applicazioni di Machine Learning.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Analisi dei dati in tempo reale e streaming in Spark
[Esaminare un'esercitazione](hdinsight-apache-spark-eventhub-streaming.md)

I cluster Spark in HDInsight offrono un supporto completo per la creazione di soluzioni di analisi in tempo reale. Mentre Spark ha già i dati dei connettori tooingest da molte origini, ad esempio di socket Kafka, Flume, Twitter, ZeroMQ o TCP, Spark in HDInsight aggiunge il supporto di prima classe per l'inserimento di dati di hub di eventi di Azure. Gli hub eventi sono hello più diffuse servizio di Accodamento messaggi in Azure. La disponibilità di un supporto per Hub eventi rende i cluster Spark in HDInsight la piattaforma ideale per la compilazione della pipeline di analisi in tempo reale.

## <a name="next-steps"></a>Quali componenti sono inclusi come parte di un cluster di Spark?
Il cluster Spark in HDInsight include hello seguenti componenti che sono disponibili nei cluster hello per impostazione predefinita.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Viene fornito con Spark Core, Spark SQL, streaming API Spark, GraphX e MLlib Spark.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter Notebook](https://jupyter.org)
* [Notebook Zeppelin](http://zeppelin-project.org/)

I cluster Spark in HDInsight includono inoltre un [driver ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) per connettività tooSpark cluster HDInsight da strumenti di Business Intelligence, ad esempio Microsoft Power BI e Tableau.

## <a name="where-do-i-start"></a>Dove iniziare?
Iniziare con la creazione di un cluster Spark in HDInsight. Vedere [Guida introduttiva: creare un cluster di Spark in HDInsight ed eseguire query interattive usando Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Passaggi successivi
### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernel disponibili per notebook di Jupyter nel cluster Spark per HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
* [Problemi noti di Apache Spark in Azure HDInsight](hdinsight-apache-spark-known-issues.md).
