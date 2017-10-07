---
title: cluster aaaTroubleshoot problemi con Apache Spark in HDInsight di Azure | Documenti Microsoft
description: Informazioni sui problemi correlati tooApache i cluster Spark in Azure HDInsight e come toowork intorno quelli.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Problemi noti del cluster Apache Spark in HDInsight

Questo documento tiene traccia di hello tutti i problemi per l'anteprima pubblica di HDInsight Spark hello noti.  

## <a name="livy-leaks-interactive-session"></a>Livy perde la sessione interattiva
Quando inserire il riavvio (Ambari o a causa il riavvio del computer virtuale tooheadnode 0) con una sessione interattiva ancora attiva, è possibile che una sessione interattiva andrà perso. Per questo motivo, può essere di nuovo i processi bloccato nello stato accettato hello e non può essere avviato.

**Soluzione:**

Utilizzare hello problema hello tooworkaround di stored procedure seguente:

1. Eseguire SSH nel nodo head. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Esecuzione hello seguente un'applicazione hello toofind comando ID dei processi interattivi hello avviato tramite inserire il. 
   
        yarn application –list
   
    Hello nomi di processo predefiniti saranno inserire il se hello processi sono stati avviati con una sessione interattiva di inserire il senza nomi esplicita specificata, per hello sessione avviata dal server Jupyter notebook inserire il nome del processo hello inizierà con remotesparkmagics_ *. 
3. Comando che segue hello esecuzione tookill tali processi. 
   
        yarn application –kill <Application ID>

Verranno avviati nuovi processi. 

## <a name="spark-history-server-not-started"></a>Il server cronologia Spark non viene avviato
Il server cronologia Spark non viene avviato automaticamente dopo la creazione di un cluster.  

**Soluzione:** 

Avviare manualmente il server di cronologia hello da Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problema di autorizzazioni nella directory log Spark
Quando hdiuser invia un processo con spark-submit, si verifica un errore java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (autorizzazione negata) e hello log driver non è stato scritto. 

**Soluzione:**

1. Aggiungere il gruppo hdiuser toohello Hadoop. 
2. Indicare 777 autorizzazioni in /var/log/spark dopo la creazione del cluster. 
3. Percorso di log spark hello utilizzando Ambari toobe una directory con 777 autorizzazioni di aggiornamento.  
4. Eseguire spark-submit come sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Il connettore Spark-Phoenix non è supportato

Attualmente, il connettore di Spark Phoenix hello non è supportato con un cluster HDInsight Spark.

**Soluzione:**

È invece necessario utilizzare connettore Spark HBase hello. Per istruzioni, vedere [come connettore Spark HBase toouse](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>I problemi relativi a notebook tooJupyter
Di seguito sono i blocchi appunti tooJupyter correlati alcuni problemi noti.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notebook con nomi di file contenenti caratteri non ASCII
I notebook Jupyter utilizzabili nei cluster HDInsight Spark non devono contenere nei nomi di file caratteri non ASCII. Se si tenta di tooupload un file tramite hello UI Jupyter che ha un nome di file non ASCII, ne verrà eseguito automaticamente (vale a dire Jupyter non consente di caricare file hello, ma non genererà un errore visibile sia). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Errore durante il caricamento di notebook di maggiori dimensioni
Quando si caricano notebook di maggiori dimensioni, potrebbe comparire l'errore **`Error loading notebook`** .  

**Soluzione:**

Se viene visualizzato questo errore, non significa che i dati sono danneggiati o persi.  I blocchi appunti sono ancora nell'unità disco in `/var/lib/jupyter`, ed è possibile SSH in hello cluster tooaccess li. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Dopo avere connesso il cluster toohello tramite SSH, è possibile copiare i blocchi appunti dal cluster tooyour computer locale (tramite SCP o WinSCP) come una perdita di hello tooprevent backup dei dati importanti nel blocco note hello. È quindi possibile tunnel SSH nel nodo head in porte 8001 tooaccess Jupyter senza passare attraverso il gateway hello.  Da qui, è possibile cancellare l'output di hello del blocco note e salvarlo nuovamente la dimensione del blocco per Appunti toominimize hello.

tooprevent l'errore accada in futuro, è necessario seguire alcune procedure consigliate hello:

* È importante tookeep dimensioni di blocco per Appunti hello piccole. Da processi di Spark l'output viene inviato nuovamente tooJupyter è persistente nel blocco note hello.  È buona norma con Jupyter in tooavoid generale in esecuzione `.collect()` su grandi RDD o frame di dati; in alternativa, se si desidera toopeek contenuto del RDD, si consideri l'esecuzione `.take()` o `.sample()` in modo che l'output non ottiene troppo grande.
* Inoltre, quando si salva un notebook, deselezionare tutto l'output dimensioni hello tooreduce di celle.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>L'avvio iniziale del notebook richiede più tempo del previsto
La prima istruzione del codice nel notebook di Jupyter tramite il magic Spark potrebbe richiedere più di un minuto.  

**Spiegazione:**

Ciò accade perché quando si esegue prima cella di codice hello. In background hello verrà avviata la configurazione di sessione e Spark, SQL e contesti di Hive sono impostati. Dopo aver impostati questi contesti, viene eseguita prima istruzione hello e in questo modo l'impressione di hello che istruzione hello ha richiesto un toocomplete molto tempo.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Server Jupyter notebook timeout per la creazione della sessione hello
Quando il cluster Spark è esaurito le risorse, hello Spark e Pyspark kernel in notebook Jupyter hello verrà timeout sessione hello toocreate durante il tentativo. 

**Soluzioni:** 

1. Liberare alcune risorse nel cluster Spark nei modi seguenti:
   
   * L'arresto di altri blocchi appunti Spark passare toohello chiudere e menu di arresto o facendo clic su arresto in Esplora notebook hello.
   * Arrestando altre applicazioni Spark da YARN.
2. Riavviare notebook hello che si stava cercando toostart backup. Numero sufficiente di risorse devono essere disponibili per toocreate è ora una sessione.

## <a name="see-also"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

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

