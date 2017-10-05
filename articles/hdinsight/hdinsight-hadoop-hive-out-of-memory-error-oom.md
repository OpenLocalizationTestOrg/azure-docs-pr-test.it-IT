---
title: Correggere un errore Hive di memoria insufficiente in Azure HDInsight | Documentazione Microsoft
description: Correggere un errore Hive di memoria insufficiente in HDInsight. Lo scenario del cliente fa riferimento a una query in molte tabelle di grandi dimensioni.
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
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="b5a1b-105">Correggere un errore Hive di memoria insufficiente in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5a1b-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="b5a1b-106">Informazioni su come risolvere un errore Hive di memoria insufficiente durante l'elaborazione tabelle di grandi dimensioni configurando le impostazioni di memoria Hive.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="b5a1b-107">Eseguire una query Hive su tabelle di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="b5a1b-107">Run Hive query against large tables</span></span>

<span data-ttu-id="b5a1b-108">Un cliente ha eseguito una query Hive:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="b5a1b-109">Dettagli della query:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-109">Some nuances of this query:</span></span>

* <span data-ttu-id="b5a1b-110">T1 è l'alias di una tabella di grandi dimensioni, TABLE1, che ha molti tipi di colonna STRING.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="b5a1b-111">Le altre tabelle non hanno tali dimensioni, ma dispongono di un numero elevato di colonne.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="b5a1b-112">Tutte le tabelle sono unite tra loro, in alcuni casi con più colonne in TABLE1 e altre.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="b5a1b-113">La query Hive ha richiesto 26 minuti in un nodo del cluster HDInsight A3 24.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="b5a1b-114">Il cliente ha notato i messaggi di avviso seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="b5a1b-115">Tramite il motore di esecuzione di Tez.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-115">By using the Tez execution engine.</span></span> <span data-ttu-id="b5a1b-116">La stessa query ha richiesto 15 minuti e quindi ha generato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

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

<span data-ttu-id="b5a1b-117">L'errore persiste quando si usa una macchina virtuale più grande (ad esempio, D12).</span><span class="sxs-lookup"><span data-stu-id="b5a1b-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="b5a1b-118">Debug dell'errore di memoria insufficiente</span><span class="sxs-lookup"><span data-stu-id="b5a1b-118">Debug the out of memory error</span></span>

<span data-ttu-id="b5a1b-119">Il supporto Microsoft insieme al team di progettazione ha rilevato che uno dei problemi che provocava l'errore di memoria insufficiente era un [problema noto descritto in Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="b5a1b-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="b5a1b-120">**hive.auto.convert.join.noconditionaltask** nel file hive-site.xml file è stato impostato su **true**:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="b5a1b-121">È probabile che map join sia la causa dell'errore di memoria insufficiente nello spazio dell'heap di Java.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="b5a1b-122">Come illustrato nel post di blog sulle [impostazioni della memoria Yarn di Hadoop in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando si usa il motore di esecuzione Tez lo spazio dell'heap effettivamente usato appartiene al contenitore Tez.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="b5a1b-123">Vedere l'immagine seguente che descrive la memoria del contenitore Tez.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-123">See the following image describing the Tez container memory.</span></span>

![Diagramma della memoria del contenitore Tez: errore Hive di memoria insufficiente](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="b5a1b-125">Come suggerisce il post di blog, le due impostazioni di memoria seguenti definiscono la memoria del contenitore per l'heap: **hive.tez.container.size** e **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="b5a1b-126">In base all'esperienza attuale, l'eccezione di memoria insufficiente non è correlata alle dimensioni ridotte del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="b5a1b-127">Ossia, ad essere ridotte solo le dimensioni dell'heap di Java (hive.tez.java.opts).</span><span class="sxs-lookup"><span data-stu-id="b5a1b-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="b5a1b-128">Pertanto ogni volta che viene visualizzato un errore di memoria insufficiente, è possibile provare ad aumentare **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="b5a1b-129">Se necessario, può essere necessario aumentare **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="b5a1b-130">L'impostazione **java.opts** deve essere circa l'80% di **container.size**.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a1b-131">L'impostazione **hive.tez.java.opts** deve sempre essere inferiore a **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="b5a1b-132">Poiché una macchina D12 ha una memoria di 28 GB, si è deciso di usare una dimensione del contenitore di 10 GB (10.240 MB) e assegnare l'80% a java.opts:</span><span class="sxs-lookup"><span data-stu-id="b5a1b-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="b5a1b-133">Con le nuove impostazioni, la query è stata eseguita in meno di dieci minuti.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5a1b-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5a1b-134">Next steps</span></span>

<span data-ttu-id="b5a1b-135">Un errore di memoria insufficiente non indica necessariamente che le dimensioni del contenitore sono troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="b5a1b-136">Al contrario, è necessario configurare le impostazioni della memoria in modo che le dimensioni dell'heap aumentino e raggiungano almeno l'80% delle dimensioni della memoria del contenitore.</span><span class="sxs-lookup"><span data-stu-id="b5a1b-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="b5a1b-137">Per l'ottimizzazione delle query Hive, vedere [Ottimizzare le query Hive per Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="b5a1b-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>