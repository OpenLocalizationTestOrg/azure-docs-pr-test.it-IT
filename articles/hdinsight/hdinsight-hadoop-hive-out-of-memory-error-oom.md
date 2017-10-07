---
title: un Hive errore di memoria in Azure HDInsight insufficiente aaaFix | Documenti Microsoft
description: Correggere un errore Hive di memoria insufficiente in HDInsight. gli scenari dei clienti Hello sono una query tra molte tabelle di grandi dimensioni.
keywords: errore di memoria insufficiente, OOM, impostazioni Hive
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Correggere un errore Hive di memoria insufficiente in Azure HDInsight

Informazioni su come toofix un Hive errore di memoria insufficiente quando elaborare tabelle di grandi dimensioni, configurare le impostazioni di memoria Hive.

## <a name="run-hive-query-against-large-tables"></a>Eseguire una query Hive su tabelle di grandi dimensioni

Un cliente ha eseguito una query Hive:

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

Dettagli della query:

* T1 è una tabella big tooa alias, Tabella1, che dispone di molti tipi di colonna stringa.
* Le altre tabelle non hanno tali dimensioni, ma dispongono di un numero elevato di colonne.
* Tutte le tabelle sono unite tra loro, in alcuni casi con più colonne in TABLE1 e altre.

query Hive Hello ha richiesto 26 minuti toofinish in un cluster di HDInsight A3 24 nodo. Hello cliente notificato hello messaggi di avviso seguente:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Tramite il motore di esecuzione di hello Tez. Hello stessa query è stato eseguito per 15 minuti e quindi ha generato il seguente errore hello:

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

Errore Hello rimane quando si utilizza una macchina virtuale più grande (ad esempio, D12).


## <a name="debug-hello-out-of-memory-error"></a>Eseguire il debug di hello errore di memoria insufficiente

Il supporto e i team di progettazione insieme rilevato uno dei problemi di hello hello errore di memoria insufficiente causa un [noto problema descritto nel hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Hello **hive.auto.convert.join.noconditionaltask** hello hive-Site.XML file è stato impostato troppo**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

È probabile causa hello di hello lo spazio dell'Heap Java è stato di join mappa l'errore di memoria. Come descritto nel post di blog hello [le impostazioni della memoria Hadoop Yarn in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando il motore di esecuzione viene utilizzato lo spazio dell'heap hello utilizzati Tez appartiene effettivamente toohello Tez contenitore. Vedere hello seguente memoria immagine descrittivo hello Tez contenitore.

![Diagramma della memoria del contenitore Tez: errore Hive di memoria insufficiente](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

Come suggerito dal post di blog di hello, hello seguenti due impostazioni di memoria definisce hello contenitore di memoria per heap hello: **hive.tez.container.size** e **hive.tez.java.opts**. L'esperienza, hello eccezione per memoria insufficiente non significa dimensione del contenitore hello è troppo piccolo. Significa hello dimensione heap Java (hive.tez.java.opts) è troppo piccolo. Pertanto ogni volta che viene visualizzato di memoria insufficiente, è possibile provare tooincrease **hive.tez.java.opts**. Se necessario è possibile avere tooincrease **hive.tez.container.size**. Hello **java.opts** impostazione deve essere circa l'80% del **container.size**.

> [!NOTE]
> impostazione di Hello **hive.tez.java.opts** deve sempre essere minore di **hive.tez.container.size**.
> 
> 

Poiché dispone di una macchina D12 28GB di memoria, abbiamo deciso toouse una dimensione del contenitore di 10GB (10240MB) e assegnare l'80% toojava.opts:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Con le nuove impostazioni hello, è stata eseguita la query hello in meno di 10 minuti.

## <a name="next-steps"></a>Passaggi successivi

Un messaggio di errore di memoria insufficiente non significa necessariamente che dimensione del contenitore hello è troppo piccolo. In alternativa, è necessario configurare le impostazioni della memoria hello in modo che la dimensione dell'heap hello viene aumentata e almeno l'80% della dimensione della memoria di hello contenitore. Per l'ottimizzazione delle query Hive, vedere [Ottimizzare le query Hive per Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).
