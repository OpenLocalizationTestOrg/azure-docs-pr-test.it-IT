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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="c0b78-105">Correggere un errore Hive di memoria insufficiente in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0b78-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="c0b78-106">Informazioni su come toofix un Hive errore di memoria insufficiente quando elaborare tabelle di grandi dimensioni, configurare le impostazioni di memoria Hive.</span><span class="sxs-lookup"><span data-stu-id="c0b78-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="c0b78-107">Eseguire una query Hive su tabelle di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="c0b78-107">Run Hive query against large tables</span></span>

<span data-ttu-id="c0b78-108">Un cliente ha eseguito una query Hive:</span><span class="sxs-lookup"><span data-stu-id="c0b78-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="c0b78-109">Dettagli della query:</span><span class="sxs-lookup"><span data-stu-id="c0b78-109">Some nuances of this query:</span></span>

* <span data-ttu-id="c0b78-110">T1 è una tabella big tooa alias, Tabella1, che dispone di molti tipi di colonna stringa.</span><span class="sxs-lookup"><span data-stu-id="c0b78-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="c0b78-111">Le altre tabelle non hanno tali dimensioni, ma dispongono di un numero elevato di colonne.</span><span class="sxs-lookup"><span data-stu-id="c0b78-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="c0b78-112">Tutte le tabelle sono unite tra loro, in alcuni casi con più colonne in TABLE1 e altre.</span><span class="sxs-lookup"><span data-stu-id="c0b78-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="c0b78-113">query Hive Hello ha richiesto 26 minuti toofinish in un cluster di HDInsight A3 24 nodo.</span><span class="sxs-lookup"><span data-stu-id="c0b78-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="c0b78-114">Hello cliente notificato hello messaggi di avviso seguente:</span><span class="sxs-lookup"><span data-stu-id="c0b78-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="c0b78-115">Tramite il motore di esecuzione di hello Tez.</span><span class="sxs-lookup"><span data-stu-id="c0b78-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="c0b78-116">Hello stessa query è stato eseguito per 15 minuti e quindi ha generato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="c0b78-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="c0b78-117">Errore Hello rimane quando si utilizza una macchina virtuale più grande (ad esempio, D12).</span><span class="sxs-lookup"><span data-stu-id="c0b78-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="c0b78-118">Eseguire il debug di hello errore di memoria insufficiente</span><span class="sxs-lookup"><span data-stu-id="c0b78-118">Debug hello out of memory error</span></span>

<span data-ttu-id="c0b78-119">Il supporto e i team di progettazione insieme rilevato uno dei problemi di hello hello errore di memoria insufficiente causa un [noto problema descritto nel hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="c0b78-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="c0b78-120">Hello **hive.auto.convert.join.noconditionaltask** hello hive-Site.XML file è stato impostato troppo**true**:</span><span class="sxs-lookup"><span data-stu-id="c0b78-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="c0b78-121">È probabile causa hello di hello lo spazio dell'Heap Java è stato di join mappa l'errore di memoria.</span><span class="sxs-lookup"><span data-stu-id="c0b78-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="c0b78-122">Come descritto nel post di blog hello [le impostazioni della memoria Hadoop Yarn in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), quando il motore di esecuzione viene utilizzato lo spazio dell'heap hello utilizzati Tez appartiene effettivamente toohello Tez contenitore.</span><span class="sxs-lookup"><span data-stu-id="c0b78-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="c0b78-123">Vedere hello seguente memoria immagine descrittivo hello Tez contenitore.</span><span class="sxs-lookup"><span data-stu-id="c0b78-123">See hello following image describing hello Tez container memory.</span></span>

![Diagramma della memoria del contenitore Tez: errore Hive di memoria insufficiente](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="c0b78-125">Come suggerito dal post di blog di hello, hello seguenti due impostazioni di memoria definisce hello contenitore di memoria per heap hello: **hive.tez.container.size** e **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="c0b78-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="c0b78-126">L'esperienza, hello eccezione per memoria insufficiente non significa dimensione del contenitore hello è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c0b78-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="c0b78-127">Significa hello dimensione heap Java (hive.tez.java.opts) è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c0b78-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="c0b78-128">Pertanto ogni volta che viene visualizzato di memoria insufficiente, è possibile provare tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="c0b78-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="c0b78-129">Se necessario è possibile avere tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="c0b78-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="c0b78-130">Hello **java.opts** impostazione deve essere circa l'80% del **container.size**.</span><span class="sxs-lookup"><span data-stu-id="c0b78-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b78-131">impostazione di Hello **hive.tez.java.opts** deve sempre essere minore di **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="c0b78-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="c0b78-132">Poiché dispone di una macchina D12 28GB di memoria, abbiamo deciso toouse una dimensione del contenitore di 10GB (10240MB) e assegnare l'80% toojava.opts:</span><span class="sxs-lookup"><span data-stu-id="c0b78-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="c0b78-133">Con le nuove impostazioni hello, è stata eseguita la query hello in meno di 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="c0b78-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0b78-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0b78-134">Next steps</span></span>

<span data-ttu-id="c0b78-135">Un messaggio di errore di memoria insufficiente non significa necessariamente che dimensione del contenitore hello è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c0b78-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="c0b78-136">In alternativa, è necessario configurare le impostazioni della memoria hello in modo che la dimensione dell'heap hello viene aumentata e almeno l'80% della dimensione della memoria di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="c0b78-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="c0b78-137">Per l'ottimizzazione delle query Hive, vedere [Ottimizzare le query Hive per Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="c0b78-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
