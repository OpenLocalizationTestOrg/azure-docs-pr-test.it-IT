---
title: aaaTroubleshoot Storm tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Storm con Azure HDInsight.
keywords: Azure HDInsight, Storm, domande frequenti, guida alla risoluzione dei problemi, problemi comuni
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Risolvere i problemi di Storm usando Azure HDInsight

Informazioni sui problemi principali hello e le relative soluzioni per l'utilizzo di payload Apache Storm in Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>La modalità di accesso di hello Storm UI in un cluster
Sono disponibili due opzioni per l'accesso a hello Storm UI da un browser:

### <a name="ambari-ui"></a>Tramite l'interfaccia utente di Ambari
1. Passare toohello Ambari dashboard.
2. Nell'elenco di hello dei servizi, selezionare **Storm**.
3. In hello **collegamenti rapidi** dal menu **dell'interfaccia utente Storm**.

### <a name="direct-link"></a>Collegamento diretto
È possibile accedere hello Storm UI in hello URL seguente:

https://\<nome DNS del cluster\>/stormui

Esempio:

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Come è possibile trasferire informazioni di checkpoint beccuccio hub eventi Storm da una topologia tooanother

Quando si sviluppano le topologie di lettura dagli hub di eventi di Azure tramite hello JAR beccuccio hub eventi di HDInsight Storm, è necessario distribuire una topologia con hello stesso nome in un nuovo cluster. Tuttavia, è necessario conservare i dati di checkpoint hello che è stato eseguito il commit tooApache ZooKeeper nel vecchio cluster hello.

### <a name="where-checkpoint-data-is-stored"></a>Dove vengono archiviati i dati dei checkpoint
I dati di checkpoint per l'offset sono archiviati da hello evento hub beccuccio in ZooKeeper in due percorsi principali:
- I checkpoint dello spout non transazionali vengono archiviati in /eventhubspout.
- I dati dei checkpoint dello spout transazionali vengono archiviati in /transactional.

### <a name="how-toorestore"></a>Come toorestore
gli script hello tooget e raccolte che si utilizzano dati di tooexport fuori ZooKeeper e quindi importare hello tooZooKeeper indietro di dati con un nuovo nome, vedere [esempi HDInsight Storm](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

cartella lib Hello è file JAR che contengono l'implementazione di hello per l'operazione di esportazione/importazione hello. cartella bash Hello è uno script di esempio che illustra come dati tooexport hello server ZooKeeper nel vecchio cluster hello e quindi importarlo server ZooKeeper toohello indietro nel nuovo cluster hello.

Eseguire hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) generare uno script da hello ZooKeeper nodi tooexport e quindi importare i dati. Aggiornamento hello script toohello Hortonworks Data Platform (HDP) versione corretta. A breve questi script saranno generici in HDInsight. Script generico può eseguire da qualsiasi nodo nel cluster hello senza modifiche dall'utente hello.)

comando Esporta Hello scrive hello percorso dei metadati tooan Apache Hadoop Distributed File System (HDFS) (in un archivio di archiviazione Blob di Azure o archivio Azure Data Lake) in una posizione che è impostato.

### <a name="examples"></a>esempi

