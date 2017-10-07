---
title: aaaWhat sono HDInsight, stack di tecnologie Hadoop hello & cluster? - Azure | Microsoft Docs
description: Un'introduzione tooHDInsight e hello Hadoop allo stack di tecnologie e i componenti, inclusi Spark, Kafka, Hive, HBase per analisi dei dati di grandi dimensioni.
keywords: "hadoop Azure, azure hadoop, introduzione di hadoop, introduzione di hadoop, allo stack di tecnologie di hadoop, introduzione toohadoop, toohadoop introduzione, che cos'è un cluster hadoop, qual è il cluster hadoop, ciò che viene utilizzato per hadoop"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Introduzione tooAzure HDInsight, hello Hadoop allo stack di tecnologie e i cluster Hadoop
 Questo articolo fornisce un'introduzione tooAzure HDInsight, una distribuzione cloud di stack di tecnologie di hello Hadoop. Illustra anche il cluster Hadoop e quando viene usato. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Che cos'è HDInsight e hello Hadoop allo stack di tecnologie? 
Azure HDInsight è una distribuzione cloud dei componenti di Hadoop hello da hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) stato framework open source originale di hello per l'elaborazione distribuita e l'analisi di grandi set di dati nei cluster di computer. 


stack di tecnologie Hadoop Hello include software correlati e le utilità, inclusi Apache Hive, HBase, Spark, Kafka e molti altri. toosee Hadoop tecnologia stack componenti disponibili in HDInsight, vedere [componenti e le versioni disponibili con HDInsight][component-versioning]. tooread ulteriori informazioni su Hadoop in HDInsight, vedere hello [pagina di funzionalità di Azure per HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Definizione di cluster Hadoop e casi d'uso
*Hadoop* è anche un tipo di cluster con:

* YARN per la pianificazione dei processi e la gestione delle risorse
* MapReduce per l'elaborazione parallela
* Hello file system distribuito Hadoop (HDFS)
  
I cluster Hadoop vengono spesso usati per l'elaborazione batch di dati archiviati. Altri tipi di cluster in HDInsight hanno funzionalità aggiuntive: Spark è particolarmente diffuso in virtù dell'elaborazione in memoria più rapida. Vedere [Tipi di cluster in HDInsight](#overview) per informazioni dettagliate.

## <a name="what-is-big-data"></a>Informazioni sui Big Data
I Big Data descrivono qualsiasi corpo di informazioni digitali di grandi dimensioni, ad esempio:

* Dati di sensori di macchine industriali
* Attività dei clienti raccolta da un sito Web
* Un newsfeed Twitter

I Big Data vengono raccolti in volumi sempre più elevati, a velocità crescenti e in una gamma crescente di formati. Può essere cronologico (significato archiviati) o in tempo reale (significato streaming dall'origine hello). 

## <a name="overview"></a>Tipi di cluster in HDInsight
HDInsight include tipi di cluster specifici e funzionalità di personalizzazione dei cluster, ad esempio l'aggiunta di componenti, utilità e linguaggi.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Tipi di cluster Spark, Kafka, Interactive Hive, HBase, personalizzati e di altro tipo
HDInsight offre i seguenti tipi di cluster hello:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: Usa [HDFS](#hdfs), [YARN](#yarn) gestione delle risorse e un semplice [MapReduce](#mapreduce) tooprocess modello di programmazione e analizzare i dati di batch in parallelo.
* **[Apache Spark](http://spark.apache.org/)**: un framework di elaborazione parallela che supporta l'elaborazione in memoria tooboost hello prestazioni di applicazioni per l'analisi di big data, nascita works per SQL, flusso di dati e machine learning. Vedere [Informazioni su Apache Spark in HDInsight](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: un database NoSQL basato su Hadoop che fornisce accesso casuale e coerenza assoluta per quantità elevate di dati non strutturati e semistrutturati. Può gestire potenzialmente milioni di righe e colonne. Vedere [Informazioni su HBase in HDInsight](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: un server che ospita e gestisce processi R paralleli e distribuiti. Fornisce gli esperti di dati statistici e i programmatori di R con tooscalable accesso su richiesta, metodi distribuiti di analitica in HDInsight. Vedere [Panoramica di R Server su HDInsight](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)**: un sistema di calcolo distribuito e in tempo reale per l'elaborazione rapida di grandi flussi di dati. Storm viene offerto come cluster gestito in HDInsight. Vedere [Analizzare i dati del sensore in tempo reale con Storm e Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Anteprima di Apache Interactive Hive (cioè lunga durata e funzionamento)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: la memorizzazione nella cache integrata per query Hive interattive e più veloci. Vedere [Usare Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)**: una piattaforma open source usata per creare applicazioni e pipeline di dati di streaming. Kafka fornisce anche funzionalità di coda di messaggi che consente toopublish e toodata flussi di sottoscrizione. Vedere [tooApache introduzione Kafka in HDInsight](hdinsight-apache-kafka-introduction.md).

È inoltre possibile configurare i cluster usando hello dei seguenti metodi:
* **[Anteprima di cluster appartenenti a un dominio](hdinsight-domain-joined-introduction.md)**: un cluster aggiunti a un dominio di Active Directory tooan in modo che sia possibile controllare l'accesso e fornire governance per i dati.
* **[Cluster personalizzati con le azioni script](hdinsight-hadoop-customize-cluster-linux.md)**: cluster con script eseguiti durante il provisioning e che possono installare componenti aggiuntivi.

### <a name="example-cluster-customization-scripts"></a>Script di personalizzazione cluster di esempio
Le azioni script sono script Bash su Linux in esecuzione durante il provisioning del cluster e che può essere utilizzato tooinstall i componenti aggiuntivi nel cluster hello. 

Hello gli script di esempio seguente vengono forniti dal team di HDInsight hello:

* **[Tonalità](hdinsight-hadoop-hue-linux.md)**: insieme di toointeract di applicazioni web con un cluster. Solamente cluster Linux
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: grafico toomodel relazioni tra persone o di operazioni di elaborazione.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: una piattaforma di ricerca su scala aziendale che consente di eseguire ricerche full-text sui dati.

Per informazioni su come sviluppare azioni script personalizzate, vedere [Sviluppo di azioni script con HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Componenti e utilità nei cluster HDInsight
Hello componenti e le utilità seguenti sono inclusi nei cluster HDInsight:

* **[Ambari](#ambari)**: provisioning, gestione, monitoraggio e utilità dei cluster.
* **[Avro](#avro)**  (libreria .NET di Microsoft per Avro): la serializzazione dei dati per l'ambiente di Microsoft .NET hello. 
* **[Hive e HCatalog](#hive)**: query simili a SQL e un livello di gestione di tabelle e archiviazione.
* **[Mahout](#mahout)**: per applicazioni Machine Learning scalabili.
* **[MapReduce](#mapreduce)**: framework legacy per l'elaborazione distribuita e la gestione delle risorse Hadoop. Vedere [YARN](#yarn).
* **[Oozie](#oozie)**: gestione dei flussi di lavoro.
* **[Phoenix](#phoenix)**: un livello di database relazionale su HBase.
* **[Pig](#pig)**: script semplice per le trasformazioni MapReduce.
* **[Sqoop](#sqoop)**: importazione ed esportazione dei dati.
* **[Tez](#tez)**: consente di toorun processi a elevato utilizzo di dati in modo efficiente su larga scala.
* **[YARN](#yarn)**: gestione delle risorse che fa parte della libreria principale di hello Hadoop.
* **[ZooKeeper](#zookeeper)**: coordinamento di processi in sistemi distribuiti.

> [!NOTE]
> Per informazioni sui componenti specifici di hello e informazioni sulla versione, vedere [Hadoop componenti e le versioni in HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari viene usato per il provisioning, la gestione e il monitoraggio di cluster Apache Hadoop. Include un insieme di strumenti di operatore intuitivo e un set affidabile di API che nascondono la complessità hello di Hadoop, semplificando l'operazione di hello dei cluster. Cluster HDInsight su Linux forniscono entrambi hello Ambari web dell'interfaccia utente e hello Ambari REST API. Le viste di Ambari nei cluster HDInsight consentono funzionalità di plug-in dell'interfaccia utente.
Vedere [Gestire i cluster HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md) e le <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">informazioni di riferimento sull'API Apache Ambari</a>.

### <a name="avro"></a>Avro (Libreria Microsoft .NET per Avro)
Libreria di Microsoft .NET per Avro Hello implementa formato di interscambio di dati binari compact hello Apache Avro per la serializzazione per l'ambiente di Microsoft .NET hello. Definisce uno schema indipendente dal linguaggio in modo che i dati serializzati in un linguaggio possano essere letti in un altro. Informazioni dettagliate sul formato hello sono reperibile in hello < destinazione = _ "vuoto" href = "http://avro.apache.org/docs/current/spec.html" > specifica di Apache Avro</a>. formato Hello di hello supporta di file Avro distributed MapReduce modello di programmazione: i file sono "divisibili", di conseguenza è possibile cercare qualsiasi punto in un file e avviare la lettura da un blocco specifico. toofind informazioni, vedere [serializzare i dati con hello libreria .NET di Microsoft per Avro](hdinsight-dotnet-avro-serialization.md). Toocome supporto cluster basati su Linux.

### <a name="hdfs"></a>HDFS
Hadoop Distributed File System (HDFS) è un file system, con YARN e MapReduce, base hello della tecnologia di Hadoop. 'S hello del file system standard per i cluster Hadoop in HDInsight. Vedere [Eseguire query sui dati da un archivio compatibile con HDFS](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Apache Hive e HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> dati warehouse software basato su Hadoop che consente di tooquery e gestire grandi set di dati in archiviazione distribuita tramite un linguaggio simile a SQL denominato HiveQL. Hive, analogamente a Pig, è un'astrazione basata su MapReduce e converte le query in una serie di processi MapReduce. Hive è più vicino sistema di gestione di database relazionale di tooa di Pig e viene usato con dati strutturati più. Per dati non strutturati, Pig è preferibile hello. Vedere [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> è un livello di gestione tabella e archiviazione per Hadoop che fornisce agli utenti una visualizzazione relazionale dei dati. In HCatalog, è possibile leggere e scrivere file in qualsiasi formato adatto per un SerDe (serializzatore-deserializzatore) Hive.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> è una libreria di algoritmi di Machine Learning eseguita in Hadoop. Utilizza i principi delle statistiche, le applicazioni di machine learning addestrare toolearn sistemi dai dati e toouse risultati toodetermine future comportamento precedente. Vedere [Generare consigli sui film usando Mahout in Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce è framework legacy software hello per Hadoop per la creazione di set di dati big toobatch processo applicazioni in parallelo. Un processo MapReduce suddivide il set di dati di grandi dimensioni e organizza i dati di hello in coppie chiave-valore per l'elaborazione. I processi MapReduce vengono eseguiti in [YARN](#yarn). Vedere <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> in hello Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> è un sistema di coordinamento dei flussi di lavoro che consente di gestire i processi Hadoop. È integrato con lo stack di Hadoop hello e supporta i processi di Hadoop per MapReduce, Pig, Hive e Sqoop. Può inoltre essere utilizzati tooschedule processi tooa specifico sistema, come programmi Java o gli script della shell. Vedere [Usare Oozie con Hadoop per definire ed eseguire un flusso di lavoro in HDInsight](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> è un livello di database relazionale su HBase. Phoenix include un driver JDBC per tooquery e gestione direttamente le tabelle SQL. Anziché utilizzare MapReduce, Phoenix converte query e altre istruzioni in chiamate API NoSQL native, consentendo in tal modo applicazioni più rapide in archivi NoSQL. Vedere [Usare Apache Phoenix e SQuirreL con i cluster HBase](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> è una piattaforma di alto livello che consente trasformazioni MapReduce complesse tooperform su grandi set di dati tramite un linguaggio di scripting semplice chiamato Pig latino. In modo che viene eseguita all'interno di Hadoop, Pig traduce script Pig latino hello. È possibile creare funzioni definite dall'utente (UDF) tooextend Pig latino. Vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> è uno strumento che consente di trasferire dati in blocco tra Hadoop e i database relazionali, ad esempio SQL o altri archivi dati strutturati, nel modo più efficace possibile. Vedere [Uso di Sqoop con HDInsight](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> è un framework di applicazione basato su Hadoop YARN che esegue grafici complessi, aciclici di elaborazione dati generali. È più flessibile e potente successore toohello MapReduce framework che consente i processi a elevato utilizzo di dati, ad esempio Hive, toorun in modo più efficiente su larga scala. Vedere ["Usare Apache Tez per ottenere prestazioni migliorate" in Uso di Hive e HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache è hello prossima generazione di MapReduce (MapReduce 2.0 o MRv2) e supporta scenari di elaborazione dei dati oltre con maggiore scalabilità e l'elaborazione in tempo reale di elaborazione batch di MapReduce. YARN offre un framework applicazioni distribuito e gestione delle risorse. I processi MapReduce vengono eseguiti in YARN. Vedere <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coordina i processi in sistemi distribuiti di grandi dimensioni usando uno spazio dei nomi gerarchico condiviso di registri di dati (znode). Znodes contenere piccole quantità di metadati necessita toocoordinate processi: lo stato, posizione, configurazione e così via. Vedere un esempio di [ZooKeeper con un cluster HBase e Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Linguaggi di programmazione in HDInsight
I cluster di HDInsight, ovvero cluster Spark, HBase, Kafka, Hadoop e altri, supportano molti linguaggi di programmazione, ma alcuni di questi non sono installati per impostazione predefinita. Per le librerie, i moduli o pacchetti non installati per impostazione predefinita, [utilizzare un componente di script azione tooinstall hello](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Supporto per i linguaggi di programmazione predefiniti
Per impostazione predefinita, i cluster HDInsight supportano:

* Java
* Python

È possibile installare linguaggi aggiuntivi usando [azioni script](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Linguaggi per macchine virtuali Java
Molti linguaggi diversi da Java è possono eseguire in Java virtual machine (JVM); Tuttavia, l'esecuzione di alcuni di questi linguaggi potrebbe richiedere i componenti aggiuntivi installati nel cluster hello.

I linguaggi basati su JVM sono supportati nei cluster HDInsight:

* Clojure
* Jython (Python per Java)
* Scala

### <a name="hadoop-specific-languages"></a>Linguaggi specifici di Hadoop
Cluster HDInsight supportano hello allo stack di tecnologie di Hadoop toohello specifica le lingue seguenti:

* Pig Latin per processi Pig
* HiveQL per processi Hive e SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard e HDInsight Premium
HDInsight fornisce offerte cloud per i Big Data in due categorie, Standard e Premium. HDInsight Standard fornisce un cluster su larga scala che è possibile utilizzare toorun i carichi di lavoro di big data. HDInsight Premium si basa sulle funzionalità del piano Standard e offre funzionalità di analisi e sicurezza avanzate per un cluster HDInsight. Per altre informazioni, vedere [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft business intelligence e HDInsight
Strumenti familiari business intelligence (BI) recupero, analizzano e integrati con HDInsight tramite una hello componente aggiuntivo Power Query di dati del report o il Driver ODBC di Hive Microsoft hello:

* [Connettere Excel tooHadoop con Power Query](hdinsight-connect-excel-power-query.md): informazioni su come tooconnect Excel toohello account di archiviazione di Azure che archivia hello dati dal cluster HDInsight tramite Microsoft Power Query per Excel. Workstation Windows necessaria. 
* [Connettere Excel tooHadoop con il Driver ODBC di Hive Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md): informazioni su come dati tooimport di HDInsight con hello Hive Driver ODBC per Microsoft. Workstation Windows necessaria. 
* [Microsoft Cloud Platform](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): informazioni su Power BI per Office 365, scaricare una versione di valutazione di SQL Server hello e configurare SharePoint Server 2013 e SQL Server Business Intelligence.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Passaggi successivi

* [Introduzione all'uso di Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): esercitazione introduttiva per il provisioning di cluster Hadoop di HDInsight e l'esecuzione di semplici query Hive.
* [Introduzione: creare cluster Apache Spark in HDInsight Linux ed eseguire query interattive usando Spark SQL](hdinsight-apache-spark-jupyter-spark-sql.md): esercitazione introduttiva per la creazione di un cluster Spark e l'esecuzione di query interattive Spark SQL.
* [Introduzione all'uso di R Server su HDInsight](hdinsight-hadoop-r-server-get-started.md): introduzione all'uso di R Server in HDInsight Premium.
* [Eseguire il provisioning di cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informazioni su come hello di tooprovision un HDInsight Hadoop cluster tramite il portale di Azure, CLI di Azure o Azure PowerShell.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/