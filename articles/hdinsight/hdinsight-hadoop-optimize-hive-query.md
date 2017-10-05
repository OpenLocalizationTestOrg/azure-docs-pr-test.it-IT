---
title: Ottimizzare le query Hive in Azure HDInsight | Microsoft Docs
description: Informazioni su come ottimizzare le query Hive per Hadoop in HDInsight
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="e3193-103">Ottimizzare le query Hive in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3193-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="e3193-104">Per impostazione predefinita, i cluster Hadoop non sono ottimizzati per le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e3193-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="e3193-105">Questo articolo descrive alcuni metodi di ottimizzazione delle prestazioni Hive più comuni che è possibile applicare alle query.</span><span class="sxs-lookup"><span data-stu-id="e3193-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="e3193-106">Scalabilità orizzontale dei nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="e3193-106">Scale out worker nodes</span></span>

<span data-ttu-id="e3193-107">Aumentando il numero di nodi di lavoro in un cluster è possibile usare più mapper e reducer da eseguire in parallelo.</span><span class="sxs-lookup"><span data-stu-id="e3193-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="e3193-108">Esistono due modi per aumentare la scalabilità orizzontale in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e3193-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="e3193-109">In fase di provisioning è possibile specificare il numero di nodi di lavoro usando il portale di Azure, Azure PowerShell o l'interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="e3193-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="e3193-110">Per altre informazioni, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e3193-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="e3193-111">La schermata seguente mostra la configurazione dei nodi del ruolo di lavoro nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="e3193-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="e3193-113">In fase di esecuzione è anche possibile scalare orizzontalmente un cluster senza ricreare uno:</span><span class="sxs-lookup"><span data-stu-id="e3193-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="e3193-115">Per altre informazioni sulle diverse macchine virtuali supportate da HDInsight, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e3193-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="e3193-116">Abilitare Tez</span><span class="sxs-lookup"><span data-stu-id="e3193-116">Enable Tez</span></span>

<span data-ttu-id="e3193-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) è un motore di esecuzione alternativo al motore di MapReduce:</span><span class="sxs-lookup"><span data-stu-id="e3193-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="e3193-119">Tez è più veloce perché:</span><span class="sxs-lookup"><span data-stu-id="e3193-119">Tez is faster because:</span></span>

* <span data-ttu-id="e3193-120">**Esegue un grafo aciclico diretto (DAG) come un singolo processo nel motore di MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="e3193-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="e3193-121">Il DAG richiede che ogni set di mapper sia seguito da un set di reducer.</span><span class="sxs-lookup"><span data-stu-id="e3193-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="e3193-122">In questo modo, più processi MapReduce vengono eseguiti per ciascuna query Hive.</span><span class="sxs-lookup"><span data-stu-id="e3193-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="e3193-123">Tez non presenta questo vincolo e può elaborare DAG complessi con un unico processo, riducendo così il sovraccarico di avvio del processo.</span><span class="sxs-lookup"><span data-stu-id="e3193-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="e3193-124">**Evita scritture non necessarie**.</span><span class="sxs-lookup"><span data-stu-id="e3193-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="e3193-125">Poiché più processi vengono eseguiti per la stessa query Hive nel motore di MapReduce, l'output di ogni processo viene scritto in HDFS per dati intermedi.</span><span class="sxs-lookup"><span data-stu-id="e3193-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="e3193-126">Poiché Tez riduce il numero di processi per ciascuna query Hive è in grado di evitare scritture non necessarie.</span><span class="sxs-lookup"><span data-stu-id="e3193-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="e3193-127">**Riduce al minimo i ritardi di avvio**.</span><span class="sxs-lookup"><span data-stu-id="e3193-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="e3193-128">Tez è in grado di ridurre al minimo il ritardo di avvio limitando il numero di mapper da avviare e migliorando anche l'ottimizzazione complessiva.</span><span class="sxs-lookup"><span data-stu-id="e3193-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="e3193-129">**Riusa i contenitori**.</span><span class="sxs-lookup"><span data-stu-id="e3193-129">**Reuses containers**.</span></span> <span data-ttu-id="e3193-130">Quando possibile, Tez è in grado di riusare i contenitori per assicurare che la latenza dovuta all'avvio dei contenitori venga ridotta.</span><span class="sxs-lookup"><span data-stu-id="e3193-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="e3193-131">**Usa tecniche di ottimizzazione continua**.</span><span class="sxs-lookup"><span data-stu-id="e3193-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="e3193-132">In genere l'ottimizzazione viene eseguita durante la fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="e3193-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="e3193-133">Tuttavia, sono disponibili ulteriori informazioni sugli input che consentono una migliore ottimizzazione durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="e3193-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="e3193-134">Tez usa tecniche di ottimizzazione continua che consentono di ottimizzare ulteriormente il piano nella fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="e3193-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="e3193-135">Per altre informazioni su questi concetti, vedere [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="e3193-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="e3193-136">È possibile eseguire qualsiasi query Hive a cui Tez è abilitato anteponendovi l'impostazione seguente:</span><span class="sxs-lookup"><span data-stu-id="e3193-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="e3193-137">I cluster HDInsight basati su Linux hanno Tez abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e3193-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="e3193-138">Partizionamento Hive</span><span class="sxs-lookup"><span data-stu-id="e3193-138">Hive partitioning</span></span>