#### <a name="export-offset-metadata"></a>Esportare i metadati dell'offset
1. Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.
2. Hello esecuzione comando che segue (dopo l'aggiornamento hello stringa di versione HDP) tooexport ZooKeeper offset dati toohello /stormmetadta/zkdata HDFS percorso:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importare i metadati dell'offset
1. Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.
2. Esecuzione hello il seguente comando (dopo l'aggiornamento di stringa di versione di hello HDP) tooimport ZooKeeper offset dati hello HDFS percorso stormmetadata/zkdata toohello ZooKeeper server nel cluster di destinazione hello:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Eliminare i metadati di offset, in modo che topologie è possono avviare l'elaborazione dei dati dall'inizio hello o da un timestamp sceglie tale utente hello
1. Usare SSH toogo toohello ZooKeeper cluster nel cluster hello dal quale checkpoint hello offset deve toobe esportato.
2. Esecuzione hello il seguente comando (dopo l'aggiornamento di stringa di versione di hello HDP) toodelete tutti ZooKeeper offset dati in cluster corrente hello:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Individuare i binari Storm in un cluster
File binari di Storm per stack HDP corrente hello sono /usr/hdp/current/storm-client. percorso Hello è hello stesso sia per i nodi head e per i nodi di lavoro.
 
Potrebbero essere presenti più file binari per versioni HDP specifiche in /usr/hdp (ad esempio, /usr/hdp/2.5.0.1233/storm). cartella /usr/hdp/current/storm-client hello è symlinked toohello versione più recente che è in esecuzione nel cluster hello.

Per ulteriori informazioni, vedere [cluster HDInsight tooan di connettersi tramite SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Come è possibile determinare la topologia di distribuzione hello di un cluster Storm
Identificare prima tutti i componenti installati in HDInsight Storm. Un cluster Storm è costituito da quattro categorie di nodi:

* Nodi gateway
* Nodi head
* Nodi ZooKeeper
* Nodi di lavoro
 
### <a name="gateway-nodes"></a>Nodi gateway
Un nodo di gateway è un gateway e un servizio di proxy inverso che consente di servizio di gestione di accesso pubblico tooan active Ambari. Gestisce anche l'algoritmo di elezione di Ambari.
 
### <a name="head-nodes"></a>Nodi head
I nodi head Storm eseguire hello seguenti servizi:
* Nimbus
* Server Ambari
* Server delle metriche Ambari
* Agente di raccolta delle metriche Ambari
 
### <a name="zookeeper-nodes"></a>Nodi ZooKeeper
HDInsight viene offerto con un quorum ZooKeeper di tre nodi. dimensione di Hello quorum è fissa e non può essere riconfigurati.
 
Servizi di Storm cluster hello sono quorum di ZooKeeper hello utilizzare tooautomatically configurato.
 
### <a name="worker-nodes"></a>Nodi di lavoro
Nodi di lavoro Storm eseguire hello seguenti servizi:
* Supervisore
* Java Virtual Machine (JVM) di lavoro, per le topologie in esecuzione
* Agente Ambari
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Come individuare i file binari dello spout dell'hub eventi di Storm per lo sviluppo
 
Per ulteriori informazioni sull'utilizzo dei file JAR di Storm evento hub beccuccio con la topologia, vedere hello seguenti risorse.
 
### <a name="java-based-topology"></a>Topologia basata su Java
[Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Topologia basata su C# (Mono in cluster HDInsight 3.4+ Linux Storm)
[Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>File binari dello spout dell'hub eventi di Storm più recenti per cluster HDInsight 3.5+ Linux Storm
toolearn come toouse hello più recente Storm evento hub beccuccio che funziona con HDInsight 3.5 + cluster Linux Storm, vedere hello mvn-repo [file readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Esempi di codice sorgente
Vedere [esempi](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) come tooread e scrivere da Hub di eventi di Azure usando una topologia di Apache Storm (scritta in linguaggio) in un cluster HDInsight di Azure.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Individuare i file di configurazione Storm Log4J nei cluster
 
file di configurazione tooidentify Apache Log4J per i servizi di Storm.
 
### <a name="on-head-nodes"></a>Nei nodi head
configurazione di Hello Nimbus Log4J viene letta in /usr. hdp/\<versione HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Nei nodi di lavoro
configurazione del Supervisore Log4J Hello viene letto in /usr. hdp/\<versione HDP\>/storm/log4j2/cluster.xml.
 
file di configurazione di lavoro Log4J Hello viene letto in /usr. hdp/\<versione HDP\>/storm/log4j2/worker.xml.
 
Esempi: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

