---
title: aaaTroubleshoot Spark usando Azure HDInsight | Documenti Microsoft
description: Ottenere risposte toocommon domande sull'uso di Apache Spark e Azure HDInsight.
keywords: Azure HDInsight, Spark, domande frequenti, guida alla risoluzione dei problemi, problemi comuni, configurazione dell'applicazione, Ambari
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Risolvere i problemi di Spark tramite Azure HDInsight

Informazioni sui problemi principali hello e le relative soluzioni quando si lavora con payload Apache Spark in Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Come configurare un'applicazione Spark tramite Ambari nei cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

i valori di configurazione Hello per questa procedura sono stati impostati in precedenza in HDInsight. vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Nell'elenco di hello del cluster, selezionare **Spark2**.

    ![Selezionare un cluster dall'elenco](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Seleziona hello **configurazioni** scheda.

    ![Selezionare scheda configurazioni hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Nell'elenco di hello delle configurazioni, selezionare **impostazioni predefinite personalizzate-spark2**.

    ![Selezionare custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Cercare il valore di hello impostazione necessarie tooadjust, ad esempio **spark.executor.memory**. In questo caso, hello valore **m 4608** è troppo alto.

    ![Selezionare il campo di spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Set hello valore toohello impostazione consigliata. valore di Hello **m 2048** è consigliato per questa impostazione.

    ![Modifica valore too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Salvare il valore di hello e quindi salvare la configurazione hello. Sulla barra degli strumenti hello, selezionare **salvare**.

    ![Salva la configurazione e l'impostazione di hello](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Si riceve una notifica se una delle configurazioni richiede attenzione. Tenere presente hello e quindi selezionare **continuare comunque**. 

    ![Selezionare Proceed Anyway (Continuare comunque)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Scrivere una nota sulle modifiche di configurazione hello e quindi selezionare **salvare**.

    ![Immettere una nota relativa hello le modifiche](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Ogni volta che viene salvata una configurazione, viene richiesto il servizio di hello toorestart. Selezionare **Restart** (Riavvia).

    ![Selezionare Restart (Riavvia)](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Confermare il riavvio di hello.

    ![Selezionare la conferma del riavvio completo](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    È possibile esaminare i processi di hello in esecuzione.

    ![Esaminare i processi in esecuzione](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. È possibile aggiungere configurazioni. Nell'elenco di hello delle configurazioni, selezionare **impostazioni predefinite di spark2 personalizzate**, quindi selezionare **Aggiungi proprietà**.

    ![Selezionare Add property (Aggiungi proprietà)](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Definire una nuova proprietà. È possibile definire una singola proprietà tramite una finestra di dialogo per le impostazioni specifiche, ad esempio il tipo di dati di hello. In alternativa, è possibile definire più proprietà usando una definizione per riga. 

    In questo esempio hello **spark.driver.memory** proprietà è definita con un valore di **4g**.

    ![Definire una nuova proprietà](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Salvare la configurazione hello e quindi riavviare il servizio di hello, come descritto nei passaggi 6 e 7.

Queste modifiche sono a livello di cluster, ma possono essere ignorate quando si invia il processo di Spark hello.

### <a name="additional-reading"></a>Informazioni aggiuntive

[Invio del processo Spark nei cluster HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Come configurare un'applicazione Spark tramite un notebook di Jupyter nei cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Nella prima cella di hello del server Jupyter notebook hello, dopo aver hello **% % configurare** direttiva, specificare le configurazioni di Spark hello nel formato JSON valido. Modificare i valori effettivi di hello in base alle esigenze:

    ![Aggiungere una configurazione](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Informazioni aggiuntive

[Invio del processo Spark nei cluster HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Come configurare un'applicazione Spark tramite Livy nei cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Inviare hello Spark applicazione tooLivy tramite un client REST come cURL. Utilizzare una comando simile toohello che segue. Modificare i valori effettivi di hello in base alle esigenze:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Informazioni aggiuntive

[Invio del processo Spark nei cluster HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Come configurare un'applicazione Spark tramite spark-submit nei cluster

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. vedere quali configurazioni di Spark, sono necessari valori di set e toowhat toobe, toodetermine [cosa provoca l'eccezione dell'applicazione OutofMemoryError un Spark](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Avviare shell di spark usando un comando simile toohello. Modificare il valore effettivo di hello delle configurazioni di hello in base alle esigenze: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Informazioni aggiuntive

[Invio del processo Spark nei cluster HDInsight](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Causa dell'eccezione OutOfMemoryError in un'applicazione Spark

### <a name="detailed-description"></a>Descrizione dettagliata

applicazione di Spark Hello non riesce, con i seguenti tipi di eccezioni non rilevate hello:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Possibile causa

causa più probabile di Hello di questa eccezione è che non è sufficiente memoria heap è allocata toohello Java virtual machine (JVMs). Questi JVMs vengono avviate come executor o i driver come parte dell'applicazione di Spark hello. 

### <a name="resolution-steps"></a>Procedura per la risoluzione

1. Determinare hello dimensioni massime di hello dati hello Spark applicazione handle. È possibile rendere un'ipotesi basata sulla dimensione massima di hello hello di dati di input, i dati intermedi hello prodotto dalla trasformazione di dati di input hello e dati di output di hello che viene generati quando un'applicazione hello è ulteriormente la trasformazione di dati intermedi hello. Questo processo può essere iterativo se non si riesce a ottenere una stima iniziale formale. 

2. Verificare che il cluster HDInsight hello che si userà toouse disponga di sufficienti risorse in termini di memoria e core tooaccommodate hello Spark dell'applicazione. È possibile determinare questo visualizzando una sezione di metriche di cluster hello di hello YARN UI per i valori hello di **di memoria utilizzata** Visual Studio. **Memory Total** (Memoria totale) e i valori di **VCores Used** (VCore in uso) e **VCores Total** (VCore totali).

3. Impostare hello seguente Spark valori tooappropriate delle configurazioni non devono superare il 90% di memoria disponibile hello e di core. i valori Hello devono essere anche all'interno di requisiti di memoria hello di hello applicazione Spark: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello memoria totale utilizzata da tutti gli esecutori, Esegui hello comando seguente: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello memoria totale utilizzata dal driver hello, eseguire hello comando seguente:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Informazioni aggiuntive

- [Spark memory management overview (Panoramica della gestione della memoria Spark)](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Eseguire il debug di un'applicazione Spark in un cluster HDInsight)

