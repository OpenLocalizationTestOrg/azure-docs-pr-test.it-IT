---
title: esegue una query aaaOptimize Hive in HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toooptimize l'Hive esegue una query per Hadoop in HDInsight.
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
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="34eac-103">Ottimizzare le query Hive in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="34eac-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="34eac-104">Per impostazione predefinita, i cluster Hadoop non sono ottimizzati per le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="34eac-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="34eac-105">Questo articolo descrive alcuni metodi di ottimizzazione delle prestazioni Hive più comuni che è possibile applicare tooyour query.</span><span class="sxs-lookup"><span data-stu-id="34eac-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="34eac-106">Scalabilità orizzontale dei nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="34eac-106">Scale out worker nodes</span></span>

<span data-ttu-id="34eac-107">Aumentare il numero di hello nodi di lavoro in un cluster, è possibile sfruttare più toobe di BizTalk Mapper e riduttori eseguite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="34eac-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="34eac-108">Esistono due modi per aumentare la scalabilità orizzontale in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="34eac-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="34eac-109">In fase di disposizione hello, è possibile specificare il numero di hello di nodi di lavoro utilizzando hello portale di Azure, Azure PowerShell o interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="34eac-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="34eac-110">Per altre informazioni, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="34eac-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="34eac-111">Hello schermata seguente mostra il lavoro hello configurazione del nodo nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="34eac-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="34eac-113">In fase di esecuzione di hello, è anche possibile scalare orizzontalmente un cluster senza ricreare uno:</span><span class="sxs-lookup"><span data-stu-id="34eac-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="34eac-115">Per ulteriori informazioni sulle macchine virtuali diverse hello è supportato da HDInsight, vedere [prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="34eac-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="34eac-116">Abilitare Tez</span><span class="sxs-lookup"><span data-stu-id="34eac-116">Enable Tez</span></span>

<span data-ttu-id="34eac-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) è un motore di esecuzione alternativo motore toohello MapReduce:</span><span class="sxs-lookup"><span data-stu-id="34eac-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="34eac-119">Tez è più veloce perché:</span><span class="sxs-lookup"><span data-stu-id="34eac-119">Tez is faster because:</span></span>

* <span data-ttu-id="34eac-120">**Eseguire indirizzate aciclico Graph (DAG) come un singolo processo di motore MapReduce hello**.</span><span class="sxs-lookup"><span data-stu-id="34eac-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="34eac-121">Hello DAG richiede ogni set di BizTalk Mapper toobe seguita da una serie di riduttori.</span><span class="sxs-lookup"><span data-stu-id="34eac-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="34eac-122">In questo modo toobe di processi MapReduce più rimosso per ogni query Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="34eac-123">Tez non presenta questo vincolo e può elaborare DAG complessi con un unico processo, riducendo così il sovraccarico di avvio del processo.</span><span class="sxs-lookup"><span data-stu-id="34eac-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="34eac-124">**Evita scritture non necessarie**.</span><span class="sxs-lookup"><span data-stu-id="34eac-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="34eac-125">A causa di processi toomultiple viene ruotati per hello stessa query Hive nel motore MapReduce hello, output di hello di ogni processo viene scritto tooHDFS per i dati intermedi.</span><span class="sxs-lookup"><span data-stu-id="34eac-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="34eac-126">Poiché Tez riduce al minimo numero di processi per ogni query Hive è in grado di tooavoid scrittura non necessari.</span><span class="sxs-lookup"><span data-stu-id="34eac-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="34eac-127">**Riduce al minimo i ritardi di avvio**.</span><span class="sxs-lookup"><span data-stu-id="34eac-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="34eac-128">Tez è migliore ritardo di avvio in grado di toominimize riducendo il numero di hello di BizTalk Mapper che è necessario toostart e anche migliorare di ottimizzazione in tutto.</span><span class="sxs-lookup"><span data-stu-id="34eac-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="34eac-129">**Riusa i contenitori**.</span><span class="sxs-lookup"><span data-stu-id="34eac-129">**Reuses containers**.</span></span> <span data-ttu-id="34eac-130">Ogni volta che Tez possibili è in grado di tooreuse contenitori tooensure tale latenza a causa di toostarting dei contenitori viene ridotto.</span><span class="sxs-lookup"><span data-stu-id="34eac-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="34eac-131">**Usa tecniche di ottimizzazione continua**.</span><span class="sxs-lookup"><span data-stu-id="34eac-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="34eac-132">In genere l'ottimizzazione viene eseguita durante la fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="34eac-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="34eac-133">Tuttavia, sono disponibili ulteriori informazioni sugli input hello che consentono di migliore ottimizzazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="34eac-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="34eac-134">Tez utilizza tecniche di ottimizzazione continua che consenta a tale piano di hello toooptimize ulteriormente in fase di runtime hello.</span><span class="sxs-lookup"><span data-stu-id="34eac-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="34eac-135">Per altre informazioni su questi concetti, vedere [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="34eac-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="34eac-136">È possibile apportare tutte le query Hive Tez abilitata aggiungendo il prefisso query hello con impostazione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="34eac-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="34eac-137">I cluster HDInsight basati su Linux hanno Tez abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="34eac-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="34eac-138">Partizionamento Hive</span><span class="sxs-lookup"><span data-stu-id="34eac-138">Hive partitioning</span></span>

<span data-ttu-id="34eac-139">Operazione dei / o è hello principali collo di bottiglia per l'esecuzione di query Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="34eac-140">possono migliorare le prestazioni di Hello se quantità hello di dati che devono essere toobe lettura può essere ridotto.</span><span class="sxs-lookup"><span data-stu-id="34eac-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="34eac-141">Per impostazione predefinita, le query Hive analizzano intere tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="34eac-142">Questa operazione è utile per query come le analisi di tabella,</span><span class="sxs-lookup"><span data-stu-id="34eac-142">This is great for queries like table scans.</span></span> <span data-ttu-id="34eac-143">Tuttavia per le query che richiedono solo una piccola quantità di dati, ad esempio, le query con il filtro, tooscan, questo comportamento crea un inutile overhead.</span><span class="sxs-lookup"><span data-stu-id="34eac-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="34eac-144">Partizionamento hive consente Hive query tooaccess solo hello necessarie quantità di dati nelle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="34eac-145">Partizionamento hive viene implementato tramite la riorganizzazione di dati non elaborati hello in directory di nuovo a ciascuna partizione con una propria directory, in cui la partizione hello è definita da utente hello.</span><span class="sxs-lookup"><span data-stu-id="34eac-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="34eac-146">Hello diagramma seguente illustra il partizionamento di una tabella Hive per colonna hello *anno*.</span><span class="sxs-lookup"><span data-stu-id="34eac-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="34eac-147">Viene creata una nuova directory per ogni anno.</span><span class="sxs-lookup"><span data-stu-id="34eac-147">A new directory is created for each year.</span></span>

![partizionamento][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="34eac-149">Alcune considerazioni sul partizionamento:</span><span class="sxs-lookup"><span data-stu-id="34eac-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="34eac-150">**Non creare un numero eccessivamente ridotto di partizioni**: il partizionamento in colonne con pochi valori può causare un numero ridotto di partizioni.</span><span class="sxs-lookup"><span data-stu-id="34eac-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="34eac-151">Ad esempio, solo il partizionamento in genere crea due toobe partizioni creato (maschio e femmina), pertanto solo ridurre la latenza di hello da un massimo di metà.</span><span class="sxs-lookup"><span data-stu-id="34eac-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="34eac-152">**Eseguire non su una partizione** : nel hello altra estremità, creazione di una partizione in una colonna con un valore univoco (ad esempio, userid) fa sì che più partizioni.</span><span class="sxs-lookup"><span data-stu-id="34eac-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="34eac-153">Sulla partizione impone quantità stress hello cluster namenode perché contiene numerosi hello toohandle delle directory.</span><span class="sxs-lookup"><span data-stu-id="34eac-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="34eac-154">**Evitare lo sfasamento di dati** : scegliere la chiave di partizionamento con attenzione, in modo che tutte le partizioni siano di dimensioni pari.</span><span class="sxs-lookup"><span data-stu-id="34eac-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="34eac-155">Un esempio è partizionamento in *stato* può causare il numero di hello di record in California toobe quasi 30 x che di Vermont a causa di differenza toohello popolazione.</span><span class="sxs-lookup"><span data-stu-id="34eac-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="34eac-156">toocreate una tabella di partizione, utilizzare hello *partizionata da* clausola:</span><span class="sxs-lookup"><span data-stu-id="34eac-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="34eac-157">Una volta creata la tabella partizionata hello, è possibile creare il partizionamento statico o il partizionamento dinamico.</span><span class="sxs-lookup"><span data-stu-id="34eac-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="34eac-158">**Il partizionamento statico** significa che sono presenti dati già partizionati hello le directory appropriate che è possibile richiedere Hive partizioni manualmente in base alla posizione di directory hello.</span><span class="sxs-lookup"><span data-stu-id="34eac-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="34eac-159">Hello frammento di codice seguente è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="34eac-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="34eac-160">**Partizionamento dinamico** significa che le partizioni toocreate Hive automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="34eac-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="34eac-161">Poiché sono già stati creati hello partizionamento tabella dalla tabella di gestione temporanea hello, è sufficiente toodo è insert dati partizionato toohello tabella:</span><span class="sxs-lookup"><span data-stu-id="34eac-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="34eac-162">Per ulteriori informazioni, vedere [Tabelle partizionate](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="34eac-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="34eac-163">Utilizzare il formato ORCFile hello</span><span class="sxs-lookup"><span data-stu-id="34eac-163">Use hello ORCFile format</span></span>
<span data-ttu-id="34eac-164">Hive supporta diversi formati di file.</span><span class="sxs-lookup"><span data-stu-id="34eac-164">Hive supports different file formats.</span></span> <span data-ttu-id="34eac-165">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="34eac-165">For example:</span></span>

* <span data-ttu-id="34eac-166">**Testo**: questo è il formato di file predefinito hello e funziona con la maggior parte degli scenari</span><span class="sxs-lookup"><span data-stu-id="34eac-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="34eac-167">**Avro**: funziona bene per scenari di interoperabilità</span><span class="sxs-lookup"><span data-stu-id="34eac-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="34eac-168">**ORC/Parquet**: particolarmente indicato per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="34eac-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="34eac-169">Il formato ORC (con ottimizzazione per la riga a colonne) è un toostore molto efficiente dati Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="34eac-170">Formati tooother confrontati, ORC ha hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="34eac-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="34eac-171">supporto per tipi complessi, inclusi i tipi complessi e semistrutturati e DateTime</span><span class="sxs-lookup"><span data-stu-id="34eac-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="34eac-172">configurare la compressione % too70</span><span class="sxs-lookup"><span data-stu-id="34eac-172">up too70% compression</span></span>
* <span data-ttu-id="34eac-173">indici ogni 10.000 righe, che consentono di ignorare le righe</span><span class="sxs-lookup"><span data-stu-id="34eac-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="34eac-174">significativa riduzione in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="34eac-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="34eac-175">il formato ORC tooenable, creare innanzitutto una tabella con clausola hello *archiviati come ORC*:</span><span class="sxs-lookup"><span data-stu-id="34eac-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="34eac-176">Successivamente, si inserisce nella tabella dati toohello ORC dalla tabella di gestione temporanea hello.</span><span class="sxs-lookup"><span data-stu-id="34eac-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="34eac-177">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="34eac-177">For example:</span></span>

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

<span data-ttu-id="34eac-178">Altre informazioni sul formato ORC hello [qui](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="34eac-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="34eac-179">Vettorizzazione</span><span class="sxs-lookup"><span data-stu-id="34eac-179">Vectorization</span></span>

<span data-ttu-id="34eac-180">Consente di vettorizzazione Hive tooprocess un batch di 1024 righe insieme anziché l'elaborazione di una riga alla volta.</span><span class="sxs-lookup"><span data-stu-id="34eac-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="34eac-181">Significa che le operazioni semplici vengono eseguite più velocemente perché meno codice interno deve essere toorun.</span><span class="sxs-lookup"><span data-stu-id="34eac-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="34eac-182">la vettorializzazione tooenable prefisso query Hive con hello seguente impostazione:</span><span class="sxs-lookup"><span data-stu-id="34eac-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="34eac-183">Per altre informazioni, vedere [Esecuzione di query vettorizzate](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="34eac-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="34eac-184">Altri metodi di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="34eac-184">Other optimization methods</span></span>
<span data-ttu-id="34eac-185">Esistono altri metodi di ottimizzazione che è possibile considerare, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="34eac-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="34eac-186">**Hive bucket:** una tecnica che consente di segmento o toocluster grandi set di dati toooptimize le prestazioni delle query.</span><span class="sxs-lookup"><span data-stu-id="34eac-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="34eac-187">**L'ottimizzazione del join:** ottimizzazione dell'esecuzione di query Hive pianificazione tooimprove hello l'efficienza di join e ridurre hello necessità per gli hint per utente.</span><span class="sxs-lookup"><span data-stu-id="34eac-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="34eac-188">Per altre informazioni, vedere [Ottimizzazione join](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="34eac-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="34eac-189">**Aumento dei reducer**.</span><span class="sxs-lookup"><span data-stu-id="34eac-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34eac-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34eac-190">Next steps</span></span>
<span data-ttu-id="34eac-191">In questo articolo sono stati illustrati vari metodi di ottimizzazione delle query comuni di Hive.</span><span class="sxs-lookup"><span data-stu-id="34eac-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="34eac-192">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="34eac-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="34eac-193">Usare Apache Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="34eac-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="34eac-194">Analizzare i dati sui ritardi dei voli mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="34eac-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="34eac-195">Analizzare i dati Twitter mediante Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="34eac-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="34eac-196">Analizzare i dati del sensore utilizzando la Console di Query Hive hello in Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="34eac-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="34eac-197">Usare l'Hive con log tooanalyze HDInsight da siti Web</span><span class="sxs-lookup"><span data-stu-id="34eac-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