<span data-ttu-id="e3193-139">L'operazione di I/O rappresenta il principale collo di bottiglia delle prestazioni per l'esecuzione di query Hive.</span><span class="sxs-lookup"><span data-stu-id="e3193-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="e3193-140">Le prestazioni possono essere migliorate se è possibile ridurre la quantità di dati da leggere.</span><span class="sxs-lookup"><span data-stu-id="e3193-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="e3193-141">Per impostazione predefinita, le query Hive analizzano intere tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="e3193-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="e3193-142">Questa operazione è utile per query come le analisi di tabella,</span><span class="sxs-lookup"><span data-stu-id="e3193-142">This is great for queries like table scans.</span></span> <span data-ttu-id="e3193-143">ma per le query che devono analizzare solo una piccola quantità di dati, ad esempio le query con filtro, viene creato un sovraccarico non necessario.</span><span class="sxs-lookup"><span data-stu-id="e3193-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="e3193-144">Il partizionamento Hive consente alle query Hive di accedere solo alla quantità di dati presente nelle tabelle Hive necessaria.</span><span class="sxs-lookup"><span data-stu-id="e3193-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="e3193-145">Il partizionamento Hive viene implementato riorganizzando i dati non elaborati in nuove directory in cui ciascuna partizione dispone di una propria directory, dove la partizione è definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="e3193-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="e3193-146">Il diagramma seguente illustra il partizionamento di una tabella Hive mediante la colonna *Anno*.</span><span class="sxs-lookup"><span data-stu-id="e3193-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="e3193-147">Viene creata una nuova directory per ogni anno.</span><span class="sxs-lookup"><span data-stu-id="e3193-147">A new directory is created for each year.</span></span>

