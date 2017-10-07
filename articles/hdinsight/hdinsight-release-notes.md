---
title: aaaRelease note per i componenti di Hadoop in HDInsight di Azure | Documenti Microsoft
description: "Note sulla versione più recente e le versioni di componenti Hadoop per Azure HDInsight. Ottenere suggerimenti e dettagli sullo sviluppo per Spark, R Server, Hive e altro."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.assetid: a363e5f6-dd75-476a-87fa-46beb480c1fe
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: nitinme
ms.openlocfilehash: ab08a74380fe0bbd7430c1096dca7eb177c11fe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-hadoop-components-on-azure-hdinsight"></a>Note sulla versione di componenti Hadoop in Azure HDInsight

Questo articolo fornisce informazioni su hello **più recente** gli aggiornamenti di versione di Azure HDInsight. Per informazioni sulle versioni precedenti, vedere [Archivio delle note di versione di HDInsight](hdinsight-release-notes-archive.md).

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere l'[articolo sul controllo delle versioni di HDInsight](hdinsight-component-versioning.md).


## <a name="notes-for-08012017-release-of-hdinsight"></a>Note per la versione di HDInsight rilasciata in data 01/08/2017

| Titolo | Descrizione | Area interessata  | Tipo di cluster  | 
| --- | --- | --- | --- | --- |
| Versione di Microsoft R Server 9.1 in HDInsight |HDInsight supporta ora il provisioning dei cluster R Server 9.1 in HDInsight. Per altre informazioni sulla versione di Microsoft R Server 9.1, vedere [questo blog](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/). |Service |R Server |
| HDInsight 3.6 include ora le versioni più recenti dello stack di Hadoop hello|<ul><li>Per un elenco dettagliato delle versioni aggiornate, vedere [Componenti di Hadoop disponibili con diverse versioni di HDInsight](hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions).</li><li>Per un elenco di bug risolti nelle versioni più recenti di hello dello stack di hello Hadoop, vedere [informazioni Patch Apache](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/patch_parent.html).</li><li>Per un elenco delle modifiche importanti in HDP 2.6.1 (ora disponibile in HDInsight 3.6), vedere [https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html).</li><li>Per un elenco dei problemi noti di HDP 2.6.1, vedere la pagina relativa ai [problemi noti](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/known_issues.html).</li></ul> |Service |Tutti |N/D |
| Aggiorna i cluster tooInteractive Hive (anteprima) |<ul><li><b>Miglioramento della funzionalità.</b> Implementazione di metastore memorizzati nella cache che riduce il carico hello in hello back-end SQL memorizzando nella cache dei metadati hello e migliora le prestazioni per tutte le operazioni dei metadati.  Questo miglioramento è ora un'impostazione predefinita in tutti i cluster Interactive Hive. Per altre informazioni, vedere [https://issues.apache.org/jira/browse/HIVE-16520](https://issues.apache.org/jira/browse/HIVE-16520).</li><li><b>Miglioramento della funzionalità.</b> Il caricamento della partizione dinamica è ottimizzato. Per altre informazioni, vedere [https://issues.apache.org/jira/browse/HIVE-14204] (https://issues.apache.org/jira/browse/HIVE-14204).</li><li><b>Miglioramento della funzionalità.</b> Ottimizzazioni di configurazione per HDInsight su Linux.</li><li><b>Correzione di bug.</b> `CredentialProviderFactory$getProviders` non è thread-safe. Questo problema ora è stato corretto. Per altre informazioni, vedere [https://issues.apache.org/jira/browse/HADOOP-14195](https://issues.apache.org/jira/browse/HADOOP-14195).</li><li><b>Correzione di bug.</b> L'utilizzo elevato della CPU con API `liststatus` del driver WASB genera prestazioni ATS non valide. Questo problema ora è stato corretto. Per altre informazioni, vedere [https://github.com/Azure/azure-storage-java/pull/154](https://github.com/Azure/azure-storage-java/pull/154).</li></ul> |Service |Interactive Hive (anteprima) |
| Aggiornamenti tooHadoop cluster |L'affidabilità dell'operazione del processo Templeton è migliorata. Per altre informazioni, vedere [https://issues.apache.org/jira/browse/HIVE-15947](https://issues.apache.org/jira/browse/HIVE-15947). |Service |Hadoop |
| Aggiornamenti di YARN | HDInsight ora crea un database Ambari da 250 GB (senza l'aumento dei costi), che comporta una migliore esperienza per i clienti. Questa modifica dovrebbe impedire il riempimento di ATS e migliorare le prestazioni. |Service |Tutti |
| Aggiornamenti di Spark | Versione di Spark 2.1.1. Per altre informazioni, vedere la pagina relativa alle [note sulla versione di Spark 2.1.1](https://spark.apache.org/releases/spark-release-2-1-1.html). | Service | Spark |

  



## <a name="04062017---general-availability-of-hdinsight-36"></a>04/06/2017 - Disponibilità generale di HDInsight 3.6

* Con questa versione, Azure HDInsight aggiunge la versione 3.6, basata su HDP 2.6. Le note sulla versione di HDP 2.6 sono disponibili [qui](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html) e altre informazioni sulle versioni di HDInsight sono disponibili [qui](hdinsight-component-versioning.md). 3.6 HDInsight è disponibile per hello carichi di lavoro seguente:

    * Hadoop v2.7.3
    * HBase v1.1.2
    * Storm v1.1.0
    * Spark v2.1.0
    * Interactive Hive v2.1.0

* **Supporto per Hive View 2.0**. Questo dovrebbe migliorare l'esperienza utente hello Hive interattivo. Per altre informazioni, vedere la [documentazione di Hortonworks](http://docs.hortonworks.com/HDPDocuments/Ambari-2.5.0.3/bk_ambari-views/content/ch_using_hive_view.html).

* **Miglioramenti delle prestazioni con Hive LLAP**. Per altre informazioni, vedere la [documentazione di Hortonworks](https://hortonworks.com/blog/top-5-performance-boosters-with-apache-hive-llap/).

* **Nuove funzionalità di Hive**. Vedere la [documentazione di Hortonworks](https://hortonworks.com/apache/hive/#section_4).

* **Hive CLI deprecazione**: Hive CLI è deprecato e i clienti sono invitati toouse Beeline invece. Per altre informazioni, vedere la [documentazione Apache](https://cwiki.apache.org/confluence/display/Hive/Replacing+the+Implementation+of+Hive+CLI+Using+Beeline). Per istruzioni su come toouse Beeline con HDInsight, vedere [cluster utilizzare Beeline con HDInsight Hadoop](hdinsight-hadoop-use-hive-beeline.md).

* **Nuove funzionalità di Apache Phoenix e HBase**.
    * Supporto di quota di archiviazione: comunemente usato negli ambienti multi-tenant, consente uno spazio di archiviazione limitato a livello di tabella e di spazio dei nomi.
    * Miglioramenti di indicizzazione Phoenix: creazione dell'indice incrementale e ricompilazione o ripresa dell'indicizzazione da errori precedenti.
    * Strumento di integrità dei dati di Phoenix: supporta la convalida di schema, indice e altri metadati.


* **Problema con HBase**: durante l'esecuzione di un blocco CSV, caricare il processo MapReduce, hello sintassi potrebbe verificarsi un errore.

        HADOOP_CLASSPATH=$(hbase mapredcp):/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv

    Utilizzare invece la seguente sintassi hello:

        HADOOP_CLASSPATH=/path/to/hbase-protocol.jar:/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv


## <a name="02282017---release-of-spark-21-on-hdinsight-36-preview"></a>02/28/2017 - Versione di Spark 2.1 in HDInsight 3.6 (Anteprima)
* [Spark 2.1](http://spark.apache.org/releases/spark-release-2-1-0.html) risolve i molti problemi relativi a usabilità e stabilità riscontrati con le versioni precedenti. Offre anche nuove funzionalità in tutti i carichi di lavoro di Spark, ad esempio Spark Core, SQL, ML e Streaming.
* Streaming strutturati presentano una migliore scalabilità con il supporto per soglie di tempo dell'evento e con il connettore Kafka 0.10.
* Il partizionamento Spark SQL viene ora gestito usando il nuovo meccanismo di gestione di partizioni scalabili. Visualizzare ulteriori dettagli [qui](http://spark.apache.org/releases/spark-release-2-1-0.html) sulla tooupgrade.
* Spark 2.1 in Azure HDInsight 3.6 Preview attualmente non supporta la connettività degli strumenti di Business Intelligence tramite il driver ODBC.
* L'accesso di Azure Data Lake Store dai cluster Spark 2.1 non è supportato in questa versione di anteprima.


## <a name="11182016---release-of-spark-201-on-hdinsight-35"></a>11/18/2016 - Versione di Spark 2.0.1 in HDInsight 3.5
Spark 2.0.1 è ora disponibile in cluster Spark (HDInsight versione 3.5).

## <a name="11162016---release-of-r-server-90-on-hdinsight-35-spark-20"></a>11/16/2016 - Versione di R Server 9.0 in HDInsight 3.5 (Spark 2.0)
*   R Server cluster includono ora il possibilità di hello per le due versioni: R Server 9.0 HDI 3.5 (Spark 2.0) e R Server 8.0 in HDI 3.4 (Spark 1.6).
*   R Server 9.0 HDI 3.5 (2.0 Spark) si basa su R 3.3.2 e include nuovi ScaleR funzioni denominate RxHiveData e RxParquetData per il caricamento dei dati dall'Hive dell'origine dati e Parquet direttamente tooSpark frame di dati per l'analisi da ScaleR. Per ulteriori informazioni, vedere hello inline la Guida su queste funzioni in R tramite l'utilizzo di hello **? RxHiveData** e **? RxParquetData** comandi.
*   Edizione community RStudio Server è ora installato per impostazione predefinita (con un'opzione opt-out) nel Pannello di configurazione del Cluster hello come parte di hello provisioning flusso.

## <a name="11092016---release-of-spark-20-on-hdinsight"></a>11/09/2016 - Versione di Spark 2.0 in HDInsight
* I cluster Spark 2.0 in HDInsight 3.5 supportano ora servizi Livy e Jupyter.

## <a name="10262016---release-of-r-server-on-hdinsight"></a>10/26/2016 - Versione di R Server in HDInsight
* Hello URI per l'accesso edge nodo è stato modificato troppo**clustername**-ed-ssh.azurehdinsight.net
* Il provisioning del cluster R Server in HDInsight è stato semplificato.
* R Server in HDInsight ora è disponibile come normale tipo di cluster "R Server" in HDInsight e non viene più installato come applicazione HDInsight separata. nodo edge Hello e file binari del Server di R vengono ora eseguito il provisioning come parte della distribuzione di cluster di Server R hello. In questo modo il provisioning è più veloce e affidabile. Il modello di determinazione prezzi per R Server viene aggiornato di conseguenza.
* Il prezzo del tipo di cluster R Server ora corrisponde al prezzo del piano Standard più la maggiorazione per R Server. Il piano Premium è riservato alle funzionalità Premium disponibili in tipi di cluster diversi e non viene usato per il tipo di cluster R Server. Questa modifica non influisce sul prezzo effettivo del Server di R. modifica solo come addebiti hello vengono presentati in distinta hello. Tutti i cluster di Server R esistenti continuano toowork e modelli di gestione risorse per proseguire toofunction notare deprecazione. **È consigliabile tuttavia tooupdate il modello di gestione risorse nuove distribuzioni con script toouse.**






