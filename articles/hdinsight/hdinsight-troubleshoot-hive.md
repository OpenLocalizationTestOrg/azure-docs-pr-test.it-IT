---
title: aaaTroubleshoot Hive tramite Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Hive e Azure HDInsight.
keywords: Azure HDInsight, Hive, domande frequenti, guida alla risoluzione dei problemi, domande comuni
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Risolvere i problemi di Hive tramite Azure HDInsight

Informazioni sulle domande hello e le relative soluzioni quando si lavora con Apache Hive payload in Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Come esportare un metastore Hive e importarlo in un altro cluster


### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Connettere il cluster di HDInsight toohello tramite un client Secure Shell (SSH). Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).

2. Eseguire i comando seguente nel cluster HDInsight hello da cui si desidera tooexport hello metastore hello:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Questo comando genera un file denominato alltables.sql.

3. Copiare hello file alltables.sql toohello nuovo cluster HDInsight e quindi eseguire hello comando seguente:

  ```apache
  hive -f alltables.sql
  ```

codice Hello nei passaggi di risoluzione hello si presuppone che i dati vengono tracciati nel nuovo cluster hello hello stesso come percorsi di dati hello vecchio cluster hello. Se i percorsi dati hello sono diversi, è possibile modificare manualmente hello generato alltables.sql file tooreflect tutte le modifiche.

### <a name="additional-reading"></a>Informazioni aggiuntive

- [Connettere il cluster di HDInsight tooan tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Come individuare i log di Hive in un cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Connettere il cluster di HDInsight toohello utilizzando SSH. Per altre informazioni, vedere **Informazioni aggiuntive**.

2. i registri del client tooview Hive, usare hello comando seguente:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. i log metastore Hive tooview, utilizzare hello comando seguente:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver log, utilizzare hello comando seguente:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Informazioni aggiuntive

- [Connettere il cluster di HDInsight tooan tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Modalità avvio hello shell Hive con configurazioni specifiche in un cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Specificare una coppia chiave-valore di configurazione quando si avvia hello Hive shell. Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist tutte le configurazioni valide nel Hive shell, utilizzare hello seguente comando:

  ```apache
  hive> set;
  ```

  Ad esempio, utilizzare hello seguente toostart Hive shell dei comandi con la registrazione di debug abilitata nella console di hello:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Informazioni aggiuntive

- [Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Proprietà di configurazione di Hive)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Come analizzare i dati di un grafo aciclico diretto di Tez in un percorso critico del cluster


### <a name="resolution-steps"></a>Procedura per la risoluzione
 
1. tooanalyze un Tez Apache indirizzare grafico aciclico diretto (DAG) in un grafico critici del cluster, connettere il cluster di HDInsight toohello utilizzando SSH. Per altre informazioni, vedere [Informazioni aggiuntive](#additional-reading-end).

2. Al prompt dei comandi eseguire hello comando seguente:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist altri analizzatori che possono essere utilizzati tooanalyze Tez DAG, utilizzare hello comando seguente:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  È necessario fornire un programma di esempio come primo argomento hello.

  I nomi di programma validi includono:
    - **ContainerReuseAnalyzer**: stampare i dettagli di riutilizzo dei contenitori in un grafo aciclico diretto
    - **CriticalPath**: percorso critico hello di ricerca di un DAG
    - **LocalityAnalyzer**: stampare i dettagli della località in un grafo aciclico diretto
    - **ShuffleTimeAnalyzer**: analizzare i dettagli di tempo casuale di hello in un DAG
    - **SkewAnalyzer**: analizzare i dettagli di inclinazione hello in un DAG
    - **SlowNodeAnalyzer**: stampare i dettagli del nodo in un grafo aciclico diretto
    - **SlowTaskIdentifier**: stampare i dettagli sulle attività lente in un grafo aciclico diretto
    - **SlowestVertexAnalyzer**: stampare i dettagli relativi ai vertici più lenti in un grafo aciclico diretto
    - **SpillAnalyzer**: stampare i dettagli relativi all'espansione in un grafo aciclico diretto
    - **TaskConcurrencyAnalyzer**: stampare i dettagli di concorrenza hello attività in un DAG
    - **VertexLevelCriticalPathAnalyzer**: percorso critico hello di ricerca a livello di vertici in un DAG


### <a name="additional-reading"></a>Informazioni aggiuntive

- [Connettere il cluster di HDInsight tooan tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Come scaricare i dati DAG di Tez da un cluster


#### <a name="resolution-steps"></a>Procedura per la risoluzione

Non esistono due modi toocollect hello DAG Tez dati:

- Dalla riga di comando hello:
 
    Connettere il cluster di HDInsight toohello utilizzando SSH. Al prompt dei comandi di hello, eseguire hello comando seguente:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Utilizzare hello Ambari Tez Vista:
   
  1. Passare tooAmbari. 
  2. Visualizzazione di passare tooTez (sotto l'icona di riquadri hello nell'angolo superiore destro hello). 
  3. Selezionare hello desiderato tooview DAG.
  4. Selezionare **Download data** (Scarica dati).

### <a name="additional-reading-end"></a>Informazioni aggiuntive

[Connettere il cluster di HDInsight tooan tramite SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