![partizionamento][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="e3193-149">Alcune considerazioni sul partizionamento:</span><span class="sxs-lookup"><span data-stu-id="e3193-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="e3193-150">**Non creare un numero eccessivamente ridotto di partizioni**: il partizionamento in colonne con pochi valori può causare un numero ridotto di partizioni.</span><span class="sxs-lookup"><span data-stu-id="e3193-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="e3193-151">Il partizionamento in base al sesso, ad esempio, crea solo due partizioni (maschio e femmina) e riduce quindi la latenza al massimo solo della metà.</span><span class="sxs-lookup"><span data-stu-id="e3193-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="e3193-152">**Non creare un numero eccessivo di partizioni**: al contrario, la creazione di una partizione in una colonna con un valore univoco (ad esempio ID utente) causa più partizioni</span><span class="sxs-lookup"><span data-stu-id="e3193-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="e3193-153">generando un sovraccarico nel nodo dei nomi del cluster, che dovrà gestire una grande quantità di directory.</span><span class="sxs-lookup"><span data-stu-id="e3193-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="e3193-154">**Evitare lo sfasamento di dati** : scegliere la chiave di partizionamento con attenzione, in modo che tutte le partizioni siano di dimensioni pari.</span><span class="sxs-lookup"><span data-stu-id="e3193-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="e3193-155">Ad esempio, con il partizionamento in *Stato* , il numero di record in California potrebbe essere quasi 30 volte quello del Vermont, a causa della differenza di popolazione.</span><span class="sxs-lookup"><span data-stu-id="e3193-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="e3193-156">Per creare una tabella di partizione, usare la clausola *Partizionato da* :</span><span class="sxs-lookup"><span data-stu-id="e3193-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="e3193-157">Una volta creata la tabella partizionata, è possibile creare il partizionamento statico o il partizionamento dinamico.</span><span class="sxs-lookup"><span data-stu-id="e3193-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="e3193-158">**Partizionamento statico** indica che i dati sono già stati partizionati nelle directory appropriate ed è possibile richiedere le partizioni Hive manualmente, in base al percorso di directory.</span><span class="sxs-lookup"><span data-stu-id="e3193-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="e3193-159">Il frammento di codice seguente rappresenta un esempio.</span><span class="sxs-lookup"><span data-stu-id="e3193-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="e3193-160">**Partizionamento dinamico** indica che si desidera che Hive crei le partizioni automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e3193-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="e3193-161">Poiché la tabella di partizionamento è già stata creata dalla tabella di gestione temporanea, è sufficiente inserire i dati nella tabella partizionata.</span><span class="sxs-lookup"><span data-stu-id="e3193-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="e3193-162">Per ulteriori informazioni, vedere [Tabelle partizionate](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="e3193-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="e3193-163">Utilizzare il formato ORCFile</span><span class="sxs-lookup"><span data-stu-id="e3193-163">Use the ORCFile format</span></span>
<span data-ttu-id="e3193-164">Hive supporta diversi formati di file.</span><span class="sxs-lookup"><span data-stu-id="e3193-164">Hive supports different file formats.</span></span> <span data-ttu-id="e3193-165">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e3193-165">For example:</span></span>

* <span data-ttu-id="e3193-166">**Testo**: questo è il formato di file predefinito e funziona con la maggior parte degli scenari</span><span class="sxs-lookup"><span data-stu-id="e3193-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="e3193-167">**Avro**: funziona bene per scenari di interoperabilità</span><span class="sxs-lookup"><span data-stu-id="e3193-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="e3193-168">**ORC/Parquet**: particolarmente indicato per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="e3193-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="e3193-169">Il formato ORC (Optimized Row Columnar) è un modo particolarmente efficace per archiviare i dati Hive.</span><span class="sxs-lookup"><span data-stu-id="e3193-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="e3193-170">Rispetto ad altri formati, ORC offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3193-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="e3193-171">supporto per tipi complessi, inclusi i tipi complessi e semistrutturati e DateTime</span><span class="sxs-lookup"><span data-stu-id="e3193-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="e3193-172">fino al 70% di compressione</span><span class="sxs-lookup"><span data-stu-id="e3193-172">up to 70% compression</span></span>
* <span data-ttu-id="e3193-173">indici ogni 10.000 righe, che consentono di ignorare le righe</span><span class="sxs-lookup"><span data-stu-id="e3193-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="e3193-174">significativa riduzione in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="e3193-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="e3193-175">Per abilitare il formato ORC, creare innanzitutto una tabella con la clausola *Archiviato come ORC*:</span><span class="sxs-lookup"><span data-stu-id="e3193-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="e3193-176">Inserire quindi i dati nella tabella ORC dalla tabella di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="e3193-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="e3193-177">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e3193-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="e3193-178">Ulteriori informazioni sul formato ORC sono disponibili [qui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="e3193-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="e3193-179">Vettorizzazione</span><span class="sxs-lookup"><span data-stu-id="e3193-179">Vectorization</span></span>

<span data-ttu-id="e3193-180">La vettorizzazione consente ad Hive di elaborare un batch di 1024 righe insieme invece di elaborare una riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="e3193-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="e3193-181">Ciò significa che le operazioni semplici vengono eseguite più rapidamente poiché è necessario eseguire una quantità inferiore di codice interno.</span><span class="sxs-lookup"><span data-stu-id="e3193-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="e3193-182">Per abilitare la vettorizzazione, anteporre alla query Hive la seguente impostazione:</span><span class="sxs-lookup"><span data-stu-id="e3193-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="e3193-183">Per altre informazioni, vedere [Esecuzione di query vettorizzate](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="e3193-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="e3193-184">Altri metodi di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="e3193-184">Other optimization methods</span></span>
<span data-ttu-id="e3193-185">Esistono altri metodi di ottimizzazione che è possibile considerare, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e3193-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="e3193-186">**Hive bucket:** una tecnica che consente di raggruppare o segmentare grandi set di dati per ottimizzare le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="e3193-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="e3193-187">**Ottimizzazione join:** ottimizzazione dell'esecuzione di query Hive pianificata per migliorare l'efficienza di join e ridurre la necessità di suggerimenti dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e3193-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="e3193-188">Per altre informazioni, vedere [Ottimizzazione join](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="e3193-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="e3193-189">**Aumento dei reducer**.</span><span class="sxs-lookup"><span data-stu-id="e3193-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3193-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3193-190">Next steps</span></span>
<span data-ttu-id="e3193-191">In questo articolo sono stati illustrati vari metodi di ottimizzazione delle query comuni di Hive.</span><span class="sxs-lookup"><span data-stu-id="e3193-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="e3193-192">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3193-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="e3193-193">Usare Apache Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3193-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e3193-194">Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3193-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="e3193-195">Analizzare i dati Twitter mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3193-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="e3193-196">Analizzare i dati dei sensori mediante Hive Query Console su Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3193-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="e3193-197">Usare Hive con HDInsight per analizzare i log dei siti Web</span><span class="sxs-lookup"><span data-stu-id="e3193-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
