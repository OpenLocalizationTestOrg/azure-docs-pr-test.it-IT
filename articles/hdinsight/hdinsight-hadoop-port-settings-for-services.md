---
title: utilizzato dai servizi di Hadoop in HDInsight - Azure aaaPorts | Documenti Microsoft
description: Un elenco di porte usate dai servizi Hadoop in esecuzione su HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Porte usate dai servizi Hadoop su HDInsight

Questo documento fornisce un elenco delle porte hello utilizzate da servizi di Hadoop in esecuzione nel cluster HDInsight basati su Linux. Fornisce inoltre informazioni sulle porte utilizzate tooconnect toohello cluster con SSH.

## <a name="public-ports-vs-non-public-ports"></a>Porte pubbliche e porte non pubbliche

Hello di HDInsight basati su Linux cluster esporre solo tre porte pubblicamente su internet. 22 e 23, 443. Queste porte sono cluster hello di accesso utilizzato toosecurely tramite SSH e dei servizi esposti tramite il protocollo HTTPS protetto di hello.

Internamente, HDInsight viene implementata da più macchine virtuali di Azure (nodi hello all'interno di cluster hello) in esecuzione in una rete virtuale di Azure. All'interno della rete virtuale di hello, consente di accedere non esposte tramite hello porte internet. Ad esempio, se ci si connette tooone dei nodi head di hello tramite SSH, dal nodo head hello è possibile quindi direttamente ai servizi in esecuzione nei nodi del cluster hello.

> [!IMPORTANT]
> Se non si specifica una rete virtuale di Azure come opzione di configurazione per HDInsight, se ne crea automaticamente una. Tuttavia, è possibile collegare rete virtuale di toothis altri computer (ad esempio altre macchine virtuali di Azure o il computer di sviluppo client).


rete virtuale toohello computer aggiuntivi toojoin, è necessario creare prima rete virtuale hello e specificare quindi quando si crea il cluster HDInsight. Per altre informazioni, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Porte pubbliche

Hello tutti i nodi in un cluster HDInsight si trovano in una rete virtuale di Azure e non sono direttamente accessibili da hello internet. Un gateway pubblico fornisce toohello accesso internet seguenti porte, che sono comuni a tutti i tipi di cluster HDInsight.

| Service | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Si connette toosshd client nel nodo head primario hello. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Si connette toosshd client nel nodo edge hello. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Si connette toosshd client nel nodo head secondario hello. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Interfaccia utente Web Ambari Vedere [gestire HDInsight utilizzando hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |API REST Ambari Vedere [gestire HDInsight con Ambari REST API di hello](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |API REST HCatalog Vedere gli articoli sull'[uso di Hive con Curl](hdinsight-hadoop-use-pig-curl.md), l'[uso di Pig con Curl](hdinsight-hadoop-use-pig-curl.md) e l'[uso di MapReduce con Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |Si connette tooHive tramite ODBC. Vedere [tooHDInsight connessione Excel con il driver ODBC Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Si connette utilizzando JDBC tooHive. Vedere [connettersi tooHive in HDInsight mediante hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md) |

sono disponibili per i tipi di cluster specifico Hello seguenti:

| Service | Port | Protocol | Tipo di cluster | Descrizione |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |API REST HBase Vedere [Introduzione all'uso di HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |API REST Spark Vedere [Inviare processi Spark in modalità remota con Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Interfaccia utente Web di Storm Vedere [Distribuire e gestire topologie Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Autenticazione

Tutti i servizi esposti pubblicamente su internet devono essere autenticate hello:

| Porta | Credenziali |
| --- | --- |
| 22 o 23 |credenziali utente SSH Hello specificate durante la creazione del cluster |
| 443 |nome di account di accesso Hello (impostazione predefinita: amministratore) e la password che sono stati impostati durante la creazione del cluster |

## <a name="non-public-ports"></a>Porte non pubbliche

> [!NOTE]
> Alcuni servizi sono disponibili solo su tipi di cluster specifici. Ad esempio, HBase è disponibile solo su tipi di cluster HBase.

> [!IMPORTANT]
> Alcuni servizi vengono eseguiti in un solo nodo head alla volta. Se si tenta di tooconnect toohello servizio nel nodo head primario hello e riceve un errore 404, provare a con nodo head secondario hello.

### <a name="ambari"></a>Ambari

| Service | Nodi | Porta | Percorso URL | Protocol | 
| --- | --- | --- | --- | --- |
| Interfaccia utente Web Ambari | Nodi head | 8080 | / | HTTP |
| API REST Ambari | Nodi head | 8080 | /api/v1 | HTTP |

Esempi:

* API REST Ambari: `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Porte HDFS

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| Interfaccia utente Web NameNode |Nodi head |30070 |HTTPS |Lo stato tooview dell'interfaccia utente Web |
| Servizio metadati NameNode |Nodi head |8020 |IPC |Metadati del file system |
| DataNode |Tutti i nodi di lavoro |30075 |HTTPS |Lo stato tooview dell'interfaccia utente Web, registri e così via. |
| DataNode |Tutti i nodi di lavoro |30010 |&nbsp; |Trasferimento dati |
| DataNode |Tutti i nodi di lavoro |30020 |IPC |Operazioni sui metadati |
| NameNode secondario |Nodi head |50090 |HTTP |Checkpoint per i metadati NameNode |

### <a name="yarn-ports"></a>Porte YARN

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| Interfaccia utente Web di Resource Manager |Nodi head |8088 |HTTP |Interfaccia utente Web per Resource Manager |
| Interfaccia utente Web di Resource Manager |Nodi head |8090 |HTTPS |Interfaccia utente Web per Resource Manager |
| Interfaccia di amministrazione di Resource Manager |Nodi head |8141 |IPC |Per gli invii delle applicazioni (Hive, server Hive, Pig e così via) |
| Utilità di pianificazione di Resource Manager |Nodi head |8030 |HTTP |Interfaccia di amministrazione |
| Interfaccia dell'applicazione Resource Manager |Nodi head |8050 |HTTP |Indirizzo dell'interfaccia di gestione di applicazioni hello |
| NodeManager |Tutti i nodi di lavoro |30050 |&nbsp; |indirizzo Hello del gestore del contenitore di hello |
| Interfaccia utente Web di NodeManager |Tutti i nodi di lavoro |30060 |HTTP |Interfaccia di Resource Manager |
| Indirizzo di Timeline |Nodi head |10200 |RPC |Hello sequenza temporale del servizio RPC. |
| Interfaccia utente Web di Timeline |Nodi head |8181 |HTTP |interfaccia utente web di servizio della sequenza temporale Hello |

### <a name="hive-ports"></a>Porte Hive

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| HiveServer2 |Nodi head |10001 |Thrift |Servizio per la connessione tooHive (Thrift/JDBC) |
| Metastore Hive |Nodi head |9083 |Thrift |Servizio per la connessione tooHive metadati (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Porte WebHCat

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| Server WebHCat |Nodi head |30111 |HTTP |API Web su HCatalog e su altri servizi Hadoop |

### <a name="mapreduce-ports"></a>Porte MapReduce

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| JobHistory |Nodi head |19888 |HTTP |Interfaccia utente Web di MapReduce JobHistory |
| JobHistory |Nodi head |10020 |&nbsp; |Server di MapReduce JobHistory |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |I trasferimenti intermedia mappa genera toorequesting riduttori |

### <a name="oozie"></a>Oozie

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| Server di Oozie |Nodi head |11000 |HTTP |URL per il servizio Oozie |
| Server di Oozie |Nodi head |11001 |HTTP |Porta per l'amministrazione di Oozie |

### <a name="ambari-metrics"></a>Metriche di Ambari

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| TimeLine (cronologia delle applicazioni) |Nodi head |6188 |HTTP |interfaccia utente web di servizio della sequenza temporale Hello |
| TimeLine (cronologia delle applicazioni) |Nodi head |30200 |RPC |interfaccia utente web di servizio della sequenza temporale Hello |

### <a name="hbase-ports"></a>Porte HBase

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| HMaster |Nodi head |16000 |&nbsp; |&nbsp; |
| Interfaccia utente Web informativa di HMaster |Nodi head |16010 |HTTP |porta Hello per interfaccia utente web Master HBase di hello |
| Server dell'area |Tutti i nodi di lavoro |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |porta Hello che i client utilizzino tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Porte Kafka

| Service | Nodi | Port | Protocol | Descrizione |
| --- | --- | --- | --- | --- |
| Gestore |Nodi di lavoro |9092 |[Protocollo di trasmissione Kafka](http://kafka.apache.org/protocol.html) |Usato per la comunicazione di client |
| &nbsp; |Nodi Zookeeper |2181 |&nbsp; |porta Hello che i client utilizzino tooconnect tooZookeeper |

### <a name="spark-ports"></a>Porte Spark

| Service | Nodi | Port | Protocol | Percorso URL | Descrizione |
| --- | --- | --- | --- | --- | --- |
| Server Spark Thrift |Nodi head |10002 |Thrift | &nbsp; | Servizio per la connessione tooSpark SQL (Thrift/JDBC) |
| Server Livy | Nodi head | 8998 | HTTP | /batches | Servizio per l'esecuzione di istruzioni, processi e applicazioni |

Esempi:

* Livy: `curl "http://10.0.0.11:8998/batches"`. In questo esempio, `10.0.0.11` è l'indirizzo IP hello del nodo head hello che ospita il servizio di inserire il hello.
